---
layout: default
title: "Strategies Not Directly Simulable"
permalink: /hab-modeling/hab-management-scenarios/other-strategies/
---

{% include section-nav.html section="hab-management-scenarios" %}

# Strategies Not Directly Simulable in CE-QUAL-W2

Several widely discussed Harmful Algal Bloom (HAB) management strategies target chemical, biological, or physical processes that lie outside the computational framework of CE-QUAL-W2. Because the model solves laterally averaged conservation equations for momentum, heat, and constituent mass, it cannot represent processes such as algaecide pharmacokinetics, sediment amendment geochemistry, or photocatalytic cell destruction that operate through mechanisms not included in the governing equations. Nonetheless, modelers may wish to bound the potential water quality benefits of these strategies within a scenario analysis framework. Table 8 summarizes each strategy, explains why it cannot be simulated directly, and identifies boundary condition adjustments that can serve as approximate workarounds.

## Interpreting Workaround Scenarios

Workaround scenarios do not simulate the mechanism of a given strategy; rather, they impose an assumed outcome on the model by modifying one or more boundary conditions or rate parameters. For example, reducing the sediment phosphorus flux to approximate alum treatment presupposes the magnitude of phosphorus binding without modeling the geochemical reactions that produce it. Similarly, elevating algal mortality rates to represent algaecide application requires the user to specify the kill rate, spatial extent, and duration of effect from external information. Consequently, these approximations are useful for exploring the sensitivity of bloom dynamics to changes in nutrient supply, light availability, or algal loss rates, but the results should not be interpreted as predictions of strategy performance. Users should document all assumptions underlying workaround scenarios and, where feasible, constrain imposed parameter values using field data or published treatment efficacy studies (Cooke et al. 2005; Matthijs et al. 2012).

**Table 8. Management Strategies Not Directly Represented in CE-QUAL-W2**

| Strategy | Mechanism | Why Not Directly Simulable | Possible Workaround |
|----------|-----------|----------------------------|---------------------|
| Chemical treatment (algaecides) | Direct cell lysis or growth inhibition via copper sulfate, hydrogen peroxide, or other biocidal agents | No chemical agent fate-and-transport module; algaecide dose-response kinetics are not represented | Impose an elevated algal mortality rate over the target segment(s) for the treatment duration |
| P inactivation (alum/iron addition) | Binding of dissolved phosphorus to aluminum or iron floc, which settles and caps sediment release | No sediment amendment geochemistry; precipitant fate is not tracked | Reduce the sediment phosphorus flux boundary condition by the expected inactivation efficiency |
| Floating treatment wetlands | Nutrient uptake and sequestration by emergent macrophytes grown on buoyant platforms | No macrophyte growth module; plant-mediated nutrient cycling is absent | Reduce inflow or in-reservoir nutrient concentrations proportionally to estimated wetland uptake rates |
| TiO2-coated floating media | Photocatalytic generation of reactive oxygen species at the water surface, causing oxidative damage to algal cells | Photocatalytic reactions are outside the model framework; no mechanism exists to represent surface-localized oxidative stress | No practical workaround; this strategy cannot be approximated through standard boundary condition adjustments |
| Physical enclosures and shading | Attenuation of photosynthetically active radiation (PAR) by opaque covers, shade cloth, or suspended barriers | Model grid cells receive uniform surface shortwave radiation; localized, structure-based shading is not a native feature | Reduce the surface solar radiation input or increase the light extinction coefficient over the affected segments |
| Riparian vegetation management | Nearshore shading by overhanging canopy combined with nutrient filtration through root-zone biogeochemistry | Watershed-scale terrestrial processes (canopy shading geometry, root-zone denitrification, and sediment trapping) operate outside the model domain | Modify the light extinction coefficient for nearshore segments and reduce tributary nutrient concentrations to reflect riparian buffer performance |
| Floating solar photovoltaics | Reduction of incident PAR by panel arrays covering a fraction of the water surface | Same limitation as physical shading: the model does not support spatially variable surface radiation within a segment | Reduce the surface solar radiation input proportionally to panel coverage area and transmittance |

{% include section-nav-bottom.html section="hab-management-scenarios" %}

