# This is data wrangling work for isolating Chicago's census tracts from the "US Tracts" shapefile, which includes all US census tracts used in the 2020 nationwide census. 

# Loading libraries
library(sf)
library(tidyverse)

# Loading the Chicago census tract shapefile
US.Census.Tracts <- st_read("C:/Users/kengo/OneDrive/Documents/QGIS Files/UChicago SIR CTA project/Chicago_Census_Tract.gpkg")
# Defines variables that I'll be analyzing (which is the numerical label for each US census tract)
var <- c("NAME")
# Extracts only the "NAME" column data out from the US census tract shapefile
Tract.subset <- (US.Census.Tracts[var])
# Allows me to double-check if I got the right values for my labels, which I did.
glimpse(Tract.subset)
# renames "NAME" column to "ChiTractNum" to easily identify what I'm analyzing
names(Tract.subset)[1]<- c("ChiTractNum")
glimpse(Tract.subset)

# Importing the super-demographic csv file with 16 separate census metrics into R and isolating the following ones from the codebook: (1), (2), (12), (13), (14). Eventually, the goal is to merging the data with Chicago census tract gpkg
Chicago.Data <- read.csv("C:/Users/kengo/OneDrive/Documents/QGIS%20Files/UChicago%20SIR%20CTA%20project/Demography_and_Vacancy_Tallies_ACS_2017_2021/nhgis0009_csv/Demography_Tallies_2017_2021.csv")
datavar <- c()