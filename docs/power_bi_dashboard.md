# Power BI dashboard

File: `dashboard/Customer_behavior_dashboard.pbix` · Canvas 1920×1080 · Source: PostgreSQL table `customer`.

Reading the file showed three pages. Items marked **to verify** or **to fix** were found during validation and are tracked in the validation checklist.

## Purpose of each page

| Page | Purpose | Main question |
|---|---|---|
| 1. Overview ("Customer Behavior") | High-level customers, revenue and spend by category and age group; subscription split | Who buys, how much, and what? |
| 2. Customer Loyalty & Subscriptions | Segments, subscription, discount use by segment, purchase frequency | How loyal are customers and what do subscription and discounts do? |
| 3. Products & Purchasing | Top-rated products, category revenue, seasonality, payment methods, discount effect | Which products, seasons and payment methods matter? |

Suggested page names: **Overview**, **Customer Loyalty & Subscriptions**, **Products & Purchasing**.

## KPI names and calculation definitions

| KPI | Definition | Expected (no filters) |
|---|---|---|
| Number of customers | Distinct count of `customer_id` | 3,900 |
| Total revenue (add this card) | Sum of `purchase_amount` | $233,081 |
| Average purchase amount | Total revenue ÷ customers | $59.76 |
| Average review rating | Average `review_rating` (after imputation) | 3.75 |
| Loyal customers (page 2) | Customers with `previous_purchases` ≥ 11 | 3,116 |
| Discount users (page 3) | Count of rows with `discount_applied` = Yes | 1,677 |
| Customer Segment (column) | New = 1; Returning = 2–10; Loyal = 11+ | 83 / 701 / 3,116 |

DAX measures were not readable from the file; confirm these definitions in Model view.

## Visuals and why they were selected

| Page | Visual | Why |
|---|---|---|
| 1 | Donut: % of customers by subscription status | Two-part share of whole |
| 1 | Column: customers by category (rename from "Sales by Category") | Compares category volume |
| 1 | Column: revenue by category | Ranks categories by money |
| 1 | Bar: customers by age group (rename from "Sales by Age Group") | Compares group size |
| 1 | Bar: revenue by age group | Shows revenue contribution |
| 2 | Donut: customer segmentation | Share of three segments. **To fix:** uses Minimum of `customer_id`; change to distinct count. |
| 2 | Bar: subscription status | Subscriber counts. **To fix:** same aggregation issue. |
| 2 | Column: discount usage by segment | Whether discount use differs by loyalty |
| 2 | Column: purchase frequency | **To fix:** currently averages days per label; change to customer count by frequency. |
| 3 | Bar: top 5 highest-rated products | Ranked comparison (Top N filter on average rating; ties at 3.78) |
| 3 | Bar: purchase amount by category | Category revenue |
| 3 | Pie: seasonal purchasing | Four slices, share of revenue |
| 3 | Bar: payment method preferences | Ranked categories |
| 3 | Pie: discount vs purchase amount | **To fix:** a pie of averages misleads; use a bar. |
| All | KPI card strip | Headline metrics at a glance |

Design rules: navy (`#173b5b`) titles, consistent grid, same colour for the same meaning on every page, 12 pt minimum labels.

## Slicers and interactions

| Page | Slicers |
|---|---|
| 1 | Gender · Subscription Status · Category · Shipping Type |
| 2 | Gender · Subscription Status · Age Group · Location |
| 3 | Gender · Category · Season · Location · Shipping Type |

- Slicers work per page. Use **Sync slicers** if Gender or Subscription should carry across pages.
- Expected behaviour worth documenting: selecting **Gender = Female** shows 1,248 customers and $75,191 revenue, and **no** subscribers or discount users (see finding 2 in the insights). A blank chart there is correct, not a bug.
- Selecting **Subscription = Yes** shows 1,053 customers, all male.
- Use Edit interactions to exclude any visual that should not react to a slicer.

## Screenshots and navigation

| Page | Screenshot file |
|---|---|
| Overview | `screenshots/01_overview.png` |
| Customer Loyalty & Subscriptions | `screenshots/02_loyalty.png` |
| Products & Purchasing | `screenshots/03_products.png` |

Take screenshots at 1920×1080 with no slicers selected (File → Export → PDF, or Windows Snipping Tool at 100% zoom). Navigation: the pages appear as tabs at the bottom of the report. Consider adding a button row (Page navigator) in the title band so viewers can move between pages without the tab bar.
