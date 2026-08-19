# Data_Analysis_Credit-Card 💳 

## 📌 Project Overview

The **Credit Card Financial Weekly Status Dashboard** is a data analytics and business intelligence project built to analyze customer transactions, revenue, payment patterns, card usage, and customer demographics.

The objective of this project is to transform raw credit-card data into an interactive **Power BI dashboard** that can help financial teams understand customer behavior, monitor revenue performance, identify important customer segments, and track key financial metrics on a weekly basis.

The project combines **SQL, Power BI, DAX, and CSV-based data** to create an end-to-end analytics workflow.

![Transaction Report](https://github.com/Piyushsingh006/Data_Analysis_Credit-Card/blob/main/Screenshot%202026-08-19%20202709.png?raw=true)

---

## 🎯 Business Problem

Credit-card businesses generate large amounts of transactional and customer data. Looking at this information directly from raw datasets makes it difficult to identify trends and make quick business decisions.

This project addresses that problem by creating a centralized dashboard capable of answering questions such as:

* How much revenue is being generated?
* Which states contribute the most revenue?
* Which age groups generate the most business?
* Which card categories are used the most?
* What payment methods do customers prefer?
* What is the current delinquency rate?
* How many customers are actively using their cards?
* How is revenue changing from week to week?
* Which customer segments have the highest financial contribution?

---

# 🛠️ Technology Stack

* **SQL** — Database creation, data storage and querying
* **Microsoft Power BI** — Dashboard development and visualization
* **DAX** — Measures and calculated columns
* **CSV** — Source data
* **Power BI Service** — Dashboard publishing
* **GitHub** — Project documentation and version control

---

# 🔄 Project Workflow

## Step 1 — Data Preparation

The CSV datasets were first examined to understand the available customer and transaction fields.

SQL tables were then designed according to the structure of the datasets and the CSV files were imported into the database.

---

## Step 2 — Connecting SQL with Power BI

The SQL database was connected to **Power BI Desktop** so that the data could be transformed, analyzed and visualized.

This created a complete flow from:

**CSV → SQL Database → Power BI → Dashboard**

---

## Step 3 — Data Quality Analysis

Power BI's data profiling functionality was configured to analyze the **complete dataset rather than only the default sample of 1,000 rows**.

This helped in identifying potential data-quality issues across the entire dataset.

---

# 📊 Dashboard Development

Several interactive filters were added to make the dashboard easier to explore.

### Filters / Slicers

The dashboard contains slicers for:

* Quarter
* Gender
* Income Type
* Card Category
* Week Start Date

These filters allow users to dynamically change the dashboard and analyze specific customer segments.

---

# 📈 KPI Cards

Important business metrics were displayed using Power BI card visuals.

The dashboard tracks metrics such as:

* Total Revenue
* Total Interest Earned
* Total Income
* Average Customer Metrics
* Total Transaction Amount
* Customer Activation Rate
* Customer Delinquency Rate

These KPIs provide a quick overview of the overall financial performance.

---

# 📊 Customer & Transaction Analysis

Multiple visualizations were created to analyze different dimensions of the credit-card dataset.

The dashboard includes analysis of:

* Top-performing states
* Customer age groups
* Education levels
* Income segments
* Card categories
* Transaction methods
* Revenue trends
* Customer activity
* Utilization ratios

Bar charts, tables, cards and line charts were used depending on the type of information being presented.

---

# 🧮 DAX Calculations

DAX was used to create additional analytical fields and measures.

## 1. Customer Age Segmentation

Customers were divided into different age brackets to make demographic analysis easier.

```DAX
Age Group =
SWITCH(
    TRUE(),
    customer_detail[Customer_Age] < 30, "20-30",
    customer_detail[Customer_Age] >= 30 &&
    customer_detail[Customer_Age] < 40, "30-40",
    customer_detail[Customer_Age] >= 40 &&
    customer_detail[Customer_Age] < 50, "40-50",
    customer_detail[Customer_Age] >= 50 &&
    customer_detail[Customer_Age] < 60, "50-60",
    customer_detail[Customer_Age] >= 60, "60+",
    "Unknown"
)
```

This segmentation makes it easier to compare customer behavior across different age categories.

---

## 2. Income Segmentation

Customers were also categorized according to their income.

```DAX
Income Group =
SWITCH(
    TRUE(),
    customer_detail[Income] < 35000, "Low Income",
    customer_detail[Income] >= 35000 &&
    customer_detail[Income] < 70000, "Med Income",
    customer_detail[Income] >= 70000, "High Income",
    "Unknown"
)
```

This allows revenue and customer behavior to be studied across different income levels.

---

## 3. Week Number

A week number was generated from the week-start date to support weekly trend analysis.

```DAX
Week num2 =
WEEKNUM(credit_card_detail[Week_Start_Date])
```

This field was later used for week-over-week revenue calculations.

---

# 💰 Revenue Calculation

A calculated revenue measure was created by combining annual fees, transaction amount and interest earned.

```DAX
Revenue =
credit_card_detail[Annual_Fees]
+
credit_card_detail[Total_Trans_Amt]
+
credit_card_detail[Interest_Earned]
```

This metric is used throughout the dashboard to evaluate overall revenue generation.

---

# 📅 Week-over-Week Revenue Analysis

To understand short-term revenue movement, a **Week-over-Week (WoW) Revenue** metric was developed.

### Current Week Revenue

```DAX
Current_week_revenue =
CALCULATE(
    SUM(credit_card_detail[Revenue]),
    ALL(credit_card_detail),
    credit_card_detail[Week num2] =
        MAX(credit_card_detail[Week num2])
)
```

### Previous Week Revenue

```DAX
Previous_week_revenue =
CALCULATE(
    SUM(credit_card_detail[Revenue]),
    FILTER(
        ALL(credit_card_detail),
        credit_card_detail[Week num2] =
            MAX(credit_card_detail[Week num2]) - 1
    )
)
```

### WoW Revenue %

```DAX
WoW_Revenue =
DIVIDE(
    [Current_week_revenue] - [Previous_week_revenue],
    [Previous_week_revenue]
)
```

This calculation helps identify whether revenue is increasing or decreasing compared with the previous week.

---

# 🖥️ Dashboard Pages

The Power BI report contains two primary analytical pages.

## 1. Transaction Report

The **Transaction Report** focuses on financial and transaction-related metrics.

It provides information about:

* Revenue
* Transaction amount
* Card categories
* Transaction methods
* Weekly revenue trends
* State-wise performance
* Customer spending behavior

---

## 2. Customer Report

The **Customer Report** focuses on customer demographics and engagement.

It includes analysis based on:

* Age
* Gender
* Income
* Education
* Card category
* Customer activation
* Delinquency
* Utilization ratio

---

# 🔎 Key Insights

The completed dashboard produced several interesting findings from the dataset.

### Overall Customer Base

* **Total Customers:** 10,108
* **Total Transaction Amount:** approximately **$46M**

### Revenue by Gender

* **Male customers:** approximately **$30M — 54.64%**
* **Female customers:** approximately **$25M — 45.36%**

Male customers therefore generated a slightly larger share of total revenue.

---

### Card Category

**Blue and Silver cards together account for approximately 93% of overall transactions**, making them the dominant card categories within the dataset.

---

### State Performance

**Texas (TX), New York (NY), and California (CA)** together contribute approximately **68%** of the overall business, making these states the strongest contributors in the dataset.

---

# 💳 Transaction Method Analysis

Customer transactions were divided into three major payment methods.

| Transaction Method | Customer Share |
| ------------------ | -------------: |
| Swipe              |         63.12% |
| Chip               |         30.67% |
| Online             |          6.21% |

The analysis shows that **swipe transactions are the most common payment method**, representing more than half of the observed transactions.

---

# 👥 Age Group Analysis

The customer base was divided into five age groups.

| Age Group | Customer Share |
| --------- | -------------: |
| 20–30     |          2.13% |
| 30–40     |         18.19% |
| 40–50     |         44.81% |
| 50–60     |         29.61% |
| 60+       |          5.26% |

The **40–50 age group represents the largest customer segment**, accounting for approximately 44.81% of customers.

---

# ⚠️ Delinquency Analysis

The overall **customer delinquency rate is approximately 6.06%**.

This metric provides an indication of the proportion of customers showing delayed or problematic payment behavior.

---

# ⚡ Customer Activation

The overall **customer activation rate is approximately 57.5%**.

This metric can be used to understand the proportion of customers who are actively engaged with their credit cards.

---

# 💳 Card Utilization

The dashboard also compares the average utilization ratio across different card categories.

Among the available card categories, the **Blue Card category records the highest average utilization ratio**.

This can provide useful insight into how actively customers are using different card products.

---

# 📸 Dashboard Preview

## Transaction Report

![Transaction Report](https://github.com/Piyushsingh006/Data_Analysis_Credit-Card/blob/main/Screenshot%202026-08-19%20202709.png?raw=true)


## Customer Report




![Customer Report](https://github.com/Piyushsingh006/Data_Analysis_Credit-Card/blob/main/Screenshot%202026-08-19%20203348.png?raw=true)


---

# 🚀 What This Project Demonstrates

This project demonstrates my ability to work with a complete business-intelligence workflow, including:

* Importing and structuring raw data
* Designing SQL tables
* Connecting SQL databases with Power BI
* Performing data profiling
* Creating calculated columns
* Writing DAX measures
* Building interactive dashboards
* Performing customer segmentation
* Analyzing financial KPIs
* Performing time-based revenue analysis
* Extracting actionable business insights
* Publishing reports through Power BI Service

---

# 📌 Future Improvements

Some possible extensions for this project include:

* Adding automated data refresh
* Connecting the dashboard to a live financial data source
* Building predictive models for delinquency
* Creating customer churn predictions
* Adding customer lifetime value analysis
* Developing fraud-risk indicators
* Adding forecasting for future revenue
* Integrating machine-learning models with the Power BI workflow

---

# 👨‍💻 Project Summary

The **Credit Card Financial Weekly Status Dashboard** converts raw customer and transaction data into an interactive analytical solution.

By combining **SQL, Power BI and DAX**, the project provides a consolidated view of customer behavior, transaction activity, revenue performance and credit-card usage.

The final dashboard can help financial teams identify important customer segments, monitor business performance and make more informed decisions using data rather than relying solely on static reports.
