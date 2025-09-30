# Bank Customer Churn Prediction 🏦

## Overview

This project aims to *analyze bank customer demographics and financial information* to *predict whether a customer will leave the bank (churn)*. The analysis utilizes machine learning classification models to determine which customers are most likely to close their accounts, providing the bank with actionable insights for customer retention.

---

## Dataset Context

The dataset is sourced from Kaggle and contains *10,000 rows and 14 columns*. The objective is to predict the target variable, **'Exited' (renamed to 'Churn')**, which is a binary flag:
* *0*: The customer is retained (did not churn).
* *1*: The customer closed the account (churned).

The initial analysis reveals that the dataset is heavily imbalanced, with a *churn rate of approximately 20.37%* (20.37% 'Yes', 79.63% 'No').

---

## Data Dictionary

| Column Name | Description |
| :--- | :--- |
| *CreditScore* | Credit score of the customer |
| *Geography* | Country of the customer |
| *Gender* | Gender of the customer |
| *Age* | Age of the customer |
| *Tenure* | Number of years the customer has been with the bank |
| *Balance* | Bank balance of the customer |
| *NumOfProducts* | Number of bank products the customer is utilizing |
| *HasCrCard* | Binary flag: 1 if the customer holds a credit card, 0 otherwise |
| *IsActiveMember* | Binary flag: 1 if the customer is an active member, 0 otherwise |
| *EstimatedSalary* | Estimated salary of the customer in Dollars |
| *Churn (Exited)* | *Target Variable*: 1 if the customer closed the account (churned), 0 if retained |

**Note:** The columns **RowNumber**, **CustomerId**, and **Surname** were dropped during preprocessing as they were deemed unnecessary for the prediction model. No missing or duplicate values were found in the dataset.

---

## Exploratory Data Analysis (EDA) Summary

The following factors were found to influence customer churn:

* *Age* 👵: Customers in the *late adult age group (40 and 50)* have the highest churn count, indicating they are more likely to churn compared to young adults (20-25 years old) who show the lowest churn count.
* *Geography* 🌎: *German customers* have the highest number of churns and are therefore more likely to leave the bank compared to customers from France and Spain.
* *Balance* 💰: A *huge number of customers with zero bank balance* left the bank. Customers with balances between *$100,000 and $150,000* also show a high propensity to churn.
* *NumOfProducts* 🛍: Customers utilizing *3 or 4 bank products* have a much higher churn count than non-leaving customers in those categories, making this a good indicator of churn.
* *IsActiveMember* ✅: The churn count is significantly *higher for non-active members* compared to active members.
* *Tenure* ⏱: Customers with *tenure between 1-9 years* have a higher churn count, particularly those with *1 year tenure*, while customers with more than 9 years of tenure are the least likely to churn, suggesting higher loyalty.
* *HasCrCard* 💳: More customers who *possess a credit card* (nearly 70% of the dataset) are leaving the bank compared to those without one.
* *Gender and CreditScore* 🧑‍🤝‍🧑: Neither *Gender* (females show a slightly higher, but not significant, tendency to churn) nor *CreditScore* were found to be good predictors of churn.
* *EstimatedSalary* 💵: No definite pattern was found in the salary distribution of customers who churned versus those who didn't, making *Estimated Salary not a good predictor of churn*.

---

## Data Preprocessing

1.  *Categorical Encoding*: The categorical variables **'Geography'** and **'Gender'** were converted to numerical representations using *Label Encoding*.
2.  *Feature Scaling (Normalization)*: The continuous variables **'CreditScore'**, **'Balance'**, and **'EstimatedSalary'** were scaled using *StandardScaler* (Normalization) to prepare them for modeling.
3.  *Correlation Check*: A correlation matrix heatmap showed **no significant correlation** among the variables, indicating that multicollinearity would not be a major issue for the chosen models.

---

## Modeling and Hyperparameter Tuning

The processed data was split into training and testing sets, and two classification models were selected for prediction:

1.  *Decision Tree Classifier*
2.  *Random Forest Classifier*

Both models were optimized using *GridSearchCV* with cv=5 and a scoring metric of 'roc_auc'.

| Model | Best Hyperparameters Found | Training Accuracy |
| :--- | :--- | :--- |
| *Decision Tree Classifier* | criterion: 'gini', max_depth: 6, min_samples_leaf: 10, random_state: 42 | ≈ 85.81% |
| *Random Forest Classifier* | criterion: 'entropy', max_depth: 10, min_samples_leaf: 8, random_state: 0 | ≈ 87.67% |

---

## Model Evaluation

Both models exhibited high accuracy scores, with the Random Forest Classifier slightly outperforming the Decision Tree Classifier.

| Model | Test Accuracy Score | Class 1 (Churn) Precision | Class 1 (Churn) Recall |
| :--- | :--- | :--- | :--- |
| *Random Forest Classifier* | **86.8%** | 0.82 | 0.41 |
| *Decision Tree Classifier* | **86.13%** | 0.80 | 0.39 |

The *Random Forest Classifier* has a better overall accuracy and precision score for predicting churn (Class 1). It is more reliable when it predicts a customer will churn (Precision: 0.82), but still misses a majority of actual churn cases (Recall: 0.41).

---

## Conclusion

The *Random Forest Classifier* is chosen as the *best-performing model* for this project, achieving a test accuracy of **86.8%**. The model successfully captures the non-linear relationship between customer features and the decision to churn.

The bank should focus its retention efforts on:
* *Non-Active Members* and customers utilizing *3 or 4 bank products*.
* Customers with a *bank balance between $100,000 and $150,000* or a *zero bank balance*.
* Customers in the *40-50 age bracket* and those who have been with the bank for *1 year*.
* Customers located in *Germany*.
