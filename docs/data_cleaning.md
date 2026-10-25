# Data Cleaning & Preparation

<p align="center">
  <strong>FROM RAW DATA TO ANALYSIS-READY DATA</strong><br />
  <sub>Python · pandas · PostgreSQL</sub>
</p>

---

## 01 — Dataset at a Glance

| Dataset attribute    | Details                          |
| -------------------- | -------------------------------- |
| Source file          | `customer_shopping_behavior.csv` |
| Original size        | 3,900 rows × 18 columns          |
| Data grain           | One row per customer             |
| Unique identifier    | `Customer ID`                    |
| Missing values       | 37 review ratings (0.9%)         |
| Duplicate rows / IDs | 0 / 0                            |

**Source:** The original dataset source and URL still need to be verified and documented.

### What the data covers

Customer demographics, purchased items, product categories, purchase amounts, locations, ratings, discounts, subscriptions, shipping, payment methods, purchase history, and purchase frequency.

| Data group       | Key fields                                 |
| ---------------- | ------------------------------------------ |
| Customer profile | Age, Gender, Location                      |
| Product & sales  | Item Purchased, Category, Purchase Amount  |
| Experience       | Review Rating, Shipping Type, Size, Color  |
| Engagement       | Subscription Status, Discount Applied      |
| Purchase history | Previous Purchases, Frequency of Purchases |

## 02 — Data Quality Assessment

The initial inspection identified one missing-value issue. Other validation checks found no duplicate records, duplicate customer IDs, unwanted text whitespace, or inconsistent category labels.

<details>
<summary><strong>Validation results</strong></summary>

| Check                  | Result                                 |
| ---------------------- | -------------------------------------- |
| Missing values         | 37 in `Review Rating`                  |
| Duplicate records      | None                                   |
| Duplicate customer IDs | None                                   |
| Text whitespace        | No issues found                        |
| Category consistency   | No inconsistent labels found           |
| Data types             | Numeric fields already correctly typed |

</details>

## 03 — Cleaning & Transformation Pipeline

<ol>
  <li>

**Handle missing review ratings**

Filled the 37 missing values using the median rating within each product category, preserving category-specific rating patterns.

  </li>
  <li>

**Standardize column names**

Converted column names to lowercase, snake_case, and SQL-friendly names. Renamed `purchase_amount_(usd)` to `purchase_amount`.

  </li>
  <li>

**Create age groups**

Used `pandas.qcut()` to divide customers into four age groups for demographic comparisons.

| Age group   | Age range |
| ----------- | --------: |
| Young Adult |     18–31 |
| Adult       |     32–44 |
| Middle_aged |     45–57 |
| Senior      |     58–70 |

  </li>
  <li>

**Convert purchase frequency to numeric intervals**

Created `purchase_frequency_days` from the original frequency labels.

| Frequency label            | Assigned days |
| -------------------------- | ------------: |
| Weekly                     |             7 |
| Bi-Weekly / Fortnightly    |            14 |
| Monthly                    |            30 |
| Quarterly / Every 3 Months |            90 |
| Annually                   |           365 |

  </li>
  <li>

**Remove redundant information**

Dropped `promo_code_used` because it was identical to `discount_applied` across all 3,900 rows.

  </li>
  <li>

**Load into PostgreSQL**

Loaded the prepared dataset into the `customer` table for SQL analysis and Power BI reporting.

  </li>
</ol>

## 04 — Final Dataset

<box border radius="lg" padding={4} gap={3}>
  <grid columns={2} gap={3}>
    <grid-item>
      <text color="secondary" size="sm">Records</text>
      <title size="xl">3,900</title>
    </grid-item>
    <grid-item>
      <text color="secondary" size="sm">Final columns</text>
      <title size="xl">18</title>
    </grid-item>
    <grid-item>
      <text color="secondary" size="sm">New features</text>
      <title size="xl">2</title>
    </grid-item>
    <grid-item>
      <text color="secondary" size="sm">Removed columns</text>
      <title size="xl">1</title>
    </grid-item>
  </grid>
  <divider color="subtle"/>
  <text color="secondary" size="sm">Final table: `customer` · PostgreSQL</text>
</box>

The final dataset retains 18 columns: 17 original columns after removing the redundant promo-code field, plus `age_group` and `purchase_frequency_days`.

## 05 — Limitations & Data Quality Considerations

* **Imputed ratings:** 37 review ratings are estimated rather than observed.
* **Frequency assumptions:** Bi-Weekly and Fortnightly are both mapped to 14 days; Quarterly and Every 3 Months are mapped to 90 days. These interpretations should be confirmed against the source definitions.
* **Age groups:** The age bands are sample-specific quartile groups, not universal demographic categories.
* **Potential source-data anomaly:** All discount users and subscribers are male, and every subscriber used a discount. This pattern requires source validation.
* **Limited analytical scope:** No transaction dates or sales-channel field are available, preventing time-series, retention, and online-versus-offline analysis.

### Reproducibility & Security

Notebook: [`Customer_Shopping_Behavior_Analysis.ipynb`](../notebooks/Customer_Shopping_Behavior_Analysis.ipynb)

Before publishing, remove hard-coded database credentials, clear sensitive notebook outputs, and document the duplicate checks directly in the notebook.

---

<p align="center">
  <strong>Prepared data. Reliable queries. Clearer business insights.</strong>
</p>
