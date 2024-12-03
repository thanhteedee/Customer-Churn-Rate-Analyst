# Banking Customer Churn Analysis and Prediction
In this project, we will analyze a datasets about Telco Telecom customers and identify the factors influencing customer churn rates, as well as build an churn prediction model

## 1. Profiling the data
Firstly, we will review the customer data we have. Specially, we check the data types and missing values:

Input:
```python
import pandas as pd
##Import dataset and checking data types of all columns##
data = pd.read_excel('C:/Users/semv/Desktop/Customer Churn Analyst/Dataset/Telco_customer_churn.xlsx')
data.info()
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

To summarize, we have data about:
- The Personal information of each customer
- The services that customers use
- The total cost in services
- reason for churn (with clients in the churn)

Howerver, the data type of TotalCharges is object, so we need to change this column to float (because the money is number)

Input:
```python
data['Total Charges'] = pd.to_numeric(data['Total Charges'], errors='coerce')
```

Next, we will check the missing value:

Input:
```python
data.isnull().sum()
```

Output:
| Column             | Missing Values |
|--------------------|-----------------|
| CustomerID         | 0               |
| Count              | 0               |
| Country            | 0               |
| State              | 0               |
| City               | 0               |
| Zip Code           | 0               |
|....................|.................|
| Monthly Charges    | 0               |
| Total Charges      | 11              |
| Churn Label        | 0               |
| Churn Value        | 0               |
| Churn Score        | 0               |
| CLTV               | 0               |
| Churn Reason       | 5174            |

There are two columns have null values:
- Churn Reason (5174 Null Values): Not all of Customer in Churn, so they dont have Churn Reason
- Total Charges (11 Null Values): We will check the information of customers which have Null values

Input:
```python
nullvalue = data[data['Total Charges'].isnull()]
displaycolumn = ['CustomerID', 'Monthly Charges', 'Tenure Months','Churn Value','Total Charges',]
print(nullvalue[displaycolumn])
```

Output:

| CustomerID    | Monthly Charges | Tenure Months | Churn Value | Total Charges |
|---------------|-----------------|---------------|-------------|---------------|
| 4472-LVYGI    | 52.55           | 0             | 0           | NaN           |
| 3115-CZMZD    | 20.25           | 0             | 0           | NaN           |
| 5709-LVOEQ    | 80.85           | 0             | 0           | NaN           |
| 4367-NUYAO    | 25.75           | 0             | 0           | NaN           |
| 1371-DWPAZ    | 56.05           | 0             | 0           | NaN           |
| 7644-OMVMY    | 19.85           | 0             | 0           | NaN           |
| 3213-VVOLG    | 25.35           | 0             | 0           | NaN           |
| 2520-SGTTA    | 20.00           | 0             | 0           | NaN           |
| 2923-ARZLG    | 19.70           | 0             | 0           | NaN           |
| 4075-WKNIU    | 73.35           | 0             | 0           | NaN           |
| 2775-SEFEE    | 61.90           | 0             | 0           | NaN           |

Based on the table, we can conclude that: 

All Customer whose TotalCharges is NUll have Tenure Months = 0 (New Customer) and Churn Value = 0, therefore they are new customer and not in Churn
So we need to remove those rows:
Input:
```python
new_data = data.dropna(subset=['Total Charges'])
print(new_data)
```
