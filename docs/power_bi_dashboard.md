# Power BI Dashboard

<p align="center">
  <strong>RETAIL PERFORMANCE · CUSTOMER LOYALTY · PURCHASING INSIGHTS</strong><br />
  <sub>Power BI Desktop · PostgreSQL · 1920 × 1080 canvas</sub>
</p>

---

## 01 — Dashboard at a Glance

The dashboard transforms customer shopping data into three connected views, helping users explore revenue, customer segments, product performance, and purchasing preferences.

|   3,900   |    $233,081   |     $59.76    |   3.75 / 5  |
| :-------: | :-----------: | :-----------: | :---------: |
| Customers | Total Revenue | Avg. Purchase | Avg. Rating |

**Data source:** PostgreSQL table `customer`

**Report file:** [`Customer_behavior_dashboard.pbix`](../dashboard/Customer_behavior_dashboard.pbix)

## 02 — Explore the Three Pages

### 01 · Overview

<p align="center">
  <img src="../image/overview.png" alt="Power BI customer behavior overview" width="100%" />
</p>

**Business question:** Who buys, how much do they spend, and which categories contribute most?

* Headline KPIs for customers, revenue, average purchase, and rating.
* Customer distribution and revenue by product category.
* Age-group comparisons.
* Subscription status overview.

**Design decision:** Use cards for headline metrics and bar or column charts for comparisons between categories and age groups.

### 02 · Customer Loyalty & Subscriptions

<p align="center">
  <img src="../image/loyalty.png" alt="Power BI customer loyalty and subscription analysis" width="100%" />
</p>

**Business question:** How are customers distributed across loyalty segments, and how do subscriptions and discounts relate to purchase history?

* Customer segmentation: New, Returning, and Loyal.
* Subscriber distribution.
* Discount usage by segment.
* Purchase frequency.

**Design decision:** Use a correctly aggregated customer count for segment comparisons. Avoid averaging purchase-frequency days when the goal is to show how many customers belong to each frequency group.

### 03 · Products & Purchasing

<p align="center">
  <img src="../image/purchasing.png" alt="Power BI product ratings and purchasing analysis" width="100%" />
</p>

**Business question:** Which products, categories, seasons, and payment methods stand out?

* Top-rated products.
* Revenue by category.
* Seasonal revenue distribution.
* Payment method preferences.
* Discounted versus non-discounted purchases.

**Design decision:** Use ranked bars for product ratings and a bar chart—not a pie chart—to compare average purchase amounts between discount groups.

## 03 — KPI Definitions

| KPI                 | Calculation                     | Expected result |
| ------------------- | ------------------------------- | --------------: |
| Number of customers | Distinct count of `customer_id` |           3,900 |
| Total revenue       | Sum of `purchase_amount`        |        $233,081 |
| Average purchase    | Revenue ÷ customers             |          $59.76 |
| Average rating      | Average of `review_rating`      |            3.75 |
| Loyal customers     | `previous_purchases` ≥ 11       |           3,116 |
| Discount users      | `discount_applied` = Yes        |           1,677 |

### Customer segmentation

| Segment   | Previous purchases | Customers |
| --------- | -----------------: | --------: |
| New       |                  1 |        83 |
| Returning |               2–10 |       701 |
| Loyal     |                11+ |     3,116 |

**Validation note:** Confirm the actual DAX measures and field aggregations in Power BI Model view. In particular, customer segments and subscriber counts must use appropriate counts, not the minimum of `customer_id`.

## 04 — Filters & Interactions

Slicers allow users to explore how purchasing patterns differ across customer groups.

| Page                             | Recommended slicers                                  |
| -------------------------------- | ---------------------------------------------------- |
| Overview                         | Gender, Subscription Status, Category, Shipping Type |
| Customer Loyalty & Subscriptions | Gender, Subscription Status, Age Group, Location     |
| Products & Purchasing            | Gender, Category, Season, Location, Shipping Type    |

### Important data behavior

The dataset contains no female discount users or subscribers. Selecting **Female** should therefore show 1,248 customers, $75,191 revenue, and zero subscribers or discount users. Selecting **Subscription Status = Yes** should show 1,053 subscribers, all male.

These patterns should be interpreted as potential data-quality issues, not general conclusions about real-world customers.

---

<p align="center">
  <strong>From analytical queries to interactive business intelligence.</strong><br />
  <sub>A three-page dashboard designed to make customer behavior easier to explore and interpret.</sub>
</p>
