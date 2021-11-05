# Modeling the Marked Presence-Only Data: A Case Study of Estimating the Female Sex Worker Size in Malawi

# Author Contributions Checklist Form

## Data

**Abstract (Mandatory)**
The four main data components used in the analysis are the Malawi PLACE data, DHS data,
nighttime-light data, and WorldPop data. The PLACE data represent the response, while the
DHS, nighttime-light, and WorldPop data are the covariates used in analysis. A shapefile of
Malawi was also used in ArcMap to extract nighttime-light data and in R for analysis.

**Availability (Mandatory)**

- The Malawi PLACE data has not been publicly available yet. Access to the PLACE I
    data and report can be requested at https://doi.org/10.15139/S3/RIQKYD. PLACE II data
    and report can be requested by emailing Dr. Sharon Weir at sharon_weir@unc.edu.
- The DHS data can be obtained with permission from the DHS Program. Registration is
    available at https://dhsprogram.com/data/new-user-registration.cfm.
    Nighttime-light data can be obtained with permission from
    https://payneinstitute.mines.edu/eog/
- WorldPop data is publicly available at
    https://www.worldpop.org/geodata/summary?id=
- The shapefile is publicly available and can be downloaded using the link provided below.
    https://gadm.org/download_country_v3.html.

**Description (Mandatory if data available)**

- PLACE Data:
    o Permission to use the PLACE data was granted by PLACE study.
    o The PLACE data was provided from Dr. Sharon Weir directly in two files:
       “Venue_GPS.sas7bdat” and “FORM B data for willing and operational
       venues.xlsx”.
    o “Venue_GPS.sas7bdat” contained 7 values about 3013 venues: GPS, Latitude,
       Longitude, Accuracy, operational, b5a (district), and siteid.
    o “FORM B data for willing and operational venues.xlsx” contained a sheet that
       included answers from the Form B in the PLACE study. The primary columns
       used for analysis were the venue ID, district, and estimates of the number of
       FSW working at the venues
    o The sheet “RawData” from “FORM B data for willing and operational venues.xlsx”
       was saved as a csv file (with no changes) for use in R. This csv is referenced in
       “PLACE_Data_Processing.R” as “Raw_Form_b.csv”.
- The DHS data includes responses at 850 clusters around Malawi. Permission was
    granted to download DHS survey, HIV Test, and GPS data for Malawi.
       o After receiving permission to access DHS datasets, the Malawi 2015- 2016
          survey may be downloaded by navigating to “Download Datasets”, “Malawi 2015-
          16” with type Standard DHS, selecting “Data Available” under Survey Datasets,
and downloading all .DTA files under Survey Datasets as well as the Geographic
Data and the Geospatial Covariates.
      o DHS data was extracted to the MW_2015-16_DHS from the downloaded .zip file.

- The nighttime-light data is pixel level data in Malawi averaged at the month-level in
    2016. Nighttime-light data are publicly available (after registering) at
    https://payneinstitute.mines.edu/eog/ and then navigating to
    https://eogdata.mines.edu/products/vnl/.
       o From this second link, the user can download the nighttime-light data by
          navigating to Download Tiled under Monthly Cloud-free DNB Composite -> 2016
          -> the desired month (e.g. 201601) -> cvmcfg -> and download the required tiles.
       o Using the downloaded tiles, the nighttime-light is processed for each month in
          ArcMap using the Zonal Statistics as Table tool.
       o The processed nighttime-light data is referenced as “malawi2016.csv” in the R
          code.
       o The processed nighttime-light data is available in the supplementary information.
- The WorldPop data estimates the population density at pixel level in Malawi in 2015 after
    adjusting to match UN estimates. The WorldPop data are publicly available at
    https://www.worldpop.org/geodata/summary?id=123. The specific data set may be
    downloaded by clicking “Browse Individual Files” and downloading
    “MWI_ppp_2015_adj_v2.tif”.
- The shape file contains information about the boundaries of Malawi. It was used to
    extract nighttime-light data and perform analysis. It is publicly available at
    https://gadm.org/download_country_v3.html. Version 3.6 was used in this study.

