---
layout: default
title: "Quick Start Guide - User Manual"
permalink: /hab-modeling/quick-start/
---

# Quick Start Guide

To enable any combination of HAB features, copy the relevant CSV file(s) into your model run directory (the same directory containing `w2_con.npt` or `w2_con.csv`):

| To enable... | Copy these files to the run directory |
|--------------|---------------------------------------|
| Minimum algae only | `low_do_mort_input.csv` (set `ALG_O2LIM = 0.0`, set `ALG_MIN` to desired seed value) |
| Low DO mortality only | `low_do_mort_input.csv` (set `ALG_MIN = 0.0` if no seed needed) |
| Both minimum algae and low DO mortality | `low_do_mort_input.csv` (set both `ALG_O2LIM > 0` and `ALG_MIN > 0`) |
| Nitrogen fixation | `nfix_option_input.csv` |
| Algal harvesting | `harvest_option_input.csv` + the time-series file named inside it |
| All features | All three CSV files + the harvest time-series file |

To disable a feature, simply remove (or rename) its input file from the run directory. No changes to the main control file are needed.

## Important Notes

- The number of values in per-algal-group arrays must match `NAL` as defined in the main control file.
- Algal harvesting and minimum algae interact: harvesting is applied first, then the `ALG_MIN` floor is enforced. Algae will not be harvested below the seed concentration.
- All features are independent and can be used in any combination.
- `ALG_MIN` is a single scalar value applied uniformly to all algal groups -- it cannot vary by group.
- `AM_LOW_DO` is a replacement mortality rate (d⁻¹), not a multiplier applied to the existing rate.
- `FHA` is an instantaneous fractional removal, not a per-day rate. Values are automatically clamped to [0, 1].
- The first data row of the harvest time-series file is loaded at initialization. Include a leading row with `FHA = 0.0` if harvesting should not start at the first timestep.

## Chapter Reference

| Chapter | Feature |
|---------|---------|
| [1. Minimum Algae](/hab-modeling/minimum-algae/) | Seed population floor |
| [2. Low DO Mortality](/hab-modeling/low-do-mortality/) | Hypoxic mortality override |
| [3. Algal Harvesting](/hab-modeling/algal-harvesting/) | Scheduled algal removal |
| [4. Nitrogen Fixation](/hab-modeling/nitrogen-fixation/) | Atmospheric N₂ fixation |

---

[Previous: Chapter 4 - Low DO Mortality](/hab-modeling/low-do-mortality/) | [User Manual Overview](/hab-modeling/)

