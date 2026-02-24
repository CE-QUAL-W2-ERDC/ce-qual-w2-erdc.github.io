---
layout: default
title: "Minimum Algae (Seed Population) - User Manual"
permalink: /hab-modeling/minimum-algae/
---

{% include section-nav.html section="hab-users-manual" %}

# Chapter 1: Minimum Algae (Seed Population)

## Purpose

Prevents algal concentrations from dropping below a minimum "seed" value. This ensures a residual population exists for regrowth after die-off events such as hypoxic mortality or harvesting.

## Activation

This feature is controlled by the `ALG_MIN` parameter in `low_do_mort_input.csv`. If the file does not exist, `ALG_MIN` defaults to `0.0` and the feature has no effect.

## How It Works

After all transport, kinetics, and harvesting calculations are applied for a time step, the model checks every cell for every algal group:

```
IF C1(K,I,algae) < ALG_MIN THEN C1(K,I,algae) = ALG_MIN
```

This floor is applied uniformly to all algal groups and all cells. `ALG_MIN` is a single scalar value and cannot vary by group.

## Parameters

| Parameter | Units | Description |
|-----------|-------|-------------|
| `ALG_MIN` | mg L⁻¹ | Minimum algal concentration. Set to `0.0` to disable. |

## Input File Format

The `ALG_MIN` parameter is specified in `low_do_mort_input.csv`, which also contains the low DO mortality parameters. See [Chapter 2: Low DO Mortality](/hab-modeling/low-do-mortality/) for the complete file format and an inline listing of the example file.

## Source Code References

- Read: `input.F90` ~line 2317
- Applied: `update.F90` ~line 120


