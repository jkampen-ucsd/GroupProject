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

The visualizations were created using Spark DataFrame operations for aggregation and sampling. Aggregated or sampled results were then converted to Pandas only for plotting with Matplotlib.

### Review Sentiment Distribution
This bar chart shows the distribution of the target variable `voted_up`. It helps identify whether the dataset is balanced between positive and negative reviews.

### Top Review Languages
This bar chart shows the most common review languages in the dataset. It helps determine whether the dataset is dominated by a small number of languages.

### Top Games by Review Count
This chart shows which games have the largest number of reviews. This is useful for identifying whether certain games dominate the dataset.

### Total Playtime Distribution
The histogram of `author_playtime_forever` shows how total playtime is distributed among reviewers. This variable is expected to be right-skewed, with most users having lower playtime and a smaller number having very high playtime.

### Review Length Distribution
The review length histogram shows the distribution of text length in the `review` column. This is useful for understanding the structure of the text data before applying NLP methods.

### Average Playtime by Review Sentiment
This bar chart compares average playtime between positive and negative reviews. It helps evaluate whether users who recommend a game tend to have more playtime.

### Playtime vs Weighted Vote Score
This scatter plot shows the relationship between total playtime and weighted vote score. It helps identify whether reviews from users with more playtime tend to receive higher helpfulness scores.




## 5. Preprocessing

- How will you handle missing values?

**`Since the data set is so large removing the rows with null values will be my first approach`**

- How will you handle data imbalance (if applicable)?

**`N/A`**

- What transformations will you apply (scaling, encoding, feature engineering)?

**`Scaling and feature engineering will be useful with this data set`**

- What Spark operations will you use for preprocessing?



## Data Preprocessing Strategy

### Handling Missing Values
Missing values will be handled based on the type and importance of each feature:

- **Numerical columns** (e.g., playtime, votes):
  - Impute with median or mean using Spark’s `Imputer` to reduce the impact of outliers.
- **Categorical columns** (e.g., language, location):
  - Replace missing values with `"Unknown"` or the most frequent category.
- **Text data (`review`)**:
  - Drop rows where the review text is missing, as it is critical for analysis.
- **Datetime columns**:
  - Convert to timestamps and either impute or derive features (e.g., time since last played).
- Columns with excessive missing values may be dropped if they do not add meaningful signal.

---

### Handling Data Imbalance
The target variable `voted_up` may be imbalanced (more positive than negative reviews). To address this:

- Analyze class distribution using `groupBy().count()`.
- Apply:
  - **Downsampling** of the majority class, or
  - **Upsampling** of the minority class using Spark sampling techniques.
- Alternatively, use **class weights** in modeling (if supported).
- Evaluate models using metrics robust to imbalance (e.g., F1-score, precision/recall) instead of accuracy.

---

### Transformations

#### Feature Engineering
- Create new features such as:
  - `review_length` from the `review` text
  - Time-based features (e.g., days since review, recency)
- Log-transform highly skewed variables (e.g., playtime, votes) to normalize distributions.

#### Scaling
- Apply scaling (e.g., `StandardScaler`) to numerical features when required for modeling.
- Tree-based models may not require scaling.

#### Encoding
- Convert categorical variables using:
  - `StringIndexer` for label encoding
  - `OneHotEncoder` for nominal categories
- Binary variables can remain as 0/1.

#### Text Processing
- Tokenize and clean the `review` column using:
  - `Tokenizer` or `RegexTokenizer`
  - Remove stopwords
  - Convert to numerical features using `TF-IDF` or embeddings

---

### Spark Operations for Preprocessing

The following Spark DataFrame and MLlib operations will be used:

- **Data Cleaning**
  - `df.dropna()`, `df.fillna()`
  - `withColumn()` for feature creation
  - `filter()` for removing invalid records

- **Aggregation & Analysis**
  - `groupBy().agg()` for summaries
  - `select().distinct()` for unique values

- **Feature Engineering**
  - `withColumn()` for derived features
  - `when()` for conditional logic

- **MLlib Transformers**
  - `Imputer` for missing values
  - `StringIndexer` and `OneHotEncoder` for categorical encoding
  - `VectorAssembler` to combine features
  - `StandardScaler` for normalization
  - `Tokenizer`, `StopWordsRemover`, `HashingTF`, `IDF` for text processing

- **Sampling**
  - `sample()` for downsampling
  - `sampleBy()` for stratified sampling
