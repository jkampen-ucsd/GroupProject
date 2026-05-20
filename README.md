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

<img width="2242" height="983" alt="SDSC Expanse Environment Screenshot" src="https://github.com/user-attachments/assets/80254bb5-31e4-46f4-802c-8a0657ee7c14" />

Spark UI Screenshots
Data Loading

Distributed Training

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
| Metric   | Training | Validation | Testing |
| -------- | -------- | ---------- | ------- |
| Accuracy | INSERT   | INSERT     | INSERT  |
| AUC      | INSERT   | INSERT     | INSERT  |

# Hyperparameter Tuning

Model 2 Configuration:
| Model   | Num Trees | Max Depth | Train Accuracy | Validation Accuracy | Test Accuracy | Train AUC | Validation AUC | Test AUC |
| ------- | --------- | --------- | -------------- | ------------------- | ------------- | --------- | -------------- | -------- |
| Model 1 | 50        | 10        | INSERT         | INSERT              | INSERT        | INSERT    | INSERT         | INSERT   |
| Model 2 | 100       | 15        | INSERT         | INSERT              | INSERT        | INSERT    | INSERT         | INSERT   |

