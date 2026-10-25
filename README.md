# Customer Shopping Behavior Analysis

End-to-end retail analytics project: **Python** (cleaning) → **PostgreSQL** (business queries) → **Power BI** (3-page dashboard) → written insights and recommendations.

![Dashboard overview](screenshots/01_overview.png)

## 1. Project summary and business problem

A retail company wants to understand how its customers shop, in order to improve sales, customer satisfaction and loyalty. Management has seen shifting purchase patterns across demographics, product categories and seasons, and wants to know how discounts, reviews, payment preferences and purchase frequency relate to buying decisions.

**Overarching question:** *How can the company use shopping data to identify trends, improve customer engagement, and optimise marketing and product strategy?*

Full background: [docs/project_overview.md](docs/project_overview.md).

## 2. Tools used

| Stage | Tool | Used for |
|---|---|---|
| Data preparation | Python (pandas, SQLAlchemy, psycopg2) | Inspection, missing values, feature creation, loading to database |
| Analysis | PostgreSQL | 10 business queries (aggregation, CASE, CTE, window functions) |
| Visualisation | Power BI Desktop | 3-page interactive dashboard |

## 3. Business questions and workflow

```
customer_shopping_behavior.csv (3,900 rows, 18 columns)
        │  Python: clean, enrich            → docs/data_cleaning.md
        ▼
PostgreSQL table "customer"
        │  10 SQL business queries          → docs/sql_analysis.md
        ▼
Power BI dashboard (3 pages)                → docs/power_bi_dashboard.md
        ▼
Insights and recommendations                → docs/business_insights.md
```

Questions answered: who generates revenue; how loyal customers are; whether subscribers spend more; whether discounts raise spend; which products rate highest; and how category, season, shipping and payment method differ.

## 4. Key findings (verified against the data)

3,900 customers · **$233,081** revenue · **$59.76** average purchase · **3.75** average rating.

1. **Revenue follows customer count, not spend per head.** Men generate $157,890 (67.7%) because they are 68% of customers. Average spend is almost equal: $59.54 (men) vs $60.25 (women).
2. **Discounts and subscriptions exist only among male customers.** No woman in the data used a discount or subscribed. 63.2% of men used a discount and 39.7% subscribe. Every one of the 1,053 subscribers also used a discount.
3. **Discounts do not lift spend.** Among men, discount users average $59.28 vs $59.98 without. Subscribers average $59.49 vs $59.57 for non-subscribing men.
4. **Customers are mostly loyal.** 3,116 (79.9%) have 11+ previous purchases; 701 (18.0%) have 2–10; 83 (2.1%) have 1.
5. **Subscription rises modestly with loyalty:** 18.1% (New), 24.1% (Returning), 27.9% (Loyal). The New group is small (83 customers).
6. **Clothing is the revenue engine:** $104,264 (44.7%), then Accessories $74,200, Footwear $36,093, Outerwear $18,524.
7. **Ratings are tightly bunched** (3.62–3.86). Top: Gloves 3.86, Sandals 3.84, Boots 3.82, Hat 3.80. Lowest: Shirt 3.62, Jeans 3.65.
8. **Seasonality is mild.** Fall leads on revenue ($60,018) and average order ($61.56); Summer is lowest ($55,777, $58.41).
9. **Age, shipping, payment and frequency show little variation.** Age-group revenue ranges 23.9%–26.7%; shipping averages $58.46–$60.73.

Details, caveats and recommendations: [docs/business_insights.md](docs/business_insights.md).

## 5. Dashboard screenshots and links

| Page | Screenshot | Notes |
|---|---|---|
| Overview | ![](screenshots/01_overview.png) | KPIs, category and age views |
| Customer Loyalty & Subscriptions | ![](screenshots/02_loyalty.png) | Segments, subscriptions, discounts |
| Products & Purchasing | ![](screenshots/03_products.png) | Ratings, seasons, payments |

- Dashboard file: [`dashboard/Customer_behavior_dashboard.pbix`](dashboard/Customer_behavior_dashboard.pbix)
- Page-by-page guide: [docs/power_bi_dashboard.md](docs/power_bi_dashboard.md)
- Live link (optional): `<add Power BI publish-to-web or Fabric link here>`

## 6. How to explore or reproduce

1. Clone the repo and install: `pip install pandas sqlalchemy psycopg2-binary jupyter`.
2. Create a PostgreSQL database `customer_behavior`; set credentials as environment variables (never hard-code them).
3. Run `notebooks/Customer_Shopping_Behavior_Analysis.ipynb` to clean the data and create the `customer` table.
4. Run `sql/customer_behaviour_analysis_v2.sql`; compare with the "Expected" comments.
5. Open the `.pbix` in Power BI Desktop, repoint the source to your `customer` table, and refresh.

## 7. Repository structure

```
├── README.md
├── docs/  project_overview.md · data_cleaning.md · sql_analysis.md
│          business_insights.md · power_bi_dashboard.md
├── data/  customer_shopping_behavior.csv
├── notebooks/  Customer_Shopping_Behavior_Analysis.ipynb
├── sql/   customer_behaviour_analysis_v2.sql
├── dashboard/  Customer_behavior_dashboard.pbix
└── screenshots/
```

## 8. Limitations (short version)

One row per customer (no time dimension); no online/offline channel field; group differences are small and untested for significance; the gender pattern in discounts and subscriptions looks like a data artifact and should be checked at source. See each doc for detail.

**Author:** Myat Min Kyaw · MIS, INTI International University
