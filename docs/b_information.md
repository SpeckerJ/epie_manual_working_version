# Theoretical Background
## The ePiE model

The first version of the ePiE model was developed in 2018 by Oldenkamp et al. (2018) (<mark>**CITATION**</mark>) as part of the IMI's iPiE (Innovative Medicines Initiative; Intelligence-led Assessment of Pharmaceuticals in the Environment) project and was subsequently further developed as part of the PREMIER (Prioritisation and Risk Evaluation
of Medicines in the EnviRonment) project.


The ePiE model predicts concentration of APIs for human use in European rivers and waters based on consumption data of APIs, and API and environmental characteristics. It provides a broad-scale, steady-state assessment of PECs in European river basins and combines the need for a spatial explicit model, computational efficiency, and potential limited API data availability. 

Schematically, this is shown in the figure below. ePiE uses as its basis a specific API's consumption and its human metabolism and excretion to calculate the overall excreted fraction per capita. In combination with the number of inhabitants connected to the sewage system, the overall fraction emitted to wastewater treatment plants (WWTPs) is calculated. Information on specific WWTPs are based on the European Environmental Agency database, which is limited to WWTP connected to at least 2000 population equivalents.

<br>
<img src="/img/overview_epie2.png" alt="Draft Flowchart" style="width: 100%; max-width: 600px; height: auto;" />
<figcaption>Figure X: Dummy caption.</figcaption>
<br>

The API's removal inside the WWTP is based on the API's physico-chemical properties and is modelled according to SimpleTreat 4.0 (<mark>**Struijs 2014**</mark>). Afterwards, the emitted API fraction from WWTPs into the aquatic environment is tracked along its river network. This can further be predicted for different hydrological scenarios assuming high, low flow events as well as average river flows across 1609 river basins for 31 European countries with a resolution of 1 km. River flows are based on long-term-yearly averages from 2000 – 2015. Furthermore, the predicted concentrations are compounded by environmental processes such as dilution, bio- and photodegradation, sedimentation, and hydrolysis. 
 
Based on intensive validation, ePiE was found to provide an accuracy between measured environmental concentrations (MECs) and PECs of approximately a factor of 10, with factors of 2 for river basins with reliable API consumption and monitoring data. Nevertheless, the model has specific inherent limitations. For example, ePiE was not developed to account for veterinary medicines and it does not cover drinking water sources or groundwater. Moreover, the model is constrained in terms of its precision of its modelling results with regards to temporal and spatial resolution within a river. As a result, predictions cannot be made for a specific date or time point. Furthermore, predictions are not possible for rivers without upstream WWTPs. Moreover, all WWTPs are assumed to perform generally the same and individual WWTP characteristics, except its size, cannot be accounted for. Consequently, this means that all WWTPs across Europe are modelled to have the same API removal rate and that the model is not intended to be used to simulate the effects of upgrading a specific WWTP. For further details on these constraints, please refer to the section on limitations later in the document.



## Pathways from human pharmaceutical usage to surface water 

APIs can enter the environment via multiple direct and indirect entry routes (see Figure below). Direct entry routes stem from human excretion after their administration. After consumption, APIs are metabolised in the human body, but fractions are also excreted unchanged or as active metabolites via urine and faeces. These end up in the sewer system and travel through the sewage system towards WWTPs. While conventional WWTPs are effective at removing many pollutants from the wastewater, they were not specifically designed to remove anthropogenic chemicals such as pharmaceuticals. Inside the WWTP numerous processes govern the degradation and removal of chemicals. Some are partially degraded through biological processes or removed through sorption to sludge, while others persist and pass through treatment largely unchanged. Consequently, treated wastewater effluent still contains measurable concentrations of APIs, ultimately ending up in receiving surface waters. 


<img src="/img/draft_overview_API_entry_20260415.png" alt="Draft Flowchart" style="width: 100%; max-width: 600px; height: 50%;" />
<figcaption>Figure X: Dummy caption.</figcaption>
<br>


Indirect entry sources originate from the (improper) disposal of APIs. Improper disposal refers, for example, to the disposal of unused pharmaceutical products down the toilet. Official disposal routes originate from waste collection of households, hospitals, or health care facilities in general. These may still present an indirect entry to the environment via landfills. Here, waste collected at landfills may leach into the soil and thus into adjacent groundwater or surface water.
Leaking pipes in the sewer system and overflowing sewer represent further potential indirect entry routes of APIs into the aquatic environment. These indirect routes are, however, much more complicated to model realistically and are not covered by the ePiE model. 
While this manual does not aim to provide an exhaustive explanation of all these entry routes, it is important to be aware of these routes and how they influence the environmental exposure assessments as they introduce a certain level of uncertainty.  


## Pharmaceutical Fate in Surface Water

Once APIs reach the aquatic environment, they can still have detrimental effects on aquatic organisms and may even end up in drinking water sources, warranting their proper management in a given river basin to protect human and environmental health.
Numerous degradation processes affect APIs in surface waters such as photodegradation, biodegradation, hydrolysis, and sorption. 

Sorption includes two similar, but distinctive processes: adsorption and absorptions. Adsorption describes the transfer from the water or gaseous phase to the solid phase. For example, the attachment of dissolved APIs to the surface of organic particles such as suspended solid particles in the water column or the sediment. In contrast, absorption describes the uptake or retention of a dissolved compound by another compound, material, or organism. For example, APIs that are taken up by aquatic plants from the water phase.

Organisms play another pivotal role in governing the fate of APIs in the environment as they can biodegrade APIs. However, as mentioned above, APIs can also be taken up by an organisms, also referred to as bioaccumulation[^1]. If such organisms serve as prey, APIs can be transported up the food chain to higher trophic levels, also referred to as biomagnification.

[^1]: Strictly speaking, bioaccumulation refers to the uptake of *xenobiotics* (This is mainly a test for me to see how to implement footnotes).

Photodegradation occurs either directly, when APIs degrades upon absorbing, or indirectly, when an API is degraded by radicals or other intermediates that were generated by sunlight. 
Hydrolysis refers to the process by which a compound reacts with a water molecule, leading to its degradation.

These degradation processes are in turn influenced by multiple abiotic and biotic factors. These include the pH, temperature, radiation intensity, redox conditions, microbial communities, or for example the organic matter content. Furthermore, the individual physico-chemical properties of the specific API influence these fate processes as well. For example, the acid dissociation constant pK<sub>A</sub> of a specific API in combination with the environmental pH will dictate the API's ionisation state which in turn is a decisive factor for an APIs solubility and mobility.






