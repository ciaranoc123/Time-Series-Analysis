# Balancing-Market-Forecast

This repository contains code and datasets used for forecasting in both the Day-Ahead (DAM) market and the balancing market (BM).
Access to the full datasets can be found at: [Google Drive Link](https://drive.google.com/drive/u/0/folders/1GSJhwvhRZ5X5A0uJRZzkzCuJ8xu9kDcX)

### Balancing Market

For the Balancing Market (BM), we predict BM prices for the next 16 open settlement periods. The forecast horizon starts at \( t+2 \) as at time \( t \), the market periods \( t \) and \( t+1 \) are already closed, and adjustments can only be made from \( t+2 \), denoted as:

Y_{BM}=[BMP_{t+2},...,BMP_{t+17}].


In the BM dataset file this is presented as:

Y_{BM}=[lag_2y,...,lag_17y].


#### Historic data

The historical data used for BM price prediction includes:

- *BM Prices (BMP)*: BM prices from the most recent and available 24 hours: \( [BMP_{t-51},...,BMP_{t-3}] \).
- *BM Volume (BMV)*: The most recent 48 observations of BM volume: \( [BMV_{t-51},...,BMV_{t-3}] \).
- *Forecast Wind - Actual Wind (WDiff)*: Difference in forecast and actual wind data for the last 48 settlement periods: \( [WDiff_{t-50},...,WDiff_{t-2}] \).
- *Interconnector Values (I)*: Interconnector flows from the previous 24 hours: \( [I_{t-50},...,I_{t-2}] \).
- *DAM Prices (DAM)*: DAM prices from the previous 24 hours, used at an hourly granularity for each half-hour settlement period: \( [DAM_{t-48},...,DAM_t] \).

In the BM dataset file the headers are:

BMP=[lag_-3x1,...,lag_-51x1]; BMV=[lag_-3x2,...,lag_-51x2]; WDiff=[lag_-2x3,...,lag_-50x3]; I=[lag_-2x12,...,lag_-50x12]; DAM=[lag_0x6,...,lag_-47x6]

Unused Data:

Carbon Price Data - lag\_0x4

Gas Price Data - lag\_0x5

#### Forward/future-looking data

The future-looking data for BM price prediction includes:

- *Physical Notifications Volume (PHPN)*: The sum of physical notifications for the forecast horizon, spanning \( [PHPN_{t+2},...,PHPN_{t+17}] \).
- *Net Interconnector Schedule (PHI)*: Interconnector schedule for the forecast horizon: \( [PHI_{t+2},...,PHI_{t+17}] \).
- *Renewable Forecast (PHFW)*: TSO renewables forecast for non-dispatchable renewables for the forecast horizon: \( [PHFW_{t+2},...,PHFW_{t+17}] \).
- *Demand Forecast (PHFD)*: TSO demand forecast for the forecast horizon: \( [PHFD_{t+2},...,PHFD_{t+17}] \).
- *DAM Prices (DAM)*: DAM prices for the next 8 hours: \( [DAM_{t+1},...,DAM_{t+16}] \).

In the BM dataset file these headers are:

PHPN=[lag_2x7},...,lag_17x7]; PHI=[lag_2x8},...,lag_17x8]; PHFW=[lag_2x9},...,lag_17x9]; PHFD=[lag_2x10},...,lag_17x10]; DAM=[lag_2x11},...,lag_17x11]  

### Day-Ahead Market (DAM)
In our analysis, we focus on predicting DAM prices, with the forecast horizon extending to the subsequent 24 settlement periods.
The historical data considered for DAM price prediction includes DAM prices for the previous 168 hours and the wind and demand forecasts for the same interval. We then consider the TSO wind and demand forecasts for the forecasting horizon of 24 settlement periods.

The variation in time intervals for historical data is due to availability, limited to the most recent and accessible 48 observations from the data source. For further details on our forecasting approach, market structure, datasets, and variables for both the DAM and BM.


#### Data Pre-Processing
We remove day light savings days and we impute missing variables with the mean of the previous 30 days or with the most recent data point depending on the context.


## Purpose
The purpose of this project is to analyze and compare different forecasting models for both the DAM and BM markets, aiming to improve price forecasting accuracy.

## Code

### Forecasting Library

The 'Forecasting Library' directory contains the main code files used for forecasting. Below is a list of files included:

- BM Forecasting.ipynb: This is the main notebook file containing code for running different forecasting models.

- Modelling_Functions_LEAR.py: Python script containing functions related to Linear Regression modeling.
- Modelling_Functions_ARIMA.py: Python script containing functions related to ARIMA modeling.
- Modelling_Functions_SVR_XGB_RF.py: Python script containing functions related to Support Vector Regression, XGBoost, and Random Forest modeling.
- Modelling_Functions_SH_DNN.py: Python script containing functions related to Single-Head Deep Neural Network modeling.
- Modelling_Functions_MH_DNN.py: Python script containing functions related to Multi-Head Deep Neural Network modeling.

The 'BM Forecasting.ipynb' notebook serves as the main file for running different forecasting models. It imports and utilizes the functions defined in the Python scripts mentioned above.


Please note that access to the full datasets and additional code may be provided upon request or after the paper's review process is complete.
