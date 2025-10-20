# Age Detection - Computer Vision Project

A computer vision project implementing deep learning models to help "Хлеб-Соль" supermarket determine customer age from photos for personalized marketing and compliance monitoring.

## 📋 Project Overview

This project develops computer vision models to assist a supermarket chain with two key business objectives:
1. **Customer Analytics** - Analyze purchases and recommend age-appropriate products
2. **Compliance Control** - Monitor alcohol sales compliance at checkout

The solution implements convolutional neural networks with transfer learning to solve this regression problem.

## 🎯 Business Problem

"Хлеб-Соль" supermarket needs to implement photo analysis at checkout to:
- Predict customer age from facial images
- Enable age-based product recommendations
- Ensure compliance with alcohol sales regulations
- Analyze purchasing patterns by age groups

## 📊 Data Sources

### Dataset Description
- **Source**: ChaLearn Looking at People dataset
- **Total Images**: 7,591 facial images
- **Image Format**: 114×114 pixels, RGB channels
- **Age Range**: 1 to 100 years
- **Features**: Various lighting conditions, angles, and image quality

### Data Distribution
- **Mean Age**: 31.2 years
- **Median Age**: 29 years
- **Standard Deviation**: 17.1 years
- **Key Age Groups**: 20-41 years (interquartile range)

## 🛠️ Technical Implementation

### Model Architecture

#### Base Model: ResNet50
- **Pre-trained Weights**: ImageNet
- **Input Shape**: (114, 114, 3)
- **Transfer Learning**: Frozen base layers initially, then fine-tuned

#### Custom Layers Added
- **Convolutional Blocks**: 3 layers (256, 128, 64 filters)
- **Pooling**: MaxPooling2D after each conv layer
- **Global Average Pooling**: For feature extraction
- **Batch Normalization**: For training stability
- **Dense Layers**: 256 and 128 units with ReLU activation
- **Dropout**: 0.5 rate for regularization
- **Output Layer**: Single unit with linear activation for regression

### Training Configuration

#### Data Augmentation
- Horizontal flipping
- Rotation (±40 degrees)
- Rescaling (1./255)

#### Optimization
- **Optimizer**: Adam (learning_rate=0.0001)
- **Loss Function**: Mean Squared Error (MSE)
- **Primary Metric**: Mean Absolute Error (MAE)
- **Batch Size**: 32
- **Epochs**: 20

#### Callbacks
- **Early Stopping**: Patience of 5 epochs
- **Model Checkpoint**: Save best weights
- **ReduceLROnPlateau**: Factor 0.2, patience 3 epochs

## 📈 Key Findings

### Data Insights
- **Age Distribution**: Right-skewed with concentration in 20-41 age range
- **Data Imbalance**: Underrepresented groups at age extremes (children, elderly)
- **Image Quality**: Varied conditions (lighting, angles, quality)

### Model Performance

#### Training Progress
- **Initial MAE**: 22.5 (Epoch 1)
- **Final Training MAE**: 6.34
- **Final Validation MAE**: 7.49
- **Validation Loss**: 103.55 (MSE)

#### Key Milestones
- **Epoch 5**: MAE dropped to 9.7
- **Epoch 11**: MAE reached 7.76
- **Best Validation**: ~7.29 MAE (around epoch 15-16)

### Performance Analysis
- **Target Achievement**: MAE of 7.49 meets business requirement (< 8.0)
- **Overfitting Signs**: Slight increase in validation MAE after epoch 16
- **Training Stability**: Consistent improvement with minor fluctuations

## 🚀 How to Use

### Prerequisites
```bash
pip install tensorflow pandas matplotlib pillow scikit-learn
```
### Model Training

1. Ensure dataset is in http://chalearnlap.cvc.uab.es/dataset/26/description/ directory
2. Run the training script with predefined functions:

- `load_train()` - Load training data with augmentation
- `load_test()` - Load test data
- `create_model()` - Initialize ResNet50-based architecture
- `train_model()` - Train with callbacks and validation

### Model Deployment

The trained model can be used to:
1. Predict age from new customer photos
2. Integrate with checkout systems for real-time analysis
3. Generate age-based product recommendations
4. Monitor compliance with age-restricted sales

### 📝 Conclusion

This project successfully developed a computer vision system for age detection that meets business requirements. The ResNet50-based model achieved a validation MAE of 7.49 years, exceeding the target of 8.0 years.
