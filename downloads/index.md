---
layout: default
title: Downloads - CE-QUAL-W2
---

# Downloads

## CE-QUAL-W2

### Model Versions

CE-QUAL-W2 is available in two versions:

| Version                                     | Description                                                                                                                                           | Status |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| ERDC Version 2026 with New HAB Capabilities | Based on PSU's CE-QUAL-W2 v4.5, ERDC's CE-QUAL-W2 v2026 adds nitrogen fixation, algal harvesting, minimum algae concentration, and mortality associated with hypoxic conditions | Stable |
| PSU Version 4.5                             | Standard release with ongoing development by Portland State University                                                                                | Active |

Both versions share the same preprocessor and input file formats. See [HAB Modeling](/hab-modeling/) for details on the new capabilities.

### Model Executables

Download the appropriate executable for your operating system:

| Platform | Version    | Download                                                                                   | Size    | Requirements           |
| -------- | ---------- | ------------------------------------------------------------------------------------------ | ------- | ---------------------- |
| Windows  | ERDC v2026 | [w2_v2026.02_win64.exe](/executables/ERDC_CE-QUAL-W2_v2026.02/w2_2026.02_erdc_win_x64.exe) | 16.7 MB | Windows 10/11 (64-bit) |
| Linux    | ERDC v2026 | [w2_v2026.02_linux](/executables/ERDC_CE-QUAL-W2_v2026.02/w2_2026.02_erdc_linux)           | 10.8 MB | gfortran libraries     |
| macOS    | ERDC v2026 | [w2_v2026.02_macOS](/executables/ERDC_CE-QUAL-W2_v2026.02/w2_2026.02_erdc_macos)           | 10.8 MB | macOS 26.1+            |
| Windows  | PSU v4.5   | [w2_v45_win64.exe](/executables/PSU_CE-QUAL-W2_v45_x64/w2_v45_64.exe)                      | 6.5 MB  | Windows 10/11 (64-bit) |


**Note:** ERDC's CE-QUAL-W2 Version 2026 has new capabilities for Harmful Algal Bloom (HAB) simulations.

### Pre-Processor Executables

Download the appropriate executable for your operating system:

| Platform    | Version | Download                                          | Size   | Requirements           |
| ----------- | ------- | ------------------------------------------------- | ------ | ---------------------- |
| **Windows** | v4.5    | [preW2-v45_64.exe](/executables/PSU_CE-QUAL-W2_v45_x64/preW2-v45_64.exe) | 9.6 MB | Windows 10/11 (64-bit) |

### Source Code

| Item                             |                                                                                   |
| -------------------------------- | --------------------------------------------------------------------------------- |
| CE-QUAL-W2 model (ERDC v2026)   | [ERDC_CE-QUAL-W2_source_v2026.02.zip](/src/ERDC_CE-QUAL-W2_source_v2026.02.zip)   |
| CE-QUAL-W2 model (PSU v4.5)     | [PSU_CE-QUAL-W2_source_2025_07_07.zip](/src/PSU_CE-QUAL-W2_source_2025_07_07.zip) |
| CE-QUAL-W2 pre-processor         | [PreW2_source_July2025.zip](/src/PreW2_source_July2025.zip)                       |

### Documentation

The complete 5-part user manual (PDF) is available on the [Documentation](/documentation/) page.

### Example Applications

Downloadable model applications are available on the [Examples](/examples/) page.

## Installation Instructions

### Windows

1. Download the Windows executable (`w2_2026.02_erdc_win_x64.exe` or `w2_v45_64.exe`)
2. Place in your desired directory (e.g., `C:\CE-QUAL-W2`)
3. Add the directory to your system PATH (optional)
4. Test by running the executable from a command prompt

### Linux

1. Download `w2_2026.02_erdc_linux`
2. Make executable: `chmod +x w2_2026.02_erdc_linux`
3. Ensure gfortran runtime libraries are installed

### macOS

1. Download `w2_2026.02_erdc_macos`
2. Make executable: `chmod +x w2_2026.02_erdc_macos`
3. On first run, you may need to allow execution in System Settings > Privacy & Security

## System Requirements

### Minimum Requirements

- **Processor**: Intel/AMD x86-64
- **RAM**: 8 GB (16 GB recommended)
- **Storage**: 500 MB for program files
- **OS**: Windows 10/11, Linux, or macOS

### Recommended for Large Models

- **RAM**: 32 GB or more
- **Processor**: Multi-core for parallel processing
- **Storage**: SSD for faster I/O operations

## Credit

Please cite CE-QUAL-W2 in publications as:

> Cole, T.M., and Wells, S.A. (2023). "CE-QUAL-W2: A Two-Dimensional, Laterally Averaged, Hydrodynamic and Water Quality Model, Version 4.5." U.S. Army Engineer Research and Development Center, Vicksburg, MS.

*Last updated: February 2026*
