```r
# This is an example of R code
data <- read.csv("data.csv")
summary(data)
```

## Installing R and RStudio

*R* is a free, open-source programming language and software environment
for statistical computing and graphics. While R is mandatory to have
installed, RStudio is not. However, RStudio provides a user-friendly
interface for *R*. It makes it easier to write, run, and debug R code,
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

## R ePiE

Before running the ePiE model, you need to install some additional
packages. These packages provide extra functionality for handling data,
maps, and calculations. In the console panel, copy and paste the
following code, then press Enter. The code will check if the required
packages are installed. If not, it install them automatically.

    # # Install dependencies 
    # if(!require("Rcpp")) install.packages("Rcpp")      # For source code in C++
    # if(!require("terra")) install.packages("terra")     # For flow rasters
    # if(!require("sf")) install.packages("sf")          # For rivers and lakes
    # if(!require("mapview")) install.packages("mapview") # For interactive maps

The ePiE package is not yet available on CRAN. Accordingly, it needs to
be installed directly from GitHub. Copy and paste the appropriate
command for your operating system into the console and press Enter:

    # Windows
    # install.packages("https://github.com/SHoeks/ePiE/raw/refs/heads/main/Builds/ePiE_1.25.zip",
    #                  repos = NULL,
    #                  method = "libcurl")
    # # macOS
    # install.packages("https://github.com/SHoeks/ePiE/raw/refs/heads/main/Builds/ePiE_1.25.tgz",
    #                  repos = NULL,
    #                  method = "libcurl")
    # # Linux
    # install.packages("https://github.com/SHoeks/ePiE/raw/refs/heads/main/Builds/ePiE_1.25.tar.gz",
    #                  repos = NULL,
    #                  method = "libcurl")

Afterwards the ePiE package can be loaded with the following command:

    library(ePiE)

    ## ePiE version: 1.25

    # Open API-specific data
    chem = LoadExampleChemProperties()

    # View the contents of the chemical properties
    str(chem)

    ## 'data.frame':    1 obs. of  23 variables:
    ##  $ API                            : chr "Ibuprofen"
    ##  $ CAS                            : chr "15687-27-1"
    ##  $ class                          : chr "acid"
    ##  $ MW                             : num 206
    ##  $ KOW_n                          : num 9333
    ##  $ Pv                             : num 0.0248
    ##  $ S                              : num 21
    ##  $ pKa                            : num 4.85
    ##  $ f_u                            : num 0.2
    ##  $ f_f                            : logi NA
    ##  $ metab                          : logi NA
    ##  $ API_metab                      : logi NA
    ##  $ k_bio_wwtp_n                   : num 0.000197
    ##  $ k_bio_wwtp_alt                 : num 0.000197
    ##  $ custom_wwtp_primary_removal    : logi NA
    ##  $ custom_wwtp_secondary_removal  : logi NA
    ##  $ custom_wwtp_N_removal          : num 0
    ##  $ custom_wwtp_P_removal          : num 0
    ##  $ custom_wwtp_UV_removal         : num 0
    ##  $ custom_wwtp_Cl_removal         : num 0
    ##  $ custom_wwtp_O3_removal         : num 0
    ##  $ custom_wwtp_sandfilter_removal : num 0
    ##  $ custom_wwtp_microfilter_removal: num 0

## Running the ePiE Model

Similar to the web application, the ePiE package includes example data
for Ibuprofen. Again, we will use to this data to run the model. Copy
and paste the following code into the console. It will load the chemical
properties of ibuprofen and fills in any missing values automatically.
These values are the same values as presented in the web application.

    chem = LoadExampleChemProperties()
    chem = CompleteChemProperties(chem = chem)

    ## [1] "WWTP primary and secondary removal rates evaluated with SimpleTreat 4.0 for Ibuprofen"

To estimate the removal fractions inside the WWTP, the SimpleTreat model
is used. Copy and paste the following code into the console:

    removal = SimpleTreat4_0(chem_class = chem$class[1], MW = chem$MW[1], Pv = chem$Pv[1], S = chem$S[1], pKa = chem$pKa[1], Kp_ps = chem$Kp_ps[1], Kp_as = chem$Kp_as[1], k_bio_WWTP = chem$k_bio_wwtp[1], T_air = 285, Wind = 4, Inh = 1000, E_rate = 1, PRIM = -1, SEC = -1)

Next we load the consumption data for ibuprofen with the code below.

    # Load example consumption data
    cons = LoadExampleConsumption()

Please note that for other compounds the respective data frame needs to
contain exactly the same column names and structure as shown below. The
str() function shows the structure of any arbitrary R object.  

    str(cons)

    ## 'data.frame':    51 obs. of  4 variables:
    ##  $ cnt       : chr  "AD" "AL" "AM" "AT" ...
    ##  $ population: num  76177 2862427 2965269 8858775 9981457 ...
    ##  $ year      : num  2019 2019 2019 2019 2019 ...
    ##  $ Ibuprofen : num  343 12881 13344 39864 44917 ...

Getting European river basins IDs can be achieved using the following
code. With the ViewBasinsMap() function, an interactive map will open up
that allows you to select individual basins similar to the web
application.

    basins = LoadEuropeanBasins()
    # ViewBasinMap()

To select individual basins, their id number needs to be attached to an
object which will be used as input argument to actually select the
specific river basins.

    basin_ids = c(124863, 107287) # Rhine and Ouse
    basins = SelectBasins(basins_data = basins, basin_ids = basin_ids)

We need to ensure that the consumption data is available for the
selected basins. This can be achieved with the following code

    cons = CheckConsumptionData(basins$pts, chem, cons)

After checking the consumption data, we need to specify the flow
conditions as specified below. Other options for the LoadLongTermFlow()
function are “maximum” and “minimum”.

    flow_avg = LoadLongTermFlow("average")

    ## [1] "Loading average flow..."

    basins_avg = AddFlowToBasinData(basin_data = basins, flow_rast = flow_avg)

Now all required parameters have been specified and ePiE is able to
predict the environmental concentrations. The code below runs the ePiE
model and attaches it to an object called “results”.

    results = ComputeEnvConcentrations(basin_data = basins_avg,
                                        chem = chem,
                                        cons = cons,
                                        verbose = TRUE,
    cpp = TRUE)

Visualising the predicted concentrations can be achieved with the code
below.

    # InteractiveResultMap(results, basin_id = basin_ids[2], cex = 4) # Ouse


