---
layout: default
title: "Low DO Mortality - User Manual"
permalink: /hab-modeling/low-do-mortality/
---

{% include section-nav.html section="hab-users-manual" %}

# Chapter 2: Low DO Mortality (Hypoxic Conditions)

## Purpose

CE-QUAL-W2 simulates enhanced algal die-off under prolonged low dissolved oxygen (hypoxic) conditions. When DO drops below a user-specified threshold and remains low for longer than a critical duration, CE-QUAL-W2 replaces the normal algal mortality rate with an elevated rate.

## Activation

Place `low_do_mort_input.csv` in the model run directory. CE-QUAL-W2 activates the feature when `ALG_O2LIM > 0.0`.

## How It Works

CE-QUAL-W2 tracks hypoxia in two steps:

**Step 1 -- Track low DO duration (every time step, every cell):**

At each cell (K,I), CE-QUAL-W2 checks whether the current DO concentration is at or below the threshold `ALG_O2LIM`. If so, a cumulative low-DO timer (`DELT_LOW_DO`) accumulates. If DO rises above the threshold, the timer resets to zero. The entire tracking step is guarded by `ALG_O2LIM > 0.0`, so CE-QUAL-W2 performs no work when the feature is disabled.

The implementation uses a branchless multiplicative approach with the Fortran `SIGN` intrinsic:

```
IF (ALG_O2LIM > 0.0) THEN                                        ! feature enabled guard
    DO4(K,I) = (1.0 + SIGN(1.0, ALG_O2LIM - O2(K,I))) * 0.5     ! 1.0 if DO <= threshold, 0.0 if DO > threshold
ELSE
    DO4(K,I) = 0.0                                                ! feature disabled
END IF
DELT_LOW_DO(K,I) = (DELT_LOW_DO(K,I) + DLT) * DO4(K,I)          ! accumulate or reset timer
```

When `DO4 = 1.0` (DO at or below threshold), the timer accumulates normally. When `DO4 = 0.0` (DO above threshold or feature disabled), the entire expression evaluates to zero, providing an automatic reset without a separate branch. Note that at equality (`O2 = ALG_O2LIM`), `SIGN(1.0, 0.0)` returns `+1.0`, so accumulation continues -- the boundary condition is `<=`.

**Step 2 -- Override mortality rate (per algal group):**

For each algal group JA, CE-QUAL-W2 first computes the normal mortality rate `AMR(K,I,JA)`. If the cumulative low-DO duration at that cell exceeds the group-specific critical time `CRIT_T(JA)`, CE-QUAL-W2 replaces the normal mortality rate with the elevated rate `AM_LOW_DO(JA)`:

```
AMR(K,I,JA) = (ATRMR(K,I,JA) + 1.0 - ATRMF(K,I,JA)) * AM(JA)       ! normal mortality
IF (DELT_LOW_DO(K,I) > CRIT_T(JA)) AMR(K,I,JA) = AM_LOW_DO(JA)      ! override with elevated rate
```

Note that `AM_LOW_DO` is a **replacement** mortality rate (d⁻¹), not a multiplier applied to the existing rate.

## Parameters

| Parameter | Units | Per-group? | Description |
|-----------|-------|------------|-------------|
| `ALG_O2LIM` | mg L⁻¹ | No (scalar) | DO concentration threshold. CE-QUAL-W2 considers cells with DO at or below this value to be hypoxic. |
| `ALG_MIN` | mg L⁻¹ | No (scalar) | Minimum algae seed concentration (see [Chapter 1](/hab-modeling/minimum-algae/)). |
| `CRIT_T(JA)` | days | Yes (one per algal group) | Duration that DO must remain at or below `ALG_O2LIM` before CE-QUAL-W2 activates elevated mortality for that group. |
| `AM_LOW_DO(JA)` | d⁻¹ | Yes (one per algal group) | Elevated mortality rate that CE-QUAL-W2 applies when the critical duration is exceeded. |

## Input File: `low_do_mort_input.csv`

### Field Descriptions

| Line | Content |
|------|---------|
| 1 | Header (skipped) |
| 2 | Description (skipped) |
| 3 | `ALG_O2LIM, ALG_MIN` -- two comma-separated values |
| 4 | Description (skipped) |
| 5 | `CRIT_T(1), CRIT_T(2), ... CRIT_T(NAL)` -- one value per algal group, in **days** |
| 6 | Description (skipped) |
| 7 | `AM_LOW_DO(1), AM_LOW_DO(2), ... AM_LOW_DO(NAL)` -- one value per algal group, in **d⁻¹** |

The number of values on lines 5 and 7 must equal `NAL` (the number of algal groups defined in the main control file).

**Unit conversions (automatic):** CE-QUAL-W2 converts `CRIT_T` from days to seconds internally by multiplying by `DAY` (86400.0). CE-QUAL-W2 converts `AM_LOW_DO` from d⁻¹ to s⁻¹ internally by dividing by `DAY`.

### Example File Listing

```
Low DO - High Mortality and Minimum Algae Option Input File
ALG_O2LIM (mg/L) - DO threshold,  ALG_MIN (mg/L) - minimum algae seed concentration
2.0, 0.01
CRIT_T - Critical low-DO duration per algal group (days). One value per algal group (NAL).
5.0, 3.0, 7.0
AM_LOW_DO - Elevated mortality rate per algal group (1/day). One value per algal group (NAL).
0.5, 0.8, 0.3
```

In this example with 3 algal groups:

- `ALG_O2LIM = 2.0` mg L⁻¹ -- CE-QUAL-W2 considers cells with DO at or below 2.0 mg L⁻¹ to be hypoxic
- `ALG_MIN = 0.01` mg L⁻¹ -- CE-QUAL-W2 maintains algal concentrations at or above this floor
- Group 1: CE-QUAL-W2 increases mortality to 0.5 d⁻¹ after 5 days of continuous hypoxia
- Group 2: CE-QUAL-W2 increases mortality to 0.8 d⁻¹ after 3 days of continuous hypoxia
- Group 3: CE-QUAL-W2 increases mortality to 0.3 d⁻¹ after 7 days of continuous hypoxia

## Source Code References

- **Read input:** `input.F90` ~lines 2307--2325 -- CE-QUAL-W2 initializes `DELT_LOW_DO`, `ALG_O2LIM`, and `ALG_MIN` to zero, then checks whether `low_do_mort_input.csv` exists. If the file is present, CE-QUAL-W2 reads `ALG_O2LIM` and `ALG_MIN` on line 2317, reads `CRIT_T(JA)` for each algal group on line 2319, and reads `AM_LOW_DO(JA)` for each algal group on line 2321. Lines 2323--2324 convert the input units: `AM_LOW_DO` is divided by `DAY` (86400.0) to convert from d⁻¹ to s⁻¹, and `CRIT_T` is multiplied by `DAY` to convert from days to seconds. If the file is absent, all values remain at zero and the feature is inactive.

- **DO tracking:** `water-quality.f90` ~lines 300--305 -- Line 300 checks whether `ALG_O2LIM > 0.0` to determine if the feature is active. Line 301 computes `DO4(K,I)` using the Fortran `SIGN` intrinsic: `DO4(K,I) = (1.0 + SIGN(1.0, ALG_O2LIM - O2(K,I))) * 0.5`, which yields 1.0 when DO is at or below the threshold and 0.0 when DO is above it. If the feature is inactive, line 303 sets `DO4(K,I) = 0.0`. Line 305 accumulates the low-DO timer: `DELT_LOW_DO(K,I) = (DELT_LOW_DO(K,I) + DLT) * DO4(K,I)`, which adds the current time step when `DO4 = 1.0` or resets the timer to zero when `DO4 = 0.0`.

- **Mortality override:** `water-quality.f90` ~line 702 -- After CE-QUAL-W2 computes the normal mortality rate `AMR(K,I,JA)` on line 701, line 702 checks whether the accumulated low-DO duration exceeds the critical time for that algal group: `IF(DELT_LOW_DO(K,I) > CRIT_T(JA)) AMR(K,I,JA) = AM_LOW_DO(JA)`. If the condition is true, CE-QUAL-W2 replaces the normal mortality rate with the elevated rate.

{% include section-nav-bottom.html section="hab-users-manual" %}

