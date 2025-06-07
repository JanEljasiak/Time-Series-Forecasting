# Time Series Forecasting: SARIMA, UCM, and XGBoost Models

This project presents a comprehensive analysis and forecasting of a time series dataset using three different modeling techniques: **Seasonal ARIMA (SARIMA)**, **Unobserved Components Model (UCM)**, and **XGBoost**. The objective is to predict missing values for December 2016 based on historical hourly data.

---

## 📁 Dataset

- **File**: `ts2024.csv`
- **Observations**: 16,800 hourly data points
- **Time Range**: January 1, 2015 – November 30, 2016
- **Forecast Target**: Missing values for December 2016 (744 time steps)

---

## 🔍 Project Overview

### 1. Data Preprocessing
- The `DateTime` column was converted to a datetime index.
- Temporal features were engineered: `Year`, `Month`, `Day`, `Hour`, `DayOfWeek`, and `Quarter`.

### 2. Exploratory Data Analysis
- Strong daily seasonality identified through:
  - Seasonal decomposition (additive model with a 24-hour period)
  - Autocorrelation plots (significant lags at 24-hour intervals)

### 3. Train-Test Split
- **Training Set**: First 16,080 data points (Jan 1, 2015 – Oct 31, 2016)
- **Testing Set**: Final 720 data points (Nov 1 – Nov 30, 2016)

---

## 📈 Models Used

### 📊 SARIMA
- **Auto ARIMA** was used to determine optimal parameters:
  - `(p,d,q) = (1,0,2)`
  - Seasonal: `(P,D,Q,s) = (2,0,1,24)`
- Evaluated using MAE and MSE.
- Forecasted directly from time series values (no engineered features used).

### 🧱 Unobserved Components Model (UCM)
- Captures trend and seasonal patterns using engineered features.
- Included exogenous variables such as hour, day, month, etc.
- Evaluated using MAE and MSE.

### ⚡ XGBoost
- Selected after testing alternatives (LSTM, Prophet).
- Performed best in modeling complex patterns.
- Hyperparameters (via `RandomizedSearchCV`):
  - `n_estimators = 500`
  - `max_depth = 7`
  - `learning_rate = 0.2`

---

## 📊 Model Evaluation

| Model    | MAE     | MSE     |
|----------|---------|---------|
| SARIMA   | 0.0177  | 0.0015  |
| UCM      | 0.0181  | 0.0015  |
| XGBoost  | **0.0101**  | **0.0009**  |

✅ **XGBoost** achieved the best performance on the November 2016 test set.

---

## 📤 Final Forecast

- The models were retrained using the full training data (up to November 30, 2016).
- Final forecasts for December 2016 were generated and saved to:

