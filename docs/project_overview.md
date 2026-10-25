# Project overview

## Background and business problem

A retail company wants to understand customer shopping behaviour to improve sales performance, customer satisfaction and long-term loyalty. Management has noticed changing purchase patterns across customer demographics, product categories, seasons and sales channels. It also wants to know how discounts, product reviews, payment preferences and purchase frequency influence buying and repeat purchases.

**Overarching question:** How can the company use consumer shopping data to identify trends, improve engagement, and optimise marketing and product strategies?

## Project objectives

1. Prepare an analysis-ready dataset from raw shopping data (Python).
2. Answer defined business questions with SQL (PostgreSQL).
3. Build an interactive dashboard so stakeholders can explore behaviour by demographic, category, season and shipping type (Power BI).
4. Turn results into evidence-based recommendations.
5. Publish everything in a structured GitHub repository.

## Business questions

| # | Question | Where answered |
|---|---|---|
| 1 | Who are the customers and who generates revenue (gender, age)? | SQL Q1, Q10; dashboard p.1 |
| 2 | How loyal are customers, and how often do they buy? | SQL Q7, Q9; dashboard p.2 |
| 3 | Do subscribers spend more? | SQL Q5, Q9; dashboard p.2 |
| 4 | Do discounts change spending? | SQL Q2, Q6; dashboard p.2–3 |
| 5 | Which products and categories perform best? | SQL Q3, Q8; dashboard p.1, 3 |
| 6 | How does shipping type relate to spend? | SQL Q4 |
| 7 | How do seasons and payment methods differ? | Dashboard p.3 |

## Scope

**In scope:** the 3,900-row `customer_shopping_behavior.csv` (one row per customer); cleaning; 10 SQL queries; a 3-page dashboard; written findings and recommendations.

**Not in scope / not supported by the data:**

- **Online vs offline analysis.** The problem statement asks for it, but the dataset has no channel field. `Shipping Type = Store Pickup` (650 customers) is the closest signal and is not a true offline indicator. This analysis does not claim anything about channels.
- **Time trends.** There is no purchase date, only a `Season` field and `Previous Purchases`.
- **Simulated transactions / relational schema.** The data is a single flat table. A star schema and simulated order history are listed as future work, not done here.

## Methodology

1. **Python:** inspect, impute missing ratings, rename columns, derive `age_group` and `purchase_frequency_days`, drop redundant `promo_code_used`, load to PostgreSQL ([data_cleaning.md](data_cleaning.md)).
2. **SQL:** ten queries covering revenue, discount behaviour, ratings, shipping, subscription, segments, ranking and age groups ([sql_analysis.md](sql_analysis.md)).
3. **Power BI:** three pages with KPI cards, slicers and charts ([power_bi_dashboard.md](power_bi_dashboard.md)).
4. **Validation:** SQL results were reproduced independently in pandas and used as reference values for the dashboard.
5. **Insights:** each finding carries evidence, interpretation, recommendation and caveat ([business_insights.md](business_insights.md)).
