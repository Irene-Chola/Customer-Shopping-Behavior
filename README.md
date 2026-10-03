# Customer Shopping Behavior Analysis
#### An end-to-end analytics project that turns 3,900 retail purchases into clear insights on spending, loyalty and subscriptions, using Python, MySQL and Power BI

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)](https://powerbi.microsoft.com/)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Assets](#project-assets)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Repository Structure](#repository-structure)
- [Dataset](#dataset)
- [Data Pipeline Execution](#data-pipeline-execution)
- [Dashboard Navigation](#dashboard-navigation)
- [Key Insights](#key-insights)
- [Results & Recommendations](#results--recommendations)
- [Future Enhancements](#future-enhancements)
- [Acknowledgments](#acknowledgments)

---

## Project Overview

This project delivers a customer shopping behavior analysis for a retail company that wants to improve sales, customer satisfaction and long-term loyalty. Management has noticed shifting purchase patterns across demographics, product categories and shipping options, and wants to know which factors drive customer decisions.

The analysis answers one overarching business question:

> How can the company use consumer shopping data to identify trends, improve customer engagement, and optimize its marketing and product strategies?

The data is cleaned and prepared in Python, analyzed with ten SQL queries in MySQL, and presented in an interactive Power BI dashboard, so that marketing, product and customer-experience teams can explore the results themselves.

---

## Project Assets
1. Python Notebook (data cleaning and preparation)
2. Python Script (the same steps as a runnable script)
3. MySQL Database and SQL Queries
4. Power BI Dashboard
5. Summary Report (PDF)

### Prerequisites
- Python 3.9+ with `pandas`, `sqlalchemy` and `pymysql`
- MySQL Server and MySQL Workbench
- Power BI Desktop
- Jupyter Notebook (optional, to run the notebook)

---

### Key Features

- **End-to-End Workflow**: Takes raw data through cleaning in Python, analysis in SQL and visualization in Power BI
- **Reproducible Data Preparation**: A documented notebook and an equivalent script, with the database password requested at a prompt and never stored in code
- **Ten Business Questions Answered**: SQL queries covering revenue, discounts, ratings, shipping, subscriptions, customer segments and age groups
- **Interactive Dashboard**: Slicers and click-to-filter charts let anyone explore the data without writing a query

---
## Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Data Source   │     │   Preparation   │     │    Analysis     │     │  Visualization  │
│                 │     │                 │     │                 │     │                 │
│ • Customer CSV  │───▶ │ Python (Pandas) │───▶ │ MySQL Database  │───▶ │     Power BI    │
│ • 3,900 rows    │     │ Clean & Engineer│     │ 10 SQL Queries  │     │    Dashboard    │
│ • 18 columns    │     │    Features     │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘     └─────────────────┘
```

![Project Workflow](docs/architecture.png)

---

## Repository Structure

```
customer-shopping-behavior-analysis/
├── data/          Raw dataset goes here (not included)
├── notebooks/     Documented Jupyter notebook for data preparation
├── scripts/       customer_behavior_prep.py, the same steps as a runnable script
├── sql/           Queries answering the ten business questions
├── docs/          Architecture diagram and dashboard screenshot
└── reports/       Summary report (PDF)
```

---

## Dataset

The dataset contains **3,900 purchases** and **18 columns**, grouped into three kinds of information.
<!-- Add a link to the dataset source here -->

| Feature Group | Columns |
|---------------|---------|
| **Customer Demographics** | `customer_id`, `age`, `gender`, `location`, `subscription_status` |
| **Purchase Details** | `item_purchased`, `category`, `purchase_amount`, `size`, `color`, `season` |
| **Shopping Behavior** | `discount_applied`, `promo_code_used`, `previous_purchases`, `payment_method`, `frequency_of_purchases`, `review_rating`, `shipping_type` |

#### 1. **Missing Values**
- **Issue**: 37 missing values in `review_rating` (3,863 of 3,900 present)
- **Fix**: Each gap is filled with the median rating of its own product category, not the overall median
- **Implementation**: [Data Preparation Notebook](notebooks/customer_shopping_behavior_cleaning.ipynb)

#### 2. **Standardized Column Names**
- **Issue**: Mixed upper and lower case, spaces and brackets make Python and SQL work error-prone
- **Fix**: Every name is converted to lower snake case, and `purchase_amount_(usd)` becomes `purchase_amount`
- **Implementation**: [Data Preparation Script](scripts/customer_behavior_prep.py)

#### 3. **Engineered Features**
- **`age_group`**: Ages split into four quartile-based groups (Young Adults, Adults, Middle-aged, Seniors), so each group holds roughly a quarter of the customers
- **`purchase_frequency_days`**: The text purchase frequency converted into a number of days

#### 4. **Duplicate Column Removed**
- **Check**: `discount_applied` and `promo_code_used` matched on every row
- **Fix**: `promo_code_used` was dropped, leaving 3,900 rows and 19 columns with no missing values

---

## Data Pipeline Execution
1. **Set Up the Environment**:
   - Install the libraries: `pip install pandas sqlalchemy pymysql`
   - Create a MySQL database named `customer_behavior`
   - Place the raw `customer_shopping_behavior.csv` file in the `data/` folder

2. **Data Preparation**:
   - Open the [notebook](notebooks/customer_shopping_behavior_cleaning.ipynb) to follow each step, or run the script:
   ```bash
   python scripts/customer_behavior_prep.py --csv data/customer_shopping_behavior.csv --skip-db
   ```
   - Review the cleaned file the script saves

3. **Load Into MySQL**:
   - Run the script without `--skip-db`. It asks for your MySQL password at the prompt:
   ```bash
   python scripts/customer_behavior_prep.py --csv data/customer_shopping_behavior.csv
   ```
   - The cleaned data is written to the `customer_shopping_behavior` table (3,900 rows)

4. **SQL Analysis**:
   - Open [analysis_queries.sql](sql/analysis_queries.sql) in MySQL Workbench
   - Run each query to answer the ten business questions

5. **Dashboard Deployment**:
   - Connect Power BI Desktop to your MySQL database
   - Load the `customer_shopping_behavior` table
   - Build the KPI cards and charts, and add slicers for subscription status, gender, category and shipping type

---

## Dashboard Navigation
- **KPI Cards**: Average purchase amount, average review rating and number of customers
- **Subscription Analysis**: Share of customers who are subscribed
- **Category Analysis**: Revenue and sales by product category
- **Age Group Analysis**: Revenue and sales by age group
- **Slicers**: Filter by subscription status, gender, category and shipping type, or click any chart to highlight that segment across the whole dashboard

### Dashboard Screenshots

![Customer Behavior Dashboard](docs/dashboard.png)

*Interactive dashboard showing spending, subscription, category and age group insights*

---

## Key Insights

### Customer Analysis Results
- **Total Revenue**: $233,081 across 3,900 purchases
- **Average Purchase Amount**: $59.76
- **Average Review Rating**: 3.75
- **Customer Segments**: 3,116 Loyal, 701 Returning and 83 New customers

### Top Performing Insights
1. **Gloves**: The highest average review rating at 3.86, followed by Sandals (3.84) and Boots (3.82)
2. **Clothing and Accessories**: The leading categories by both revenue and sales
3. **Young Adults**: The top revenue age group at $62,143, with the other three groups close behind

---

## Results & Recommendations

### Key Findings
1. **Revenue by Gender**: Male customers generated $157,890 compared with $75,191 from female customers
2. **Subscriptions**: Subscribers spend about the same per purchase as non-subscribers ($59.49 vs. $59.87), but only 1,053 of 3,900 customers (27%) are subscribed
3. **Shipping**: Express shipping averages $60.48 per purchase compared with $58.46 for Standard
4. **Repeat Buyers**: 958 of 3,476 repeat buyers (about 28%) subscribe, close to the overall rate
5. **Discounts**: Hats have the highest share of discounted purchases at 50%, followed closely by Sneakers (49.66%)

### Strategic Recommendations
1. **Boost Subscriptions**: Promote exclusive subscriber benefits to convert the 73% of customers who are not yet subscribed
2. **Customer Loyalty Programs**: Reward repeat buyers to help move them into the Loyal segment
3. **Review Discount Policy**: Balance the sales boost from discounts with healthy margin control
4. **Product Positioning**: Feature top-rated products prominently in marketing campaigns
5. **Targeted Marketing**: Focus on high-revenue age groups and express-shipping customers
6. **Gender-Focused Strategy**: Target male buyers, who bring in more revenue, or offer rewards and discounts to engage more female customers

### Current Limitations
- **No Purchase Dates**: The data records the season but not the date, so long-term trends over time cannot be analyzed
- **Imputed Ratings**: The 37 missing review ratings were filled using category medians, not collected values
- **Quartile-Based Age Groups**: Age groups reflect the spread of this dataset rather than fixed age ranges
- **Descriptive Results**: The findings describe patterns in the data and do not prove cause and effect

---

## Future Enhancements

### Phase 2 - Customer Segmentation and Prediction
- Segment customers with RFM analysis or clustering
- Predict which customers are likely to subscribe
- Publish the dashboard to the Power BI Service and schedule data refreshes

---

## Acknowledgments

- **Pandas, SQLAlchemy and PyMySQL** for reliable data preparation and database loading
- **MySQL** for a dependable analysis database
- **Power BI Community** for visualization best practices

---

**⭐ If you found this project helpful, please consider giving it a star!**

---

*Built with ❤️ by [Irene Chola](https://github.com/Irene-Chola)*
