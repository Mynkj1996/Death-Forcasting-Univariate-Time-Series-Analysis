## Problem Statement
We know monthly numbers of accidental deaths in the US from January 1973 till December 1978. Build predictions for next 2 years.

## Introduction
The Data Set is Accidental Death in US Data Set  located at the following URL: https://rdrr.io/r/datasets/USAccDeaths.html. The dataset contains the variables for month and number of accidental deaths. There are 72 observations and 2 Variables in the Data Set and It is a Univariate Time series Analysis 
The values for the first six months of 1973 are 9007 8106 8928 9137 10017 10826.

## Exploratory Data Analysis and Data Cleaning
1. There were no missing values . 
2. Perform MOVING AVERAGE Process on the data by creating new column rolling mean of 12 months . So forcasting using moving average gives us a mean absolute percentage error (MAPE) of 9.16% where as  root mean squared error(RMSE) is 948.16 that is prediction by the model has standard deviation 948.16
3. Perform Exponential Smoothing by taking alpha 0.2 and got MAPE 6.64% rmse is 756.5939700408036
4. Perform AR model , here first plot partial Autocorrelation Function to find the value of p . After analyzing p value for AR Model and MAPE comes out to be 9.25%
5. Then check the stationarity of the data  by rolling statistics and Dicky fuller test . 
   
   Null Hypothesis : the time series is non stationary ( Beta = 1)
   Alternate Hypothesis: the time series is stationary ( Beta < 1)

Hypothesis say tha:
p-value > 0.05: Fail to reject the null hypothesis (H0), the data has a unit root and is non-stationary.
p-value <= 0.05: Reject the null hypothesis (H0), the data does not have a unit root and is stationary.

So here we cannot reject the null hypothesis and we can say that data is not stationary

## 2 common reasons behind non-stationarity are:
Trend – mean is not constant over time. 
Seasonality – variance is not constant over time. There are ways to correct for trend and seasonality, to make the time series stationary.

## What happens if you do not correct for these things?
Many things can happen, including:
Variance can be mis-specified Model fit can be worse. Not leveraging valuable time-dependent nature of the data.
Eliminating trend and seasonality
Transformation Examples. Log, square root, etc. We are going to look at log.
Smoothing Examples. Weekly average, monthly average, rolling averages. We are going to look at monthly average.
Differencing Examples. First-order differencing. We are going to look at first-order differencing.
Polynomial Fitting Examples. Fit a regression model. Decomposition

## As it is non stationarity perform STL decomposition
Dickey-Fuller criterion does not reject the non-stationarity null-hypothesis, but we still see a trend. Let's smoothen the trend by taking log , then check again stationarity:
Then again check the stationarity and found its non stationary so done differencing . Done unitill time series become stationary. After differencing 2 times it become stationary 

## Plot ACF PACF to find p, q for arima model 
After seeing the grapgh found lag 1,1 as p,q values
Shaded region is upper and lower bound for critical valueswhere null hypothesis cannot be rejected (auto correlation value is 0) but at lag 1 null hypothesis is rejected. so ACF is statistically significant for lag 1

After performing Arima (1,2,1) got RMSE 0.0879

Then turn the data into original form by using exponential in fitted values 
By doing cumulative then  adding those residuals to log data then exponent the data into original data format 

The values for the first six months of 1979 are 7798 7406 8363 8460 9217 9316
