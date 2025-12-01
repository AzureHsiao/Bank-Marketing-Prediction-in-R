# Bank-Marketing-Prediction-in-R

This repository contains a full predictive modeling and customer analytics project using the UCI Bank Marketing dataset.  
The purpose is to identify which customers are most likely to subscribe to a term deposit and provide marketing insights that can improve targeting efficiency.
The analysis includes logistic regression, random forest, decision tree modeling, clustering, ROC/AUC evaluation, and threshold optimization.


## Project Overview

This project follows a full analytics workflow:

1. Data loading and preprocessing  
2. Feature engineering and data cleaning  
3. Train-test split  
4. Logistic regression modeling (with stepwise selection and VIF checks)  
5. Random Forest modeling and variable importance  
6. Decision tree modeling with pruning  
7. K-means clustering for customer segmentation  
8. Evaluation using accuracy, sensitivity, specificity, and ROC/AUC  
9. Business interpretation of model outputs  

All code is included in the `.qmd` file, and visualizations can be found in the PDF.



## Dataset Summary

- Observations: 45,211  
- Target variable: `y` (subscription: yes/no)  
- Variables include demographics, account balance, previous contacts, campaign history, and macro timing indicators (month, day).  
- Duration was removed to avoid leakage.  
- A new engineered feature `previous_contact` was added to improve interpretability.



## Logistic Regression Model

A full logistic model was first fitted, then refined using AIC-based stepwise selection.  
Key significant predictors included:

- Job type (retired, student, housemaid)  
- Education level (secondary, tertiary)  
- Housing and personal loan status  
- Contact method  
- Campaign month  
- Number of campaign calls  
- Previous campaign outcome (especially “success”)  
- Account balance  

### Model Performance

- AUC: **0.7644**  
- Default threshold (0.5) sensitivity was low due to class imbalance  
- Optimal threshold selected using Youden’s Index: **0.155**  
- Improved sensitivity and maintained strong specificity  

This threshold better captures potential customers and is more appropriate for marketing targeting.



## Random Forest Model

A 500-tree Random Forest model was trained after hyperparameter tuning (mtry = 2).  
Key findings from variable importance:

1. **Month** was the strongest predictor, showing clear seasonality.  
2. **Previous campaign outcome** (success) highly increased subscription likelihood.  
3. **Age** displayed a nonlinear relationship, with middle-aged customers having the highest probability.  
4. **pdays** highlighted the importance of recency.  
5. **Higher balance** increased probability, with diminishing returns.  
6. **Campaign frequency** had a negative effect, suggesting fatigue.

The Random Forest model demonstrated stronger nonlinear detection than logistic regression.



## Decision Tree Model

A pruned classification tree (cp = 0.029) revealed a simple but highly interpretable structure:

- **Previous campaign outcome** was the only variable used in the final pruned tree.  
- Customers with prior **successful** outcomes had the highest subscription probability (~65%).  
- All other groups (“failure,” “other,” “unknown”) showed low likelihood (~10%).

Although simple, the tree provides a clear insight into the strongest single predictor.



## K-means Clustering

Clustering was performed on numeric and encoded variables (age, balance, pdays, campaign, previous, poutcome).  
A four-cluster solution was chosen as the most interpretable.

### Summary of Clusters

| Cluster | Description | Yes Rate |
|--------|-------------|----------|
| **2** | Warm re-engagement leads (recent contact, past success) | **64.9%** |
| **4** | Reactivation candidates (longer gap, moderate potential) | **13.5%** |
| **1** | Young, low-engagement customers | **9.4%** |
| **3** | Older customers with no previous contact | **9.0%** |

These clusters help prioritize marketing segments and optimize campaign resources.



## Purpose of This Project

This project demonstrates ability in:

- R-based statistical modeling
- Predictive analytics for marketing
- Customer segmentation
- Model evaluation and threshold tuning
- Translating model outputs into actionable marketing recommendations


## Conclusion

Across all models, the strongest predictors of subscription were prior campaign success,
contact month, recency of contact (pdays), account balance, and the customer’s job and
education level. Logistic regression established interpretable baseline drivers, while Random
Forest revealed nonlinear patterns and stronger seasonal effects. The clustering results
identified a high-potential segment (Cluster 2) with a 64.9% subscription rate, suggesting the
bank should prioritize warm re-engagement leads and customers with successful prior
interactions. Overall, the analysis provides a clear targeting strategy for improving campaign
efficiency and reducing wasted outreach.


