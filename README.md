# S&P 500 Price Prediction Model (using an ARIMA framework)
Created an ARIMAX model to predict future prices for the indx fund: S&P 500.

## Virtual Environment (library installations)
To run the notebook on your own machine, please activate the virtual environment connected to this repository ("arima") and run the following command:
Activate venv (virtual environment)
- On mac: ```source arima/bin/activate```
- On windows: ```arima\source\activate```

Alternatively, download the following libraries:
```
pip install pandas yfinance matplotlib statsmodels numpy <=2.0.3 pmdarima
```
### Find full report [here:](https://www.notion.so/Forecasting-a-Portfolio-s-Future-Value-using-ARIMA-19ee3c3ed73680e382d9e029cf36391d)

## Overview of Process
- Initially started by looking at the ACF and PACF of the training set we made for the S&P 500 to determine whether any patterns or seasonality occurred with our historical data. We also performed an ADF (Augmented-Dickey Fuller) test to see whether our data was stationary in levels form - and found that it was stationary with an Order of Integration of 1 $I=1$. 

- Used the pmdarima library to find the optimal number of lags for our AR and MA parts using the AIC, BIC and HQIC (info. criterions). This could have been done manually, and the outcome would be fairly similar (and potentially identical), but for efficiency we utilise the aforemationned method. More detail about the manual method can be found in the [report](https://www.notion.so/Forecasting-a-Portfolio-s-Future-Value-using-ARIMA-19ee3c3ed73680e382d9e029cf36391d)

- Proceeded to test the accuracy of our ARIMA forecast on the training and testing set, and found that there was a high following between actual values and forecast vales (of ~99%).

- Predicted future values with an ARIMA(0,1,0) and found that there was no representation on the movement of S&P prices. Decided to create an ARIMA model which included exogeneous variables.

- Decided to include NASDAQ, but found it had too high of a correlation with the S&P 500 to be included as an exogeneous variable, so we were worried about multcollinearity creating a misleading prediction. Decided to include my 'macro' variables: (i.r, pi, crude oil prices and VIX).

- Including these variables showed our previous predictions were valid (price pattern remained), whilst also emphasising predicted downturns and upturns (including the volatility index emphasised the movement of prices, thus making our predictions more market like).

- Resulted in an ARIMAX(4,1,2) model to predict S&P 500 prices.