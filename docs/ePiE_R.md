
## Installing R and RStudio

*R* is a free, open-source programming language and software environment
for statistical computing and graphics. While R is mandatory to have
installed, RStudio is not. However, RStudio provides a user-friendly
interface for *R*. It makes it easier to write, run, and debug *R* code,
and it provides tools for visualizing data and managing projects. Please
follow the steps below to install *R* and RStudio. This manual is not
intended to provide users with a full instructions on how *R* works.
Nevertheless, it will provide all necessary instructions to run ePiE in
*R*, assuming limited knowledge of the programming language.

**Step 1: Install R**

1.  Go to the [Comprehensive R Archive Network
    (CRAN)](https://cran.r-project.org/).

2.  Click on the download link for your operating system (Windows,
    macOS, or Linux).

3.  Run the installer and follow the on-screen instructions.

**Step 2: Install RStudio**

1.  Go to the [RStudio download
    page](https://www.rstudio.com/products/rstudio/download/).

2.  Download the free version of **RStudio Desktop**.

3.  Run the installer and follow the on-screen instructions.

## The *R* ePiE package

Before running the ePiE model, you need to install some additional
packages. These packages provide extra functionality for handling data,
maps, and calculations. In the console panel, copy and paste the
following code, then press Enter. The code will check if the required
packages are installed. If not, it install them automatically.

```R
 # Install dependencies 
 if(!require("Rcpp")) install.packages("Rcpp")       # For source code in C++
 if(!require("terra")) install.packages("terra")     # For flow rasters
 if(!require("sf")) install.packages("sf")           # For rivers and lakes
 if(!require("mapview")) install.packages("mapview") # For interactive maps
```

The ePiE package is not yet available on CRAN. Accordingly, it needs to
be installed directly from GitHub. Copy and paste the appropriate
command for your operating system into the console and press Enter:

```R
# Windows
install.packages("https://github.com/SHoeks/ePiE/raw/refs/heads/main/Builds/ePiE_1.25.zip",
                  repos = NULL,
                  method = "libcurl")
# macOS
install.packages("https://github.com/SHoeks/ePiE/raw/refs/heads/main/Builds/ePiE_1.25.tgz",
                 repos = NULL,
                 method = "libcurl")
# Linux
install.packages("https://github.com/SHoeks/ePiE/raw/refs/heads/main/Builds/ePiE_1.25.tar.gz",
                 repos = NULL,
                 method = "libcurl")
```

Afterwards the ePiE package can be loaded with the following command:

```R
 library(ePiE)
```

## API Properties

API properties are exemplary included for ibuprofen. These can be loaded with 
`LoadExampleChemProperties()` as shown below.


```R
# Open API-specific data
chem = LoadExampleChemProperties()

# View the contents of the chemical properties
str(chem)

# 'data.frame':    1 obs. of  23 variables:
#  $ API                            : chr "Ibuprofen"
#  $ CAS                            : chr "15687-27-1"
#  $ class                          : chr "acid"
#  $ MW                             : num 206
#  $ KOW_n                          : num 9333
#  $ Pv                             : num 0.0248
#  $ S                              : num 21
#  $ pKa                            : num 4.85
#  $ f_u                            : num 0.2
#  $ f_f                            : logi NA
#  $ metab                          : logi NA
#  $ API_metab                      : logi NA
#  $ k_bio_wwtp_n                   : num 0.000197
#  $ k_bio_wwtp_alt                 : num 0.000197
#  $ custom_wwtp_primary_removal    : logi NA
#  $ custom_wwtp_secondary_removal  : logi NA
#  $ custom_wwtp_N_removal          : num 0
#  $ custom_wwtp_P_removal          : num 0
#  $ custom_wwtp_UV_removal         : num 0
#  $ custom_wwtp_Cl_removal         : num 0
#  $ custom_wwtp_O3_removal         : num 0
#  $ custom_wwtp_sandfilter_removal : num 0
#  $ custom_wwtp_microfilter_removal: num 0
```

To load in data for a different desired API, a custom data file in any *R* readable format can be used (e.g., .csv, .xlsx). The template on the ePiE webapp can be used for this purpose; it is also included below as an .xlsx or .csv file.[^10]

[^10]: To do: Include template file as .xlsx and .csv 


[Template CSV; FILE NOT INCLUDED YET](Template CSV){: .md-button download="ePiE_R_API_template_CSV"}
[Template XLSX; FILE NOT INCLUDED YET](Template XLSX){: .md-button download="ePiE_R_API_template_XLSX"}

```R
df_metoprolol <- read.csv("DATA_FILE.csv", header = TRUE, sep = ";") # .csv
df_metoprolol <- readxl::read_excel("DATA_FILE.xlsx") # .xlsx. Ensure that readxl is installed!

```

Similar to the web application, the ePiE package includes example data
for Ibuprofen. Again, we will use to this data to run the model. Copy
and paste the following code into the console. It will load the chemical
properties of ibuprofen and fills in any missing values automatically.
These values are the same values as presented in the web application.

```R
chem = LoadExampleChemProperties()
chem = CompleteChemProperties(chem = chem)

# [1] "WWTP primary and secondary removal rates evaluated with SimpleTreat 4.0 for Ibuprofen"
```
## WWTP Removal

To estimate the removal fractions inside the WWTP, the SimpleTreat model
is used. Copy and paste the following code into the console:

```R
removal = SimpleTreat4_0(chem_class = chem$class[1], MW = chem$MW[1], Pv = chem$Pv[1], S =  chem$S[1], pKa = chem$pKa[1], Kp_ps = chem$Kp_ps[1], Kp_as = chem$Kp_as[1], k_bio_WWTP = chem$k_bio_wwtp[1], T_air = 285, Wind = 4, Inh = 1000, E_rate = 1, PRIM = -1, SEC = -1)
```

## River basin

Getting European river basins IDs can be achieved using the following
code. With the `ViewBasinsMap()` function, an interactive map will open up
that allows you to select individual basins similar to the web
application.

```R
    basins = LoadEuropeanBasins()
    ViewBasinMap()
```

To select individual basins, their id number needs to be attached to an
object which will be used as input argument to actually select the
specific river basins.


```R
    basin_ids = c(124863, 107287) # Rhine and Ouse
    basins = SelectBasins(basins_data = basins, basin_ids = basin_ids)
```

The flow conditions can be specified as shown below. Other options for the `LoadLongTermFlow()`
function are “maximum” and “minimum”.

```R
    flow_avg = LoadLongTermFlow("average")

    ## [1] "Loading average flow..."

    basins_avg = AddFlowToBasinData(basin_data = basins, flow_rast = flow_avg)
```


## API Consumption

Next we load the consumption data for ibuprofen with the code below.

    # Load example consumption data
    cons = LoadExampleConsumption()

Please note that for other compounds the respective data frame needs to
contain exactly the same column names and structure as shown below. 

```R
str(cons)

# 'data.frame':    51 obs. of  4 variables:
#  $ cnt       : chr  "AD" "AL" "AM" "AT" ...
#  $ population: num  76177 2862427 2965269 8858775 9981457 ...
#  $ year      : num  2019 2019 2019 2019 2019 ...
#  $ Ibuprofen : num  343 12881 13344 39864 44917 ...
```

We need to ensure that the consumption data is available for the
selected basins. This can be achieved with the following code

```R
    cons = CheckConsumptionData(basins$pts, chem, cons)
```

## Run ePiE

All required parameters have now been specified and ePiE is able to
predict the environmental concentrations. The code below runs the ePiE
model and attaches it to an object called “results”.

```R
    results = ComputeEnvConcentrations(basin_data = basins_avg,
                                        chem = chem,
                                        cons = cons,
                                        verbose = TRUE,
    cpp = TRUE)
```

- Show here also the output of the file and mention what the individual columns mean
    - X, Y- coordinates, the flow, Concentration water and sediment (not validated)

## Map results 

Visualising the predicted concentrations can be achieved with the code
below.

```R
    # InteractiveResultMap(results, basin_id = basin_ids[2], cex = 4) # Ouse
```

## Output statistics

Next we want to calculate summary statistics for the predicted concentrations.

```R
PEC_summary_stats <- result %>%
  group_by(API, basin_id, flow) %>%
  summarise(
    mean_conc = mean(C_w, na.rm = TRUE),
    perc5_conc = quantile(C_w, 0.05, na.rm = TRUE),
    median_conc = median(C_w, na.rm = TRUE),
    perc95_conc = quantile(C_w, 0.95, na.rm = TRUE),
    mean_WWTP_conc = mean(C_w[Pt_type == "WWTP"], na.rm = TRUE),
    median_WWTP_conc = median(C_w[Pt_type == "WWTP"], na.rm = TRUE)
  )
```

## Risk statistics

To calculate risk quotients (RQs), the respective risk threshold value needs to be added to the data. Afterwards, the summary statistics for the RQs can be calculated as well as exemplary shown below.

```r
results$risk_threshold <- 10
RQ <- results %>% mutate(
    RQ = C_w / risk_threshold
)

RQ_summary_stats <- RQ %
  group_by(API, basin_id, flow) %>%
  summarise(
    abs_RQ_less_0.1 = sum(RQ < 0.1, na.rm = TRUE),
    abs_RQ_0.1_to_1 = sum(RQ >= 0.1 & RQ <= 1.0, na.rm = TRUE),
    abs_RQ_1_to_10 = sum(RQ >= 1 & RQ <= 10, na.rm = TRUE),
    abs_RQ_abv_10 = sum(RQ >= 10, na.rm = TRUE),
    tot.RQ = n(),
    rel_RQ_less_0.1 = abs_RQ_less_0.1 / tot.RQ,
    rel_RQ_0.1_to_1 = abs_RQ_0.1_to_1 / tot.RQ,
    rel_RQ_1_to_10 = abs_RQ_1_to_10 / tot.RQ,
    rel_RQ_abv_10 = abs_RQ_abv_10 / tot.RQ,
    .groups = "keep"
  ) %>%
  select(-matches("tot."))
```

## Map risks 

