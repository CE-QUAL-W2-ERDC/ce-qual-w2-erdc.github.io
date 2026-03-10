---
layout: default
title: "CE-QUAL-W2 Harmful Algal Bloom Modeling User's Manual"
permalink: /hab-modeling/
---

# CE-QUAL-W2 Harmful Algal Bloom User's Manual

## Overview

ERDC's CE-QUAL-W2 Version 2026.02 (based on PSU's Version 4.5 of CE-QUAL-W2) includes four new capabilities for Harmful Algal Bloom (HAB) simulation:

1. **Nitrogen Fixation** -- the model allows selected algal groups to fix atmospheric N₂ when inorganic nitrogen is depleted
2. **Algal Harvesting** -- the model removes a fraction of algae from specified segments on a time-varying schedule
3. **Minimum Algae Concentration** -- the model maintains a floor concentration (seed population) so algae can regrow after crash events
4. **Low DO Mortality** -- the model increases algal mortality when dissolved oxygen stays low for an extended period

All four features use **file-existence-based activation**. None of these features are controlled by settings in the main control file (`w2_con.npt` or `w2_con.csv`). Instead, each feature has its own dedicated CSV input file. If the file is present in the model run directory, CE-QUAL-W2 activates the feature. If the file is absent, the feature is off.

## Chapters

| Chapter                                              | Feature                                       | Input File(s)                                 |
| ---------------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| [1. Nitrogen Fixation](nitrogen-fixation/)           | Atmospheric N₂ fixation when TIN is depleted  | `nfix_option_input.csv`                       |
| [2. Algal Harvesting](algal-harvesting/)             | Time-scheduled removal of algae from segments | `harvest_option_input.csv` + time-series file |
| [3. Minimum Algae (Seed Population)](minimum-algae/) | Floor algal concentration maintained by model  | `low_do_mort_input.csv` (shared)              |
| [4. Low DO Mortality](low-do-mortality/)             | Elevated mortality under prolonged hypoxia    | `low_do_mort_input.csv`                       |
| [Quick Start Guide](quick-start/)                    | Setup instructions and important notes        | --                                            |

## Feature Summary

| Feature                          | Input File                                    | Activation Condition                          |
| -------------------------------- | --------------------------------------------- | --------------------------------------------- |
| Minimum algae + Low DO mortality | `low_do_mort_input.csv`                       | File exists in run directory                  |
| Nitrogen fixation                | `nfix_option_input.csv`                       | File exists in run directory                  |
| Algal harvesting                 | `harvest_option_input.csv` + time-series file | File exists and `NHF > 0`                     |

To disable any feature, remove (or rename) its input file from the run directory. You do not need to change the main control file.
