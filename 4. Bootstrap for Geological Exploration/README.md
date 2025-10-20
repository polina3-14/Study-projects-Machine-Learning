# Geological Exploration: Oil Well Location Selection

A machine learning and statistical analysis project for selecting the most profitable oil drilling location using bootstrap techniques.

## 📋 Project Overview

This project addresses the strategic decision of selecting optimal oil drilling locations for "ГлавРосГосНефть" company. The solution combines machine learning prediction with statistical risk analysis to identify the region with the highest profit potential and acceptable risk levels.

## 🎯 Business Problem

The company needs to determine which of three geological regions offers the best investment opportunity for new oil well development, considering:
- **Budget**: 10 billion RUB for development
- **Target**: 200 best wells selected from 500 exploration points
- **Revenue**: 450,000 RUB per thousand barrels
- **Risk Tolerance**: Maximum 2.5% probability of losses

## 📊 Data Sources

### Geological Survey Data
Three regions with 100,000 oil fields each:
- **Region 0**: `geo_data_0.csv`
- **Region 1**: `geo_data_1.csv` 
- **Region 2**: `geo_data_2.csv`

### Features for Each Region:
- `id`: Unique well identifier
- `f0, f1, f2`: Geological features (significance unknown but relevant)
- `product`: Oil reserves in thousands of barrels (target variable)

## 🛠️ Technical Implementation

### Data Analysis & Preprocessing
- **Data Quality**: Verified no missing values or duplicates
- **Exploratory Analysis**: Distribution analysis and correlation studies
- **Feature Examination**: Identified unique characteristics of each region
- **Data Splitting**: 75/25 train-validation split for model evaluation

### Machine Learning Modeling
- **Algorithm**: Linear Regression (company requirement)
- **Preprocessing**: StandardScaler for feature normalization
- **Evaluation Metrics**: RMSE and R² for model performance
- **Regional Models**: Separate models for each geological region

### Statistical Analysis
- **Bootstrap Technique**: 1000 iterations for profit distribution
- **Risk Assessment**: Probability of loss calculation
- **Confidence Intervals**: 95% confidence intervals for profit estimates
- **Profit Simulation**: Revenue calculation for top 200 wells

## 📈 Key Findings

### Model Performance by Region

#### Region 0
- **RMSE**: 37.76 thousand barrels
- **R²**: 0.273
- **Average Predicted Reserves**: 92k barrels

#### Region 1
- **RMSE**: 0.89 thousand barrels
- **R²**: 0.9996
- **Average Predicted Reserves**: 69k barrels

#### Region 2
- **RMSE**: 40.15 thousand barrels
- **R²**: 0.196
- **Average Predicted Reserves**: 95k barrels

### Profitability Analysis

#### Region 0
- **Average Profit**: 406 million RUB
- **95% Confidence Interval**: -50 to 847 million RUB
- **Risk of Loss**: 6.7%

#### Region 1
- **Average Profit**: 441 million RUB
- **95% Confidence Interval**: 106 to 774 million RUB
- **Risk of Loss**: 1.6%

#### Region 2
- **Average Profit**: 385 million RUB
- **95% Confidence Interval**: -75 to 822 million RUB
- **Risk of Loss**: 7.8%

### Break-even Analysis
- **Minimum Required Reserves**: 111k barrels per well
- **Development Cost per Well**: 50 million RUB
- **Revenue per Well**: 450,000 RUB per thousand barrels

## 🎯 Business Recommendations

### Selected Region: Region 1

**Rationale for Selection:**
1. **Highest Average Profit**: 441 million RUB
2. **Lowest Risk**: 1.6% probability of losses (below 2.5% threshold)
3. **Most Accurate Predictions**: Near-perfect R² score (0.9996)
4. **Predictable Returns**: Narrow confidence interval (106-774 million RUB)

**Key Advantages:**
- **Predictive Accuracy**: Model shows exceptional performance (RMSE = 0.89)
- **Risk Management**: Minimal chance of financial loss
- **Profit Maximization**: Highest expected return among all regions
- **Strategic Fit**: Meets all company risk and budget constraints

### Risk Mitigation Strategy
1. **Phased Development**: Implement in stages to validate predictions
2. **Continuous Monitoring**: Track actual vs predicted reserves
3. **Contingency Planning**: Reserve funds for potential adjustments
4. **Performance Review**: Regular assessment of well productivity

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Running the Analysis
1. Clone the repository
2. Ensure datasets are in the `Geological_exploration_dataset` directory
3. Run the Jupyter notebook: `geologogical_exploration_bootstrap.ipynb`
4. Follow the step-by-step analysis

### Key Functions
- `train_evaluate_model()`: Trains and evaluates linear regression models
- `calculate_profit()`: Simulates profit using bootstrap sampling
- `define_profit_risks()`: Calculates risk metrics and confidence intervals

## 📝 Conclusion
This project  demonstrates how machine learning and statistical analysis can guide strategic investment decisions in oil exploration. The solution provides:

1. Data-Driven Selection: Objective regional comparison based on multiple criteria
2. Risk-Aware Decision Making: Balanced approach considering both profit potential and financial risk
3. Practical Implementation: Ready-to-use methodology for similar exploration decisions

The selection of Region 1 represents the optimal balance between profit potential and risk management, ensuring the highest likelihood of successful investment within the company's constraints.
