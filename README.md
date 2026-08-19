# Rainfall Forecasting using Time Series Analysis

## Project Overview

This project focuses on analyzing historical rainfall data and building a **Time Series Forecasting model** to predict rainfall for the next **12 months**.

The project uses **SARIMA (Seasonal AutoRegressive Integrated Moving Average)** to capture trends and seasonal patterns in rainfall data.

The project also forecasts **highest daily rainfall** for the next 12 months.

---

## Objective

The main objectives of this project are:

* Analyze historical rainfall data
* Clean and preprocess the datasets
* Perform Exploratory Data Analysis (EDA)
* Analyze rainfall trends and seasonality
* Check stationarity using the ADF test
* Perform seasonal decomposition
* Analyze ACF and PACF
* Build a SARIMA forecasting model
* Evaluate model performance
* Forecast rainfall for the next 12 months
* Forecast highest daily rainfall for the next 12 months

---

## Business Problem

Rainfall forecasting is useful for:

*  Agriculture planning
*  Water resource management
*  Disaster prevention
*  Weather-related planning
*  Infrastructure planning

Accurate rainfall forecasting can help organizations make better decisions based on expected rainfall patterns.

---

##  Dataset

Three rainfall datasets were used:

1. **Monthly Total Rainfall**
2. **Monthly Highest Daily Rainfall**
3. **Monthly Number of Rainy Days**

### Dataset Period

**January 1982 – June 2020**

The datasets were merged using the common `month` column.

The final dataset contains information related to:

* Month
* Total Rainfall
* Highest Daily Rainfall
* Number of Rainy Days

---

##  Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Statsmodels
* Scikit-learn

### Time Series Libraries

* `SARIMAX`
* `ADF Test`
* `seasonal_decompose`
* `ACF`
* `PACF`

---

##  Project Workflow

```text
Historical Rainfall Data
          ↓
     Data Loading
          ↓
     Data Cleaning
          ↓
   Exploratory Data Analysis
          ↓
    Feature Engineering
          ↓
    Stationarity Test
          ↓
 Seasonal Decomposition
          ↓
       ACF & PACF
          ↓
      SARIMA Model
          ↓
    Model Evaluation
          ↓
 Forecast Next 12 Months
          ↓
   Business Insights
```

---

#  Exploratory Data Analysis

The project performs several EDA steps to understand the rainfall dataset.

### Data Analysis

* Dataset shape
* Column names
* Data types
* Missing values
* Duplicate records
* Statistical summary

### Visualizations

The following visualizations were performed:

* Monthly rainfall trend
* Highest daily rainfall trend
* Rainy days trend
* Average monthly rainfall
* Average yearly rainfall
* Histogram
* Box plot
* Scatter plot
* Pair plot
* Correlation heatmap

### EDA Insights

The analysis showed that:

* Monthly rainfall varies significantly over time.
* Some months experience very high rainfall.
* Rainy days generally increase with total rainfall.
* Seasonal patterns are visible.
* The dataset is suitable for time series forecasting.

---

# Time Series Analysis

## Stationarity

Stationarity was analyzed using:

* Rolling Mean
* Rolling Standard Deviation
* Augmented Dickey-Fuller (ADF) Test

### ADF Test

The ADF test checks whether the time series is stationary.

### Hypotheses

**Null Hypothesis (H₀):**

The time series is not stationary.

**Alternative Hypothesis (H₁):**

The time series is stationary.

### Decision Rule

```text
p-value < 0.05
       ↓
Reject H₀
       ↓
Series is Stationary
```

```text
p-value >= 0.05
       ↓
Fail to Reject H₀
       ↓
Series is Non-Stationary
```

---

#  Seasonal Decomposition

Seasonal decomposition separates the rainfall time series into:

```text
Time Series
     ↓
 ┌───────────┐
 │   Trend   │
 ├───────────┤
 │ Seasonal  │
 ├───────────┤
 │ Residual  │
 └───────────┘
```

### Trend

Shows the long-term movement of rainfall.

### Seasonal

Shows repeating yearly rainfall patterns.

### Residual

