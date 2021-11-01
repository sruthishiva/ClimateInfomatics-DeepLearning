# ClimateInfomatics-DeepLearning

The Copernicus Data Store (CDS) is a one stop shop for a wide range of historical and real time geospatial data from various remote sensing and on-the-ground weather observations. 

#### Procuring and Reading Geospatial Data 
The CDS API allows for programmatic access to this data store. This API is used to obtain the following data from the ERA5-Land Hourly Reanalysis Dataset. 

1.	Temperature of air at 2m above the surface - [2m Temperature - 2019 - December - All 31 days - 12:00 - Whole Available Region - NetCDF]
2.	Total precipitation - [Total Precipitation - 2019 - December - All 31 days -12:00 - Whole Available Region - NetCDF]
3.	Volumetric soil water layer 1 - [Volumetric soil water layer 1 - Total Precipitation - 2019 - December - All 31 days - 12:00 - Whole Available Region - NetCDF]

The first part of the notebook includes code that invokes the CDS API to download the three datasets. It then opens these three datasets and prints the basic attributes of the datasets, typically the range of latitude, longitude, data variables and other metadata.

#### Exploring and Visualising Geospatial Data

1. The basic statistics (mean, median, standard dev., variance, range, spatial resolution etc) for each of the datasets, comments about the conclusions. 
2. Also checking for missing data points, NaN values etc. 
3. Plot of a randomly chosen day from each of the datasets as a sequential colormap.

#### Preprocessing Geospatial Data
1. The spatial resolution (i.e., the separation in longitudes and latitudes between adjacent data points) of the downloaded data is 0.1 degree x 0.1 degree. The resolution is increased to 0.05 degree x 0.05 degree by upscaling using linear interpolation. This upscaling is to be performed on all three datasets. 
2. The Total Precipitation dataset is quite left skewed. Data transformation method added to tackle this data skew.

#### Deep Learning for Geospatial Data

The neural network is used to predict the [Total Precipitation] from the two input variables [Temperature of air at 2m above the surface, Volumetric soil water layer 1]. The Deep Learning framework of choice is PyTorch
