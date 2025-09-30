# Bank Customer Churn Prediction 🏦

## Overview

[cite_start]This project aims to *analyze bank customer demographics and financial information* to *predict whether a customer will leave the bank (churn)*[cite: 4]. [cite_start]The analysis utilizes machine learning classification models to determine which customers are most likely to close their accounts, providing the bank with actionable insights for customer retention[cite: 4, 7].

---

## Dataset Context

[cite_start]The dataset is sourced from Kaggle and contains *10,000 rows and 14 columns[cite: 6]. [cite_start]The objective is to predict the target variable, **'Exited' (renamed to 'Churn')*, which is a binary flag[cite: 7, 10, 73]:
* [cite_start]*0*: The customer is retained (did not churn)[cite: 10].
* [cite_start]*1*: The customer closed the account (churned)[cite: 10].

[cite_start]The initial analysis reveals that the dataset is heavily imbalanced, with a *churn rate of approximately 20.37%* (20.37% 'Yes', 79.63% 'No')[cite: 91, 104].

---

## Data Dictionary

| Column Name | Description |
| :--- | :--- |
| *CreditScore* | [cite_start]Credit score of the customer [cite: 10] |
| *Geography* | [cite_start]Country of the customer [cite: 10] |
| *Gender* | [cite_start]Gender of the customer [cite: 10] |
| *Age* | [cite_start]Age of the customer [cite: 10] |
| *Tenure* | [cite_start]Number of years the customer has been with the bank [cite: 10] |
| *Balance* | [cite_start]Bank balance of the customer [cite: 10] |
| *NumOfProducts* | [cite_start]Number of bank products the customer is utilizing [cite: 10] |
| *HasCrCard* | [cite_start]Binary flag: 1 if the customer holds a credit card, 0 otherwise [cite: 10] |
| *IsActiveMember* | [cite_start]Binary flag: 1 if the customer is an active member, 0 otherwise [cite: 10] |
| *EstimatedSalary* | [cite_start]Estimated salary of the customer in Dollars [cite: 10] |
| *Churn (Exited)* | [cite_start]*Target Variable*: 1 if the customer closed the account (churned), 0 if retained [cite: 10, 73] |

[cite_start]Note: The columns **RowNumber, **CustomerId, and **Surname* were dropped during preprocessing as they were deemed unnecessary for the prediction model[cite: 28, 30]. [cite_start]No missing or duplicate values were found in the dataset[cite: 34, 66].*

---

## Exploratory Data Analysis (EDA) Summary

The following factors were found to influence customer churn:

* [cite_start]*Age* 👵: Customers in the *late adult age group (40 and 50)* have the highest churn count, indicating they are more likely to churn compared to young adults (20-25 years old) who show the lowest churn count[cite: 165, 166].
* [cite_start]*Geography* 🌎: *German customers* have the highest number of churns and are therefore more likely to leave the bank compared to customers from France and Spain[cite: 218, 219].
* [cite_start]*Balance* 💰: A *huge number of customers with zero bank balance* left the bank[cite: 276]. [cite_start]Customers with balances between *\$100,000 and \$150,000* also show a high propensity to churn[cite: 277, 285].
* [cite_start]*NumOfProducts* 🛍: Customers utilizing *3 or 4 bank products* have a much higher churn count than non-leaving customers in those categories, making this a good indicator of churn[cite: 309, 310].
* [cite_start]*IsActiveMember* ✅: As expected, the churn count is significantly *higher for non-active members* compared to active members[cite: 352].
* [cite_start]*Tenure* ⏱: Customers with *tenure between 1-9 years* have a higher churn count, particularly those with *1 year tenure*, while customers with more than 9 years of tenure are the least likely to churn, suggesting higher loyalty[cite: 251, 252, 253].
* [cite_start]*HasCrCard* 💳: More customers who *possess a credit card* (nearly 70% of the dataset) are leaving the bank compared to those without one[cite: 331, 332].
* [cite_start]*Gender and CreditScore* 🧑‍🤝‍🧑: Neither *Gender* (females show a slightly higher, but not significant, tendency to churn) nor *CreditScore* were found to be good predictors of churn[cite: 131, 195].
* [cite_start]*EstimatedSalary* 💵: No definite pattern was found in the salary distribution of customers who churned versus those who didn't, making *Estimated Salary not a good predictor of churn*[cite: 373, 374].

---

## Data Preprocessing

1.  [cite_start]*Categorical Encoding: The categorical variables **'Geography'* and *'Gender'* were converted to numerical representations using *Label Encoding*[cite: 377, 378, 385, 386].
2.  [cite_start]*Feature Scaling (Normalization): The continuous variables **'CreditScore', **'Balance', and **'EstimatedSalary'* were scaled using *StandardScaler* (Normalization) to prepare them for modeling[cite: 388, 389, 391].
3.  [cite_start]*Correlation Check: A correlation matrix heatmap showed **no significant correlation* among the variables, indicating that multicollinearity would not be a major issue for the chosen models[cite: 509].

---

## Modeling and Hyperparameter Tuning

The processed data was split into training and testing sets, and two classification models were selected for prediction:

1.  *Decision Tree Classifier*
2.  *Random Forest Classifier*

[cite_start]Both models were optimized using *GridSearchCV* with cv=5 and a scoring metric of 'roc_auc'[cite: 528, 568].

| Model | Best Hyperparameters Found | Training Accuracy |
| :--- | :--- | :--- |
| *Decision Tree Classifier* | [cite_start]criterion: 'gini', max_depth: 6, min_samples_leaf: 10, random_state: 42 [cite: 534] | [cite_start]$\approx 85.81\%$ [cite: 551] |
| *Random Forest Classifier* | [cite_start]criterion: 'entropy', max_depth: 10, min_samples_leaf: 8, random_state: 0 [cite: 573] | [cite_start]$\approx 87.67\%$ [cite: 590] |

---

## Model Evaluation

[cite_start]Both models exhibited high accuracy scores, with the Random Forest Classifier slightly outperforming the Decision Tree Classifier[cite: 784, 785].

| Model | Test Accuracy Score | Class 1 (Churn) Precision | Class 1 (Churn) Recall |
| :--- | :--- | :--- | :--- |
| *Random Forest Classifier* | [cite_start]$86.8\%$** [cite: 764] | [cite_start]$0.82$ [cite: 745] | [cite_start]$0.41$ [cite: 746] |
| *Decision Tree Classifier* | [cite_start]$86.13\%$** [cite: 682] | [cite_start]$0.80$ [cite: 657] | [cite_start]$0.39$ [cite: 658] |

[cite_start]The *Random Forest Classifier* has a better overall accuracy and precision score for predicting churn (Class 1)[cite: 785]. It is more reliable when it predicts a customer will churn (Precision: 0.82), but still misses a majority of actual churn cases (Recall: 0.41).

---

## Conclusion

[cite_start]The *Random Forest Classifier* is chosen as the *best-performing model* for this project, achieving a test accuracy of $86.8\%$[cite: 764, 785]. The model successfully captures the non-linear relationship between customer features and the decision to churn.

The bank should focus its retention efforts on:
* *Non-Active Members* and customers utilizing *3 or 4 bank products*.
* Customers with a *bank balance between \$100,000 and \$150,000* or a *zero bank balance*.
* Customers in the *40-50 age bracket* and those who have been with the bank for *1 year*.
* Customers located in *Germany*.
