---
layout: default
title: "Factors Controlling HAB Development"
permalink: /hab-modeling/hab-management-scenarios/factors/
---

{% include section-nav.html section="hab-management-scenarios" %}

# Factors Controlling HAB Development

Cyanobacterial harmful algal blooms (HABs) arise from the convergence of physical, chemical, and biological conditions that selectively favor cyanobacteria over competing phytoplankton. Identifying which factors are most influential in a given system is a prerequisite both for selecting effective management interventions and for configuring numerical models to evaluate those interventions. The synthesis presented here draws primarily from the review by Summers and Ryder (2023, Section 3) and the references cited therein.

Table 1 summarizes the major environmental factors that govern cyanobacterial bloom development, the conditions under which each factor promotes or suppresses blooms, and key supporting references.

**Table 1. Environmental Factors Controlling HAB Development**

| Factor | Favorable for Blooms | Unfavorable for Blooms | Key References |
|--------|---------------------|----------------------|----------------|
| Thermal stratification | Strong, persistent | Weak or absent | Dantas et al. 2011; Bormans et al. 1997 |
| Water temperature | High (>25 &deg;C) | Low (<20 &deg;C) | Nalewajko and Murphy 2001; Xiao et al. 2017 |
| Residence time | Long | Short | Soballe and Kimmel 1987; Padisak et al. 1999 |
| Flow velocity | Low (<0.05 m/s) | High (>0.05 m/s) | Mitrovic et al. 2003, 2011 |
| Wind speed | Low (\<3 m/s) | High (>3 m/s) | Zhang et al. 2021; Cao et al. 2011 |
| Nutrient availability | High P and/or N | Low P and/or N | Paerl et al. 2016; Filstrup and Downing 2017 |
| N:P ratio | Low (<10:1, favors N-fixers) | High (>50:1, favors non-cyanobacteria) | Harris et al. 2014; Scott et al. 2013 |
| Light availability | High surface irradiance | Low irradiance or high turbidity | Islam and Beardall 2017; Dou et al. 2019 |
| Water depth | Shallow (<15 m mixed depth) | Deep (>15 m, enables mixing strategies) | Visser et al. 2016 |
| Water level | Low or declining | High or stable | Xia et al. 2020; Jeppesen et al. 2015 |

## Stratification and Mixing

Thermal stratification is widely recognized as the dominant physical driver of cyanobacterial dominance in lakes and reservoirs (Reynolds 2006; Summers and Ryder 2023). A persistently stratified water column provides the stable conditions required for buoyancy-regulating cyanobacteria to position themselves near the surface, gaining a competitive advantage over non-motile phytoplankton. The underlying mechanism is a carbohydrate ballasting cycle: cells accumulate carbohydrates during photosynthesis in the photic zone, become negatively buoyant and sink, then consume carbohydrates through respiration at depth, regain positive buoyancy, and rise (Visser et al. 2016). This cycle is disrupted by deep or frequent mixing, which entrains buoyant cells below the photic zone and shifts competitive advantage toward non-buoyant taxa.

Wind-driven mixing exerts an analogous control at shorter timescales. Zhang et al. (2021) demonstrated that wind speeds exceeding approximately 3 m/s dispersed surface scums of cyanobacteria, whereas sustained calm periods (wind speed \<3 m/s) permitted scum formation within hours. From a management perspective, these findings highlight that any strategy capable of deepening the mixed layer or increasing turbulent kinetic energy in the epilimnion can counteract the buoyancy advantage that cyanobacteria exploit in stratified systems.

## Nutrients

Phosphorus (P) has historically been regarded as the primary limiting nutrient for phytoplankton growth in freshwater systems, and total phosphorus (TP) remains the most common target for eutrophication management. However, the role of nitrogen (N) has received increasing attention (Paerl et al. 2016). Many bloom-forming cyanobacteria are diazotrophs capable of fixing atmospheric nitrogen, which confers a competitive advantage under conditions of low dissolved inorganic nitrogen and elevated phosphorus. Nitrogen fixation is nevertheless energetically expensive, and in systems where denitrification losses exceed fixation inputs, reducing phosphorus alone may be insufficient to suppress blooms (Scott et al. 2019).

