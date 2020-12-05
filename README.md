# PWCfilegenerator v0.1.0
### An R package for creating weather files for PWC
_D'Andrea MF, Brodeur JC_ [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.3339881.svg)](https://doi.org/10.5281/zenodo.3339881)

The goal of the function `PWCfilegenerator::PWC_fg()` is to convert a weather dataset to the input file format needed to run the models Pesticide in Water Calculator (PWC) v1.52 and Pesticide Root Zone Model (PRZM5) v5.02.

PWC and PRZM5 are mathematical models used for pesticide fate modelling and are free to download from the [USEPA website](https://www.epa.gov/pesticide-science-and-assessing-pesticide-risks/models-pesticide-risk-assessment).  These models are applied for regulatory purposes as part of surface water exposure characterization during pesticide risk assessment.

Although PWC has a simple and intuitive interface, the weather files required to run the model are only available for North America, making it difficult for users lacking programming skills to run the model in other countries.  The package `PWCfilegenerator` facilitates the construction of weather files in PWC format from common databases.

## Installation

You can install `PWCfilegenerator` from this GitHub repo using the following code:

``` r
install.packages("devtools") # if you have not installed "devtools" package
library(devtools)
devtools::install_github("flor14/PWCfilegenerator")
```
You can download the project as .zip and install it with this code:

``` r
install.packages("PWCfilegenerator.zip", repos = NULL)
```

## Example

This is a basic example:

``` r
# The weather dataset used as input require the following data:
# dates, precipitation, panevaporation, temperature, wind speed and solar radiation 
# the units are described in PRZM5 manual (http://bit.ly/2k6yV26).  

# Example of a small dataset. 
data <- data.frame( date = c("01/01/81", "02/01/81", "03/01/81", "04/01/81"),
            precip = c(0.00, 0.10, 0.00, 0.00),
            evap = c(0.30, 0.21, 0.28, 0.28),
            tmed = c(9.5, 6.3, 3.5, 5),
            wind = c(501.6, 368.0, 488.3, 404.5),
            solrad = c(240.3, 244.3, 303.0, 288.5))
 
# Load the package
library(PWCfilegenerator)
 
# Function to convert and save the weather file as a .dvf. It will generate a short weather file of 1 day. 
# You can change the period in relation to your dataset.

PWCfilegenerator::PWC_fg(data = data, # Name of your dataset 
                          date = "date", # Column name for dates
                          format = "%d/%m/%y", # Date format of your dataset (more details in strptime package documentation)
                          start ="02/01/81", # Date to start the weather file
                          end = "03/01/81", # Date to end the weather file 
                          precip_cm = "precip", # Column name for precipitation (cm/day)
                          pevp_cm = "evap", # Column name for panevaporation data (cm/day)
                          temp_celsius = "tmed", # Column name for temperature (Celsius)
                          ws10_cm_s = "wind", # Column name for wind speed values (cm/sec)
                          solr_lang = "solrad", # Column name for solar radiation (Langley)
                          save_in = "F:/folder/weatherfile_name") # The extension .dvf will be added automatically.
                               
```

## Community guidelines

Report Issues:

- Questions, feedback, bug reports: please open an issue in the issue tracker of the project [here](https://github.com/flor14/PWCfilegenerator/issues).

Contribution to the software:

- Please open an issue in the issue tracker of the project that describes the changes you would like to make to the software and open a pull request with the changes. The description of the pull request must reference the corresponding issue.

## How to cite

Maria Florencia D'Andrea, & Julie Céline Brodeur. (2019, July 17). PWCfilegenerator v0.1.0: An R package for creating weather files for PWC (Version 0.1.0). Zenodo. http://doi.org/10.5281/zenodo.3339881