The PLACE data are saved as a .sas7bdat file and a .xlsx file. The .xlsx Form B data includes a
data dictionary. The DHS data dictionaries are saved as .DO files and data are saved as .DTA
files. The nighttime-light data are saved as .tgz files before processing and as a comma-
separated values file after processing. The WorldPop data is saved as a .tif file. The shapefile is
downloaded as a .shp file for ArcMap processing and as an R object in R directly from the raster
package for analysis.

**Optional Information (complete as necessary)**
PLACE REPORT Malawi September 2018:
https://www.fhi360.org/sites/default/files/media/documents/resource-linkages-malawi-place-
report.pdf
WorldPop: 10.5258/SOTON/WP

## Code

**Abstract (Mandatory)**
A zip file named “MalawiCode.zip” contains all files to replicate the results in the paper and
generate the included figures.

**Description (Mandatory)**


The code files are in .R format. There are five .R files used to generate the results.

- PLACE_Data_Processing.R: Reads in the GPS and venue survey data, merges them,
    and saves them into PLACE I and PLACE II datasets (dat_place1.rds and
    dat_place2.rds, respectively).
- Cluster_Aggregation.R: Aggregates the DHS data to the cluster level
- Covariate_Kriging.R: Divides Malawi into cells, handles spatial misalignment, and saves
    the .rds files with response and covariate information
- Malawi_Fit.R: Fits the models, performs the calibration step described in Section 3 of the
    paper, considers model validation in Section 4.1, performs final analysis described in
    Section 5, and creates related tables and figures.
- Cell_Simulations.R: Performs the simulation study in Section 4.2 and generates the
    results, including Figure 4.

The code is licensed under the MIT license. The code and pseudo-datasets are available for
download at https://github.com/ilaga/Presence-Only-Female-Sex-Worker-Size-In-Malawi. The
required R packages and used versions to run the Malawi analysis files are: sas7bdat (0.5)
Rcpp (1.0.2) readxl (1.2.0), gridExtra (2.3.0), rstan (2.19.2), brms (2.8.0), sp (1.3.1), raster
(2.8.19), ggplot2 (3.1.0), ggmap (3.0.0), foreign (0.8.71), fields (9.6), geosphere (1.5.7), and
bayesplot (1.7.2). Additional packages to run the Covariate_Kriging file are parallel (3.6.3),
doParallel (1.0.15), foreach (1.5.0), and spatstat (1.64.1).

The analysis used R version 3.6.3.

**Optional Information (complete as necessary)**
The code is best run in parallel with 4 nodes but can still be run on one node.

## Instructions for Use

**Reproducibility (Mandatory)**
The files in the zipped file will reproduce all tables and figure from the paper if all data is
available. The run order should be:
(1) “PLACE_Data_Processing.R”
(2) “Cluster_Aggregation.R”
(3) “Covariate_Kriging.R”
(4) “Malawi_Fit.R”
(5) “Cell_Simulations.R”

The overall runtime of the main analysis is around 10 hours. The longest steps involve the
kriging found in “Covariate_Kriging.R” and initial Bayesian model fitting in “Malawi_Fit.R”.
“Cell_Simulations.R” takes an additional approximately 10 hours depending on the number of
cores used for parallel computing.

Pseudo-datasets were provided for the main file, “Malawi_Fit.R”, but should be run using
“Malawi_Fit_With_Sim.R”, which has two changes from the original file. First, the lines which


read the data refer to the simulated datasets. Second, the WorldPop and nightlight values are
not transformed since they do not replicate the true covariates. The results and images
reproduced with the pseudo-dataset will not match the results and images in the manuscript.

## Notes

The DHS Malawi 2015-16 Geographic Data has been updated from MWGC7AFL.zip to
MWGC7BFL.zip. There are additional columns added to the updated geographic data. For
shared columns, the data are almost identical with a few changes. For example, for the
All_Population_Count_2005 column, the values of 844 of the 850 rows are the same, while the
difference between the remaining 6 rows is a maximum of less than 0.4%. Differences in the
data will result not result in significant differences in final results. Some R code will have to be
changed to match the new columns (e.g. Aridity to Aridity_2015). To the best of our knowledge,
the remaining data sets available for download are identical to the datasets downloaded for this
analysis.
