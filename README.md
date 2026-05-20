# Group Project - Milestone 3

Steam Review Recommendation Prediction Using Distributed Spark ML

# Project Overview

The goal of this project is to predict whether a Steam review is positive or negative (`voted_up`) using distributed machine learning with Apache Spark on SDSC Expanse.

The project uses:
- PySpark DataFrames
- Spark MLlib
- Distributed Random Forest Classification
- Feature Engineering
- Spark ML Pipelines
- SDSC Expanse distributed computing environment

# Dataset

Dataset Source:

[100 Million+ Steam Reviews](https://www.kaggle.com/datasets/kieranpoc/steam-reviews)

# Dataset Description

The dataset contains Steam game review information including:
- Review text
- Gameplay statistics
- Voting behavior
- Purchase metadata
- Recommendation labels

# SDSC Expanse Environment Setup
<img width="935" height="645" alt="image" src="https://github.com/user-attachments/assets/30248ed6-c594-4e4e-92c9-97af17078ad8" />

# Preprocessing Pipeline

The preprocessing pipeline was implemented using Spark MLlib transformers and Spark DataFrame operations.

Scaling
- StandardScaler

Missing Value Handling
- Spark ML Imputer
- Median imputation

Encoding
- StringIndexer
- OneHotEncoder
- VectorAssembler

# Feature Engineering
The following custom features were created:

| Feature        | Description                           |
| -------------- | ------------------------------------- |
| review_length  | Length of review text                 |
| playtime_hours | Total playtime converted to hours     |
| helpful_ratio  | Ratio of helpful votes to funny votes |

# Machine Learning Model

Selected Model:
- Random Forest Classifier

# Spark ML Pipeline

Pipeline Stages:
- Imputer
- StringIndexer
- OneHotEncoder
- VectorAssembler
- StandardScaler
- RandomForestClassifier

# Model Evaluation

Evaluation Metrics
The following evaluation metrics were used:
- Accuracy
- Area Under ROC Curve (AUC)

# Model Results

Model 1 Results:
| Metric   | Training | Testing |
| -------- | ------- | ------- |
| Accuracy | 0.856   | 0.856 |
| AUC      | 0.765   | 0.762 |

# Hyperparameter Tuning

Model 2 Configuration:
Model 2 Results:
| Metric   | Training | Testing |
| -------- | -------- | ------- |
| Accuracy | 0.875   | 0.858 |
| AUC      | 0.812   | 0.768 |

## Underfitting vs Overfitting Analysis

The Random Forest model appears to be reasonably well fit and demonstrates strong generalization performance.

The training and testing metrics are extremely close:

- Train AUC: 0.7658
- Test AUC: 0.7624
- Train Accuracy: 0.8561
- Test Accuracy: 0.8562

Because the training and testing scores are nearly identical, the model does not show significant signs of overfitting. Overfitting would typically appear as very high training performance with noticeably lower testing performance.

The model also does not appear to be severely underfitting because:
- Accuracy is relatively strong at approximately 85.6%
- AUC values above 0.75 indicate the model has meaningful predictive power and can reasonably distinguish between positive and negative reviews

Overall, the model demonstrates stable and balanced performance across both the training and testing datasets, indicating good generalization to unseen data.

## Interpretation of Results

The Random Forest model was able to successfully learn patterns related to:
- Gameplay behavior
- Review engagement
- Voting activity
- Purchase information
- Engineered features such as review length and helpfulness ratio

The close alignment between training and testing performance suggests that the selected hyperparameters (`numTrees=50`, `maxDepth=10`) helped control model complexity while still capturing meaningful relationships in the data.

## Potential Improvements

Although the model performs reasonably well, performance could potentially be improved through:
- Additional hyperparameter tuning
- Larger dataset samples
- Advanced NLP preprocessing on review text
- TF-IDF or Word2Vec embeddings
- Gradient Boosted Trees or distributed XGBoost
- Better handling of class imbalance

Future milestones will explore more advanced distributed models to potentially improve predictive performance further.
