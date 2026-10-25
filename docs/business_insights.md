# Business Insights & Recommendations

<p align="center">
  <strong>FROM CUSTOMER DATA TO BUSINESS DECISIONS</strong><br />
  <sub>10 analytical findings · Evidence-based recommendations · Data quality considerations</sub>
</p>

---

## At a glance

|   3,900   |    $233,081   |     $59.76    |   3.75 / 5  |
| :-------: | :-----------: | :-----------: | :---------: |
| Customers | Total Revenue | Avg. Purchase | Avg. Rating |

**The big picture:** Customer revenue is driven mainly by customer distribution and product category. Discounts and subscriptions show unusual patterns that require validation before the business makes decisions.

## 01 — Customer Revenue & Acquisition

**Men generate more revenue, but do not spend more per customer.**

* **Evidence:** Men contribute 67.7% of revenue and represent 68% of customers. Average purchase: $59.54 for men vs. $60.25 for women.
* **Recommendation:** Investigate the gender imbalance and explore customer acquisition opportunities among underrepresented groups.
* **Caution:** Acquisition channels are unavailable, so the reason for the imbalance is unknown.

## 02 — Discounts & Subscriptions

**The strongest signal may be a data quality issue.**

* **Evidence:** No women used discounts or subscribed. Among men, 63.2% used discounts and 39.7% subscribed. Every subscriber also used a discount.
* **Recommendation:** Validate the source data before changing marketing strategy. If the pattern is genuine, test offers with underrepresented customer groups.
* **Caution:** The perfect overlap is unusual and may reflect synthetic data or recording bias.

## 03 — Discount Effectiveness

**Discount users do not have higher average purchases.**

* **Evidence:** Male discount users average $59.28 per purchase vs. $59.98 for non-users.
* **Recommendation:** Test discount holdout groups and compare conversion, incremental revenue, and profit margin before expanding promotions.
* **Caution:** No margin or pre-discount price data is available; the results do not prove discounts are ineffective.

## 04 — Subscription Value

**Subscription status is not associated with meaningfully higher spending or ratings.**

* **Evidence:** Subscribers average $59.49 vs. $59.87 overall for non-subscribers. Average ratings are nearly identical.
* **Recommendation:** Evaluate subscriptions using repeat-purchase rate, retention, and customer lifetime value.
* **Caution:** Without transaction dates, retention and long-term subscription value cannot be measured.

## 05 — Customer Loyalty

**79.9% of customers fall into the Loyal segment.**

* **Evidence:** 3,116 customers have 11+ previous purchases; only 83 are classified as New.
* **Recommendation:** Refine the segments, for example, 1–10, 11–25, and 26+ previous purchases, and use consistent definitions across SQL and Power BI.
* **Additional opportunity:** Test subscription offers around the second or third purchase, while validating the unusual subscription pattern first.

## 06 — Product & Category Performance

**Clothing is the revenue engine; Outerwear is the smallest category.**

| Category    |  Revenue | Share |
| ----------- | -------: | ----: |
| Clothing    | $104,264 | 44.7% |
| Accessories |  $74,200 | 31.8% |
| Footwear    |  $36,093 | 15.5% |
| Outerwear   |  $18,524 |  7.9% |

* **Recommendation:** Protect Clothing availability, explore Accessories cross-selling, and review Outerwear assortment and timing.
* **Product ratings:** Gloves lead at 3.86, while Shirts (3.62) and Jeans (3.65) have the lowest averages. Investigate fit and quality feedback before drawing firm conclusions.

## 07 — Seasonality & Customer Preferences

**Purchasing behavior is relatively consistent across most groups.**

* **Season:** Fall leads with $60,018 revenue and a $61.56 average purchase; Summer is lowest at $55,777.
* **Age, shipping & payment:** Average purchases and revenue shares vary only modestly across groups.
* **Recommendation:** Maintain a broad range of payment and shipping options, and test a modest Fall campaign rather than making major seasonal changes.

---

## Business Recommendations

Based on the analysis, the following actions could help improve customer insights, promotional decisions, and retail performance.

### 1. Validate Customer Data Before Making Decisions

The dataset shows an unusual pattern: no female customers used discounts or subscribed, while all subscribers were male and also reported using discounts. Investigate these records and verify the underlying data before using gender, discount usage, or subscription status to guide marketing decisions.

### 2. Improve Promotional Effectiveness

Male customers who used discounts had a slightly lower average purchase amount ($59.28) than those who did not ($59.98). This suggests that discount usage was not associated with higher average spending in this dataset. Test targeted promotions against a control group and evaluate incremental revenue, conversion, and profit margins before expanding discount campaigns.

### 3. Develop More Meaningful Customer Loyalty Strategies

Approximately 79.9% of customers had 11 or more previous purchases, indicating a customer base with substantial repeat-purchase activity. Develop actionable loyalty tiers using purchase frequency, recency, and spending value. Tailor retention campaigns and loyalty rewards to each segment, then measure repeat purchases and customer lifetime value where sufficient data is available.

### 4. Protect Clothing Revenue and Explore Growth Opportunities

Clothing generated $104,264, approximately 44.7% of total revenue, making it the largest product category. Maintain product availability and monitor customer demand in this category while investigating opportunities to grow Accessories and Footwear through product recommendations, bundles, and cross-selling. Evaluate performance using revenue, conversion, and profit margin rather than sales alone.

### 5. Investigate Customer Satisfaction Across Products

Average product ratings ranged from 3.62 to 3.86, with Gloves receiving the highest average rating (3.86) and Shirts the lowest (3.62). Review product-level feedback and customer complaints to identify potential improvement areas. Use additional review and return data to determine whether lower-rated products require changes to quality, sizing, descriptions, or customer support.

### 6. Test Seasonal Marketing Opportunities

Fall recorded the highest seasonal revenue at $60,018, followed by Summer at $55,777. Use these results as a starting point for seasonal campaign planning, inventory allocation, and product promotion. Before committing additional budget, compare seasonal demand across multiple periods and account for differences in customer volume and product availability.

> **Business impact:** Prioritize trustworthy data, evidence-based promotions, customer retention, and product-level improvement. These recommendations should be validated with more detailed transactional and profitability data before major business decisions are made.


## Limitations & Next Steps

This dataset contains one row per customer, without transaction dates, sales channels, cost, or profit margin. Consequently, it cannot establish time-based retention, true seasonal trends, or the causal impact of discounts. Statistical significance was not tested.

**Next:** Obtain transaction-level data, validate potential data artifacts, conduct significance tests, and design discount experiments.

---

<p align="center">
  <strong>Key takeaway</strong><br />
  <em>Useful analytics is not just about finding patterns. It is about knowing which patterns are reliable enough to act on.</em>
</p>
