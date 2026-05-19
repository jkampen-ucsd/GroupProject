# Group Project

Group project for DSC 232.


# Project Overview

The goal of this project is to predict whether a Steam game review is positive or negative (`voted_up`) using distributed machine learning with Apache Spark on SDSC Expanse.

This project uses:
- PySpark DataFrames
- Spark MLlib
- Distributed Random Forest Classification
- Feature Engineering
- Scalable preprocessing pipelines

---

# Dataset

## Dataset Source

[100 Million+ Steam Reviews](https://www.kaggle.com/datasets/kieranpoc/steam-reviews)

---








## 1. GitHub Repository Setup

**Dataset:** [100 Million+ Steam Reviews](https://www.kaggle.com/datasets/kieranpoc/steam-reviews)

---

## 2. SDSC Expanse Environment Setup

<img width="2242" height="983" alt="SDSC Expanse Environment Screenshot" src="https://github.com/user-attachments/assets/80254bb5-31e4-46f4-802c-8a0657ee7c14" />

---

spark = SparkSession.builder \
    .appName("SteamReviewAnalysis") \
    .config("spark.executor.instances", "7") \
    .config("spark.executor.cores", "1") \
    .config("spark.executor.memory", "6g") \
    .config("spark.driver.memory", "4g") \
    .getOrCreate()
