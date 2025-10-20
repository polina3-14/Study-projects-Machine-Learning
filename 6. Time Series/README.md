# Time Series Forecasting for Taxi Orders

A time series forecasting project to predict the number of taxi orders for the next hour using machine learning models.

## 📋 Project Overview

This project addresses the business need of "Чётенькое такси" company to forecast taxi demand at airports. The solution helps optimize driver allocation during peak hours by predicting the number of taxi orders for the next hour.

## 🎯 Business Problem

The taxi company needs to:
- **Forecast Demand**: Predict number of taxi orders for the next hour
- **Optimize Resources**: Efficiently allocate drivers during peak periods
- **Meet Quality Standards**: Achieve RMSE ≤ 48 on test data

## 📊 Data Sources

### Taxi Orders Dataset
- **Source**: `taxi.csv`
- **Period**: March 1, 2018 to August 31, 2018
- **Records**: 26,496 observations (10-minute intervals)
- **Target Variable**: `num_orders` - Number of taxi orders

### Data Characteristics
- **Time Range**: 6 months of historical data
- **Recording Interval**: Every 10 minutes
- **Final Format**: Resampled to 1-hour intervals (4,416 observations)

## 🛠️ Technical Implementation

### Data Analysis & Preprocessing

#### Data Quality Assessment
- **Missing Values**: No missing values detected
- **Data Integrity**: Chronologically ordered time series
- **Resampling**: Aggregated from 10-minute to 1-hour intervals

#### Time Series Analysis
- **Trend Analysis**: Identified increasing trend over time
- **Seasonality Detection**: 
  - Daily seasonality patterns
  - Peak hours around midnight
  - Lowest demand at 6 AM
- **Stationarity**: Non-stationary time series with trend and seasonality

#### Feature Engineering
**Temporal Features**:
- `lag_1`, `lag_2`, `lag_24`, `lag_48` - Historical values at different time lags
- `rolling_mean` - 24-hour moving average
- `day` - Day of month
- `dayofweek` - Day of week (0-6)
- `hour` - Hour of day (0-23)

### Machine Learning Modeling

#### Models Implemented
1. **DecisionTreeRegressor**
2. **LinearRegression** 
3. **RandomForestRegressor**
4. **GradientBoostingRegressor**

#### Model Training Strategy
- **Train-Test Split**: 90%-10% temporal split (no shuffling)
- **Cross-Validation**: TimeSeriesSplit (10 folds) to prevent data leakage
- **Evaluation Metric**: RMSE (Root Mean Squared Error)
- **Hyperparameter Tuning**: RandomizedSearchCV

#### Pipeline Architecture
```python
Feature Engineering → Data Preprocessing → Model Training → Time Series Validation
```

## 📈 Key Findings

### Model Performance

#### Best Model: RandomForestRegressor
- **Training RMSE**: 24.17
- **Test RMSE**: 43.58
- **Hyperparameters**:
  - `n_estimators`: 200
  - `max_depth`: 40
  - `preprocessor`: MinMaxScaler

#### Model Comparison
All models were evaluated, with RandomForestRegressor demonstrating the best performance while meeting the business requirement of RMSE ≤ 48.

### Time Series Insights

#### Seasonal Patterns
- **Daily Seasonality**: Clear 24-hour patterns
- **Peak Hours**: Maximum orders around midnight
- **Low Periods**: Minimum orders at 6 AM

#### Autocorrelation Analysis
- **Significant Lags**: 1, 2, 24, and 48 hours
- **Daily Patterns**: Strong correlation at 24-hour intervals
- **Weekly Patterns**: Less pronounced weekly seasonality

## 🎯 Business Recommendations

### Selected Model: RandomForestRegressor

**Performance Justification**:
- **RMSE**: 43.58 (below 48 threshold)
- **Reliability**: Consistent performance on test data
- **Robustness**: Handles non-linearity and complex patterns

### Operational Benefits
1. **Peak Hour Planning**: Accurate prediction of high-demand periods
2. **Driver Scheduling**: Optimized allocation during predicted peaks
3. **Resource Management**: Efficient vehicle deployment
4. **Customer Service**: Reduced wait times during high demand

### Implementation Strategy
- **Real-time Prediction**: Hourly forecasts for next hour demand
- **Driver Notifications**: Alert system for upcoming peak periods
- **Performance Monitoring**: Continuous model evaluation
- **Retraining Schedule**: Monthly model updates with new data

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels
```

### Running the Analysis
1. Clone the repository
2. Ensure datasets are in the `time_taxi_dataset` directory
3. Run the Jupyter notebook: `time_series_taxi_orders.ipynb`
4. Follow the step-by-step analysis

### Key Functions
- `make_features()`: Creates time-based features and lags
- `seasonal_decompose()`: Decomposes time series into trend, seasonality, and residuals
- `plot_acf()`/`plot_pacf()`: Autocorrelation analysis
- TimeSeriesSplit: Temporal cross-validation

## 📝 Conclusion

This project demonstrates a practical time series forecasting solution for taxi demand prediction. The implemented RandomForestRegressor model provides:

1. Business Value: Meets the RMSE ≤ 48 requirement with 43.58 test performance
2. Operational Efficiency: Enables proactive driver allocation
3. Technical Robustness: Handles complex temporal patterns and seasonality

The solution empowers the taxi company to optimize their operations by accurately predicting demand fluctuations, ultimately improving customer satisfaction and operational efficiency.
