---
layout: default
title: "Nitrogen Fixation"
permalink: /hab-modeling/nitrogen-fixation/
---

{% include section-nav.html section="hab-users-manual" %}

# Chapter 4: Nitrogen Fixation

## Purpose

Simulates the ability of certain algal groups (e.g., cyanobacteria) to fix atmospheric nitrogen (N₂) when dissolved inorganic nitrogen becomes scarce. When total inorganic nitrogen (TIN = NH₄ + NO₃) drops below a critical threshold, the algal group switches to N-fixation: nitrogen limitation is removed and the group stops consuming NH₄ and NO₃ from the water column.

## Activation

Place `nfix_option_input.csv` in the model run directory. Set `CRIT_TIN(JA) > 0` for any algal group that can fix nitrogen. Groups with `CRIT_TIN = 0.0` do not fix nitrogen.

## How It Works

The feature modifies three calculations in the water quality kinetics:

1. **Nitrogen limitation** -- When `NH₄ + NO₃ < CRIT_TIN(JA)`, the nitrogen half-saturation constant (`AHSN`) is set to zero, making the nitrogen limitation factor approach 1.0 (no limitation). The algae grow as if nitrogen were abundant. There is no growth reduction factor.
2. **NH₄ uptake** -- When N-fixation is active for a group, that group's ammonium uptake from the water is suppressed. The algae are assumed to obtain nitrogen from the atmosphere instead.
3. **NO₃ uptake** -- Similarly, nitrate uptake from the water is suppressed during N-fixation.

When TIN rises back above `CRIT_TIN(JA)`, the group returns to normal nitrogen-limited growth and resumes consuming NH₄/NO₃ from the water.

## Parameters

| Parameter      | Units  | Per-group?                | Description                                                                                       |
| -------------- | ------ | ------------------------- | ------------------------------------------------------------------------------------------------- |
| `CRIT_TIN(JA)` | mg L⁻¹ | Yes (one per algal group) | TIN threshold below which N-fixation activates. Set to `0.0` for groups that cannot fix nitrogen. |

## Input File: `nfix_option_input.csv`

### Field Descriptions

| Line | Content                                                                                   |
| ---- | ----------------------------------------------------------------------------------------- |
| 1    | Header (skipped)                                                                          |
| 2    | Description (skipped)                                                                     |
| 3    | `CRIT_TIN(1), CRIT_TIN(2), ... CRIT_TIN(NAL)` -- one value per algal group, in **mg L⁻¹** |

The number of values must equal `NAL` (the number of algal groups defined in the main control file).

### Example File Listing

```
Nitrogen Fixation Option Input File
CRIT_TIN - Critical TIN (NH4+NO3) concentration per algal group (mg/L). One value per algal group (NAL). Set to 0.0 for groups that do not fix nitrogen.
0.0, 0.0, 0.05
```

In this example with 3 algal groups, only group 3 (e.g., _Aphanizominon_) fixes nitrogen, with a threshold of 0.05 mg L⁻¹. When ambient NH₄ + NO₃ drops below 0.05 mg L⁻¹, group 3 switches to N-fixation. Groups 1 and 2 have `CRIT_TIN = 0.0` and never fix nitrogen.

## Source Code References

- **Read input:** `input.F90` ~lines 2329–2336 -- Checks whether `nfix_option_input.csv` exists; if so, reads `CRIT_TIN(JA)` for each algal group. If the file is absent, `CRIT_TIN` defaults to 0.0 for all groups and the feature is inactive.
- **N-limitation override:** `water-quality.f90` ~lines 691–694 -- Line 691 computes the normal Monod nitrogen limitation factor: `ANLIM = TIN / (TIN + AHSN)`. Lines 692–694 then check for the N-fixation condition: if `TIN < CRIT_TIN(JA)`, the limitation factor is recalculated with `AHSN` replaced by zero, yielding `ANLIM = TIN / (TIN + 0.0 + NONZERO)` ≈ 1.0. This effectively removes nitrogen limitation for that algal group, allowing it to grow as if nitrogen were abundant.
- **NH₄ uptake suppression:** `water-quality.f90` ~line 1505 -- The original code accumulated algal ammonium uptake whenever `AHSN > 0`. The N-fixation modification adds a second condition: uptake is only accumulated when `CRIT_TIN(JA) < TIN` (i.e., TIN is above the threshold). When TIN drops below `CRIT_TIN(JA)`, the condition fails, and the group's NH₄ uptake term is skipped entirely -- the algae obtain their nitrogen from atmospheric N₂ rather than from the water column.
- **NO₃ uptake suppression:** `water-quality.f90` ~line 1579 -- Identical logic to the NH₄ case. The original nitrate uptake accumulation (`NO3AG`) is conditioned on both `AHSN > 0` and `CRIT_TIN(JA) < TIN`. When N-fixation is active (TIN below the threshold), the group's NO₃ uptake is suppressed.

{% include section-nav-bottom.html section="hab-users-manual" %}
