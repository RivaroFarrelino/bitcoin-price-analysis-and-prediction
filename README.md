# Bitcoin Price Analysis and Forecasting using Prophet

This project performs an end-to-end time series analysis and forecasting of Bitcoin (BTC/USD) prices using historical minute-level data. The workflow covers data preprocessing, exploratory data analysis (EDA), correlation analysis, visualization, and price forecasting using Facebook Prophet.

---

## Dataset

- **Source**: `btcusd_1-min_data.csv`
- **Granularity**: 1-minute OHLCV data
- **Resampling**: Aggregated to daily frequency
- **Time Range**: From the earliest timestamp in the dataset **up to 6 February 2026**
- **Target Variable**: Daily closing price (USD)

---

## Project Workflow

### 1. Data Loading and Inspection
- Load raw BTC/USD minute-level data
- Inspect data types, shape, and basic statistics
- Visualize closing price over time

### 2. Data Preprocessing
- Convert UNIX timestamps to datetime format
- Set timestamp as index
- Resample data to daily frequency using mean aggregation
- Handle missing values using linear interpolation
- Optimize memory usage by downcasting floating-point types

### 3. Exploratory Data Analysis (EDA)
- Distribution analysis using:
  - Histogram
  - Boxplot
  - Violin plot
- Variables analyzed:
  - Open
  - High
  - Low
  - Close
  - Volume

### 4. Feature Engineering
- Normalized volume and price ratios for correlation analysis
- Engineered features:
  - Open/Close ratio
  - High/Low gap
- Correlation heatmap visualization
- Correlation network graph using NetworkX

### 5. Price Visualization
- Candlestick chart using Plotly
- Moving averages:
  - 30-day moving average
  - 50-day moving average
- Interactive HTML output for price trends

---

## Time Series Forecasting with Prophet

### Model Description
Prophet is an open-source forecasting library developed by Facebook that decomposes time series into:
- Trend
- Seasonality (weekly and yearly)
- Changepoints

The model is well-suited for business-oriented time series and interpretable forecasting.

### Data Preparation for Prophet
- Prophet requires two columns:
  - `ds`: date (datetime)
  - `y`: target value (BTC closing price in USD)
- The model uses **non-normalized daily closing prices** to preserve real price scale.

### Model Configuration
- Yearly seasonality enabled
- Weekly seasonality enabled
- Daily seasonality disabled
- Changepoint prior scale set to 0.05

### Forecasting
- Forecast horizon: 90 days
- Outputs:
  - `yhat`: predicted BTC price
  - `yhat_lower`: lower confidence bound
  - `yhat_upper`: upper confidence bound

### Model Evaluation
- Time series cross-validation using rolling windows
- Evaluation metrics:
  - RMSE
  - MAE
  - MAPE
- Visualization of RMSE across forecast horizons

---

## Inference: 7-Day Price Prediction

The trained Prophet model is used to perform inference for the **next 7 days beyond the last available date (6 February 2026)**.

Steps:
- Extend the time index by 7 days
- Generate forecasts without retraining the model
- Extract predicted prices and confidence intervals

This inference provides short-term directional insight and uncertainty bounds rather than exact price guarantees.

---

## Output Artifacts

- Interactive candlestick chart with moving averages (`.html`)
- Prophet forecast plots:
  - Overall forecast
  - Trend and seasonality components
  - Changepoint visualization
- Cross-validation performance metrics
- 7-day inference visualization

---

## Notes and Limitations

- Prophet models historical patterns only and does not account for:
  - Market news
  - Sudden volatility
  - External macroeconomic shocks
- Forecast results should be interpreted as probabilistic estimates, not trading signals.
- The model performs best for trend and seasonality analysis rather than short-term speculative trading.

---

## Future Improvements

- Compare Prophet with ARIMA or SARIMA models
- Use log-returns instead of raw prices
- Integrate technical indicators (RSI, MACD)
- Explore machine learning models such as LSTM or XGBoost
- Deploy forecasts to a dashboard or API

---

## Author

Muhammad Rivaro Farrelino Gozali  

