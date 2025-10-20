# Car Price Prediction with Gradient Boosting

A machine learning project for predicting used car prices using gradient boosting algorithms and traditional machine learning models.

## 📋 Project Overview

This project addresses the business need of a used car sales service "Не бит, не крашен" to develop an application that can quickly estimate the market value of customers' cars. The solution compares multiple machine learning models to find the optimal balance between prediction quality, prediction speed, and training time.

## 🎯 Business Problem

The car sales service needs a reliable price prediction model that meets three key criteria:
- **Prediction Quality**: High accuracy in estimating car prices
- **Prediction Speed**: Fast inference for real-time application use
- **Training Time**: Reasonable model training duration

## 📊 Data Sources

### Car Sales Dataset
- **Source**: `autos.csv`
- **Records**: 354,369 used car listings
- **Features**: 16 technical and descriptive attributes

### Original Features:
- `DateCrawled` - Date profile was downloaded from database
- `VehicleType` - Type of car body
- `RegistrationYear` - Year of car registration
- `Gearbox` - Type of transmission
- `Power` - Horsepower
- `Model` - Car model
- `Kilometer` - Mileage (km)
- `RegistrationMonth` - Month of registration
- `FuelType` - Type of fuel
- `Brand` - Car brand
- `Repaired` - Whether the car was repaired or not
- `DateCreated` - Date profile was created
- `NumberOfPictures` - Number of car photos
- `PostalCode` - Owner's postal code
- `LastSeen` - Date of last user activity

**Target Variable**: `Price` - Price in euros

## 🛠️ Technical Implementation

### Data Analysis & Preprocessing

#### Data Quality Assessment
- **Missing Values**: Handled in VehicleType, Gearbox, Model, FuelType, Repaired
- **Duplicates**: No duplicates found
- **Data Types**: Mixed numerical and categorical features

#### Feature Engineering
**Categorical Features**:
- `VehicleType`, `Gearbox`, `Model`, `FuelType`, `Brand`, `Repaired`

**Numerical Features**:
- `RegistrationYear`, `Power`, `Kilometer`

#### Data Cleaning
- **Price Filtering**: Removed prices below 200€ (5th percentile)
- **Registration Year**: Filtered to 1980-2016 range
- **Power**: Filtered to 50-500 HP range
- **Missing Value Treatment**:
  - VehicleType and Model: Filled with mode by Brand
  - Gearbox and FuelType: Filled with mode by (Brand, Model)
  - Repaired: Filled with 'yes' and converted to binary

#### Feature Encoding
- **Ordinal Encoding**: VehicleType, Brand, FuelType
- **Binary Encoding**: Gearbox (manual=0, auto=1), Repaired (no=0, yes=1)
- **Scaling**: MinMaxScaler for numerical features

### Machine Learning Modeling

#### Models Implemented
1. **DecisionTreeRegressor** (Non-boosting baseline)
2. **LightGBMRegressor** (Gradient boosting)
3. **CatBoostRegressor** (Gradient boosting with categorical support)

#### Model Training Strategy
- **Train-Test Split**: 75%-25% split
- **Cross-Validation**: 5-fold for hyperparameter tuning
- **Evaluation Metric**: RMSE (Root Mean Squared Error)
- **Hyperparameter Tuning**: RandomizedSearchCV

#### Pipeline Architecture
```python
Data Preprocessing → Feature Engineering → Model Training → Evaluation
```

## 📈 Key Findings

### Model Performance Comparison

| Model | Best RMSE | Fit Time (sec) | Prediction Time (sec) |
|-------|-----------|----------------|----------------------|
| DecisionTreeRegressor | 1,818.59 | 0.32 | 0.03 |
| LightGBM | 1,723.53 | 4.07 | 0.20 |
| CatBoost | 2,374.49 | 0.26 | 0.01 |

### Final Test Performance
- **DecisionTreeRegressor Test RMSE**: 1,771.83

### Feature Importance Analysis

#### Most Influential Features:
1. **RegistrationYear** - Most significant predictor
2. **Power** - Engine horsepower
3. **Kilometer** - Vehicle mileage
4. **Brand** - Car manufacturer
5. **Repaired** - Repair history
6. **VehicleType** - Body type
7. **Gearbox** - Transmission type
8. **FuelType** - Least influential but still relevant

## 🎯 Business Recommendations

### Selected Model: DecisionTreeRegressor

**Rationale for Selection:**

1. **Performance Balance**: 
   - RMSE of 1,771.83 meets the <2,500 requirement
   - Only 2.8% performance gap from LightGBM

2. **Speed Advantages**:
   - **Training Time**: 8x faster than LightGBM
   - **Prediction Time**: 6x faster than LightGBM
   - Suitable for real-time applications

3. **Practical Considerations**:
   - Meets all business criteria
   - Better computational efficiency
   - Easier model interpretation

### Model Strengths for Business Use

**Prediction Quality**: ✓ RMSE under target threshold
**Prediction Speed**: ✓ 0.03 seconds per prediction
**Training Time**: ✓ 0.32 seconds for model updates

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn lightgbm catboost phik
```

### Running the Analysis
1. Clone the repository
2. Ensure datasets are in the `car_store_gradient_boosting_dataset` directory
3. Run the Jupyter notebook: `car_prices_prediction_boosting.ipynb`
4. Follow the step-by-step analysis

### Key Functions
- `describe_numeric()`: Exploratory analysis for numerical features
- `pie_plot()`: Visualization for categorical features
- `fill_na()`: Missing value imputation based on brand/model
- Data preprocessing pipeline with ColumnTransformer

## 📝 Conclusion

This project demonstrates a practical approach to used car price prediction that balances model performance with computational efficiency. The selected DecisionTreeRegressor model provides:

1. Business-Ready Solution: Meets all specified requirements for quality and speed
2. Cost-Effective Implementation: Lower computational requirements
3. Maintainable Architecture: Clear data preprocessing and modeling pipeline
4. Interpretable Results: Feature importance analysis provides business insights

The solution enables the car sales service to provide instant, accurate price estimates to customers while maintaining efficient model operations and update cycles.
