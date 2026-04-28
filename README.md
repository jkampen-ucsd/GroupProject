# GroupProject
Group project for DSC 232

## 1. GitHub Repository Setup

Link to dataset:
https://www.kaggle.com/datasets/kieranpoc/steam-reviews
**`100 Million+ Steam Reviews`**

## 2. SDSC Expanse Environment Setup

<img width="2242" height="983" alt="Screenshot 2026-04-27 165421" src="https://github.com/user-attachments/assets/80254bb5-31e4-46f4-802c-8a0657ee7c14" />


## 3. Data Exploration using Spark

a. How many observations does your dataset have?

**`There are 113,885,601 observations`**

b. Describe all columns in your dataset: their scales and data distributions. Describe categorical and continuous variables. Describe your target column.

The columns are:

`['recommendationid',
 'appid',
 'game',
 'author_steamid',
 'author_num_games_owned',
 'author_num_reviews',
 'author_playtime_forever',
 'author_playtime_last_two_weeks',
 'author_playtime_at_review',
 'author_last_played',
 'language',
 'review',
 'timestamp_created',
 'timestamp_updated',
 'voted_up',
 'votes_up',
 'votes_funny',
 'weighted_vote_score',
 'comment_count',
 'steam_purchase',
 'received_for_free',
 'written_during_early_access',
 'hidden_in_steam_china',
 'steam_china_location']`

## Data Type Classification

### Target Variable
- **`voted_up`**  
  - Type: Categorical (Binary)  
  - Description: Indicates whether a review is positive (`True`) or negative (`False`)

---

### Identifier Variables (Categorical - Nominal)
These variables uniquely identify records or entities and are not meaningful for modeling as numeric features.

- `recommendationid` – Unique review ID  
- `appid` – Game ID  
- `author_steamid` – User ID  

---

### Categorical Variables

#### Nominal (No inherent order)
- `game` – Game title  
- `language` – Review language  
- `steam_china_location` – User location category  

#### Binary (Boolean)
- `steam_purchase` – Purchased on Steam (True/False)  
- `received_for_free` – Received game for free (True/False)  
- `written_during_early_access` – Written during early access (True/False)  
- `hidden_in_steam_china` – Hidden in China (True/False)  

---

### Numerical Variables

#### Continuous Variables
- `author_playtime_forever` – Total playtime  
- `author_playtime_last_two_weeks` – Recent playtime  
- `author_playtime_at_review` – Playtime at time of review  
- `weighted_vote_score` – Weighted helpfulness score  

#### Discrete (Count-Based) Variables
- `author_num_games_owned` – Number of games owned  
- `author_num_reviews` – Number of reviews written  
- `votes_up` – Number of helpful votes  
- `votes_funny` – Number of funny votes  
- `comment_count` – Number of comments  

---

### Datetime Variables
- `author_last_played` – Last time the user played  
- `timestamp_created` – Review creation time  
- `timestamp_updated` – Review last updated time  

---

### Text Data
- **`review`**  
  - Type: Unstructured text  
  - Description: Contains the full review text and is suitable for NLP tasks  

---

c. Do you have missing and duplicate values in your dataset?

**`Yes, there are missing values in just about every column`**

d. For image data: describe number of classes, image sizes, uniformity, cropping/normalization needs.

**`N/A`**


## 4. Data Plots

a. Create visualizations using Spark aggregations + matplotlib/plotly (sample data for plotting if needed)

b. Plot your data with various chart types: bar charts, histograms, scatter plots, etc.

c. Clearly explain each plot and what insights it provides

d. For image data: plot example classes


## 5. Preprocessing

- How will you handle missing values?

- How will you handle data imbalance (if applicable)?

- What transformations will you apply (scaling, encoding, feature engineering)?

- What Spark operations will you use for preprocessing?
