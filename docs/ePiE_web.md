This section outlines how to run the web application step-by-step with generic assumptions. Detailed explanations of individual model parameters are provided in section XYZ and more specific use applications are shown in section XYZ.

The ePiE app can be directly assessed via the button below:

[ePiE - Web Application](https://shoeks.github.io/ePiE_webApp//){target="_blank", .md-button }
<br>

 

## Legal Disclaimer

After accessing the website, a legal disclaimer and a description of the privacy policy is presented. To use the web application, you are required to accept the terms.

<br>
<img src="/img/screenshots/screens_1.png" alt="img1" style="width: 100%; max-width: 600px; height: 50%;" />
<br>

After accepting, you will be guided to the ePiE starting page, which gives you a short description about the model, first use instructions how to operate the application, where to ask for questions, and a short section with acknowledgments. On the left side are multiple links to subsections of the model. Each subsection on the webpage comes with specific instructions and tables aiding the user in the process.  Start by clicking on “API properties” (1).

<br>
<img src="/img/screenshots/screens_2.png" alt="img2" style="width: 100%; max-width: 600px; height: 50%;" />
<br>

## API Properties

On the “API properties” page, you will see two tables, i.e. one with the API properties (FIGURE X, 1) and API-specific fate parameters (FIGURE X, 2). By hovering over one of the specific columns, a pop- up will appear above the respective table, explaining the individual column (FIGURE X, 3). 

<img src="/img/screenshots/screens_3.png" alt="img3" style="width: 100%; max-width: 600px; height: 50%;" />

By default, the data for ibuprofen are included in the web application, which serves as an illustrative example throughout the process. If the user wants to add a new API, an excel template is provided which can be downloaded by clicking on “Get Excel template” (FIGURE X, 4). The template contains data for 36 APIs with 41 data columns for individual variables. 9 of these column are mandatory and are also presented in Table 1 (FIGURE X, 1). The mandatory columns are:

- MW = Molecular Weight [g/mol]
- KOW_n = Octanol/water partitioning coefficient of the neutral form [unitless *or* L H<sub>2</sub>O/L Octanol]
- Pv = Vapour pressure at 25 °C [Pa]
- S = Solubility in water at 25 °C [mg/L]
- pkA = Acid dissociation coefficient [unitless]
- F_uf = Fraction of dose excreted unchanged via urine and faeces, including conjugate metabolites (glucuronides and sulphates) [unitless]

Not mandatory to fill in, but still essential for ePiE, is the k_bio_wwtp column, which indicates the first order biodegradation rate constant for secondary WWTP treatment. In case this parameter is not known, the SimpleTreat model will estimate it. Thus, it can be left empty. This factor is one of the most important and sensitive parameters for the model and is furthermore discussed in section XYZ.

Table 2 (FIGURE X, 2) contains supplementary physico-chemical parameters for both the neutral and alternative form of the API. While these properties are not mandatory to run the ePiE model, they refine the model outputs. 

As mentioned above, the excel template contains overall 41 variables that are used in the modelling process. While not all of these can be adjusted within the ePiE App, they can be adjusted in the excel file. For example, the default temperature for surface waters for the neutral form (T_hydro_sw_n) of 293.15 K (20 °C) could be adjusted to reflect measured temperature data in a specific basin.

## WWTP removal

On this page, the removal inside the WWTP is modelled. Table 3 contains the API and estimates the removal during primary and secondary treatment (FIGURE X, 1). The table is by default empty but relevant values must be entered here. After clicking  “Run Simple Treat 4.0” under Table 3 (FIGURE X, 2), SimpleTreat will estimate the removed fractions and automatically fills the table (FIGURE X1). If experimental values are available, the modelled values can also be overwritten. Afterwards, click on river basin.  

<img src="/img/screenshots/screens_4.png" alt="img4" style="width: 100%; max-width: 600px; height: 50%;" />
<img src="/img/screenshots/screens_5.png" alt="img5" style="width: 100%; max-width: 600px; height: 50%;" />

## River basin

On the river basin tab, a map of Europe will appear (FIGURE X, 1). One or multiple river basins can be selected by manually selecting the desired river basin on the map. Basins can be deleted by clicking on them again on the map or clicking on the ID below the map. Note that not all river basins are covered by ePiE, especially the ones close to coastal areas, that there is a minimum size requirement  for their inclusion in the underlying database. Moreover, due to the model’s spatial resolution, larger basins generally provide more robust results, and that WWTP serve as starting points for modelling.

<img src="/img/screenshots/screens_6.png" alt="img6" style="width: 100%; max-width: 600px; height: 50%;" />

As ePiE is estimating concentrations based on consumption data, the consumption data needs to be known for each country a river basin flows through. For example, estimating the concentrations in the Danube river basin would require the consumption data for overall 12 countries. For illustrative purposes, we will continue the example with the river basin Ouse (FIGURE X, 2), which only requires consumption data for the United Kingdom. Moreover, the river basin has been thoroughly validated previously (<mark>**Oldenkamp et al., 2018**</mark>).  
At the bottom of the page, the specific flow conditions can be chosen which are by default set to average yearly flow conditions. Minimum and maximum flow conditions are also possible to select. Keep the default options and after having selected the river basin Ouse, click on the tab “Consumption data”.
 
 <img src="/img/screenshots/screens_7.png" alt="img7" style="width: 100%; max-width: 600px; height: 50%;" />

## Consumption data 

On the consumption data tab, the consumption of an API in a given country needs to be included. At first, the page is empty but a table will be generated for all required countries in the selected river basin after clicking  “Generate table” (FIGURE X, 1). 

<img src="/img/screenshots/screens_8.png" alt="img8" style="width: 100%; max-width: 600px; height: 50%;" />

Afterwards, add the per capita consumption to the top table and select a year for which the respective population size should be retrieved. The values in the table can manually be overwritten by clicking “Edit Table” (FIGURE X, 2) if other, reliable data sources are available. After having filled in the necessary data, continue by clicking on “Run ePiE”.

<img src="/img/screenshots/screens_9.png" alt="img9" style="width: 100%; max-width: 600px; height: 50%;" />

## Run ePiE

At the top of the page, you will see two buttons: “Save current settings” and “Load settings from file”.
Clicking on “Save current settings” (FIGURE X, 1) will generate and download a JavaScript Object Notation (JSON) file. The fill will be called by default “ePie_settings” followed by the current data and a unique identifier, such as “ePiE_settings_2026-03-16_13402.json”. JSON files are compact data files that enable the efficient storage of data. Accordingly, the .json file will contain all parameters that were put previously into the individual tables. Moreover, a .json file could also be used to parameterise ePiE, skipping all previous steps by manually generating the file, and loading it into the web application by clicking on “Load settings from file” (FIGURE X, 2). 

<img src="/img/screenshots/screens_10.png" alt="img10" style="width: 100%; max-width: 600px; height: 50%;" />

Clicking on the button “Run ePiE” will run the model (FIGURE X, 3). Model progress can be seen in the grey box below the button (FIGURE X, 1). Once ePiE finalised its run, the message “ePiE run completed.” will appear at the bottom and a blue rectangular bar will appear (FIGURE X, 2). Next, click “Map results”.

<img src="/img/screenshots/screens_11.png" alt="img11" style="width: 100%; max-width: 600px; height: 50%;" />

## Map results

The page will at first show only the introduction text at the top and a grey square. After clicking “Generate Map” (FIGURE X, 1) the predicted environmental concentrations in the respective river basins will be visualised, with red values indicating high and blue values low concentrations (FIGURE X). 

<img src="/img/screenshots/screens_12.png" alt="img12" style="width: 100%; max-width: 600px; height: 50%;" />

By clicking on the +/- (FIGURE Y, 1) or using the mouse wheel, you can zoom in the map. By clicking on the map and dragging the mouse, the map can be moved. 

<img src="/img/screenshots/screens_13.png" alt="img13" style="width: 100%; max-width: 600px; height: 50%;" />

Individual data points on the map represent predicted concentrations in ng/L. While the legend is using a log10 scale (FIGURE Z, 1), hovering over individual points and clicking them shows the non-logarithmic value (FIGURE Z, 2). If desired, the data can also be exported as a GeoJSON or excel file (FIGURE Z, 3). Furthermore, the ID and pt type can also be seen. While IDs represent an individual numerical identifier, pt types represent specific locations within a river network, called nodes in ePiE. These locations are based on the HydroLakeS3[^1] and UWWTD-Waterbase[^2] database and are:
 
- Hydro_lake: Node representing a lake
- START: Nodes representing a river source
- JNCT: Nodes where two streams meet
- MOUTH: Nodes where a river flows into the sea
- WWTP & Agglomerations: Node representing a WWTP or agglomeration, respectively. Both are classified as emission sources
- Node: Regular node representing an individual location within a river


<img src="/img/screenshots/screens_14.png" alt="img14" style="width: 100%; max-width: 600px; height: 50%;" />

After inspecting the map, continue to “Output statistics”. 

[^1]: [https://www.hydrosheds.org/products/hydrolakes](https://www.hydrosheds.org/products/hydrolakes)
[^2]: [https://www.eea.europa.eu/en/datahub/datahubitem-view/6244937d-1c2c-47f5-bdf1-33ca01ff1715](https://www.eea.europa.eu/en/datahub/datahubitem-view/6244937d-1c2c-47f5-bdf1-33ca01ff1715)

## Output statistics

On this tab, summary statistics of the predicted environmental concentrations are shown after clicking on “Calculate statistics” (FIGURE X, 1). Results can also be exported to excel by clicking on “Export statistics to Excel” (FIGURE X, 2).
Default values are calculated in ng/L and cover the mean and median for all predicted concentrations, as well as the 5th and 95th percentile. Furthermore, the mean and median downstream of all WWTPs in the river basin are calculated (FIGURE X, 3). Next, we will go to the tab “Map risks”.

<img src="/img/screenshots/screens_15.png" alt="img15" style="width: 100%; max-width: 600px; height: 50%;" />

## Map risks

Under the map risk tab, the respective risk thresholds need to be specified. This is by default set to 1.0 ng/L, but needs to be changed for the specific API (Figure X, 1). 

After clicking on “Generate Map” (Figure X, 2), a map visualising predicted risks will appear. The map behaves the same as described previously under “Map results”. However, hovering over individual data points will only show predicted concentrations, not the specific risk quotient (Figure X, 3). 

<img src="/img/screenshots/screens_16.png" alt="img16" style="width: 100%; max-width: 600px; height: 50%;" />

## Risk statistics

Summary statistics of the predicted risks are shown under this tab after clicking on “Calculate risk statistics” (Figure X, 1). Again, results can also be exported to excel by clicking on “Export statistics to Excel” (Figure X, 2).
The risk statistics provided in the table (Figure X, 3) show how many values fall into specific range of the RQ which are:

-	RQ < 0.1
-	RQ between 0.1 – 1.0
-	RQ between 1.0 – 10
-	RQ > 10

Next click on the “View Settings ” tab.

<img src="/img/screenshots/screens_17.png" alt="img17" style="width: 100%; max-width: 600px; height: 50%;" />


## View settings

This tab provides a complete overview of all parameters that were used in the current ePiE run (Figure X, 1). These can be saved and downloaded again as a .json file (Figure X, 2) and can be reused for future runs by loading them into the web application (Figure X, 3). As mentioned under “API properties”, overall 41 data variables are used in the modelling process, which can be adjusted in the excel file. However, they can also be adjusted in the .json file.

<img src="/img/screenshots/screens_18.png" alt="img18" style="width: 100%; max-width: 600px; height: 50%;" />


## Downloads

Please download the following files to follow the manual:
(<mark>**Just a test for now**</mark>) <br>
[Download file](test.txt){: download="test_txt_file"}
<br>