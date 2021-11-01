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

1. Since the dataset is extremely large, its more beneficial to use most of the data to train rather testing. So 90-10 is the train-test split and a 90-10 is the tain-validation split. 
2. Since there are only two input variables, I used a smaller neural network of one hidden layer with two units. Any more would give great training accuracy but terrible testing accuracy due to overfitting. 
3. Multiple Regression is the model defined. And it is run through the GPU. It is run through the loop 5 times, improving form its previous reults. It is then validated after each loop to identify overfitting. And finally tested with a completely new dataset to recheck. The model has been trained multiple times to reach this result, where it reached a training and test error of zero. It has then been checked with a completely new dataset not used for training and has achieved good scores, making it a pretty good model for futher predictions, giving extremely low variance and error scores.
4. Relu activation function, along with adam optimizer an a mseloss function was used. The rectified linear activation function is a piecewise linear function that will output the input directly if it is positive, otherwise, it will output zero. It is the default activation function for many types of neural networks because a model that uses it is easier to train and often achieves better performance. MSELoss creates a criterion that measures the mean squared error (squared L2 norm) between each element in the input x and target y. The mean operation still operates over all the elements, and divides by n. Adam is an optimization algorithm that can be used instead of the classical stochastic gradient descent procedure to update network weights iterative based in training data. 
5. I have used Train and validation loss to understand how my model is doing, and tracking its progress over multiple epoches. Performance was measured using various regression metrics such as explained_variance_score, max_error, mean_absolute_error, mean_squared_error, and r2_score. Explained variation measures the proportion to which a mathematical model accounts for the variation of a data set. Max_error metric calculates the maximum residual error. MAE an arithmetic average of the absolute errors. MSE measures the average of the squares of the errors, the average squared difference between the estimated values and the actual value. R2 is the proportion of the variance in the dependent variable that is predictable from the independent variable(s). 
