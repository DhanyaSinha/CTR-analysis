# CTR-analysis
CTR analysis: EDA &amp; Ranking system of products in Quick Commerce Platform
Documentation for Click-Through Rate (CTR) Prediction ModelEDA & Data Pre Processing
1.Insights from EDA
      a.    Distribution of Target Variable:and n
The target variable is_clicked is imbalanced, with significantly more 0s (non-clicks) than 1s (clicks). This indicates that click-thrugh events are less frequent, which is common in CTR prediction datasets.
Correlation Analysis:
Most features have low to moderate correlations with each other.
Features like CTR_last_30_days, CTR_last_7_days, CTR_product_30_days, and 77m7nhn7jo8.ncncj7kum777nm7mm7if7lkkokiishow moderate positive correlations with is_clicked.
ad_revenue and savings have weak correlations with other features, indicating they might not be strong predictors.
Distribution of Numerical Features:
Numerical features like total_clicks, session_views, query_products_clicks_last_30_days, and others have highly skewed distributions, with a few entries having extremely high values (potential outliers).
Click-through rates (CTR_last_30_days, CTR_last_7_days, etc.) have distributions that are heavily skewed towards 0, indicating that many queries/products/cities have low CTRs.
d.Profit Margin and CTR Analysis
i.Head Queries: These queries exhibit a higher profit margin (~60) and higher CTR (~0.0089).
                      ii.Tail Queries: These queries show a lower profit margin (~50) and lower CTR (~0.0085).
iii.Business Strategy: Focus on head queries for increased profitability and optimize tail queries to boost performance.
	e. CTR and Clicks by Query Type
I. Head Queries: Exhibit higher average CTR and total clicks compared to tail queries.
II. Tail Queries: Show lower average CTR and total clicks, highlighting a need for optimization to improve performance
d. City-wise Clicks vs. Impressions
Data Aggregation: Grouped data by city_id to calculate total clicks and total impressions.
Visualization: Scatter plot revealed cities with high impressions but low clicks, indicating potential areas for improving engagement.
e.  CTR vs. Ad Revenue
		Barely effect the CTR right now. Right incentives may have a positive effect.



Feature Engineering
For feature engineering, I focused on encoding categorical variables and aggregating features. I used TF-IDF vectorization for search terms and binary encoding for city IDs. I also created a new feature, click_view_ratio, which represents the ratio of total clicks to session views, providing insight into click behavior relative to views.
Model Building
I split the data into training and test sets to evaluate model performance. I initially built two models:
XGBoost Model: This model was trained using the XGBoost regressor with an objective of minimizing squared error. It was evaluated using Mean Squared Error (MSE) and R-squared (R²) metrics.
MSE: 6.67e-05 –  Slightly lower than Random Forest, indicating slightly higher accuracy.
R^2 Score: 0.99 – Same high fit as Random Forest.
Log Loss: 3.46 – Marginally higher than Random Forest.
AUROC Score: 0.997 – Excellent but slightly less perfect classification

Random Forest Classifier: I replaced the Factorization Machines (FM) model with a Random Forest Classifier to predict the click_view_ratio. This model was chosen for its robustness and ability to handle complex interactions between features.
 `			1.MSE: 8.02e-05 – Very low, indicating high accuracy in predictions.
2.R^2 Score: 0.99 – Excellent fit, explaining 99% of variance.
3.Log Loss: 3.43 – Slightly better than XGBoost, indicating reliable probabilistic predictions.
4.AUROC Score: 1.0 – Perfect classification performance

*Challenges and Insights: During the project, I intended to use Factorization Machines (FM) based on insights from relevant research papers. However, I faced challenges integrating the FM model into the workflow and eventually opted for the Random Forest Classifier as an alternative. Despite this, the metrics and ranking techniques I employed align with those discussed in the research paper, ensuring that my approach was well-founded.

Evaluation Metrics
In my project, I evaluated the performance of my recommendation and click-through rate (CTR) prediction models using several key metrics. For the recommendation task, I focused on three ranking metrics:
Mean Reciprocal Rank (MRR): This metric calculates the average of the reciprocal ranks of the test items, providing a measure of how well the model ranks positive items relative to the entire ranking list.
Hit Rate at 10 (HR@10): This metric assesses whether any of the top 10 recommendations include a positive item, giving insight into how well the model performs in the top ranks.
Normalized Discounted Cumulative Gain (NDCG): NDCG accounts for the position of test items, assigning higher scores to items ranked closer to the top of the list, thereby emphasizing the importance of higher ranks.
For CTR prediction, I employed two metrics:
Area Under the ROC Curve (AUC): AUC measures the probability that a positive instance will be ranked higher than a randomly chosen negative instance, offering an assessment of the model’s ability to discriminate between positive and negative instances.
Log Loss (Binary Cross-Entropy): This metric measures the distance between the predicted probability and the actual binary outcome, indicating the accuracy of the probability predictions.
I took reference from a research paper to guide my selection of these metrics, ensuring a robust evaluation framework for my models.

5. Ranking Products
Based on the predictions from the Random Forest Classifier and XGBoost model, I ranked the products. The top 10 products were identified based on their predicted click-view ratio.
Analysis of Top 10 Ranks
XGBoost Model:
Higher Precision: Ranks show a broader range in click-view ratios, indicating precise differentiation between high and low-performing products.
Consistent Top Items: High values for "goodlife" and "sting" suggest accurate ranking of top products.
Random Forest Model:
Narrower Range: Shows less variation in predicted ratios, with generally lower values for top items compared to XGBoost.
Consistent Ranking: Identifies similar top products but with less sensitivity in ranking.
Summary: XGBoost provides more differentiated and higher precision rankings compared to Random Forest, reflecting better performance in identifying high-value items.



