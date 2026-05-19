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

# Dataset

[100 Million+ Steam Reviews](https://www.kaggle.com/datasets/kieranpoc/steam-reviews)

---


## 2. SDSC Expanse Environment Setup

<img width="2242" height="983" alt="SDSC Expanse Environment Screenshot" src="https://github.com/user-attachments/assets/80254bb5-31e4-46f4-802c-8a0657ee7c14" />

---

| Column                         | Description               |
| ------------------------------ | ------------------------- |
| recommendationid               | Unique review ID          |
| appid                          | Steam game ID             |
| game                           | Game title                |
| author_steamid                 | Steam user ID             |
| author_num_games_owned         | Number of games owned     |
| author_num_reviews             | Number of reviews written |
| author_playtime_forever        | Total gameplay time       |
| author_playtime_last_two_weeks | Recent gameplay time      |
| author_playtime_at_review      | Gameplay time at review   |
| author_last_played             | Last played timestamp     |
| language                       | Review language           |
| review                         | User review text          |
| timestamp_created              | Review creation timestamp |
| timestamp_updated              | Review update timestamp   |
| voted_up                       | Target label              |
| votes_up                       | Helpful votes             |
| votes_funny                    | Funny votes               |
| weighted_vote_score            | Weighted score            |
| comment_count                  | Comment count             |
| steam_purchase                 | Purchased on Steam        |
| received_for_free              | Received for free         |
| written_during_early_access    | Early access review       |
| hidden_in_steam_china          | Hidden in China           |
| steam_china_location           | China region              |


Data Preprocessing
Preprocessing Techniques Used
Scaling
StandardScaler
Imputation
Spark ML Imputer using median strategy
Encoding
StringIndexer
OneHotEncoder
VectorAssembler
Feature Engineering

Custom engineered features:

review_length
playtime_hours
helpful_ratio
Missing Value Handling
Null replacement
NaN cleanup
Categorical fallback values
