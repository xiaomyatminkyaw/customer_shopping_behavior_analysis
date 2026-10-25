# Data cleaning

Notebook: `notebooks/Customer_Shopping_Behavior_Analysis.ipynb`

## Dataset source, size and columns

| Item | Detail |
|---|---|
| File | `customer_shopping_behavior.csv` |
| Source | Add the original source and link here (not stated in the files provided) |
| Rows / columns | 3,900 / 18 |
| Grain | One row per customer (`Customer ID` is unique) |

| Column | Type | Notes |
|---|---|---|
| Customer ID | int | 1–3,900 |
| Age | int | 18–70 |
| Gender | text | Male 2,652, Female 1,248 |
| Item Purchased | text | 25 items |
| Category | text | Clothing, Accessories, Footwear, Outerwear |
| Purchase Amount (USD) | int | $20–$100, mean $59.76 |
| Location | text | 50 US states |
| Size, Color | text | 4 sizes, 25 colours |
| Season | text | Fall, Spring, Summer, Winter |
| Review Rating | float | 2.5–5.0 (37 blanks) |
| Subscription Status | text | Yes / No |
| Shipping Type | text | 6 types |
| Discount Applied, Promo Code Used | text | Yes / No (identical on every row) |
| Previous Purchases | int | 1–50, mean 25 |
| Payment Method | text | 6 methods |
| Frequency of Purchases | text | 7 labels |

## Missing values and duplicates checks

| Check | Result |
|---|---|
| Missing values | Only `Review Rating`: 37 of 3,900 (0.9%) |
| Duplicate rows | 0 |
| Duplicate Customer IDs | 0 |
| Leading/trailing whitespace in text columns | None found |
| Inconsistent category labels | None (4 categories, 4 seasons, 2 genders, 6 shipping types, 6 payment methods) |
| Data types | Numeric fields are numeric; no conversion needed |

## Cleaning and transformation decisions

| Step | Decision | Reason |
|---|---|---|
| 1 | Fill missing `Review Rating` with the **median of the same category** | Median resists skew; category-level is more specific than global. Category medians: Accessories 3.8, Clothing 3.7, Footwear 3.8, Outerwear 3.8. The overall mean is 3.75 before and after. |
| 2 | Rename columns: lower case, underscores, `purchase_amount_(usd)` → `purchase_amount` | SQL-friendly names |
| 3 | Create `age_group` with `qcut(age, 4)`: Young Adult 18–31, Adult 32–44, Middle_aged 45–57, Senior 58–70 | Equal-sized groups for comparison |
| 4 | Create `purchase_frequency_days` from frequency labels (Weekly 7; Fortnightly and Bi-Weekly 14; Monthly 30; Quarterly and Every 3 Months 90; Annually 365) | Numeric version of frequency |
| 5 | Drop `promo_code_used` | Identical to `discount_applied` on all rows |
| 6 | Load to PostgreSQL table `customer` with `to_sql` | Source for SQL and Power BI |

## Final dataset structure and limitations

Final table `customer`: 3,900 rows, 18 columns (17 original minus `promo_code_used`, plus `age_group` and `purchase_frequency_days`).

Limitations and open items:

- **Bi-Weekly vs Fortnightly:** both mapped to 14 days. "Bi-Weekly" can also mean twice a week; confirm the source meaning. The same applies to "Every 3 Months" and "Quarterly" (both 90).
- **Imputed ratings:** 37 values are estimates.
- **Quartile age groups** are sample-specific, not standard bands.
- **Structured fields:** every discount and every subscription belongs to a male customer, and every subscriber used a discount ([business_insights.md](business_insights.md), finding 2). This is unusual and should be checked with the data provider.
- **No dates or channel field** (see [project_overview.md](project_overview.md)).
- **Security:** the notebook contains hard-coded database credentials. Remove them and clear cell outputs before pushing to GitHub.
- **Missing duplicates/inconsistency checks in the notebook:** the checks above were run during validation; add `df.duplicated().sum()` and `df['Customer ID'].is_unique` cells so the notebook documents them.
