---
layout: default
title: HAB Modeling - CE-QUAL-W2
permalink: /hab-modeling/
---

# Harmful Algal Bloom (HAB) Modeling

This section provides user guidance for the HAB simulation capabilities implemented in CE-QUAL-W2 Version 4.5. These enhancements extend the model's ability to simulate cyanobacteria population dynamics and evaluate management interventions for HAB control.

## New HAB Capabilities

Four capabilities have been added to CE-QUAL-W2:

| Enhancement | Description |
|-------------|-------------|
| **[Nitrogen Fixation (CE-2)](nitrogen-fixation/)** | Enables designated algal groups to access atmospheric nitrogen when dissolved inorganic nitrogen concentrations fall below a user-specified threshold |
| **[Hypoxic Mortality (CE-3)](hypoxic-mortality/)** | Increases algal mortality rates when dissolved oxygen concentrations remain below a critical level for a specified duration |
| **[Minimum Algae Concentration (CE-4)](minimum-algae/)** | Maintains a seed population of algae to enable regrowth after bloom collapse or seasonal die-off |
| **[Algal Harvesting (CE-5)](algal-harvesting/)** | Simulates mechanical removal of algae from specified model segments at user-defined times and removal efficiencies |

Each capability is implemented as an optional feature activated through external input files, preserving backward compatibility with existing CE-QUAL-W2 applications.

## Documentation

### User Guide Chapters

- [Chapter 1: Introduction](introduction/) - Purpose, background, and document organization
- [Chapter 2: Nitrogen Fixation (CE-2)](nitrogen-fixation/) - Input files, parameters, and examples
- [Chapter 3: Hypoxic Mortality (CE-3)](hypoxic-mortality/) - Low DO mortality implementation
- [Chapter 4: Minimum Algae Concentration (CE-4)](minimum-algae/) - Seed population maintenance
- [Chapter 5: Algal Harvesting (CE-5)](algal-harvesting/) - Mechanical removal simulation
- [Chapter 6: Conclusions](conclusions/) - Summary and recommendations

### Appendices

- [Appendix A: Mathematical Derivations](appendix-math/) - Detailed equations and notation
- [Appendix B: Input File Templates](appendix-templates/) - Complete file templates
- [Appendix C: Case Study](appendix-case-study/) - Sierra Vista Reservoir demonstration

## Operations Guidance

For guidance on using CE-QUAL-W2 to evaluate HAB management strategies, see:

**[Operations Guidance: Evaluating HAB Management Strategies](operations-guidance/)**

Covers 15+ operational and treatment approaches including:

- **Hydrodynamic controls** - withdrawals, pulsed inflows, water level management
- **Mixing and aeration** - destratification, hypolimnetic aeration
- **Chemical treatments** - phosphorus inactivation (alum), algaecides
- **Biological approaches** - biomanipulation, algal harvesting, floating wetlands
- **Model setup guidance** - calibration, validation, uncertainty analysis

## Download

[Download CE-QUAL-W2 V4.5 with New HAB Capabilities](/downloads/#hab-version)

## Quick Start

1. Download the HAB-enabled CE-QUAL-W2 executable
2. Create the appropriate input files for the capabilities you want to use:
   - `nfix_option_input.csv` for nitrogen fixation
   - `low_do_mort_input.csv` for hypoxic mortality and minimum algae
   - `harvest_option_input.csv` for algal harvesting
3. Place input files in the model run directory alongside `w2_con.npt`
4. Run the model - features are automatically enabled when their input files are present

---

*Based on ERDC Technical Report documenting HAB simulation capabilities for CE-QUAL-W2 Version 4.5*
