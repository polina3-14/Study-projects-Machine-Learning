# Linear Models - Farm Prediction Project

A machine learning project implementing linear models to help "Вольный луг" farm make data-driven decisions about cow purchases from "ЭкоФерма" association.

## 📋 Project Overview

This project develops predictive models to assist a farm in selecting cows based on two key criteria:
1. **Annual milk yield** - at least 6000 kilograms
2. **Milk taste quality** - producing tasty milk

The solution implements both regression and classification models using linear algorithms to address these business requirements.

## 🎯 Business Problem

"Вольный луг" farm needs to objectively evaluate cows from "ЭкоФерма" association to:
- Predict potential milk yield
- Assess probability of producing tasty milk
- Minimize purchasing risks
- Make informed decisions about which cows to buy

## 📊 Data Sources

The project utilizes three main datasets:

### `ferma_main.csv`
- **Description**: Current herd data from "Вольный луг" farm
- **Records**: 634 cows initially (629 after preprocessing)
- **Features**:
  - Cow characteristics: ID, Breed, Father's breed, Age
  - Feed characteristics: Energy Feed Unit, Crude Protein, Sugar-Protein Ratio
  - Pasture characteristics: Pasture type
  - Milk characteristics: Yield, Fat%, Protein%, Taste

### `ferma_dad.csv`
- **Description**: Father information for cows in the main dataset
- **Records**: 629 entries
- **Features**: Cow ID, Father's name

### `cow_buy.csv`
- **Description**: Potential cows for purchase from "ЭкоФерма"
- **Records**: 20 cows
- **Features**: Breed, Pasture type, Father's breed, Father's name, Current fat%, Current protein%, Age

## 🛠️ Technical Implementation

### Models Developed

#### 1. Linear Regression Models (for Milk Yield Prediction)
- **Model 1**: Basic linear regression with core features
- **Model 2**: Enhanced with feature engineering (EKE squared, SPO categorization)
- **Model 3**: Added father's name feature
- **Model 3.1**: Final model excluding multicollinearity

**Best Model**: Model 3.1 achieved:
- R² Score: 0.827
- RMSE: 187.93
- MSA: 144.64

#### 2. Logistic Regression Model (for Milk Taste Classification)
- **Objective**: Predict probability of tasty milk
- **Features**: EKE squared, SPO categorization, Fat%, Pasture type, Protein%
- **Optimization**: Threshold tuning to minimize False Positives

### Key Techniques Applied

- **Data Preprocessing**: Handling duplicates, fixing typos, type conversions
- **Feature Engineering**: 
  - EKE squared for non-linear relationships
  - SPO binary categorization (>0.92)
  - Age and taste as boolean features
- **Model Evaluation**: Comprehensive metrics including R², MSE, RMSE, MSA, Precision, Recall, Accuracy
- **Cross-validation**: Train-test split with random state 42

## 📈 Key Findings

### Data Insights
- Milk yield follows near-normal distribution after removing outliers
- Strong correlations found between yield and EKE (0.72), Fat% (0.71), SPO (0.66)
- Age significantly impacts yield (correlation coefficient: 1.0)
- Four main father bulls with varying offspring counts

### Model Performance
- **Linear Regression**: Successfully predicts yields above 6000kg for all potential purchases
- **Logistic Regression**: High precision (1.0) achievable but with low recall, requiring business trade-off decisions

### Business Recommendations
- With conservative threshold (0.809): No cows meet both criteria risk-free
- With balanced threshold (0.66): 3 cows meet both criteria with acceptable risk
- Recommendation: Purchase cows 1, 9, and 16 from the candidate list

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn phik
```

### Running the Analysis
1. Clone the repository
2. Ensure datasets are in the `datasets/` directory
3. Run the Jupyter notebook: `farm_prediction_with_linear_models.ipynb`
4. Follow the step-by-step analysis and model training process

### Model Deployment
The trained models can be used to:
- Predict milk yield for new cow candidates
- Assess milk taste probability
- Generate purchase recommendations based on business criteria

## 📝 Conclusion
This project demonstrates practical application of linear models to solve real business problems in agriculture. The solution provides a data-driven framework for livestock purchasing decisions, balancing predictive accuracy with business risk considerations.

The modular approach allows for easy adaptation to similar agricultural decision-making scenarios where multiple criteria need to be evaluated simultaneously.


