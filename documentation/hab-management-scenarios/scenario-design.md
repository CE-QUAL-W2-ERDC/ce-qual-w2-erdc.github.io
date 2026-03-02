---
layout: default
title: "Designing and Evaluating Model Scenarios"
permalink: /hab-modeling/hab-management-scenarios/scenario-design/
---

{% include section-nav.html section="hab-management-scenarios" %}

# Designing and Evaluating Model Scenarios

Numerical scenario analysis provides a structured means of quantifying how a proposed management action would alter harmful algal bloom (HAB) dynamics relative to current conditions. In this context, a scenario is defined as a CE-QUAL-W2 simulation in which one or more boundary conditions, structural features, or operational rules have been modified from the calibrated baseline. By comparing scenario and baseline outputs, modelers can isolate the expected effect of each intervention on bloom intensity, duration, spatial extent, and downstream water quality.

## General Approach

A validated baseline model is the prerequisite for all scenario work. The baseline should reproduce observed hydrodynamic and water quality conditions under current or historical operations, with calibration targets that include water surface elevation, vertical temperature profiles, nutrient concentrations, dissolved oxygen (DO), and chlorophyll-a or group-specific algal biomass. This calibrated baseline serves as the reference condition against which all management scenarios are evaluated.

Each scenario is constructed by modifying one or more aspects of the baseline to represent a specific management action. Modifications should be physically realistic and operationally feasible, reflecting actual infrastructure constraints and available water supplies. The difference between scenario and baseline outputs then quantifies the expected water quality response to the proposed action.

In practice, single-strategy scenarios should be evaluated first to establish the individual sensitivity of the system to each intervention. Once individual responses are understood, combined scenarios (e.g., hypolimnetic withdrawal paired with nutrient load reduction) can reveal synergies or trade-offs that single-strategy analyses cannot capture (Summers and Ryder 2023). Multi-strategy combinations are particularly important for highly eutrophic systems where no single intervention is likely to be sufficient.

## Scenario Design Matrix

Table 6 provides a structured guide for configuring scenarios for each of the eight management strategies. For each strategy, the table identifies the model element to modify, the key variables to vary across scenario runs, and the primary output metrics for evaluating the response.

**Table 6. Scenario Design Matrix**

| Strategy | What to Modify | Key Variables to Vary | Primary Output Metrics |
|----------|---------------|----------------------|----------------------|
| Hypolimnetic withdrawal | Bottom outlet flow schedule | Withdrawal rate, timing, outlet elevation | Surface TP, Chl-a, thermocline depth, hypolimnetic DO |
| Horizontal flushing | Surface outlet release rates | Flushing rate, duration, trigger threshold | Surface Chl-a, biomass export, residence time, downstream temperature |
| Pulsed inflows | Upstream inflow time series | Pulse magnitude, duration, frequency, timing relative to bloom onset | Stratification strength, Chl-a, flow velocity, turbidity |
| Artificial mixing | Vertical mixing representation | Mixing intensity, depth of influence, areal coverage, operating schedule | Mixed-layer depth, Chl-a by algal group, DO profile |
| Hypolimnetic aeration | Aeration module parameters | O2 mass delivery rate, layer range, timing, DO probe thresholds | Hypolimnetic DO, sediment P flux, surface TP, Chl-a, thermocline depth |
| Water level management | Outflows to achieve target elevations | Target pool elevations, drawdown rate, timing | Water surface elevation, Chl-a, light climate, littoral zone exposure |
| Temperature control curtain | Internal curtain structure | Curtain depth, longitudinal location, seasonal deployment period | Outflow temperature, thermocline depth, Chl-a, DO |
| Nutrient load reduction | Inflow nutrient concentrations | Percent reduction in TP, TN, or both; N:P ratio | Chl-a, TP, TN, algal group composition |
| Algal harvesting | Harvesting operation parameters | Removal rate, maximum harvest depth, location, timing, frequency | Chl-a reduction, regrowth interval, cumulative biomass removed |
| Toxin fate assessment | Toxin tracking module parameters | Toxin production and decay rates per algal group | Intracellular and extracellular toxin concentrations, toxin persistence after treatment |

## Evaluating Results

### Performance Metrics

