# Customer Shopping Behavior Analysis

An end-to-end analytics project that turns 3,900 retail purchases into insights on spending, loyalty and subscriptions. The data is cleaned in **Python**, analyzed in **MySQL** and presented in an interactive **Power BI** dashboard.

![Project workflow](docs/architecture.png)

## Business Question

How can a retail company use consumer shopping data to identify trends, improve customer engagement and optimize its marketing and product strategies?

## Tools

- **Python** (Pandas, SQLAlchemy, PyMySQL) for cleaning and feature engineering
- **MySQL** for structured analysis
- **Power BI** for the interactive dashboard

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

## Data Preparation

- Filled 37 missing review ratings with the median rating of each product category
- Standardized column names to snake case
- Created `age_group` (quartile-based) and `purchase_frequency_days`
- Dropped `promo_code_used`, which was identical to `discount_applied`
- Loaded the cleaned data into MySQL

## How to Run

```bash
pip install pandas sqlalchemy pymysql
python scripts/customer_behavior_prep.py --csv data/customer_shopping_behavior.csv --skip-db   # clean and save a CSV
python scripts/customer_behavior_prep.py --csv data/customer_shopping_behavior.csv             # clean and load into MySQL
```

The MySQL password is requested at the prompt and is never stored in the code.

## Key Findings

| Question | Result |
| --- | --- |
| Revenue, male vs. female | $157,890 vs. $75,191 |
| Average spend, subscribers vs. non-subscribers | $59.49 vs. $59.87 |
| Average purchase, Express vs. Standard shipping | $60.48 vs. $58.46 |
| Customer segments | 3,116 Loyal, 701 Returning, 83 New |
| Top revenue age group | Young Adults ($62,143) |
| Repeat buyers who subscribe | 958 of 3,476 (about 28%) |

## Dashboard

The dashboard is fully interactive: use the slicers on the left or click any chart to filter the whole report.

![Customer Behavior Dashboard](docs/dashboard.png)

## Report

See [reports/Customer_Shopping_Behavior_Report.pdf](reports/Customer_Shopping_Behavior_Report.pdf) for the full summary and recommendations.
