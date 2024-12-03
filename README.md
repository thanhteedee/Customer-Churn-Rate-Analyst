# Banking Customer Churn Analysis and Prediction
In this project, we will analyze a datasets about Telco Telecom customers and identify the factors influencing customer churn rates, as well as build an churn prediction model

## 1. Profiling the data
Firstly, we will review the customer data we have. Specially, we check the data types and missing values:

Input:
```python
import pandas as pd
##Import dataset and checking data types of all columns##
df = pd.read_excel('C:/Users/semv/Desktop/Customer Churn Analyst/Dataset/Telco_customer_churn.xlsx')
df.info()
```
Output:

| #   | Column            | Non-Null Count   | Dtype   |
|-----|-------------------|------------------|---------|
| 0   | CustomerID        | 7043 non-null    | object  |
| 1   | Count             | 7043 non-null    | int64   |
| 2   | Country           | 7043 non-null    | object  |
| 3   | State             | 7043 non-null    | object  |
| 4   | City              | 7043 non-null    | object  |
| 5   | Zip Code          | 7043 non-null    | int64   |
| ....| ..................| .................| ........|
| 27  | Total Charges     | 7043 non-null    | <mark>object</mark>  |
| 28  | Churn Label       | 7043 non-null    | object  |
| 29  | Churn Value       | 7043 non-null    | int64   |
| 30  | Churn Score       | 7043 non-null    | int64   |
| 31  | CLTV              | 7043 non-null    | int64   |
| 32  | Churn Reason      | 1869 non-null    | object  |