Scenario results should be assessed using metrics that capture both the intensity and duration of bloom conditions and the broader water quality consequences of the management action. Bloom intensity metrics (peak chlorophyll-a, bloom volume) indicate whether a strategy reduces the severity of individual events, while duration metrics reveal whether blooms are shortened or prevented entirely. Metrics such as thermocline depth and Schmidt stability provide mechanistic insight into whether a hydrodynamic strategy is achieving the intended physical change. Downstream outflow quality metrics are essential for strategies that alter discharge characteristics, because an intervention that improves in-reservoir conditions at the expense of downstream water quality may not represent a net benefit.

Table 7 lists recommended performance metrics, the information each provides, and the strategies for which each metric is most informative.

**Table 7. Recommended Performance Metrics**

| Metric | What It Indicates | Relevant Strategies |
|--------|-------------------|---------------------|
| Peak surface Chl-a (ug/L) | Maximum bloom intensity | All |
| Bloom duration (days above threshold) | Temporal persistence of HAB conditions | All |
| Bloom volume (m^3 above threshold) | Spatial extent and severity of bloom | All |
| Habitat volume (m^3 or % meeting criteria) | Volume of water meeting user-defined temperature and DO criteria | Aeration, mixing, withdrawals |
| Thermocline depth (m) | Stratification state and mixed-layer response | Mixing, pulsed inflows, withdrawals, aeration |
| Schmidt stability (J/m^2) | Resistance of water column to mixing | Mixing, pulsed inflows |
| Hydraulic residence time (days) | Rate of water replacement | Flushing, pulsed inflows |
| Surface TP, TN (mg/L) | Nutrient availability in the photic zone | Withdrawals, aeration, nutrient reduction |
| Hypolimnetic DO (mg/L) | Bottom-water oxygen conditions | Withdrawals, aeration, mixing |
| Sediment P flux (mg/m^2/day) | Internal phosphorus loading from bottom sediments | Aeration, withdrawals, water level management |
| Algal group composition (%) | Community shift toward or away from cyanobacteria | Mixing, nutrient reduction |
| Outflow quality (temperature, DO, nutrients) | Downstream impact of the management action | Withdrawals, flushing, curtains |
| Intracellular toxin concentration (ug/L) | Cell-bound cyanotoxin levels | All strategies that affect algal biomass |
| Extracellular toxin concentration (ug/L) | Dissolved cyanotoxin levels at intakes or recreation sites | Harvesting, flushing, chemical treatment workarounds |
| Cumulative harvested biomass (kg) | Total biomass removed across harvesting events | Algal harvesting |

### Key Quantitative Relationships

Several fundamental relationships are useful for guiding scenario design and interpreting results.

Hydraulic residence time is defined as

> *tau* = *V* / *Q*

where *V* is reservoir volume (m^3) and *Q* is total outflow (m^3/s). Longer residence times favor bloom development by allowing phytoplankton populations to accumulate faster than they are exported (Soballe and Kimmel 1987). The flushing rate is the inverse of residence time (*rho* = *Q* / *V*) and provides a direct measure of the volumetric turnover rate. Higher flushing rates reduce bloom potential by exporting biomass more rapidly than it can grow.

Mitrovic et al. (2003) identified a critical flow velocity of approximately 0.05 m/s for suppressing persistent blooms of *Anabaena circinalis* in riverine systems. Velocities above this threshold disrupt the quiescent conditions that buoyancy-regulating cyanobacteria require to maintain surface accumulations. This threshold provides a practical design target for pulsed-inflow and flushing scenarios.

The intermediate disturbance hypothesis offers additional guidance for pulsed-inflow design. Padisak et al. (1999) found that pulsed disturbances recurring every 20--30 days at intensities of 1--2% of reservoir volume per day were sufficient to shift phytoplankton community composition away from cyanobacteria dominance. Disturbances that are too infrequent allow cyanobacteria to re-establish dominance between pulses, while overly frequent disturbances may select for fast-growing taxa without eliminating bloom risk.

Schmidt stability quantifies the mechanical energy per unit surface area (J/m^2) required to mix the entire water column to uniform density. Higher values indicate stronger thermal stratification and greater resistance to mixing. Comparing Schmidt stability between baseline and scenario simulations provides a quantitative measure of how effectively a mixing or destratification strategy disrupts the stratified conditions that favor buoyant cyanobacteria (Visser et al. 2016).

{% include section-nav-bottom.html section="hab-management-scenarios" %}

