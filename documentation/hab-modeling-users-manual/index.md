---
layout: default
title: "HAB Features User Manual"
permalink: /hab-modeling/
---

# CE-QUAL-W2 HAB Features User's Manual

## Overview

ERDC's CE-QUAL-W2 Version 2026.02 (based on PSU's Version 4.5 of CE-QUAL-W2) includes four new capabilities for Harmful Algal Bloom (HAB) simulation:

1. **Nitrogen Fixation** -- allows selected algal groups to fix atmospheric N₂ when inorganic nitrogen is depleted
2. **Algal Harvesting** -- removes a fraction of algae from specified segments on a time-varying schedule
3. **Minimum Algae (Seed Population)** -- maintains a floor concentration so algae can regrow after crash events
4. **Low DO Mortality** -- increases algal mortality when dissolved oxygen stays low for an extended period

All four features use **file-existence-based activation**. None are controlled by settings in the main control file (`w2_con.npt` or `w2_con.csv`). Instead, each feature has its own dedicated CSV input file. If the file is present in the model run directory, the feature is active. If absent, the feature is off.

## Chapters

| Chapter | Feature | Input File(s) |
|---------|---------|----------------|
| [1. Nitrogen Fixation](nitrogen-fixation/) | Atmospheric N₂ fixation when TIN is depleted | `nfix_option_input.csv` |
| [2. Algal Harvesting](algal-harvesting/) | Time-scheduled removal of algae from segments | `harvest_option_input.csv` + time-series file |
| [3. Minimum Algae (Seed Population)](minimum-algae/) | Maintains a floor algal concentration | `low_do_mort_input.csv` (shared) |
| [4. Low DO Mortality](low-do-mortality/) | Elevated mortality under prolonged hypoxia | `low_do_mort_input.csv` |
| [Quick Start Guide](quick-start/) | Setup instructions and important notes | -- |

## Feature Summary

| Feature | Input File | Activation Condition |
|---------|-----------|----------------------|
| Minimum algae + Low DO mortality | `low_do_mort_input.csv` | File exists in run directory |
| Nitrogen fixation | `nfix_option_input.csv` | File exists in run directory |
| Algal harvesting | `harvest_option_input.csv` + time-series file | File exists and `NHF > 0` |

To disable any feature, remove (or rename) its input file from the run directory. No changes to the main control file are needed.

---
