---
layout: default
title: "Algal Harvesting - User Manual"
permalink: /hab-modeling/algal-harvesting/
---

{% include section-nav.html section="hab-users-manual" %}

# Chapter 3: Algal Harvesting

## Purpose

The algal harvesting feature simulates physical removal of algae from specified segments at scheduled times. This feature can represent mechanical harvesting, skimming operations, or other management actions. CE-QUAL-W2 supports depth-limited harvesting and tracks the mass removed per event and cumulatively.

## Activation

Place `harvest_option_input.csv` in the model run directory. CE-QUAL-W2 activates the feature when `NHF > 0` (at least one harvest segment is defined). A second file containing the time-series of harvest events (named inside the option file) must also be present.

## How It Works

1. At each time step, CE-QUAL-W2 checks whether the current Julian day (`JDAY`) has reached the next scheduled harvest event from the time-series file.
2. When a harvest event occurs, CE-QUAL-W2 loops over each harvested segment and each active algal group and removes a fraction `FHA` of the algal concentration from each cell in the water column.
3. If a maximum harvest depth (`HADEP`) is specified for a segment, CE-QUAL-W2 skips cells whose center lies deeper than `HADEP` below the water surface.
4. CE-QUAL-W2 tracks the harvested mass per event and cumulatively and writes the results to `harvest_mass_output.csv`.
5. After harvesting, CE-QUAL-W2 applies the [minimum algae floor](/hab-modeling/minimum-algae/) (`ALG_MIN`), so the model cannot harvest algae below the seed concentration.

**Harvesting is instantaneous** -- CE-QUAL-W2 applies the fractional removal `FHA` once at the event JDAY, then resets `FHA` to zero internally. The model automatically clamps `FHA` values to the range [0, 1].

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

Lines 8--9 are optional. If the lines are missing or unreadable, CE-QUAL-W2 defaults `HADEP` to `0.0` for all segments (harvest the full water column).

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

In this example, CE-QUAL-W2 harvests segment 15 to a maximum depth of 3.0 m (only layers with their center within 3 m of the surface) and harvests segment 22 through the full water column.

## Time-Series File (e.g., `harvest_timeseries.csv`)

### Field Descriptions

| Line | Content |
|------|---------|
| 1 | Header (skipped) |
| 2 | Column labels (skipped) |
| 3+ | `JDAY, FHA(1), FHA(2), ... FHA(NHF)` -- one row per harvest event |

- `JDAY` is the Julian day of the harvest event.
- `FHA` is the fractional removal (0.0 to 1.0). For example, `0.50` removes 50% of algae. CE-QUAL-W2 automatically clamps values to [0, 1].
- Set `FHA = 0.0` for a segment to skip harvesting at that segment for that event.
- Rows must be in chronological order.
- CE-QUAL-W2 reads the file sequentially; when the model reaches the end of file, no further harvesting occurs.

**Important:** CE-QUAL-W2 loads the first data row at initialization. If harvesting should not begin at the start of the simulation, include a leading row with `FHA = 0.0` for all segments at a JDAY before or at the simulation start time.

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

- On JDAY 150, CE-QUAL-W2 removes 50% of algae from segment 15 (above 3 m depth) and 30% from segment 22 (all layers).
- On JDAY 165, the model skips segment 15 (`FHA = 0.0`) and removes 80% from segment 22.
- On JDAY 200, the model removes 25% from segment 15 and skips segment 22.
- On JDAY 250, the model removes 10% from both segments.
- After JDAY 250, no further harvesting occurs because CE-QUAL-W2 has reached the end of the time-series file.

## Output File: `harvest_mass_output.csv`

CE-QUAL-W2 automatically creates this file in the run directory when harvesting is active. The model logs every harvest event with the following columns:

| Column | Description |
|--------|-------------|
| `JDAY` | Julian day of the event |
| `Segment` | Segment number |
| `Fraction` | Fraction removed (`FHA`) |
| `Event_Mass_kg` | Mass removed in this event (kg), summed across all algal groups |
| `Cumulative_Mass_kg` | Running total of mass removed at this segment (kg), summed across all algal groups |

`Event_Mass_kg` and `Cumulative_Mass_kg` report totals across all algal groups, not per-group values.

## Source Code References

- **Read static config:** `input.F90` ~lines 2338--2359 -- CE-QUAL-W2 initializes `NHF` to 0 and checks whether `harvest_option_input.csv` exists. If so, the model reads `HAFFN`, `NHF`, `IHA(1:NHF)`, and optionally `HADEP(1:NHF)`. If the file is absent, `NHF` remains 0 and the feature is inactive. If the `HADEP` lines are missing or unreadable, the model defaults `HADEP` to 0.0 for all segments.
- **Read time-series (initialization):** `time-varying-data.f90` ~lines 476--492 -- When `NHF > 0`, CE-QUAL-W2 opens the time-series file specified by `HAFFN`, skips the two header lines, and reads the first data row into `NXFHA2` and `FHANX`. The model clamps each `FHANX` value to [0, 1] and copies the result into `FHA`. CE-QUAL-W2 then reads ahead one row (`NXFHA1`, `FHANX`) so the model knows the JDAY of the next event. If the read-ahead reaches end-of-file, the model sets `NXFHA1` to a large value and zeroes `FHANX` so no further events occur.
- **Read time-series (runtime update):** `time-varying-data.f90` ~lines 1705--1722 -- At each time step when `NHF > 0`, CE-QUAL-W2 checks whether `JDAY >= NXFHA1`. If so, the model advances the harvest schedule: it clamps `FHANX` values to [0, 1], copies the result into `FHA`, and reads the next row from the time-series file. If the read reaches end-of-file, the model sets `NXFHA1` to a large value, zeroes `FHANX`, and exits the loop.
- **Branch mapping:** `init-geom.F90` ~lines 221--227 -- CE-QUAL-W2 maps each harvested segment `IHA(JHA)` to its branch index `JBHA(JHA)` by checking whether the segment falls between the upstream and downstream segments of each branch. The model uses this mapping during the harvesting calculation to match segments to branches.
- **Apply harvesting:** `update.F90` ~lines 96--145 -- For each algal constituent in each cell, CE-QUAL-W2 checks whether the cell belongs to a harvested segment. If `HADEP > 0`, the model computes the cell depth below the water surface and skips cells deeper than `HADEP`. The model computes the removed concentration as `C1 * FHA`, accumulates the removed mass (`REMOVED * CELL_VOL`) into `HAMASS_EVENT`, and subtracts the removed concentration from `C1`. After all spatial loops complete, the model writes harvest event data to `harvest_mass_output.csv`, updates cumulative mass totals, and resets `FHA` to zero.
- **Open mass output file:** `init.F90` ~lines 132--137 -- CE-QUAL-W2 sets the `HARVESTING` flag to `.TRUE.` when `NHF > 0`. If `HARVESTING` is true, the model opens `harvest_mass_output.csv` and writes the column header line.

{% include section-nav-bottom.html section="hab-users-manual" %}
