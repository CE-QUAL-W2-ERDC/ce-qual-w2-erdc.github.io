---
layout: default
title: Documentation - CE-QUAL-W2
---

# CE-QUAL-W2 Documentation

## User Manual Version 4.5

The CE-QUAL-W2 User Manual is organized into five comprehensive parts covering all aspects of model theory, application, and utilities. Each part is available as a PDF download.

### Part 1: Introduction

[Download PDF](W2manual45_Part1_Intro_rev9.pdf) (1.6 MB)

- Model overview, terminology, and history
- Capabilities and limitations
- New features and planned enhancements
- Overview of data preparation requirements
- How to download, set up, and run the model
- Batch processing and command line usage
- Contributors and selected publications list

### Part 2: Theory

[Download PDF](W2manual45_Part2_Theory_rev8.pdf) (4.8 MB)

- Governing equations and lateral averaging
- Hydrodynamic algorithms and turbulence formulations
- Hydraulic structures (pipes, weirs, spillways, gates)
- Particle tracking algorithm
- Heat exchange, dynamic shading, and ice cover
- Water quality kinetics for 30+ constituents:
  - Algae, zooplankton, and macrophytes
  - Nutrients (phosphorus, nitrogen, silica)
  - Dissolved oxygen and reaeration
  - Organic matter (DOM, POM, CBOD)
  - Metals (iron, manganese) and pH/alkalinity
- Sediment diagenesis modeling
- Numerical solution techniques (QUICKEST/ULTIMATE schemes)

### Part 3: Input/Output Files

[Download PDF](W2manual45_Part3_InputOutputFiles_rev8.pdf) (15 MB)

- Control file parameters (grid, timestep, heat exchange, ice, transport, structures, kinetics)
- Bathymetry file formats (fixed and CSV)
- Meteorological, shading, and light extinction files
- Boundary conditions (inflows, tributaries, precipitation, external heads)
- Hydraulic structure operations (pipes, spillways, gates, pumps)
- Sediment diagenesis and SYSTDG (dissolved gas) input files
- Fish habitat volumes and environmental performance criteria
- Output formats (snapshots, time series, profiles, contour plots, fluxes)
- Particle transport configuration
- Multi-processor setup for cascaded waterbodies
- Preprocessor output, warnings, and error messages

### Part 4: Model Examples

[Download PDF](W2manual45_Part4_ModelExamples_rev3.pdf) (8.5 MB)

- Example applications distributed with model release:
  - Columbia Slough Estuary
  - DeGray Reservoir (sediment diagenesis, algae migration)
  - Detroit Lake and Long Lake/Spokane Lake
  - Spokane River
  - Multiple waterbody cascade
  - Particle tracking and SysTDG examples
- Calibration guidance by waterbody type:
  - Lakes/reservoirs: water budget, hydrodynamics, temperature, water quality
  - Estuaries: boundary conditions, tides, salinity
  - Rivers: channel slope, bottom roughness, temperature

### Part 5: Model Utilities

[Download PDF](W2manual45_Part5_ModelUtilities_rev9.pdf) (3.7 MB)

- Water balance utility (GUI and console versions)
- Control file converter
- GUI interface for control file and bathymetry editing
- Post-processor for output analysis (DSI, Inc.)
- Excel macro utility
- Frequently asked questions
- Known code limitations
- Version history and differences (v3.1 through v4.5)
- Bug fixes and enhancements by version

## Quick Reference Guides

### Model Setup Checklist

1. Define model domain and segmentation
2. Prepare bathymetry file
3. Set up control file parameters
4. Prepare meteorological data
5. Define initial conditions
6. Set boundary conditions
7. Configure water quality (if needed)
8. Run model and review outputs

### Common Applications

| Application | Key Processes | Required Data |
|------------|--------------|---------------|
| **Reservoir Stratification** | Temperature, density, mixing | Bathymetry, meteorology, inflows |
| **River Temperature** | Heat exchange, advection | Flow, meteorology, shading |
| **Eutrophication** | Nutrients, algae, DO | Loads, light, temperature |
| **Selective Withdrawal** | Stratification, outlet dynamics | Operations, temperature profiles |
| **Water Age/Residence Time** | Transport, mixing | Flows, bathymetry |

## Additional Resources

### Training Materials

- [Workshop Presentations](/publications/)

### Technical Support

- [Frequently Asked Questions](/support/#faq)

### Related Publications

- [Peer-reviewed Papers](/publications/)
- [Technical Reports](/publications/#reports)
- [Conference Proceedings](/publications/#conferences)

*Last updated: February 2026*
