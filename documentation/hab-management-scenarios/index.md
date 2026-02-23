---
layout: default
title: "HAB Management Scenarios"
permalink: /hab-modeling/hab-management-scenarios/
---

# Using CE-QUAL-W2 to Evaluate HAB Management Scenarios

## Problem Context

Harmful algal blooms (HABs) dominated by cyanobacteria represent a growing threat to the ecological integrity and beneficial uses of lakes and reservoirs worldwide. Satellite-based analyses have documented a widespread increase in the intensity of phytoplankton blooms since the 1980s (Ho et al. 2019), and climate projections suggest that rising water temperatures, prolonged stratification, and shifting precipitation patterns will further favor bloom-forming cyanobacteria (Paerl and Huisman 2008; Paerl et al. 2016). When these blooms occur, they can produce cyanotoxins that impair drinking water supplies, restrict recreation, degrade aquatic habitat, and impose substantial economic costs on water utilities and communities.

Water resource managers responsible for reservoir operations increasingly face decisions about whether and how to intervene. A range of operational strategies has been proposed, from hypolimnetic withdrawal and artificial mixing to nutrient load reduction and mechanical removal. However, the effectiveness of any given strategy depends on site-specific factors including reservoir morphometry, thermal regime, nutrient loading, and the species composition of the phytoplankton community. Field-scale experimentation with these strategies is often costly, slow, and difficult to replicate. Numerical models that simulate the coupled hydrodynamic and biogeochemical processes governing bloom dynamics can help managers evaluate candidate strategies systematically before committing resources to implementation.

## Purpose of This Guidance

This document provides guidance for using the CE-QUAL-W2 hydrodynamic and water quality model to design, execute, and interpret simulation scenarios that evaluate operational strategies for cyanobacterial bloom management in reservoirs and lakes. The approach is grounded in the comprehensive review by Summers and Ryder (2023), which synthesizes the scientific basis for HAB management tactics and identifies the environmental factors that control bloom development. That review serves as the primary reference throughout this guidance.

The intent is conceptual rather than procedural. Each page describes what model parameters or boundary conditions to adjust and why those changes represent a given management action, but does not prescribe specific input file formats or model syntax. Readers seeking implementation-level detail should consult the CE-QUAL-W2 user manual (Cole and Wells 2023) and the [HAB modeling user's manual](/hab-modeling/).

## About CE-QUAL-W2

CE-QUAL-W2 is a two-dimensional, laterally averaged hydrodynamic and water quality model that solves the equations of motion in the longitudinal and vertical dimensions. The model simulates water surface elevations, velocity fields, temperature, and a comprehensive suite of water quality constituents, including multiple algal groups, nitrogen and phosphorus species, dissolved oxygen (DO), and organic matter. Its laterally averaged formulation is well suited for reservoirs and narrow lakes where longitudinal and vertical gradients dominate over lateral variation.

Version 4.5 of CE-QUAL-W2 (Cole and Wells 2023) includes cyanobacteria vertical migration (buoyancy regulation). Version 4.5 also includes algae toxin tracking and reduced reaeration from surface blooms. ERDC's Version 2026, built on PSU's Version 4.5, introduced four additional capabilities: nitrogen fixation enhancement, mortality under hypoxic conditions, persistent minimum algal concentrations, and mechanical algal harvesting. These features, described on the [CE-QUAL-W2 Capabilities](model-capabilities.md) page, substantially expand the model's ability to represent the processes that distinguish cyanobacterial blooms from other phytoplankton dynamics.

## Audience and Document Organization

This guidance is organized to serve two complementary audiences: water resource managers who need to understand what drives blooms and what interventions are available, and water quality modelers who need to translate management questions into model experiments.

Managers will find the most relevant material on the [Factors Controlling HAB Development](factors.md) page, which summarizes the physical, chemical, and biological drivers of cyanobacterial blooms, and the [Operational Management Strategies](strategies.md) page, which catalogs eight intervention approaches along with their mechanisms, applicability, and limitations. Modelers will benefit most from the [CE-QUAL-W2 Capabilities](model-capabilities.md) page, which describes the core and HAB-specific model features, and the [Designing and Evaluating Model Scenarios](scenario-design.md) page, which provides a structured framework for baseline development, scenario construction, and output interpretation.

Both audiences should consult the [Strategies Not Directly Simulable](other-strategies.md) page, which identifies management approaches that fall outside the model's process representation and discusses possible boundary-condition workarounds where approximate evaluation may still be feasible.

---

[Next: Factors Controlling HAB Development &rarr;](factors.md)
