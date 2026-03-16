# Zakariya Shafi 596

# DSA 3050A — Business Intelligence & Data Visualization
## Practical Lab: DAX Using Your Own Dataset

This repository contains my submission for the **DSA 3050A Business Intelligence & Data Visualization Practical Lab**, which focuses on building a clean Power BI data model and implementing **DAX calculations** using a real-world dataset.

The assignment demonstrates my ability to:
- select and justify a suitable real-world dataset,
- structure the data model correctly in Power BI,
- create meaningful **DAX measures**,
- use **calculated columns** for business classification,
- apply **filter context** with `CALCULATE`,
- use **iterator functions** such as `AVERAGEX` and `SUMX`,
- perform **time intelligence analysis** using a Date table,
- and validate calculations through Power BI visuals.


## Repository Description

**Suggested GitHub repo description:**  
Power BI DAX practical lab using the Global Superstore dataset: data modelling, calculated columns, filter context, iterator functions, time intelligence, and visual validation.


## Assignment Overview

For this lab, I used the **Global Superstore 2016** dataset, a real-world retail dataset containing transactional sales records across products, customers, segments, and global regions. The dataset is appropriate for this assignment because it contains:
- more than **5,000 rows**,
- numeric measures such as **Sales, Profit, and Quantity**,
- categorical dimensions such as **Category, Segment, Country, and Region**,
- and a valid **date column** for time-based analysis.

This repository documents the modelling approach, the DAX logic used, and the expected report outputs.


## Dataset Information

- **Dataset Name:** Global Superstore 2016  
- **Source:** Kaggle  
- **Dataset Link:** https://www.kaggle.com/datasets/tahir1413/global-superstore-2016  
- **File Format:** Excel workbook (.xlsx)  
- **Main Analytical Table:** Orders  
- **Other Supporting Tables:** Returns, People

### Brief Description
The Global Superstore dataset contains retail transaction data from multiple international markets. It includes order dates, customer details, product information, sales, profit, quantity, shipping details, and geographical attributes. This makes it suitable for Power BI modelling, business analysis, and DAX-based performance reporting.


## Project Objectives

The main objectives of this assignment were to:
1. prepare a clean and structured Power BI data model,
2. identify fact and dimension tables,
3. create DAX measures relevant to business performance,
4. build calculated columns for row-level classification,
5. demonstrate understanding of row context and filter context,
6. implement time intelligence calculations,
7. and validate outputs using appropriate visuals.


## Data Model Design

The model was designed using a **star schema** to improve clarity and analytical efficiency.

### Fact Table
- `Orders_Fact`

This table contains the transactional records such as:
- Order ID
- Order Date
- Sales
- Profit
- Quantity
- Product ID
- Customer ID
- Region / City

### Dimension Tables
- `Dim_Customer`
- `Dim_Product`
- `Dim_Location`
- `Returns_Dim`
- `People_Dim`
- `DateTable`

### Relationship Design
The relationships were created as **one-to-many** from dimensions to the fact table, with single filter direction where appropriate.

This modelling approach supports:
- accurate aggregation,
- clean slicing and filtering,
- correct time intelligence,
- and better visual performance in Power BI.


## DAX Measures Implemented

The following core measures were created:

DAX
Total Sales = SUM(Orders_Fact[Sales])


DAX
Total Profit = SUM(Orders_Fact[Profit])


```DAX
Total Orders = DISTINCTCOUNT(Orders_Fact[Order ID])

DAX
Total Customers = DISTINCTCOUNT(Dim_Customer[Customer ID])

### Why these measures matter
These measures summarize key business performance indicators and respond dynamically to slicers and filters in Power BI.

---

## Calculated Columns

Two calculated columns were created to classify rows into business-relevant groups.

```DAX
Profit Category =
IF(
    Orders_Fact[Profit] > 0,
    "Profitable",
    "Loss"
)

```DAX
Sales Category =
SWITCH(
    TRUE(),
    Orders_Fact[Sales] < 100, "Low Sales",
    Orders_Fact[Sales] < 500, "Medium Sales",
    "High Sales"
)


### Purpose of calculated columns
These columns support grouping, segmentation, and slicing within report visuals.


## Filter Context and CALCULATE

To demonstrate understanding of filter context, the following DAX measures were created using `CALCULATE`:

```DAX
US Sales =
CALCULATE(
    [Total Sales],
    Dim_Location[Country] = "United States"
)

```DAX
Sales Contribution % =
DIVIDE(
    [Total Sales],
    CALCULATE([Total Sales], ALL(Dim_Location))
)

```DAX
Total Sales All Products =
CALCULATE(
    [Total Sales],
    REMOVEFILTERS(Dim_Product)
)

### Explanation
These measures were used to:
- apply filters,
- remove filters,
- and compare selected values against grand totals.

This section demonstrates practical understanding of **context transition** and **context manipulation** in DAX.


## Iterator Function

An iterator function was used to show row-by-row evaluation.

```DAX
Average Order Revenue =
AVERAGEX(
    Orders_Fact,
    Orders_Fact[Sales]
)

### Why this is important
Unlike simple aggregation functions, iterator functions evaluate expressions row by row before returning the final result. This is important when calculations require row context.

---

## Time Intelligence

A dedicated `DateTable` was created and marked as the official Date table in Power BI. This made it possible to implement time-based calculations.

### Measures created

```DAX
Sales YTD =
TOTALYTD(
    [Total Sales],
    DateTable[Date]
)


```DAX
Sales Previous Year =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DateTable[Date])
)

```DAX
YoY Growth % =
DIVIDE(
    [Total Sales] - [Sales Previous Year],
    [Sales Previous Year]
)

### Purpose
These measures help track business performance over time and compare current performance with prior periods.


## Visual Validation

The following visuals were used to validate that the DAX calculations worked correctly:
- **Card visual** for Total Sales,
- **Bar/Column chart** for Sales by Category,
- **Line chart** for Sales Trend by Year,
- **Table visual** for combined analytical view.

All visuals are expected to respond dynamically to filters and slicers.


## Challenge Encountered

One of the main challenges in this assignment was ensuring that time intelligence calculations worked correctly. Initially, the formulas did not return the expected results because there was no dedicated Date table. This was resolved by creating a proper calendar table, relating it to the fact table through the order date, and marking it as the report's Date table in Power BI.


## Repository Structure

```text
dsa3050a-bi-dax-lab/
│
├── README.md
├── repo_description.txt
├── .gitignore
├── docs/
│   ├── Assignment_Instructions.pdf
│   ├── Submission_Report.pdf
│   └── Screenshots/
│       ├── Model_View.png
│       ├── DAX_Measures.png
│       ├── Calculated_Columns.png
│       ├── Card_Visual.png
│       ├── Bar_Chart.png
│       ├── Line_Chart.png
│       └── Table_Visual.png
│
├── data/
│   └── dataset_source_link.txt
│
└── pbix/
    └── DSA3050A_DAX_Lab.pbix


## How to Use This Repository

1. Download or clone the repository.
2. Open the Power BI file in the `pbix/` folder.
3. Review the report model, DAX measures, and visuals.
4. Use the screenshots and report document in `docs/` for submission or presentation.


## Tools Used

- **Power BI Desktop** for modelling, DAX, and visualization
- **Microsoft Excel / Kaggle dataset source** for input data
- **GitHub** for project documentation and version control