Represents random variations remaining after removing trend and seasonality.

---

#  ACF & PACF

## ACF

**Autocorrelation Function (ACF)** measures the correlation between the current observation and previous observations.

ACF helps in selecting the **MA (q)** component.

## PACF

**Partial Autocorrelation Function (PACF)** measures the relationship between observations after removing the effects of intermediate lags.

PACF helps in selecting the **AR (p)** component.

---

#  SARIMA Model

The project uses **SARIMA** because rainfall data contains seasonal behavior.

SARIMA stands for:

**Seasonal AutoRegressive Integrated Moving Average**

### Model Parameters

```text
p = 1
d = 0
q = 1
```

### Seasonal Parameters

```text
P = 1
D = 1
Q = 1
m = 12
```

Therefore, the model used is:

```text
SARIMA(1,0,1)(1,1,1,12)
```

The seasonal period of `12` represents yearly seasonality in monthly rainfall data.

---

#  Model Training

The SARIMA model was implemented using `SARIMAX`.

```python
model = SARIMAX(
    train,
    order=(1,0,1),
    seasonal_order=(1,1,1,12),
    enforce_stationarity=False,
    enforce_invertibility=False
)

sarima_model = model.fit()
```

---

#  Model Evaluation

The model was evaluated using:

### 1. MAE — Mean Absolute Error

Measures the average absolute difference between actual and predicted values.

### 2. MSE — Mean Squared Error

Measures the average squared difference between actual and predicted values.

### 3. RMSE — Root Mean Squared Error

The square root of MSE.

```text
Lower MAE  → Better
Lower MSE  → Better
Lower RMSE → Better
```

The project uses an **80% training and 20% testing split** for model evaluation.

---

#  12-Month Rainfall Forecast

After evaluating the model, the SARIMA model was fitted using the full time series and used to forecast the next **12 months**.

```python
forecast = final_model.forecast(steps=12)
```

A forecast dataframe is created containing:

| Column              | Description        |
| ------------------- | ------------------ |
| Month               | Future month       |
| Forecasted_Rainfall | Predicted rainfall |

The forecast is also saved as:

```text
Rainfall_Forecast_12_Months.csv
```

---

#  Highest Daily Rainfall Forecast

A second SARIMA model was created to forecast **highest daily rainfall**.

```python
highest_model = SARIMAX(
    highest_series,
    order=(1,0,1),
    seasonal_order=(1,1,1,12),
    enforce_stationarity=False,
    enforce_invertibility=False
)
```

The model forecasts the highest daily rainfall for the next 12 months.

Output file:

```text
Highest_Daily_Rainfall_Forecast.csv
```

---


# Key Learning Outcomes

Through this project, I gained practical experience in:

* Time Series Analysis
* Time Series Data Preprocessing
* Exploratory Data Analysis
* Stationarity Testing
* Augmented Dickey-Fuller Test
* Seasonal Decomposition
* ACF and PACF
* SARIMA
* Time Series Forecasting
* Model Evaluation
* MAE, MSE and RMSE
* Forecast Visualization
* Pandas and NumPy
* Matplotlib and Seaborn
* Statsmodels

---

#  Future Improvements

The project can be further improved by:

* Comparing SARIMA with ARIMA and Prophet
* Performing automated hyperparameter tuning
* Using walk-forward validation
* Adding external weather variables
* Including temperature and humidity
* Using advanced forecasting models
* Building an interactive forecasting dashboard
* Deploying the forecasting model as a web application

---

#  Final Result

This project successfully analyzes historical rainfall data and builds a **SARIMA-based time series forecasting model**.

The model generates:

*  Monthly rainfall forecasts for the next 12 months
*  Highest daily rainfall forecasts for the next 12 months

The project demonstrates how historical time series data can be analyzed to identify **trend, seasonality, and temporal patterns** and then used to generate future forecasts.

---

##  Author

**Aravind T**

### Skills Demonstrated

`Python` `Pandas` `NumPy` `Time Series` `SARIMA` `Statistics` `EDA` `Matplotlib` `Seaborn` `Statsmodels` `Machine Learning`

---
