---
layout: default
title: "Low DO Mortality - User Manual"
permalink: /hab-modeling/low-do-mortality/
---

{% include section-nav.html section="hab-users-manual" %}

# Chapter 2: Low DO Mortality (Hypoxic Conditions)

## Purpose

Simulates enhanced algal die-off under prolonged low dissolved oxygen (hypoxic) conditions. When DO drops below a threshold and stays low for longer than a critical duration, algal mortality rates are elevated.

## Activation

Place `low_do_mort_input.csv` in the model run directory. The feature activates when `ALG_O2LIM > 0.0`.

## How It Works

The model tracks hypoxia in two steps:

**Step 1 -- Track low DO duration (every time step, every cell):**

At each cell (K,I), the model checks whether current DO is at or below the threshold `ALG_O2LIM`. If yes, a cumulative low-DO timer (`DELT_LOW_DO`) accumulates. If DO rises above the threshold, the timer resets to zero. The entire tracking step is guarded by `ALG_O2LIM > 0.0`, so no work is done when the feature is disabled.

The implementation uses a branchless multiplicative approach:

```
IF ALG_O2LIM > 0.0 THEN                              ! feature enabled guard
    DO4 = 0.0                                          ! default: will reset
    IF DO(K,I) <= ALG_O2LIM THEN DO4 = 1.0            ! low DO: will accumulate
    DELT_LOW_DO(K,I) = (DELT_LOW_DO(K,I) + DLT) * DO4
END IF
```

When `DO4 = 1.0` (DO at or below threshold), the timer accumulates normally. When `DO4 = 0.0` (DO above threshold), the entire expression evaluates to zero, providing an automatic reset without a separate branch. Note that at equality (`DO = ALG_O2LIM`), accumulation continues -- the boundary condition is `<=`.

**Step 2 -- Override mortality rate (per algal group):**

For each algal group JA, if the cumulative low-DO duration exceeds the group-specific critical time `CRIT_T(JA)`, the normal mortality rate is replaced by the elevated rate `AM_LOW_DO(JA)`:

```
IF DELT_LOW_DO(K,I) > CRIT_T(JA) THEN
    mortality(K,I,JA) = AM_LOW_DO(JA)
END IF
```

Note that `AM_LOW_DO` is a **replacement** mortality rate (d⁻¹), not a multiplier applied to the existing rate.

## Parameters

| Parameter | Units | Per-group? | Description |
|-----------|-------|------------|-------------|
| `ALG_O2LIM` | mg L⁻¹ | No (scalar) | DO concentration threshold. Cells with DO at or below this are considered hypoxic. |
| `ALG_MIN` | mg L⁻¹ | No (scalar) | Minimum algae seed concentration (see [Chapter 1](/hab-modeling/minimum-algae/)). |
| `CRIT_T(JA)` | days | Yes (one per algal group) | How long DO must remain at or below `ALG_O2LIM` before elevated mortality activates. |
| `AM_LOW_DO(JA)` | d⁻¹ | Yes (one per algal group) | Elevated mortality rate applied when the critical duration is exceeded. |

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

**Unit conversions (automatic):** `CRIT_T` is converted from days to seconds internally. `AM_LOW_DO` is converted from d⁻¹ to s⁻¹ internally.

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

- `ALG_O2LIM = 2.0` mg L⁻¹ -- cells with DO at or below 2.0 mg L⁻¹ are considered hypoxic
- `ALG_MIN = 0.01` mg L⁻¹ -- algal concentrations are maintained at or above this floor
- Group 1: mortality increases to 0.5 d⁻¹ after 5 days of continuous hypoxia
- Group 2: mortality increases to 0.8 d⁻¹ after 3 days of continuous hypoxia
- Group 3: mortality increases to 0.3 d⁻¹ after 7 days of continuous hypoxia

## Source Code References

- Read: `input.F90` ~lines 2307-2325
- DO tracking: `water-quality.f90` ~lines 302-307
- Mortality override: `water-quality.f90` ~line 704


