---
layout: default
title: "CE-QUAL-W2 Capabilities for HAB Assessment"
permalink: /hab-modeling/hab-management-scenarios/model-capabilities/
---

{% include section-nav.html section="hab-management-scenarios" %}

# CE-QUAL-W2 Capabilities for HAB Assessment

CE-QUAL-W2 provides a comprehensive framework for simulating the physical, chemical, and biological processes that govern cyanobacterial bloom dynamics in reservoirs and lakes. The model resolves hydrodynamic transport, nutrient cycling, and algal growth at scales relevant to operational decision-making (Cole and Wells 2023). ERDC's Version 2026, built on PSU's Version 4.5, introduced four features specifically designed for HAB applications, extending the model's capacity to represent key cyanobacterial traits and management interventions. This page describes the core and HAB-specific capabilities most relevant to scenario evaluation.

## Core Model Capabilities

CE-QUAL-W2 solves the laterally averaged equations of motion in the longitudinal and vertical dimensions, producing a two-dimensional representation of reservoir hydrodynamics. For HAB applications, three categories of core capability are essential: hydrodynamic transport, water quality cycling, and the light regime.

The hydrodynamic module resolves vertical thermal stratification, including thermocline formation, seasonal deepening, and autumnal breakdown, which directly controls the habitat available to buoyancy-regulating cyanobacteria (Summers and Ryder 2023). Inflows are inserted at the depth matching their density, determining whether incoming water enters above, below, or within the thermocline. Surface wind stress drives turbulent mixing in the epilimnion, affecting mixed-layer depth and the stability of surface accumulations. Together, these processes govern the physical template on which bloom dynamics unfold.

The water quality module simulates the biogeochemical cycles most relevant to bloom formation. Multiple algal groups can be defined with independent growth, respiration, mortality, and settling rates, allowing representation of cyanobacteria competing with diatoms, green algae, and other taxa. Nutrient cycling encompasses nitrogen (ammonia, nitrate, organic nitrogen), phosphorus (orthophosphate, organic phosphorus), and carbon, including algal uptake, organic matter mineralization, and sediment fluxes. Dissolved oxygen (DO) is computed as a function of reaeration, photosynthesis, respiration, sediment oxygen demand, and organic matter decomposition, enabling direct assessment of hypoxic conditions that influence internal nutrient loading and algal mortality.

Photosynthetically active radiation is attenuated through the water column as a function of depth, suspended solids concentration, and algal self-shading. Because light availability directly modulates algal growth rates, accurate representation of the light regime is essential for evaluating strategies that alter mixing depth, turbidity, or surface accumulation patterns.

CE-QUAL-W2 includes a sediment diagenesis module that simulates the coupled biogeochemical reactions governing nutrient release from bottom sediments. The module computes sediment oxygen demand and the fluxes of phosphorus, nitrogen, and other constituents from the sediment to the overlying water column as a function of temperature, redox conditions, and organic matter deposition. Because internal nutrient loading from sediments is a primary driver of bloom persistence in eutrophic systems (Nurnberg 2009), the diagenesis module is essential for multi-year simulations and for evaluating strategies such as hypolimnetic withdrawal, aeration, and nutrient load reduction that aim to reduce legacy phosphorus availability.

## HAB-Relevant Features in Version 4.5

Version 4.5 of CE-QUAL-W2 (Cole and Wells 2023) includes three capabilities that are particularly relevant to HAB applications.

The **vertical migration** module simulates cyanobacterial buoyancy regulation. The model offers multiple migration formulations ranging from empirical sinusoidal approaches to mechanistic colony-density models based on Stokes' settling velocity, in which colony density changes as a function of light-dependent photosynthetic carbohydrate accumulation and respiratory consumption. Under the mechanistic formulation, cells near the surface accumulate carbohydrates during photosynthesis, become negatively buoyant, and sink; at depth, respiratory consumption of carbohydrates restores buoyancy, and cells rise. This diurnal cycle produces the surface accumulations characteristic of calm, stratified conditions (Summers and Ryder 2023). The vertical migration capability is critical for evaluating mixing and destratification strategies that aim to disrupt buoyancy regulation, as well as pulsed inflow and water level management scenarios.

