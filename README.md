# Group Project

Group project for DSC 232

## 1. GitHub Repository Setup

**Dataset:** [100 Million+ Steam Reviews](https://www.kaggle.com/datasets/kieranpoc/steam-reviews)

---

## 2. SDSC Expanse Environment Setup

<img width="2242" height="983" alt="SDSC Expanse Environment Screenshot" src="https://github.com/user-attachments/assets/80254bb5-31e4-46f4-802c-8a0657ee7c14" />

---

## 3. Data Exploration Using Spark

### 3a. How many observations does your dataset have?

**Answer:** The dataset has **113,885,601 observations**.

---

### 3b. Describe all columns in your dataset, including their scales and data distributions. Describe categorical and continuous variables. Describe your target column.

**Columns:**

```python
[
    'recommendationid',
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
    'steam_china_location'
]
```

#### Target Variable

| Column | Type | Description |
|---|---|---|
| `voted_up` | Categorical / Binary | Indicates whether a review is positive (`True`) or negative (`False`). |

#### Identifier Variables

These variables uniquely identify records or entities and should not be treated as meaningful numeric modeling features.

| Column | Type | Description |
|---|---|---|
| `recommendationid` | Categorical / Nominal | Unique review ID. |
| `appid` | Categorical / Nominal | Game ID. |
| `author_steamid` | Categorical / Nominal | User ID. |

#### Categorical Variables

| Column | Type | Description |
|---|---|---|
| `game` | Categorical / Nominal | Game title. |
| `language` | Categorical / Nominal | Review language. |
| `steam_china_location` | Categorical / Nominal | User location category. |
| `steam_purchase` | Categorical / Binary | Indicates whether the game was purchased on Steam. |
| `received_for_free` | Categorical / Binary | Indicates whether the game was received for free. |
| `written_during_early_access` | Categorical / Binary | Indicates whether the review was written during early access. |
| `hidden_in_steam_china` | Categorical / Binary | Indicates whether the review is hidden in Steam China. |

#### Numerical Variables

| Column | Type | Description |
|---|---|---|
| `author_playtime_forever` | Continuous | Total playtime. |
| `author_playtime_last_two_weeks` | Continuous | Recent playtime. |
| `author_playtime_at_review` | Continuous | Playtime at the time of review. |
| `weighted_vote_score` | Continuous | Weighted helpfulness score. |
| `author_num_games_owned` | Discrete / Count | Number of games owned. |
| `author_num_reviews` | Discrete / Count | Number of reviews written. |
| `votes_up` | Discrete / Count | Number of helpful votes. |
| `votes_funny` | Discrete / Count | Number of funny votes. |
| `comment_count` | Discrete / Count | Number of comments. |

#### Datetime Variables

| Column | Type | Description |
|---|---|---|
| `author_last_played` | Datetime | Last time the user played. |
| `timestamp_created` | Datetime | Review creation time. |
| `timestamp_updated` | Datetime | Review last updated time. |

#### Text Variable

| Column | Type | Description |
|---|---|---|
| `review` | Unstructured text | Full review text, suitable for NLP tasks. |

---

### 3c. Do you have missing and duplicate values in your dataset?

**Answer:** Yes. There are missing values in many columns. Duplicate values should also be checked using Spark before preprocessing.

---

### 3d. For image data, describe the number of classes, image sizes, uniformity, and cropping/normalization needs.

**Answer:** Not applicable. This dataset contains tabular and text review data, not image data.

---

## 4. Data Plots

Spark aggregations can be used to summarize the full dataset, and smaller samples can be converted to Pandas for plotting with Matplotlib or Plotly.

### Recommended Visualizations

#### Bar Chart: Review Counts by Language

**Purpose:** Shows which languages are most common in the dataset.

**Insight:** This helps identify dominant languages and whether language imbalance may affect modeling.

#### Bar Chart: Positive vs. Negative Reviews

**Purpose:** Shows the class distribution of the target variable, `voted_up`.

**Insight:** This helps determine whether the dataset has class imbalance.

#### Histogram: Author Playtime at Review

**Purpose:** Shows the distribution of playtime when the review was written.

**Insight:** This helps identify skewness and whether a log transformation may be useful.

#### Scatter Plot: Playtime vs. Weighted Vote Score

**Purpose:** Shows the relationship between user playtime and review helpfulness.

**Insight:** This helps determine whether users with more playtime tend to receive higher weighted vote scores.

---

## 5. Preprocessing

### How will you handle missing values?

Missing values will be handled based on the type and importance of each feature.

- **Numerical columns** such as playtime and vote counts will be imputed using the median or mean with Spark’s `Imputer`.
- **Categorical columns** such as `language` and `steam_china_location` will be filled with `"Unknown"` or the most frequent category.
- **Text data** in the `review` column will be dropped if missing because the review text is critical for analysis.
- **Datetime columns** will be converted to timestamp format and used to create time-based features.
- Columns with excessive missing values may be dropped if they do not add meaningful signal.

---

### How will you handle data imbalance, if applicable?

The target variable `voted_up` may be imbalanced if there are more positive reviews than negative reviews.

To handle imbalance:

- Analyze class distribution using `groupBy().count()`.
- Use downsampling for the majority class if needed.
- Use upsampling for the minority class if needed.
- Consider class weights if supported by the selected model.
- Evaluate model performance using F1-score, precision, recall, and AUC instead of accuracy alone.

---

### What transformations will you apply?

#### Feature Engineering

- Create `review_length` from the `review` text.
- Create time-based features from timestamp columns.
- Create recency features such as days since review or days since last played.
- Apply log transformations to highly skewed columns such as playtime and vote counts.

#### Scaling

- Apply `StandardScaler` to numerical features when using models that benefit from scaling.
- Tree-based models may not require scaling.

#### Encoding

- Use `StringIndexer` to convert categorical variables into numeric labels.
- Use `OneHotEncoder` for nominal categorical variables.
- Convert binary variables into 0/1 values if needed.

#### Text Processing

- Tokenize the `review` column using `Tokenizer` or `RegexTokenizer`.
- Remove stopwords using `StopWordsRemover`.
- Convert text into numerical features using `HashingTF`, `IDF`, or other TF-IDF methods.

---

### What Spark operations will you use for preprocessing?

#### Data Cleaning

- `df.dropna()` to remove rows with missing values when appropriate.
- `df.fillna()` to fill missing categorical values.
- `filter()` to remove invalid records.
- `dropDuplicates()` to remove duplicate rows.

#### Aggregation and Analysis

- `groupBy().count()` to check class balance and category counts.
- `groupBy().agg()` to calculate summary statistics.
- `select().distinct()` to identify unique values.

#### Feature Engineering

- `withColumn()` to create new features.
- `when()` for conditional feature logic.
- Spark SQL functions to transform timestamp and text columns.

#### MLlib Transformers

- `Imputer` for numerical missing values.
- `StringIndexer` for categorical encoding.
- `OneHotEncoder` for nominal variables.
- `VectorAssembler` to combine features into a single feature vector.
- `StandardScaler` for normalization.
- `Tokenizer`, `StopWordsRemover`, `HashingTF`, and `IDF` for text processing.

#### Sampling

- `sample()` for general sampling.
- `sampleBy()` for stratified sampling by the target variable.
