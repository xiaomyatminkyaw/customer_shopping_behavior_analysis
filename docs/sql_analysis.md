# SQL analysis

Query file: `sql/customer_behaviour_analysis_v2.sql` (PostgreSQL). Table: `customer` (3,900 rows). The v2 file fixes issues found during validation (integer division in Q6, overlapping segment bounds in Q7, ties in Q3 and Q8).

## SQL techniques used

| Technique | Queries |
|---|---|
| `GROUP BY` with `SUM`, `AVG`, `COUNT` | Q1, Q4, Q5, Q9, Q10 |
| Subquery in `WHERE` | Q2 |
| `CASE WHEN` for conditional counts and segmentation | Q6, Q7 |
| CTEs (`WITH`) | Q7, Q8 |
| Window functions (`DENSE_RANK`, `SUM() OVER`) | Q8, Q7, Q9, Q10 |
| Casting and rounding (`::numeric`, `ROUND`) | Q3, Q4–Q6 |

## Queries, results and business meaning

| # | Business question | Result | Business meaning |
|---|---|---|---|
| Q1 | Revenue by gender | Male $157,890 · Female $75,191 | Men are 68% of customers and 67.7% of revenue. Spend per customer is nearly equal ($59.54 vs $60.25), so the gap is a customer-count gap. |
| Q2 | Discount users who spend at least the average | 839 customers (average = $59.76) | About half (839 of 1,677) of discount users still spend at or above average. |
| Q3 | Top 5 products by average rating | Gloves 3.86 · Sandals 3.84 · Boots 3.82 · Hat 3.80 · 3.78 tie (Handbag, Skirt, T-shirt) | Ratings differ by only 0.24 across 25 products; treat rankings as light signals. |
| Q4 | Average spend by shipping type | 2-Day $60.73 · Express $60.48 · Free $60.41 · Store Pickup $59.89 · Next Day $58.63 · Standard $58.46 | Shipping has little effect on spend (range $2.27). |
| Q5 | Do subscribers spend more? | Yes: 1,053 customers, $59.49 avg, $62,645 · No: 2,847, $59.87, $170,436 | No. Subscribers are 27% of customers and 26.9% of revenue. |
| Q6 | Products with the highest discount rate | Hat 50.00% · Sneakers 49.66% · Coat 49.07% · Sweater 48.17% · Pants 47.37% | Discounting is spread widely, not concentrated in a few items (overall 43.0%). |
| Q7 | Customer segments | Loyal 3,116 · Returning 701 · New 83 | 79.9% of customers are "Loyal" (11+ previous purchases). |
| Q8 | Top 3 products per category | Accessories: Jewelry 171, Belt 161, Sunglasses 161 · Clothing: Blouse 171, Pants 171, Shirt 169 · Footwear: Sandals 160, Shoes 150, Sneakers 145 · Outerwear: Jacket 163, Coat 161 | Order counts are very close inside each category. Outerwear has only two items. |
| Q9 | Are repeat buyers (>5 prior purchases) more likely to subscribe? | 958 of 3,476 repeat buyers subscribe (27.6%) vs 27.0% overall | Almost no lift on this cut-off. By segment, subscription rises from 18.1% (New) to 27.9% (Loyal). |
| Q10 | Revenue by age group | Young Adult $62,143 (26.7%) · Middle_aged $59,197 (25.4%) · Adult $55,978 (24.0%) · Senior $55,763 (23.9%) | Age groups contribute almost equally. |

## Additional analyses covered in the dashboard and docs (not in the 10 queries)

The brief also asks for payment preferences and seasonal patterns. Equivalent SQL, to add to the file if you want it fully SQL-backed:

```sql
-- Payment preferences
SELECT payment_method, COUNT(*) AS customers, SUM(purchase_amount) AS revenue,
       ROUND(AVG(purchase_amount), 2) AS avg_spend
FROM customer GROUP BY payment_method ORDER BY customers DESC;

-- Seasonal patterns
SELECT season, COUNT(*) AS customers, SUM(purchase_amount) AS revenue,
       ROUND(AVG(purchase_amount), 2) AS avg_spend
FROM customer GROUP BY season ORDER BY revenue DESC;
```

Expected: PayPal 677, Credit Card 671, Cash 670, Debit Card 636, Venmo 634, Bank Transfer 612 customers. Fall $60,018 ($61.56 avg), Spring $58,679, Winter $58,607, Summer $55,777 ($58.41).

## Gaps against the project brief

- **Online vs offline:** not possible; no channel column.
- **Simulated transactions and a structured schema:** the data is one flat table. A suggested next step is a star schema (`dim_customer`, `dim_product`, `fact_purchase`) with a generated purchase date, which would also enable time trends.
