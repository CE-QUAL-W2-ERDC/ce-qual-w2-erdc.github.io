---
layout: default
title: "Quick Start Guide - User Manual"
permalink: /hab-modeling/quick-start/
---

{% include section-nav.html section="hab-users-manual" %}

# Quick Start Guide

To enable any combination of HAB features, copy the relevant CSV file(s) into the model run directory (the same directory containing `w2_con.npt` or `w2_con.csv`):

| To enable... | Copy these files to the run directory |
|--------------|---------------------------------------|
| Nitrogen fixation | `nfix_option_input.csv` |
| Algal harvesting | `harvest_option_input.csv` + the time-series file named inside it |
| Minimum algae only | `low_do_mort_input.csv` (set `ALG_O2LIM = 0.0`, set `ALG_MIN` to desired seed value) |
| Low DO mortality only | `low_do_mort_input.csv` (set `ALG_MIN = 0.0` if no seed needed) |
| Both minimum algae and low DO mortality | `low_do_mort_input.csv` (set both `ALG_O2LIM > 0` and `ALG_MIN > 0`) |
| All features | All three CSV files + the harvest time-series file |

To disable a feature, remove (or rename) its input file from the run directory. No changes to the main control file are needed.

## Important Notes

- The number of values in each per-algal-group array must match `NAL` as defined in the main control file.
- Algal harvesting and minimum algae interact: CE-QUAL-W2 applies harvesting first, then enforces the `ALG_MIN` floor. The model will not harvest algae below the seed concentration.
- All features are independent and can be used in any combination.
- `ALG_MIN` is a single scalar value that CE-QUAL-W2 applies uniformly to all algal groups -- it cannot vary by group.
- `AM_LOW_DO` is a replacement mortality rate (d⁻¹), not a multiplier applied to the existing rate.
- `FHA` is an instantaneous fractional removal, not a per-day rate. CE-QUAL-W2 automatically clamps values to [0, 1].
- CE-QUAL-W2 loads the first data row of the harvest time-series file at initialization. Include a leading row with `FHA = 0.0` if harvesting should not start at the first timestep.

## Chapter Reference

| Chapter | Feature |
|---------|---------|
| [1. Nitrogen Fixation](/hab-modeling/nitrogen-fixation/) | Atmospheric N₂ fixation |
| [2. Algal Harvesting](/hab-modeling/algal-harvesting/) | Scheduled algal removal |
| [3. Minimum Algae](/hab-modeling/minimum-algae/) | Seed population floor |
| [4. Low DO Mortality](/hab-modeling/low-do-mortality/) | Hypoxic mortality override |

{% include section-nav-bottom.html section="hab-users-manual" %}