The **algae toxin tracking** module simulates the production, release, and decay of up to four cyanotoxin types (e.g., microcystin, cylindrospermopsin). Toxin production is coupled to algal group biomass, with intracellular toxin content tracked separately from dissolved extracellular toxin in the water column. Toxin release occurs during cell mortality and lysis, and dissolved toxin decays at a user-specified rate. This capability is particularly important for HAB scenarios focused on drinking water supply protection or recreational use advisories, where the distinction between bloom biomass reduction and toxin concentration reduction is operationally significant.

The **reduced reaeration from surface blooms** feature reduces gas transfer across the air-water interface as a function of surface algal biomass concentration using a half-saturation relationship. Dense surface blooms suppress oxygen exchange, which can exacerbate hypoxic conditions below the bloom layer. This feedback is directly relevant to scenarios evaluating mixing or harvesting strategies that alter surface biomass concentrations.

## HAB-Specific Features (ERDC Version 2026)

ERDC Version 2026.02 introduced four features that address processes previously absent from or poorly represented in the standard formulation. Table 4 summarizes each feature, its ecological basis, and the management scenarios it supports. Implementation details are provided in the [HAB modeling user's manual](/hab-modeling/).

**Table 4. CE-QUAL-W2 HAB-Specific Features (ERDC Version 2026)**

| Feature | What It Represents | Ecological Basis | Management Scenarios Supported |
|---|---|---|---|
| Nitrogen fixation enhancement | Diazotrophic N fixation triggered at realistic dissolved inorganic nitrogen thresholds | Micro-scale nutrient heterogeneity around colonies causes fixation to initiate well above zero total inorganic nitrogen (TIN) | Nutrient load reduction, N:P ratio manipulation |
| Hypoxia-associated mortality | Elevated algal mortality under sustained low-DO conditions | Physiological stress from prolonged oxygen depletion increases cell death rates | Hypolimnetic withdrawal, aeration, post-bloom dynamics |
| Minimum algae concentration | Persistent low-level seed population that prevents extinction | Resting cells (akinetes, spores) maintain viable populations through unfavorable periods | Multi-year simulations, recovery after treatment |
| Algal harvesting | Direct mechanical removal of biomass from specified locations and times | Physical extraction of surface or near-surface cyanobacterial biomass | Mechanical harvesting scenario evaluation |

The nitrogen fixation enhancement addresses a known limitation of standard half-saturation nutrient kinetics, in which nitrogen fixation effectively begins only when TIN approaches zero. In natural systems, diazotrophic cyanobacteria initiate fixation at TIN concentrations well above zero because of micro-scale nutrient heterogeneity around cell colonies. When TIN falls below a user-specified critical threshold (CRIT_TIN), the model sets the nitrogen half-saturation constant to zero, effectively removing nitrogen limitation and representing the onset of atmospheric nitrogen fixation. Simultaneously, the model blocks dissolved inorganic nitrogen uptake from the water column for that algal group, so growth under fixation does not draw down the ambient NH4 or NO3 pool. This improves simulation of cyanobacterial dominance under moderate nitrogen limitation.

The hypoxia-associated mortality feature increases algal mortality rates when DO remains below a specified concentration threshold (ALG_O2LIM) for a sustained duration. The model tracks cumulative time (in seconds) that each cell has experienced DO below the threshold. When this accumulated duration exceeds a group-specific critical time (CRIT_T, specified per algal group), the mortality rate is elevated to a user-specified high value (AM_LOW_DO). If DO rises above the threshold, the duration counter resets to zero. This mechanism represents the physiological stress that cyanobacteria experience in oxygen-depleted waters and improves simulation of post-bloom crashes and the effects of aeration or hypolimnetic withdrawal strategies. The minimum algae concentration feature complements this by preventing algal group concentrations from declining below a specified floor (ALG_MIN), maintaining a seed population that can reinitiate growth when conditions become favorable. This capability is essential for multi-year simulations and for evaluating the persistence of treatment effects.

The algal harvesting module enables direct removal of algal biomass from designated model segments at prescribed rates and times, read from a time-varying input file. Users specify the segments where harvesting occurs, the fractional removal rate per event, and an optional maximum harvest depth per segment so that only layers above that depth are affected, representing surface skimming operations. The model produces a record of harvested biomass (in kg) per event and cumulative totals, supporting cost-effectiveness analysis of removal operations.

## Additional Capabilities Relevant to HAB Assessment

CE-QUAL-W2 includes several additional capabilities that, while not specific to HABs, are directly relevant to scenario evaluation.

The **hypolimnetic aeration module** simulates the injection of oxygen into bottom waters at specified segments and layer ranges. Users define the oxygen mass delivery rate (kg O2/day), the vertical layer range for injection, on/off timing, and DO probe feedback thresholds that control whether aeration is active. The module both adds dissolved oxygen mass to the target layers and increases vertical diffusion coefficients to represent the mixing induced by aeration devices. This capability is distinct from artificial destratification: hypolimnetic aeration can be configured to oxygenate bottom waters while preserving thermal stratification, reducing internal phosphorus loading without bringing nutrient-rich hypolimnetic water to the surface.

The **habitat volume analysis module** computes the volume of water meeting user-defined criteria for temperature and dissolved oxygen, reporting habitat volume and percentage by branch and waterbody at each output time step. While originally designed for fish habitat assessment, this module can be adapted to quantify the volume of water exceeding bloom-related thresholds (e.g., chlorophyll-a or DO criteria), providing a spatially integrated metric for scenario comparison.

The **macrophyte module** simulates submerged aquatic vegetation as stationary organisms that take up nutrients from the water column and interact with light, temperature, and flow. While not a HAB-specific feature, the macrophyte module is relevant to evaluating management strategies involving vegetation-based nutrient uptake.

## Structural Features for Scenario Design

Several structural capabilities of CE-QUAL-W2 are important for representing management interventions. Outlet structures can be defined at any elevation within the model grid, enabling simulation of hypolimnetic withdrawal and surface flushing operations. Internal weirs and curtains can represent temperature control structures that modify flow patterns near outlets. The model also accommodates multiple waterbodies and branches, allowing representation of complex reservoir geometries including embayments, side arms, and multiple inflow points. These structural elements provide the physical framework within which operational scenarios are constructed.

## Mapping Strategies to Model Features

Table 5 identifies the CE-QUAL-W2 features used to represent each management strategy and the primary boundary condition changes required to implement each scenario. Detailed scenario design guidance, including recommended parameter ranges and output metrics, is provided on the [Scenario Design](scenario-design.md) page.

**Table 5. Mapping Management Strategies to CE-QUAL-W2 Model Features**

| Strategy | Model Feature(s) Used | Key Boundary Condition Changes |
|---|---|---|
| Hypolimnetic withdrawal | Outlet structure definition; outflow boundary | Add or modify deep outlet; specify withdrawal schedule |
| Horizontal flushing | Surface outlet or spillway structure | Add or modify surface outlet; adjust release rates |
| Pulsed inflows | Inflow boundary conditions | Modify upstream inflow time series (magnitude, timing, duration) |
| Artificial mixing / destratification | Vertical diffusion representation; internal circulation | Increase vertical mixing; represent diffuser or aerator effects |
| Hypolimnetic aeration | Aeration module; DO mass injection and vertical diffusion | Specify O2 mass rate, layer range, timing, and DO probe feedback thresholds |
| Water level management | Outflow boundaries; pool elevation targets | Modify outflows to achieve target water surface elevations |
| Temperature control curtain | Internal barrier or weir structure | Add curtain at specified depth and location |
| Nutrient load reduction | Inflow constituent concentrations | Reduce phosphorus and nitrogen in inflow time series |
| Algal harvesting | Harvesting module (ERDC Version 2026) | Specify removal rate, spatial extent, and timing |
| Toxin fate assessment | Algae toxin tracking module (Version 4.5) | Enable toxin constituents; specify production and decay rates per algal group |

{% include section-nav-bottom.html section="hab-management-scenarios" %}

