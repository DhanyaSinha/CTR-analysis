# Click-Through Rate (CTR) Prediction Model Documentation

## Table of Contents
1. [Exploratory Data Analysis (EDA)](#1-exploratory-data-analysis-eda)
2. [Feature Engineering](#2-feature-engineering)
3. [Model Building](#3-model-building)
4. [Evaluation Metrics](#4-evaluation-metrics)
5. [Ranking Products](#5-ranking-products)

---

## 1. Exploratory Data Analysis (EDA)

### Insights from EDA

#### a. Distribution of Target Variable
- The target variable `is_clicked` is imbalanced, with significantly more `0`s (non-clicks) than `1`s (clicks).
- This indicates that click-through events are less frequent, which is common in CTR prediction datasets.

#### b. Correlation Analysis
- Most features have low to moderate correlations with each other.
- Features like `CTR_last_30_days`, `CTR_last_7_days`, `CTR_product_30_days`, and `77m7nhn7jo8.ncncj7kum777nm7mm7if7lkkokii` show moderate positive correlations with `is_clicked`.
- `ad_revenue` and `savings` have weak correlations with other features, indicating they might not be strong predictors.

#### c. Distribution of Numerical Features
- Numerical features like `total_clicks`, `session_views`, and `query_products_clicks_last_30_days` are highly skewed, with a few entries having extremely high values (potential outliers).
- Click-through rates (`CTR_last_30_days`, `CTR_last_7_days`, etc.) are heavily skewed towards 0, indicating many queries/products/cities have low CTRs.

#### d. Profit Margin and CTR Analysis
- **Head Queries**:
  - Higher profit margin (~60) and higher CTR (~0.0089).
- **Tail Queries**:
  - Lower profit margin (~50) and lower CTR (~0.0085).
- **Business Strategy**: Focus on head queries for increased profitability and optimize tail queries to boost performance.

#### e. CTR and Clicks by Query Type
- **Head Queries**:
  - Exhibit higher average CTR and total clicks compared to tail queries.
- **Tail Queries**:
  - Show lower average CTR and total clicks, highlighting the need for optimization to improve performance.

#### f. City-wise Clicks vs. Impressions
- **Data Aggregation**: Grouped data by `city_id` to calculate total clicks and impressions.
- **Visualization**: A scatter plot revealed cities with high impressions but low clicks, indicating potential areas for improving engagement.

#### g. CTR vs. Ad Revenue
- Currently, `ad_revenue` barely affects the CTR.
- Implementing the right incentives may have a positive effect.

---

## 2. Feature Engineering

- **Encoding**:
  - Used TF-IDF vectorization for search terms.
  - Applied binary encoding for city IDs.
- **New Features**:
  - Created `click_view_ratio`, the ratio of total clicks to session views, providing insight into click behavior relative to views.

---

## 3. Model Building

### Model Training

#### a. XGBoost Model
- **Objective**: Minimize squared error.
- **Evaluation Metrics**:
  - **MSE**: 6.67e-05 – Slightly lower than Random Forest, indicating higher accuracy.
  - **R² Score**: 0.99 – High fit.
  - **Log Loss**: 3.46 – Marginally higher than Random Forest.
  - **AUROC Score**: 0.997 – Excellent classification performance.

#### b. Random Forest Classifier
- Replaced Factorization Machines (FM) with Random Forest Classifier for predicting `click_view_ratio`.
- **Evaluation Metrics**:
  - **MSE**: 8.02e-05 – Very low, indicating high accuracy.
  - **R² Score**: 0.99 – Explains 99% of variance.
  - **Log Loss**: 3.43 – Slightly better than XGBoost.
  - **AUROC Score**: 1.0 – Perfect classification performance.

#### Challenges and Insights
- Initially planned to use Factorization Machines (FM) based on research insights but faced integration challenges.
- Opted for Random Forest Classifier, achieving metrics and ranking performance aligned with research findings.

---

## 4. Evaluation Metrics

### Recommendation Task Metrics
1. **Mean Reciprocal Rank (MRR)**:
   - Average of the reciprocal ranks of the test items.
2. **Hit Rate at 10 (HR@10)**:
   - Assesses whether the top 10 recommendations include a positive item.
3. **Normalized Discounted Cumulative Gain (NDCG)**:
   - Assigns higher scores to test items ranked closer to the top, emphasizing the importance of higher ranks.

### CTR Prediction Metrics
1. **Area Under the ROC Curve (AUC)**:
   - Measures the probability of correctly ranking positive and negative instances.
2. **Log Loss (Binary Cross-Entropy)**:
   - Indicates the accuracy of the predicted probabilities.

---

## 5. Ranking Products

### Top 10 Products Analysis

#### a. XGBoost Model
- **Higher Precision**: Ranks show a broader range in click-view ratios, indicating precise differentiation between high and low-performing products.
- **Consistent Top Items**: High values for products like "goodlife" and "sting" suggest accurate ranking of top products.

#### b. Random Forest Model
- **Narrower Range**: Shows less variation in predicted ratios, with generally lower values for top items compared to XGBoost.
- **Consistent Ranking**: Identifies similar top products but with less sensitivity in ranking.

### Summary
- XGBoost provides more differentiated and higher precision rankings compared to Random Forest, reflecting better performance in identifying high-value items.

---

## References
- Research Paper: [https://arxiv.org/pdf/1911.09821]

