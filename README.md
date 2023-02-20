# [Volatility Forecasting](introduction)
# [Air Quality PM 2.5 readings Prediction](inspiration)


## Introduction
This project is inspired by the fact that Bitcoin, the most popular and commonly utilized cryptocurrencies available on the crypto market, has experienced volatility since its
introduction unlike anything we have witnessed from traditional asset classes such as stocks and commodities among others. The heightened volatility in the crypto market indicates that
investors might or have made/lost a significant amount of money. Therefore, the in-depth technical analysis of Bitcoin volatility and other crucial fundamental factors
that drive its variability are very important for investment purposes.

---
### Overview
The dataset was extracted from [Kaggle](http://www.kaggle.com/) public datasets, a span of 5 years from 2017 to 2022. The dataset had no missing values. All Outliers
were included as such extremes are important in highlighting how the cryptocurrency behaves unexpectedly (volatile). I conducted a time series analysis to understand the trend or systemic pattern overtime on the crypto for a better forecast.
I used GARCH(1,1) as the volatility forecasting model for the crypto as proposed by Bollerslev,Tim (1986). A Walk Forward Validation evaluation method was used on the test data for the dataset.This is because the predictions over time become less and less acurate and hence it's more realistic to retrain the model as new data becomes available, giving the model good forecasts at each time step.

---
## Inspiration
Air Pollution has become a life threatening factor in many countries around the world as it damages the climate and cause various diseases including respiratory diseases and many other lung diseasea. Among air pollutants, **Particulate Matter with a diameter of of 2.5 (PM 2.5)** is considered a hazardous air pollutant to human health. Hence it is necessary to accurately forecast or **predict the PM 2.5 concentrations in the air**, in order to help citizens and the parties involved plan the measures to alleviate the harmful effect of air pollution and prevent the dangerous impact beforehand, for better Air Quality.

## Description
The dataset contains air quality data from the national capital of Delhi, India. It includes information on air pollution levels, including particulate matter (PM2.5 and PM10) levels, nitrogen dioxide (NO2), sulfur dioxide (SO2), carbon dioxide (CO2), ozone (O3), and other pollutants. The data was collected from monitoring stations located in various areas of Delhi between November 25, 2020, and January 24, 2023. This dataset is a valuable resource for researchers and policymakers to better understand air quality in Delhi and its impacts on public health.
The data is based on the amount of particulate matter in the air, which is measured in micrograms per cubic meter (µg/m³). The particulate matter includes dust, smoke, and other small particles.
The dataset had 18776 daily wise observations with no missing values, from 2020 to 2023, recorded at hourly timesatmp. After running the Augmented Dickey-Fuller (ADF) test and the Kwiatkowski–Phillips–Schmidt–Shin (KPSS) Statistical tests for **Stationarity** and the ACF (Autocorrelation Function), I confirmed that the Time series data was not Stationary, and needed **Differencing to make it stationary**. Hence I shall be fitting an **ARIMA** model, with the I part being the Integrated order or differencing order.
1. More about the two test and how a conclusion was made based on the **contradictory results** for both tests can be found here: [Stationarity Statistical tests](https://www.analyticsvidhya.com/blog/2021/06/statistical-tests-to-check-stationarity-in-time-series-part-1/).
Using the `auto_arima` function, I was able to find the best ARIMA model, based on the lowest AIC level, with optimal combination of parameters (p,d,q).
2. More about the `auto_arima` function van be found here: [auto_arima](https://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.auto_arima.html).
**ARIMA of order (5,1,3)** was selected as the best model by the function and hence fitted on the train data and entire dataset to predict or **forecast the PM 2.5 readings for te next 30 days**, form the end of the given dataset.
Plotting the **residuals** of the model,I confirmed that they are randomly in general and centered around mean = 0, normally distributed based on the histogram and density plot and the normal qq plot and that the lower lags barely show any significance, on the Correlogram plot.












