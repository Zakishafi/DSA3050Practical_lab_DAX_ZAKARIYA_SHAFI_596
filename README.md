# Zakariya Shafi 596

# DSA 3050A — Business Intelligence & Data Visualization
## Practical Lab: DAX Using Your Own Dataset


## 📊 Project Overview
This project demonstrates the application of **Data Analysis Expressions (DAX)** in Power BI using a real-world financial dataset. The goal is to build a well-structured data model, create meaningful analytical measures, and validate results using interactive visuals.

The analysis focuses on **banking transaction data in the United States (2023–2024)**, enabling insights into customer behavior, transaction trends, fraud detection, and financial performance.


## 📁 Dataset Information

- **Dataset Name:** USA Banking Transactions Dataset (2023–2024)  
- **Source:** [Kaggle Dataset](https://www.kaggle.com/datasets/pradeepkumar2424/usa-banking-transactions-dataset-2023-2024)  
- **Rows:** 5,389  
- **Time Period:** 2023 – 2024  

### Key Features
- Transaction Amounts  
- Transaction Type (Debit/Credit)  
- Categories (Travel, Grocery, etc.)  
- Payment Methods (Cash, E-Wallet)  
- Fraud Flags  
- Customer Demographics (Age, Income)  
- Account Balance  
- Timestamped transaction dates  

This dataset supports:
- Time series analysis  
- Fraud detection analysis  
- Customer segmentation  
- Financial performance tracking  


## 🧱 Data Model

A **Star Schema** was implemented:

### Fact Table
- `Transactions`

### Dimension Tables
- `DateTable`
- Category (from dataset)
- City (location-based analysis)

### Relationships
- One-to-many relationships from dimensions to fact table  
- DateTable linked to Transaction_Date  


## 📐 DAX Measures

### 🔹 Core Measures
```DAX
Total Transaction Amount = SUM(Transactions[Transaction_Amount])

Total Customer Income = SUM(Transactions[Customer_Income])

Average Transaction Amount = AVERAGE(Transactions[Transaction_Amount])

Total Loyalty Points = SUM(Transactions[Loyalty_Points_Earned])

Transaction Size =
SWITCH(
    TRUE(),
    Transactions[Transaction_Amount] < 500, "Small",
    Transactions[Transaction_Amount] < 2000, "Medium",
    "Large"
)

Age Group =
SWITCH(
    TRUE(),
    Transactions[Customer_Age] < 30, "Young",
    Transactions[Customer_Age] < 50, "Middle Aged",
    "Senior"
)

Successful Transactions Amount =
CALCULATE(
    [Total Transaction Amount],
    Transactions[Transaction_Status] = "Success"
)

Fraud Transactions Amount =
CALCULATE(
    [Total Transaction Amount],
    Transactions[Fraud_Flag] = "Yes"
)

% Category Contribution =
DIVIDE(
    [Total Transaction Amount],
    CALCULATE([Total Transaction Amount], ALL(Transactions[Category]))
)

YTD Transaction Amount =
TOTALYTD(
    [Total Transaction Amount],
    DateTable[Date]
)

Previous Year Amount =
CALCULATE(
    [Total Transaction Amount],
    SAMEPERIODLASTYEAR(DateTable[Date])
)

YoY Growth % =
DIVIDE(
    [Total Transaction Amount] - [Previous Year Amount],
    [Previous Year Amount]
)

## Visualizations

The following visuals were used to validate the DAX calculations:

Card: Total Transaction Amount

Bar Chart: Category vs Total Transaction Amount

Line Chart: Monthly Transaction Trends (2023–2024)

Table: Category breakdown with fraud, success, and contribution metrics

All visuals are interactive and respond dynamically to slicers.

