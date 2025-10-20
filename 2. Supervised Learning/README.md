# Customer Classification and Market Activity Prediction

A machine learning project for predicting customer activity decline and developing personalized marketing strategies for the "В один клик" online store.

## 📋 Project Overview

This project addresses the challenge of declining customer activity in an e-commerce store by:
1. **Predicting customer activity decline** - Identifying customers likely to reduce their purchasing activity
2. **Customer segmentation** - Grouping customers based on activity patterns and profitability
3. **Personalized strategy development** - Creating targeted marketing interventions

## 🎯 Business Problem

The "В один клик" online store (selling children's goods, home textiles, cosmetics, small appliances, and products) faces declining customer activity. Instead of focusing on new customer acquisition, the solution aims to retain existing customers through personalized offers.

### Key Objectives:
- Classify customers into "activity declined" vs. "same level" categories
- Predict probability of activity decline in the next 3 months
- Segment customers based on activity patterns and profitability
- Develop personalized marketing strategies for each segment

## 📊 Data Sources

### `market_file.csv`
- **Records**: 1,300 customers
- **Features**:
  - Customer characteristics: Service type, Communication preferences
  - Marketing activity: 6-month average and current month communications
  - Product behavior: Popular categories, Promotional purchases
  - Website behavior: Pages per visit, Categories viewed, Service errors
  - Purchase behavior: Unpaid items in cart, Customer duration

### `market_money.csv`
- **Records**: 3,900 entries (3 months × 1,300 customers)
- **Features**: Monthly revenue per customer for current, previous, and pre-previous months

### `market_time.csv`
- **Records**: 2,600 entries (2 months × 1,300 customers)
- **Features**: Time spent on website (minutes) for current and previous months

### `money.csv`
- **Records**: 1,300 customers
- **Features**: Average monthly profit per customer over last 3 months

## 🛠️ Technical Implementation

### Data Preprocessing
- **Data Cleaning**: Handled typos in categorical variables, removed outliers
- **Feature Engineering**: Created pivot tables for time-series revenue and website time data
- **Data Integration**: Merged multiple data sources using customer IDs
- **Quality Control**: Removed customers with less than 3 months activity and anomalous revenue values

### Models Developed

#### Machine Learning Pipeline
- **Preprocessing**: OneHotEncoding for categorical features, MinMaxScaler for numerical features
- **Model Selection**: RandomizedSearchCV with 5-fold cross-validation
- **Algorithms Tested**:
  - K-Nearest Neighbors (KNN)
  - Decision Trees
  - Support Vector Classifier (SVC)
  - Logistic Regression

#### Best Performing Model
- **Algorithm**: Support Vector Classifier (SVC)
- **Parameters**: C=1, kernel='linear'
- **Preprocessing**: MinMaxScaler
- **Performance**: ROC-AUC = 0.919 on test set

### Key Techniques
- **Pipeline Architecture**: Integrated preprocessing and modeling
- **Hyperparameter Tuning**: Randomized search with cross-validation
- **Model Evaluation**: ROC-AUC metric for probability-based classification
- **Feature Importance**: SHAP analysis and permutation importance

## 📈 Key Findings

### Feature Importance Analysis
**Most Influential Features:**
1. **Pages per visit** - Strongest predictor of customer activity
2. **Time spent on website** (current and previous months)
3. **Promotional purchases** - Indicator of price sensitivity
4. **Categories viewed per visit** - Engagement metric
5. **Unpaid items in cart** - Purchase intent indicator

**Less Influential Features:**
- Service type (premium/standard)
- Service errors
- Communication preferences

### Customer Segmentation

#### High-Risk High-Value Segment
- **Criteria**: Probability of decline ≥ 0.7 AND Profitability ≥ 3.0
- **Characteristics**:
  - Lower marketing communication exposure
  - Fewer pages visited per session
  - More abandoned carts
  - Less time spent on website
  - Higher preference for promotional purchases

## 🎯 Business Recommendations

### Targeted Interventions for High-Risk Segments

#### 1. Enhanced Communication Strategy
- Increase frequency of personalized communications
- Implement targeted email campaigns for promotional buyers
- Develop proactive customer service outreach

#### 2. Website Experience Optimization
- Improve product discovery and recommendation systems
- Enhance promotional section visibility
- Implement cart abandonment recovery campaigns

#### 3. Promotional Strategy
- Expand promotional product assortment
- Introduce "Deal of the Day" and "Maximum Savings" categories
- Implement price drop notifications for items in cart

#### 4. Personalization Initiatives
- Develop customized product recommendations
- Create personalized promotional offers
- Implement loyalty program enhancements

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn phik shap
```

### Running the Analysis
1. Clone the repository
2. Ensure datasets are in the `Supervised_learning_customers_datasets/` directory
3. Run the Jupyter notebook: `classification_of_customers_and_market_activity_prediction_supervised_learning.ipynb`
4. Follow the step-by-step analysis

### Model Deployment
The trained models can be used to:
- Predict customer activity decline probability
- Identify high-risk customer segments
- Generate personalized marketing recommendations
- Monitor customer activity trends

## 📝 Conclusion
This project demonstrates how supervised learning can be applied to customer behavior prediction in e-commerce. The solution provides:
1. Accurate predictions of customer activity decline
2. Targeted segmentation for personalized marketing
3. Data-driven strategies for customer retention
The approach balances technical sophistication with business practicality, making it valuable for e-commerce companies facing similar customer retention challenges.
