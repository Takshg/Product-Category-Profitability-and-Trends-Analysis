# Product-Category-Profitability-and-Trends-Analysis-for-Fashion-Retail

This project analyzes a synthetic clothing retail dataset.

Using SQL + Python + Tableau, the analysis focuses on:

- Category-level sales and profitability
- SKU performance and profit contribution
- Customer behaviour via RFM segmentation
- Markdown efficiency and margin impact
- Trends, seasonality, and sales channel mix

The project is structured so it can be reviewed end-to-end as an analytics case study.

---

## 1. Repository Structure

```text
.
├── Analysis.ipynb             # Main Jupyter notebook (SQL, Python, analysis, modeling)
├── clothing_sales_clean.csv   # Cleaned and transformed dataset used for analysis/Tableau
├── clothing_sales.db          # SQLite database created from the cleaned dataset
├── Dashboards_Images.pdf      # Exported Tableau dashboards for quick viewing
├── Dashboards.twb             # Tableau workbook containing all dashboards
├── dataset/                   # Raw dataset folder from Kaggle
├── Report.pdf                 # Final written report summarizing insights & recommendations
└── README.md                  # Project documentation (this file)
```

---

## 2. Data

Source:

Clothing Sales Transactions Dataset – Kaggle, created by *suryaprabha19*

Link: https://www.kaggle.com/datasets/suryaprabha19/clothing-sales-transactions-dataset

Granularity: One row per transaction (sale of a single clothing item).

Key fields used:

* saleID, saleDate
* productID, productName, productCategory
* quantity, unitPrice, costPrice, totalAmount, totalCost
* customerID, customerName, location
* salespersonID, salespersonName
* salesChannel (in-store, online, mobile_app, third-party)
* status (Paid, Returned, etc.)

Derived fields (in clothing_sales_clean.csv and Analysis.ipynb):

* revenue = totalAmount
* cost = totalCost
* profit = revenue - cost
* margin_pct = profit / revenue
* year, month, year_month (from saleDate)

---

## 3. Analysis Overview

All analysis logic lives in Analysis.ipynb and uses a Python + SQL hybrid workflow:

### 3.1 Data Load & Preparation

* Load raw CSV from dataset/
* Clean and transform to create clothing_sales_clean.csv
* Build a local SQLite database (clothing_sales.db) with a sales table
* Use SQL for aggregation and Python for modeling / visualization

### 3.2 Core Analytics

Category & SKU Performance

* Category revenue, units, profit, and average margin
* Top / bottom SKUs by revenue and profit
* Profit vs. units scatter to identify “hero” SKUs and long-tail items

Margin Contribution (Pareto Analysis)

* Aggregate profit by SKU using SQL
* Compute cumulative profit and SKU share
* Identify top ~20% SKUs driving the majority of profit
* Break down profit contribution of these SKUs by category
* Visuals:
  * Profit contribution curve (cumulative profit vs. % of SKUs)
  * Bar charts of top SKUs and category contributions

RFM Analysis (Recency, Frequency, Monetary)

* Build customer-level RFM table:
  * recency_days, frequency, monetary
* Score R, F, M into quartiles and create an RFM_score
* Segment customers into:
  * *Champions* ,  *Loyal* ,  *Potential / Regular* , *At Risk*
* Summarize segment size and average spend per segment
* Visuals:
  * Segment counts
  * Average monetary value per segment
  * Frequency vs. monetary scatter coloured by segment

Markdown Efficiency (Simulated)

* Compute base margin per category from paid transactions
* Simulate 10%, 20%, 30% markdowns:
  * Assume quantity and cost remain constant
* Recalculate revenue, profit, and margin after discount
* Compare base vs. 20% markdown by category
* Visuals:
  * Base vs. 20% margin bar chart by category
  * 2×2 subplot of margin-vs-discount curves for top categories

---

## 4. Tableau Dashboards

The Tableau workbook Dashboards.twb is built on top of clothing_sales_clean.csv and contains four main dashboard views:

1. Executive Overview
   * KPI cards (revenue, profit, margin, units)
   * Category revenue and profit bars
   * Category margin scatter
2. Category Deep Dive
   * Units treemap
   * Revenue vs. profit by category
   * Category margin heatmap over time
3. Product & SKU Analysis
   * Top and bottom SKUs by revenue
   * Profit vs. units scatter
   * SKU count by category
4. Trends & Seasonality
   * Monthly revenue, units, and profit trends
   * Channel split (in-store, online, mobile app, third-party)

For quick viewing without Tableau, Dashboards_Images.pdf contains exported dashboard screenshots.

---

## 5. How to Run the Project

### 5.1 Requirements

* Python 3.9+
* Common Python libraries:
  * pandas
  * numpy
  * sqlite3 (standard library)
  * matplotlib
  * mlxtend (for basket / association analysis, if used)
* Tableau Desktop (for Dashboards.twb)

### 5.2 Steps

1. Open the notebook

```
jupyter notebook Analysis.ipynb
```

2. Run all cells
   This will load the cleaned dataset then (re)build clothing_sales.db if needed. Execute all SQL + Python analyses which will generate the same plots as the report
3. Open Tableau dashboards

- Open Dashboards.twb in Tableau Desktop.
- Ensure the data source points to clothing_sales_clean.csv in the project root.
- Refresh extracts if necessary.

---



## 6. Included Deliverables

This project includes three key deliverables:

1. Technical Analysis ( Analysis.ipynb: SQL + Python code)
2. Visual Dashboards ( Dashboards.twb + PDF export)
3. Final Written Report ( Product_Categories_and_Trends_Analysis_Report.pdf )

* 14 page structured document
* References visualizations generated from the notebook
* Business context
* Dataset overview
* Executive dashboard insights
* Category performance findings
* SKU & margin insights
* RFM customer segmentation
* Markdown efficiency recommendations
* Final recommendations

---

## 7. Contact

* Author: Taksh Girdhar - UBC Data Science BSc
* Email: takshgirdhar@gmail.com
* [LinkedIn](https://www.linkedin.com/in/taksh-girdhar-0a7552260/)