The mass ratio of total nitrogen to total phosphorus (N:P) provides practical guidance on which nutrient to prioritize for reduction. Low N:P ratios (less than approximately 10:1) favor nitrogen-fixing genera such as *Anabaena* (now *Dolichospermum*) and *Aphanizomenon*, whereas high N:P ratios (greater than approximately 50:1) tend to shift community composition away from cyanobacteria (Harris et al. 2014). Internal loading of phosphorus from anoxic sediments represents an additional complication: legacy phosphorus stored in bottom sediments can sustain elevated water-column concentrations and prolong blooms long after external loads have been reduced (Nurnberg 2009). Addressing internal loading through hypolimnetic oxygenation, sediment capping, or drawdown to oxidize exposed sediments is therefore often a necessary complement to watershed-level nutrient reductions.

Table 2 presents a decision framework for nutrient management, adapted from the synthesis by Summers and Ryder (2023, Section 2.1). The framework links system trophic state and observed nutrient ratios to recommended management targets.

**Table 2. Nutrient Management Decision Framework**

| System Condition | TP Level | N:P Ratio | Recommended Focus | Rationale |
|-----------------|----------|-----------|-------------------|-----------|
| Oligotrophic to slightly eutrophic | <100 &mu;g/L | Any | Phosphorus | Algal biomass tracks TP, not TN |
| Hypereutrophic, P-N co-limited | >100 &mu;g/L | 9--23 | Both N and P | Co-limitation regardless of redox state |
| Hypereutrophic, N fixation < denitrification | >100 &mu;g/L | >23 | Phosphorus | Fixation cannot offset denitrification losses |
| Hypereutrophic, fixation &ge; denitrification | >100 &mu;g/L | 5--9 | Both (case-specific) | Outcome depends on redox conditions and sediment dynamics |
| Extreme P excess, very low N:P | >300 &mu;g/L | <5 | Non-nutrient factors | Nutrients not limiting; management should target physical controls (e.g., temperature, flow) |

## Temperature and Light

Water temperature directly governs phytoplankton growth rates, and many bloom-forming cyanobacteria possess growth optima above 25 &deg;C, which exceed those of most eukaryotic algae (Nalewajko and Murphy 2001; Robarts and Zohary 1987). This physiological trait gives cyanobacteria a competitive advantage during warm periods, particularly in systems where summer surface temperatures consistently exceed 25 &deg;C. Warming also strengthens thermal stratification indirectly, reinforcing the buoyancy-mediated competitive advantage described in the preceding section.

Light availability interacts with buoyancy regulation to determine community composition. In clear, stratified waters, buoyant cyanobacteria can monopolize the high-irradiance surface zone, photosynthesizing at rates that non-motile competitors cannot match. In turbid or well-mixed systems, non-buoyant taxa that tolerate variable light regimes may be more competitive (Islam and Beardall 2017). The coupling of temperature, stratification, and light therefore creates a positive feedback loop: warm conditions strengthen stratification, which stabilizes the water column, which in turn allows buoyant cyanobacteria to dominate the photic zone.

## Residence Time and Flow

Hydraulic residence time integrates the effects of inflow, outflow, and storage volume on bloom potential. Long residence times permit phytoplankton populations to accumulate biomass faster than advective losses can remove it, whereas short residence times dilute and flush cells downstream more rapidly than they can reproduce (Soballe and Kimmel 1987). In riverine and flow-through reservoir systems, flow velocity serves as a more direct indicator of bloom suppression potential. Mitrovic et al. (2003) identified a critical velocity threshold of approximately 0.05 m/s, above which persistent *Anabaena* blooms were suppressed in the Darling River, Australia.

Pulsed flow disturbances offer an additional management lever. Padisak et al. (1999) reported that flow pulses applied every 20--30 days at rates equivalent to 1--2% of reservoir volume per day were sufficient to shift phytoplankton dominance away from cyanobacteria, consistent with predictions of the intermediate disturbance hypothesis. These findings suggest that even modest flow augmentation, if timed to coincide with early bloom development, can meaningfully reduce bloom severity without requiring sustained high-flow releases.

