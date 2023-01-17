## Introduction/ Inspiration
This project is inspired by the fact that Bitcoin, the most popular and commonly utilized cryptocurrencies available on the crypto market, has experienced volatility since its
introduction unlike anything we have witnessed from traditional asset classes such as stocks and commodities among others. The heightened volatility in the crypto market indicates that
investors might or have made/lost a significant amount of money. Therefore, the in-depth technical analysis of Bitcoin volatility and other crucial fundamental factors
that drive its variability are very important for investment purposes.

---
### Overview
The dataset was extracted from [Kaggle](http://www.kaggle.com/) public datasets, a span of 5 years from 2017 to 2022. The dataset had no missing values. All Outliers
were included as such extremes are important in highlighting how the cryptocurrency behaves unexpectedly (volatile). I conducted a time series analysis to understand the trend or systemic pattern overtime on the crypto for a better forecast.
I used GARCH(1,1) as the volatility forecasting model for the crypto as proposed by Bollerslev,Tim (1986). A Walk Forward Validation evaluation method was used on the test data for the dataset.This is because the predictions over time become less and less acurate and hence it's more realistic to retrain the model as new data becomes available, giving the model good forecasts at each time step.
