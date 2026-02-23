---
layout: default
title: "Algal Harvesting - User Manual"
permalink: /hab-modeling/algal-harvesting/
---

# Chapter 3: Algal Harvesting

## Purpose

Simulates physical removal of algae from specified segments at scheduled times. This can represent mechanical harvesting, skimming operations, or other management actions. Features include depth-limited harvesting and mass tracking.

## Activation

Place `harvest_option_input.csv` in the model run directory. The feature activates when `NHF > 0` (at least one harvest segment is defined). A second file containing the time-series of harvest events (named inside the option file) must also be present.

## How It Works

1. At each time step, the model checks whether the current Julian day (`JDAY`) has reached the next scheduled harvest event from the time-series file.
2. When a harvest event occurs, for each harvested segment and each active algal group, the model removes a fraction `FHA` of the algal concentration from each cell in the water column.
3. If a maximum harvest depth (`HADEP`) is specified for a segment, only cells with their center above that depth (measured from the water surface) are harvested.
4. The harvested mass is tracked per-event and cumulatively, and written to `harvest_mass_output.csv`.
5. After harvesting, the minimum algae floor (`ALG_MIN`) is applied, so algae cannot be harvested below the seed concentration.

**Harvesting is instantaneous** -- the fractional removal `FHA` is applied once at the event JDAY, then `FHA` is automatically reset to zero internally. FHA values are automatically clamped to the range [0, 1].

## Parameters

| Parameter | Source | Description |
|-----------|--------|-------------|
| `HAFFN` | `harvest_option_input.csv` | Filename of the time-series file |
| `NHF` | `harvest_option_input.csv` | Number of segments with harvesting |
| `IHA(1:NHF)` | `harvest_option_input.csv` | Segment indices where harvesting occurs |
| `HADEP(1:NHF)` | `harvest_option_input.csv` | Maximum harvest depth (m) per segment. `0` = all layers. Optional. |
| `FHA(1:NHF)` | Time-series file | Fraction of algae removed per segment (0.0 to 1.0) at each event |

## Input File: `harvest_option_input.csv`

### Field Descriptions

| Line | Content |
|------|---------|
| 1 | Header (skipped) |
| 2 | Description (skipped) |
| 3 | `HAFFN` -- filename for time-series data (character string) |
| 4 | Description (skipped) |
| 5 | `NHF` -- integer, number of harvested segments |
| 6 | Description (skipped) |
| 7 | `IHA(1), IHA(2), ... IHA(NHF)` -- segment indices |
| 8 | Description (skipped) -- **optional line** |
| 9 | `HADEP(1), HADEP(2), ... HADEP(NHF)` -- max depth in meters -- **optional line** |

Lines 8-9 are optional. If missing or unreadable, `HADEP` defaults to `0.0` for all segments (harvest the full water column).

### Example File Listing

```
Algal Harvesting Option Input File
Filename for time-varying harvesting data
harvest_timeseries.csv
Number of segments with harvesting (NHF)
2
Segment numbers where harvesting occurs (IHA). One value per harvested segment (NHF).
15, 22
Maximum harvest depth per segment in meters. 0 = harvest all layers. One value per harvested segment (NHF). This line and the next are optional.
3.0, 0.0
```

In this example, segment 15 is harvested to a maximum depth of 3.0 m (only layers with their center within 3 m of the surface), and segment 22 is harvested through the full water column.

## Time-Series File (e.g., `harvest_timeseries.csv`)

### Field Descriptions

| Line | Content |
|------|---------|
| 1 | Header (skipped) |
| 2 | Column labels (skipped) |
| 3+ | `JDAY, FHA(1), FHA(2), ... FHA(NHF)` -- one row per harvest event |

- `JDAY` is the Julian day of the harvest event.
- `FHA` is the fractional removal (0.0 to 1.0). For example, `0.50` removes 50% of algae. Values are automatically clamped to [0, 1].
- Set `FHA = 0.0` for a segment to skip harvesting at that segment for that event.
- Rows must be in chronological order.
- The file is read sequentially; when the end of file is reached, no further harvesting occurs.

**Important:** The first data row is loaded at initialization. If harvesting should not begin at the start of the simulation, include a leading row with `FHA = 0.0` for all segments at a JDAY before or at the simulation start time.

### Example File Listing

```
Algal Harvesting Time Series Data
JDAY      FHA(1)    FHA(2)
150.0     0.50      0.30
165.0     0.00      0.80
200.0     0.25      0.00
250.0     0.10      0.10
```

In this example:

- On JDAY 150, 50% of algae are removed from segment 15 (above 3 m depth) and 30% from segment 22 (all layers).
- On JDAY 165, segment 15 is skipped (`FHA = 0.0`) and 80% is removed from segment 22.
- On JDAY 200, 25% is removed from segment 15 and segment 22 is skipped.
- On JDAY 250, 10% is removed from both segments.
- After JDAY 250, no further harvesting occurs.

## Output File: `harvest_mass_output.csv`

The model automatically creates this file in the run directory when harvesting is active. It logs every harvest event with the following columns:

| Column | Description |
|--------|-------------|
| `JDAY` | Julian day of the event |
| `Segment` | Segment number |
| `Fraction` | Fraction removed (`FHA`) |
| `Event_Mass_kg` | Mass removed in this event (kg), summed across all algal groups |
| `Cumulative_Mass_kg` | Running total of mass removed at this segment (kg), summed across all algal groups |

Note that `Event_Mass_kg` and `Cumulative_Mass_kg` report totals across all algal groups, not per-group values.

## Source Code References

- Static config read: `input.F90` ~lines 2341-2365
- Time-series initial read: `time-varying-data.f90` ~lines 475-494
- Time-series runtime update: `time-varying-data.f90` ~lines 1711-1730
- Branch mapping: `init-geom.F90` ~lines 221-226
- Harvesting applied: `update.F90` ~lines 96-145
- Mass output file opened: `init.F90` ~lines 134-137

---

[Previous: Chapter 1 - Nitrogen Fixation](/hab-modeling/nitrogen-fixation/) | [Next: Chapter 3 - Minimum Algae](/hab-modeling/minimum-algae/)

