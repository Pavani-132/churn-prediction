# Bank Customer Churn Prediction 📉

## Project Goal
[cite_start]The primary objective of this project is to analyze bank customer demographics and financial data to **predict whether a customer will leave the bank (churn)**[cite: 4]. [cite_start]By building a highly predictive machine learning model, the bank can proactively identify at-risk customers and implement targeted retention strategies[cite: 4, 323].

## 💾 Dataset Overview

[cite_start]The dataset, sourced from Kaggle, contains 10,000 rows and 14 columns of bank customer information[cite: 6]. [cite_start]The analysis focuses on customer age, gender, country, credit score, balance, and other financial variables[cite: 4].

| Column Name | Description | Data Type (after preprocessing) |
| :--- | :--- | :--- |
| `CreditScore` | Credit score of the customer | `float64` (Scaled) |
| `Geography` | Country of the customer | `int64` (Encoded) |
| `Gender` | Gender of the customer | `int64` (Encoded) |
| `Age` | Age of the customer | `int64` |
| `Tenure` | Number of years with the bank | `int64` |
| `Balance` | Bank balance of the customer | `float64` (Scaled) |
| `NumOfProducts` | Number of bank products the customer uses | `int64` |
| `HasCrCard` | Binary flag (1: yes, 0: no) | `int64` |
| `IsActiveMember` | Binary flag (1: active, 0: non-active) | `int64` |
| `EstimatedSalary` | Estimated salary in Dollars | `float64` (Scaled) |
| **`Churn`** | **Target Variable**: 1 if the customer closed account, 0 if retained | `int64` |

---

## 🔬 Exploratory Data Analysis (EDA) & Key Findings

The initial analysis revealed critical insights into customer attrition factors:

* [cite_start]**Imbalance**: Only **20.37%** of customers churned, while 79.63% were retained[cite: 101, 104].
* [cite_start]**Age is Significant**: Churn count is highest for customers in the **40-50 age group**[cite: 165, 166].
* [cite_start]**Geography is a Factor**: **German customers** are inferred to be more likely to churn than those from France or Spain[cite: 218, 219].
* [cite_start]**Products are Crucial**: Customers with **3 or 4 products** show a much higher churn count relative to non-leaving customers in that category, making this a strong churn indicator[cite: 309, 310].
* [cite_start]**Activity Status**: Churn count is predictably **higher for non-active members**[cite: 321]. [cite_start]The bank should focus on retaining these non-active customers[cite: 323].
* [cite_start]**Tenure**: Customers with very high tenure (more than 9 years) count for the least churn, showing loyalty, while those with **1-9 years tenure** have higher churn counts[cite: 251, 252, 253].
* [cite_start]**Credit Score & Salary**: Both the Credit Score and Estimated Salary were found to be **not a good indicator or predictor of churn**, as their distributions were similar across churned and non-churned groups[cite: 195, 327, 328].

---

## 🧹 Data Preprocessing & Feature Engineering

1.  [cite_start]**Column Management**: The columns `RowNumber`, `CustomerId`, and `Surname` were dropped as they are unnecessary for the prediction model[cite: 28]. [cite_start]The target column `Exited` was renamed to `Churn`[cite: 71, 73].
2.  [cite_start]**Missing Values**: No missing values were found [cite: 34-55].
3.  [cite_start]**Encoding**: Categorical variables (`Geography`, `Gender`) were converted into numerical format using `LabelEncoder`[cite: 329].
4.  [cite_start]**Scaling**: Continuous variables (`CreditScore`, `Balance`, `EstimatedSalary`) were normalized using `StandardScaler` to ensure features contribute equally to the model training[cite: 329].


