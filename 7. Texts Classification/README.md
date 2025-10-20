# Toxic Comments Classification - NLP Project

A natural language processing project implementing machine learning models to help "Викишоп" identify toxic comments for content moderation in their product description editing system.

## 📋 Project Overview

This project develops text classification models to assist an online marketplace with two key business objectives:
1. **Content Moderation** - Automatically detect toxic comments for human review
2. **Community Management** - Maintain positive user experience in collaborative editing environment

The solution implements both BERT-based deep learning and traditional TF-IDF approaches to solve this binary classification problem.

## 🎯 Business Problem

"Викишоп" marketplace needs to implement automated content moderation to:
- Identify toxic comments in user-generated content
- Reduce manual moderation workload
- Maintain community guidelines and positive environment
- Scale moderation as user base grows

## 📊 Data Sources

### Dataset Description
- **Source**: Toxic comments dataset with manual labeling
- **Total Comments**: 159,292 initially (86,288 after English filtering)
- **Features**: 
  - `text`: Comment content
  - `toxic`: Binary label (0=non-toxic, 1=toxic)

### Data Characteristics
- **Class Distribution**: 
  - Non-toxic: 85.6% (73,904 comments)
  - Toxic: 14.4% (12,384 comments)
- **Language**: English comments only
- **Text Length**: Up to 5,000 characters per comment

## 🛠️ Technical Implementation

### Approach 1: BERT-Based Classification

#### Model Architecture
- **Base Model**: `unitary/toxic-bert` (pre-trained on toxic content)
- **Tokenization**: BERT tokenizer with 512 token limit
- **Feature Extraction**: BERT embeddings for contextual understanding

#### Training Configuration
- **Sample Size**: 5,000 comments for computational efficiency
- **Train-Test Split**: 50-50 with stratification
- **Batch Size**: 50 for embedding generation

### Approach 2: TF-IDF with Traditional ML

#### Text Preprocessing Pipeline
- **Text Cleaning**: Remove special characters, lowercase conversion
- **Lemmatization**: Mystem for Russian text normalization
- **Stopword Removal**: NLTK English stopwords
- **Vectorization**: TF-IDF with custom parameters

#### Models Tested
- Logistic Regression
- Random Forest
- Decision Trees
- LightGBM
- CatBoost

### Hyperparameter Optimization
- **Method**: RandomizedSearchCV with 5-fold cross-validation
- **Scoring Metric**: F1-score (primary business requirement)
- **Class Handling**: Class weighting for imbalance (1:7 ratio)

## 📈 Key Findings

### Model Performance Comparison

#### BERT-Based Approach
- **Best Model**: Logistic Regression
- **Training F1**: 0.948
- **Test F1**: 0.945
- **Key Parameters**:
  - Solver: saga
  - Regularization: L2 with C=5
  - Class weight: balanced

#### TF-IDF Approach
- **Best Model**: Logistic Regression  
- **Training F1**: 0.634
- **Test F1**: 0.693
- **Key Parameters**:
  - Solver: sag
  - Regularization: None
  - C: 0.8

### Performance Analysis
- **Target Achievement**: Both approaches exceed F1 > 0.75 requirement
- **BERT Advantage**: 36% higher F1 score compared to TF-IDF
- **Context Understanding**: BERT's contextual embeddings significantly outperform bag-of-words approaches

## 🚀 How to Use

### Prerequisites
```bash
pip install transformers torch scikit-learn nltk pymystem3 catboost lightgbm
```
### Model Training

BERT Approach

```python
# Load pre-trained toxic-BERT
tokenizer = transformers.BertTokenizer.from_pretrained('unitary/toxic-bert')
model = transformers.BertModel.from_pretrained('unitary/toxic-bert')

# Generate embeddings and train classifier
best_model = LogisticRegression(class_weight='balanced', 
                               C=5, 
                               penalty='l2', 
                               solver='saga')
```

TF-IDF Approach

```python
# Text preprocessing and vectorization
tfidf = TfidfVectorizer(stop_words=stopwords)
X_tfidf = tfidf.fit_transform(texts)

# Train classifier
best_model = LogisticRegression(class_weight='balanced',
                               C=0.8,
                               penalty=None,
                               solver='sag')
```

### Model Deployment

The trained models can be used to:

1. Screen new user comments in real-time
2. Integrate with moderation dashboard
3. Generate toxicity probability scores
4. Batch process existing comment archives

### 📝 Conclusion

This project successfully developed multiple approaches for toxic comment classification, with the BERT-based model significantly outperforming traditional methods.