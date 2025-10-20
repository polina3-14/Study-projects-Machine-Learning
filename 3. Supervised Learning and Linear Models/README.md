# HR Analytics: Employee Satisfaction and Turnover Prediction

A machine learning project for predicting employee satisfaction levels and turnover risk for the "Работа с заботой" company.

## 📋 Project Overview

This project addresses two critical HR challenges through predictive modeling:
1. **Employee Satisfaction Prediction** - Regression task to predict job satisfaction rates (0-1 scale)
2. **Employee Turnover Prediction** - Classification task to predict employee attrition risk

## 🎯 Business Problem

The HR department needs data-driven solutions to:
- Monitor and predict employee satisfaction levels
- Identify employees at risk of leaving the company
- Develop proactive retention strategies
- Optimize HR resource allocation

## 📊 Data Sources

### Employee Satisfaction Dataset
- **Training**: 4,000 employees with satisfaction ratings
- **Test**: 2,000 employees for model validation
- **Features**:
  - Department, Job level, Workload
  - Employment years, Salary
  - Last year promotion, Violations
  - Supervisor evaluation (1-5 scale)

### Employee Turnover Dataset
- **Training**: 4,000 employees with turnover status
- **Test**: 2,000 employees for model validation
- **Target**: Binary classification (quit/stay)

## 🛠️ Technical Implementation

### Data Preprocessing
- **Data Cleaning**: Handled missing values in department and level columns
- **Feature Engineering**: 
  - Boolean encoding for promotion/violation features
  - Ordinal encoding for job levels and workload
  - One-hot encoding for department categories
- **Data Integration**: Merged test datasets using employee IDs

### Models Developed

#### Task 1: Satisfaction Prediction (Regression)
- **Algorithms**: Decision Tree Regressor, Linear Regression
- **Preprocessing**: MinMaxScaler for numerical features
- **Best Model**: DecisionTreeRegressor
- **Evaluation Metric**: SMAPE (Symmetric Mean Absolute Percentage Error)

#### Task 2: Turnover Prediction (Classification)
- **Algorithms**: Decision Tree, KNN, SVM, Logistic Regression
- **Feature Selection**: SelectKBest with mutual information
- **Best Model**: DecisionTreeClassifier with feature selection
- **Evaluation Metric**: ROC-AUC

### Key Techniques
- **Pipeline Architecture**: Integrated preprocessing and modeling
- **Hyperparameter Tuning**: RandomizedSearchCV with 5-fold cross-validation
- **Model Interpretation**: SHAP analysis for feature importance
- **Feature Selection**: Mutual information for optimal feature subset

## 📈 Key Findings

### Employee Satisfaction Analysis
**Most Influential Factors:**
1. **Supervisor Evaluation** - Strongest predictor (SHAP importance)
2. **Employment Years** - Longer tenure correlates with higher satisfaction
3. **Job Level** - Junior employees show higher satisfaction
4. **Salary** - Moderate correlation with satisfaction

**Model Performance:**
- **Best Model**: DecisionTreeRegressor
- **SMAPE Score**: 14.3% on test data
- **Key Parameters**: min_samples_split=6, min_samples_leaf=3

### Employee Turnover Analysis
**High-Risk Employee Profile:**
- **Department**: Technology and Sales departments highest risk
- **Job Level**: Junior employees most likely to leave
- **Tenure**: Shorter employment periods (1-3 years)
- **Compensation**: Lower salary ranges
- **Career Growth**: No recent promotions
- **Engagement**: Lower workload correlates with higher turnover

**Model Performance:**
- **Best Model**: DecisionTreeClassifier with feature selection
- **ROC-AUC Score**: 0.915 on test data
- **Key Parameters**: min_samples_split=11, min_samples_leaf=3

### Correlation Insights
- Strong correlation between workload and salary (0.74-0.79)
- Job level strongly correlates with salary and tenure
- Supervisor evaluation highly correlated with satisfaction (0.76-0.77)
- Employment years and salary key predictors for turnover

## 🎯 Business Recommendations

### Retention Strategy
1. **Targeted Interventions**
   - Focus on junior employees in technology and sales departments
   - Implement mentorship programs for high-risk groups
   - Develop clear career progression paths

2. **Compensation and Benefits**
   - Review salary structures for junior positions
   - Implement performance-based bonus systems
   - Consider tenure-based benefits

3. **Management Development**
   - Train supervisors on effective evaluation and feedback
   - Implement regular check-ins for at-risk employees
   - Develop leadership programs for middle management

4. **Workload Optimization**
   - Balance workload distribution across departments
   - Monitor workload for junior employees
   - Implement workload assessment tools

### Proactive Measures
1. **Early Warning System**
   - Use the turnover prediction model for risk assessment
   - Implement quarterly satisfaction surveys
   - Develop intervention protocols for high-risk employees

2. **Career Development**
   - Create clear promotion timelines
   - Implement skills development programs
   - Offer cross-departmental training opportunities

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn phik shap
```

### Running the Analysis

1. Clone the repository
2. Ensure datasets are in the `HR_project` directory
3. Run the Jupyter notebook: `HR-analitycs_classification_and_regression.ipynb`
4. Follow the step-by-step analysis for both tasks

### Model Deployment
The trained models can be used to:
- Predict employee satisfaction scores for new hires
- Identify turnover risk for current employees
- Generate HR dashboards with risk indicators
- Support strategic HR decision-making

## 📝 Conclusion

This project demonstrates the application of machine learning for HR analytics, providing:
1. Accurate Predictions: Reliable models for both satisfaction (14.3% SMAPE) and turnover (0.915 ROC-AUC)
2. Actionable Insights: Clear identification of key factors influencing employee experience
3. Strategic Value: Data-driven foundation for HR policy and retention strategies
