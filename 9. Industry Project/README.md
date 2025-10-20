# Steel Temperature Prediction - Industrial Optimization Project

A machine learning project implementing regression models to help "Стальная птица" metallurgical plant optimize energy consumption through precise temperature control during steel processing.

## 📋 Project Overview

This project develops predictive models to assist a steel plant in controlling alloy temperature with two key objectives:
1. **Temperature Prediction** - Accurate forecasting of final steel temperature
2. **Energy Optimization** - Reducing electricity consumption during processing

The solution implements multiple regression models with comprehensive feature engineering to address these industrial requirements.

## 🎯 Business Problem

"Стальная птица" metallurgical plant needs to optimize production costs by:
- Predicting final steel temperature with high accuracy (MAE ≤ 6.8°C)
- Understanding key factors affecting temperature changes
- Simulating technological processes for energy optimization
- Reducing electricity consumption during steel processing

## 📊 Data Sources

The project utilizes seven industrial datasets:

### `data_arc_new.csv`
- **Description**: Electrode heating process data
- **Records**: 14,876 measurements initially (14,872 after preprocessing)
- **Features**:
  - Power metrics: Active Power, Reactive Power
  - Timing: Start time, End time
  - Derived: Apparent Power, Duration, Energy calculations

### `data_bulk_new.csv`
- **Description**: Bulk material feeding volumes
- **Records**: 3,129 batches
- **Features**: 15 types of bulk additives (Bulk 1-15)

### `data_bulk_time_new.csv`
- **Description**: Bulk material feeding timestamps
- **Records**: Corresponding timing data for bulk additions

### `data_gas_new.csv`
- **Description**: Gas blowing parameters
- **Records**: 3,239 entries
- **Features**: Gas volume measurements

### `data_temp_new.csv`
- **Description**: Temperature measurement results (target variable)
- **Records**: 18,092 measurements initially (13,921 after preprocessing)
- **Features**: Measurement time, Temperature readings

### `data_wire_new.csv`
- **Description**: Wire material volumes
- **Records**: 3,081 batches
- **Features**: 9 types of wire additives (Wire 1-9)

### `data_wire_time_new.csv`
- **Description**: Wire material feeding timestamps
- **Records**: Corresponding timing data for wire additions

## 🛠️ Technical Implementation

### Models Developed

#### 1. Regression Models (for Temperature Prediction)
- **Linear Regression**: Baseline model with standardized features
- **Random Forest Regressor**: Ensemble approach with hyperparameter tuning
- **Support Vector Regressor**: Non-linear relationship modeling
- **CatBoost Regressor**: Gradient boosting with categorical support

**Best Model**: CatBoost Regressor achieved:
- MAE Score: 5.99°C (exceeds requirement of 6.8°C)
- Training MAE: 6.39°C
- No signs of overfitting

### Key Techniques Applied

- **Data Preprocessing**: Anomaly detection, missing value imputation, outlier removal
- **Feature Engineering**:
  - Power calculations: Apparent power from active/reactive components
  - Energy metrics: Active and reactive energy based on duration
  - Additive aggregation: Combined rare bulk and wire materials
  - Temporal features: Heating duration calculations
- **Feature Selection**: Eliminated multicollinearity, removed insignificant additives
- **Model Evaluation**: Comprehensive metrics including MAE, cross-validation, permutation importance

### Hyperparameter Optimization
Used RandomizedSearchCV with 5-fold cross-validation:
- **CatBoost**: Learning rate (0.01, 0.1), iterations (100-300), depth (4-8)
- **Random Forest**: n_estimators (200-300), max_depth (10-20)
- **SVR**: Kernel types, C parameter (0.01-100), gamma optimization

## 📈 Key Findings

### Data Insights
- **Heating Duration**: Strongest predictor of final temperature (direct correlation)
- **Initial Temperature**: Significant positive impact on final temperature
- **Bulk Additives**: Bulk 15 and Bulk 6 show substantial temperature influence
- **Total Bulk Volume**: Negative correlation - more additives lead to cooling effects
- **Power Metrics**: Active power more informative than reactive power

### Model Performance
- **CatBoost Regressor**: Superior performance with best generalization
- **Feature Importance**: Duration (28%), Initial Temp (22%), Bulk 15 (15%), Bulk 6 (12%)
- **SHAP Analysis**: Confirmed heating duration as primary driver, identified non-linear relationships

### Business Recommendations

#### Immediate Actions
1. **Optimize Heating Duration**: Focus on batches with high initial temperature for energy savings
2. **Additive Management**: Monitor bulk material additions to minimize temperature drops
3. **Process Simulation**: Use model for real-time temperature prediction and adjustment

#### Strategic Recommendations
- Implement automated alerts for abnormal heating patterns
- Develop additive feeding strategies to reduce cooling effects
- Create digital twin for process optimization experiments
- Establish continuous monitoring of key predictive features

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn catboost shap phik
```

### Running the Analysis

1. Clone the repository
2. Ensure datasets are in the correct directory structure
3. Run the Jupyter notebook: `industry_project_for_steel_temperature_prediction.ipynb`
4. Follow the step-by-step analysis from data loading to model deployment

### Model Deployment

The trained CatBoost model can be used to:

- Predict final steel temperature for new batches
- Simulate process changes for energy optimization
- Generate real-time recommendations for operators
- Identify potential energy savings opportunities

## 📝 Conclusion

This project demonstrates the successful application of machine learning in heavy industry, achieving temperature prediction accuracy beyond business requirements. The CatBoost model provides a robust solution for energy optimization while maintaining interpretability through comprehensive feature analysis.

The modular approach allows for easy adaptation to similar industrial processes where temperature control and energy efficiency are critical factors. The solution enables data-driven decision making for sustainable manufacturing practices.