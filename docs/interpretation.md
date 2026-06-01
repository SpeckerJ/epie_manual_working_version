## Sources of Uncertainties

Predictions are, by their very nature, ripe with uncertainty. Especially predictions concerning the environmental due to the involved complexity. 

Predicting environmental concentrations relies on several key assumptions, which inherently introduce a certain level of uncertainty in the assessment. These uncertainties can be classified as fundamentanl or operational. While fundamental uncertainties are a consequence of the specific model assumptions, operational uncertainties are related to 


Idea: *"All models are wrong, but some are useful."* (George Box, British Statistican 1919 - 2013)


## The Foundation of the model: Input Data

The predictions of the model are heavily influenced by the quality of the input data. The better and more comprehensive data is available used as input data, the better ePiE's predictions.
First and foremost, this is esppecially true for the conspumption and sales data of APIs. It directly influences the overall amount that can potentiall be expected in the environment. Another critical factor at the start of the model is human metabolism and how much of the adminsitred API is excredted in its unchanged from. For APIs, where large fractions are excreted, this data can be less precises are small differences wont have such a big input, whereas for APIs with small fractions, data needs to be more precises.

  API | A | B |
 |-----|---|---|
 | Consumption (kg/year) | 1000 | 1000 |
 | True Fraction (%) | 90 | 10 |
 | Wrong Fraction (%) | 85 | 5 |
 | True Load (kg/year) | 900 | 100 |
 | Wrong Load (kg/year) | 850 | 50 |
 | Absolute Error (kg/year) | 50 | 50 |
 | Relative Error (%) | 5.6 | 50.0 |

- Veterinary pharmaceuticals
- Changing hydrological systems / climate change
- RQs interpretation



Often uniform API usage and excretion rates across populations are assumed, overlooking regional differences. Similarly, WWTPs processes are assumed to be largely similar, which may however not fully capture the operational variability between WWTPs. As such, specific removal rates for APIs can be different for individual WWTPs. Moreover, hydrological fluctuations are also to be expected, which can significantly influence environmental concentrations. During high flow events, dilution will play a much more influential factor as opposed to during low flow events. Moreover, during high-flow events, the possibility of sewer overflows increases which would lead to the untreated emissions of the sewer into the environment. 
Further uncertainties arise from potentially limited data availability on APIs. This could for example include limited sales data, making assessment of API usage difficult. Especially for APIs that are available as over the counter drugs (OTC) or only via prescription available sales data can be vastly different. Moreover, which APIs are available as OTC or via prescription only can differ between countries.
Furthermore, the ePiE model itself introduces a certain level of uncertainty in the assessment of environmental concentration. This is due to specific model assumptions.. To reiterate these, ePiE only considers WWTP listed in the Environmental Protection Agencies database and is thus limited to WWTP connected to at least 2000 population equivalents. Hydrological scenarios  are based on average yearly flows between 2000 – 2015, and the spatially resolution is 1 km. This means that some WWTPs are not covered by ePiE, that future hydrological scenarios might not be comparable to the time window of 2000 – 2015, and that ePiE performs better for large river basins. 
While the ePiE model provides valuable information on predicted environmental concentrations of APIs in surface waters, it is important to recognize that all models have inherent limitations and uncertainties. Consequently, predicting and interpreting environmental concentrations should be done with care and knowledge of potential uncertainties and how to address them. These limitations and sources of uncertainties will be discussed later at different sections, but the main focus of this manual is to provide the practical knowledge how to run the ePiE model. For further information, we refer to the PREMIER Guidance documents [REFERENCE]


## ePiEs model parameters

<img src="/img/draft_flowchart.png" alt="Draft Flowchart" style="width: 100%; max-width: 600px; height: auto;" />
<figcaption>Figure X: Dummy caption</figcaption>

# Comments



[comment]: <> (Model uncertainties. Mention later)
One of the most influential points in the environmental risk assessment of APIs is related to production and consumption of APIs. Exact quantities for the production of APIs might be known for individual countries for well-known pharmaceuticals, less so for highly specific drugs or newly introduced products on the market. Additionally, not all pharmaceuticals that are sold are consumed, which further complicates the assessment. Accordingly, the availability of precise data on production, sales, and actual consumption is therefore critical, as this information significantly contribute to the overall uncertainty in the assessment. 