---
layout: default
title: Downloads - CE-QUAL-W2
permalink: /downloads/
---

# Downloads

## CE-QUAL-W2

### Model Versions

CE-QUAL-W2 is available in two versions:

| Version                                     | Description                                                                                                                                           | Status |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| ERDC Version 2026 with New HAB Capabilities | Based on PSU v4.5, ERDC v2006 adds nitrogen fixation, algal harvesting, minimum algae concentration, and mortality associated with hypoxic conditions | Stable |
| PSU Version 4.5                             | Standard release with ongoing development by Portland State University                                                                                | Active |

Both versions share the same preprocessor and input file formats. See [HAB Modeling](/hab-modeling/) for details on the new capabilities.

### Model Executables

Download the appropriate executable for your operating system:

| Platform | Version | Download                                                      | Size   | Requirements           |
| -------- | ------- | ------------------------------------------------------------- | ------ | ---------------------- |
| Windows  | v2006   | [w2_v2006.02_win64.exe](executables/w2_v2006_windows_x64.exe) | 9.5 MB | Windows 10/11 (64-bit) |
| Linux    | v2006   | [w2_v2006.02_macOS](executables/w2_v2006.02_macOS)            | 9.5 MB | gfortran libraries     |
| macOS    | v2006   | [w2_v2006.02_macOS](executables/w2_v2006.02_linux)            | 9.5    | macOS 26.1+            |
| Windows  | v4.5    | [w2_v45_win64.exe](executables/w2_v45_64.exe)                 | 6.5 MB | Windows 10/11 (64-bit) |

**Note:** ERDC v2006 has new capabilities for Harmful Algal Bloom (HAB) simulations.

### Pre-Processor Executables

Download the appropriate executable for your operating system:

| Platform    | Version | Download                                         | Size   | Requirements           |
| ----------- | ------- | ------------------------------------------------ | ------ | ---------------------- |
| **Windows** | v4.5    | [preW2-v45_64.exe](executables/preW2-v45_64.exe) | 9.6 MB | Windows 10/11 (64-bit) |

### Source Code

| Item                     |                                                            |
| ------------------------ | ---------------------------------------------------------- |
| CE-QUAL-W2 model         | [w2source_7_7_2025.zip](src/w2source_7_7_2025.zip)         |
| CE-QUAL-W2 pre-processor | [PreW2_source_July2025.zip](src/PreW2_source_July2025.zip) |

### Documentation

| Document                   | Description                 | Download                                                             |
| -------------------------- | --------------------------- | -------------------------------------------------------------------- |
| **Part 1: Introduction**   | Getting started guide       | [Download](documentation/W2manual45_Part1_Intro_rev6.pdf)            |
| **Part 2: Theory**         | Model theory and equations  | [Download](documentation/W2manual45_Part2_Theory_rev6.pdf)           |
| **Part 3: Input/Output**   | File formats and parameters | [Download](documentation/W2manual45_Part3_InputOutputFiles_rev6.pdf) |
| **Part 4: Examples**       | Tutorial and test cases     | [Download](documentation/W2manual45_Part4_ModelExamples_rev3.pdf)    |
| **Part 5: Utilities**      | Tools and preprocessors     | [Download](documentation/W2manual45_Part5_ModelUtilities_rev6.pdf)   |

### Example Applications

| Example                     | Description                      | Files                                                                                                                                                             |
| --------------------------- | -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bonneville Dam              | TDG Modeling                     | [Bonneville_Dam_with_TDG_computed_using_SYSTDG.zip](examples/Bonneville_Dam_with_TDG_computed_using_SYSTDG.zip)                                                   |
| Columbia Slough Estuary     | Temperature modeling             | [Columbia_Slough_Estuary.zip](examples/Columbia Slough Estuary.zip)                                                                                               |
| DeGray Reservoir            | Stratification and water quality | [DeGray_Reservoir_with_sediment_diagenesis_and_vertical_algae_migration.zip](examples/DeGray_Reservoir_with_sediment_diagenesis_and_vertical_algae_migration.zip) |
| Detroit Lake                | Stratification and water quality | [Detroit_Lake.zip](examples/Detroit_Lake.zip)                                                                                                                     |
| Long Lake                   | Stratification and water quality | [Long_Lake.zip](examples/Long_Lake.zip)                                                                                                                           |
| Multiple Water Body Cascade | Stratification and water quality | [MultipleWaterBodyCascade.zip](examples/Multiple_Water_Body_Cascade.zip)                                                                                          |
| Particle Tracking           | Particle Tracking                | [Particle_Tracking_in_Reservoirs.zip](examples/Particle_Tracking_in_Reservoirs.zip)                                                                               |
| Spokane River               | Stratification and water quality | [Spokane_River.zip](examples/Spokane_River.zip)                                                                                                                   |

## Installation Instructions

### Windows

1. Download the Windows executable
2. Extract to your desired directory (e.g., `C:\CE-QUAL-W2`)
3. Add the directory to your system PATH (optional)
4. Test installation by running `w2_v45_win64.exe` from command prompt

## System Requirements

### Minimum Requirements

- **Processor**: Intel/AMD x86-64
- **RAM**: 8 GB (16 GB recommended)
- **Storage**: 500 MB for program files
- **OS**: Windows 10/11

### Recommended for Large Models

- **RAM**: 32 GB or more
- **Processor**: Multi-core for parallel processing
- **Storage**: SSD for faster I/O operations

## Credit

Please cite CE-QUAL-W2 in publications as:

> Cole, T.M., and Wells, S.A. (2025). "CE-QUAL-W2: A Two-Dimensional, Laterally Averaged, Hydrodynamic and Water Quality Model, Version 4.5."

*Last updated: February 2026*