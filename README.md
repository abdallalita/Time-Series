# [Gold Volatility Forecasting](#Introduction-1)
# [Volatility Forecasting](#Introduction)
# [Air Quality PM 2.5 readings Prediction](#Inspiration)

## Introduction-1
Gold is one of the most important and actively traded assets in global financial markets. Its price often fluctuates with economic indicators, market indices, and geopolitical events, making volatility forecasting essential for both risk management and trading strategies. In this project, I apply the GARCH (Generalized Autoregressive Conditional Heteroskedasticity) model to forecast gold price volatility. 

**The objective is to capture and predict fluctuations in gold’s returns, providing insights that can help traders and investors refine their strategies and manage risk more effectively**

---
### Dataset definition
The dataset contains 1718 daily observations.
Source: Yahoo Finance
Time Period: November 18, 2011 – January 1, 2019
Columns:Date and Adjusted closing prices.

### Data Preprocessing
Checked for duplicates → None found.
Sorted dates chronologically to ensure proper time-series structure.
No missing values detected.
Created log returns to transform prices into a stationary series suitable for volatility modeling.

### Exploratory Data Analysis (EDA) and Model Suitability Checks
Before fitting a GARCH model, it is essential to verify that the return series has the properties that make GARCH appropriate.
**1. Price Trends**
Visualized gold price series.
The price shows a general downward trend over the sample period (2011–2018).
Since raw prices are non-stationary, we worked with log returns instead.

2. Returns series
Returns were calculated as the log difference of adjusted close prices.
The return series oscillates around zero with no visible trend.
Augmented Dickey-Fuller (ADF) test confirmed stationarity of returns.

3. Volatility Clustering
The return series exhibits volatility clustering (periods of high volatility followed by high volatility, and low by low).
This is a key characteristic that motivates GARCH-type models.

4. Autocorrelation Analysis
Uisng both Ljung-Box test & ACF plot there was significant autocorrelation in squared returns, evidence of volatility clustering, justifies GARCH use.
This strongly suggests that conditional heteroskedasticity models (GARCH) are suitable.

5. Summary Statistics
Mean: approximately 0 hence no persistent drift.
Standard Deviation: approximately 2.45 hence moderate volatility.
EXtreme values range: from -11.31% to +12.00% showing presence of large shocks.
Skewness: slight positive asymmetry since positive returns more spread out.

6. Distribution of Returns
Histogram peaked around zero with heavy tails indicating extreme price movements.
Kurtosis: excess > 0 hence leptokurtic distribution (fat tails).
Confirms that large movements occur more often than under a normal distribution.

### Modeling with GARCH(1,1), diagnostics and assumption Checks
Simple yet effective baseline model where variance depends on both past shocks (ARCH term) and past volatility (GARCH term).
After fitting the GARCH(1,1) model, it is necessary to verify that the model adequately explains the volatility structure of the data. The following diagnostics were performed:
1. Autocorrelation of Standardized Squared Residual
ACF plots of residuals showed all spikes within confidence bands hence no significant autocorrelation left. Also the Ljung-Box test confirmed that.
This indicates that volatility clustering has been captured by the model.

2. ARCH Effects Test
Performed an ARCH-LM test on standardized residuals.
Results showed no remaining ARCH effects, confirming the adequacy of the model in modeling conditional variance.

3. Parameter Significance
All estimated parameters were statistically significant.
Both α and β > 0, with α + β close to 1, the model adequately captures volatility dynamics.

### Model Validation
To ensure that the GARCH(1,1) model provides reliable forecasts beyond the training sample, I performed out-of-sample validation using a rolling window walk-forward approach. Financial time series like gold prices change over time, and old patterns may no longer reflect current market dynamics. Unlike an expanding window, which risks overweighting outdated data, the rolling approach always trains on the most recent observations, making the model more adaptive to evolving volatility conditions. It strikes a balance between learning from sufficient history and adapting to changing market dynamics, making it more realistic for financial forecasting.
- Results:
Plotted Forecasted Volatility vs Realized Volatility.
Both series moved closely together — rising and falling around the same periods.
Indicates that the GARCH(1,1) model effectively tracks volatility clustering.

### Evaluation Metrics
To quantify performance, I used standard volatility forecast loss functions:
Mean Absolute Error (MAE): measures average deviation.
Mean Squared Error (MSE): penalizes larger errors.
QLIKE Loss: specifically designed for volatility forecasts.
All metrics confirmed that the forecasts were reasonably accurate.

### Final future volatility Forecasts
Produced a 10-day ahead forecast from the end of the dataset (post-2019-01-01).
Forecasts were stable and slightly increasing:
from approximately 2.25% daily volatility on 2019-01-01. to 2.27% daily volatility by 2019-01-14.
This gradual increase is consistent with persistent volatility dynamics.

### Conclusion
This project demonstrated how the GARCH(1,1) model can effectively capture and forecast the volatility of gold prices. The final 10-day ahead forecasts indicated stable but slightly increasing volatility, providing insights that can support traders and investors in refining strategies and managing risk.

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












