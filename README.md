# Capstone2: Predicting Flight Takeoff Time Delays
Flight delays are a significant issue for airline companies, affecting operational efficiency, customer satisfaction, and financial performance. Accurately predicting whether a flight will be delayed, and by how long, can enable airlines to proactively manage operations and improve the passenger experience. Knowing that a flight is likely to be late, airlines can establish policies to immediately assuage customer complaints. The goal of this project is to create a model that predicts the difference in scheduled and actual takeoff times of flights.

## Data Collection and Cleaning:
We used a Data set of commercial domestic flights in the United States of America for the year 2018, taken from the United States’s Department of Transportation’s Bureau of Transportation Statistics. We also used the a data set of Airline Carrier names and initial, and airport names and codes. There were various issues with the main dataset that needed to be addressed prior to EDA such as removing columns that were not needed for our specific problem, renamed columns for clarity, converted certain columns to their appropriate data types (such as numeric columns to datatime columns), and merged the airline carrier names and airport names datasets for clarity. We then checked the dataset for missing and incorrect data, and either fixed or removed these rows. We started with a data frame of 7,213,446 rows and 28 columns. After cleaning, the dataframe was 7,191,323 rows and 25 columns

## Exploratory Data Analysis
We removed additional columns that were not neded, or had too few entries to be of use. We then graphs the numbers of delayed/cancelled flights and flights that left on time across multiple variables including Airline, Location, Month, Time of Day, and Day of the week. Finally, we calculated Chi-Square Statistics and Cramer's V for various featrues.

## Pre-processing
We removed uneeded columns, which included temporary columns created in EDA for calculations, and columns that had the same information in different formats. We then created dummy variables, removed outliers, created training and testing sets, and used a log transformer to scale and standardize the data 

## Modeling
We created and tested a variety of models, including K Nearest Neighbors, Random Forest, XGBoost, and two LightGBM. With a dataset this large, we created a subsample train and test set and ran each model though Bayesian Optimization to get the best hyperparameters for each model. 

The KNN model was too slow at predicting on a dataset this large. It also scored the worst on all evaluation metrics, so not a good model to use in our case.

The Random Forest model performed better than the KNN model on its metrics, but was slow on training, so may not be the best model to use.

Both LightGBM and XGBoost performed better than the Random Forest in all evaluation metrics. They also had a much faster training speed compared to the Random Forest, so these models would be better than either of the two previous models.

LightGBM is able to work with categorical features, without the need for one-hot encoding, so we tried a second LightGBM model, this keeping the categorical data intact, without using one-hot encoding. We also using sin/cos cyclical encoding on the month and time to address rollover from December to January and 23:00 to 00:00 respectively.


## Documention
The LightGBM model using categorical featrues (without one-hot encoding is the best model to use of the model's tested. That being said, there is much room for improvement. Currently, this model only explains approximately 16% of the variance in the data.


### Recomendations:
1. Airlines can use this model to determine in advance if there will likely be a delay in a flight, and estimate how long the delay will be. This in turn can be used to improve customer service by being able to notify passengers more in advance of flight delays. However, airlines should note that the MAE is 12.8 minutes, so they should take this into account when deciding how to post delay notifications. We recommend rounding this number to 15 minutes, so airlines can inform passangers that the estimated delayed length posted may be off by approximatley 15 minutes.
2. Airlines can better manage staffing personal. Knowing the length of a delay in advance can allow airlines to better schedule staff and other operation needs.
3. The work from this project not only gave a model that estimates the difference in time between the scheduled flight takeoff and the actual flight takeoff, but also produced a clean data set with flight times. As many airlines schedule the same flights every day, airlines should use this data as a starting off point to adjust flights that are consistently delayed. 

### Improvements:
The main area for improvement would be collecting more data and creating more unique features to get a more accurate predictive model. This could include the reason for each delay (weather, mechanical, staffing, etc), data across multiple years, if the previous flight was delayed, or whether the day was a holiday. 

### Next Steps:
1. Track the same flights throughout the year to see if there are specific flights that are always delayed.
2. Track the same plane throughout the day to see if there is a cascade effect that contributes to delays. 
