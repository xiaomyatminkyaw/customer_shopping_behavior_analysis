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

## Strategic Priorities

<ol>
  <li><strong>Validate data quality.</strong> Investigate the gender, discount, and subscription patterns first.</li>
  <li><strong>Measure promotional effectiveness.</strong> Use controlled experiments and profit-based metrics.</li>
  <li><strong>Refine customer segmentation.</strong> Create more useful loyalty tiers and test targeted engagement.</li>
  <li><strong>Optimize the product mix.</strong> Protect Clothing revenue and investigate weaker product categories.</li>
</ol>

## Limitations & Next Steps

This dataset contains one row per customer, without transaction dates, sales channels, cost, or profit margin. Consequently, it cannot establish time-based retention, true seasonal trends, or the causal impact of discounts. Statistical significance was not tested.

**Next:** Obtain transaction-level data, validate potential data artifacts, conduct significance tests, and design discount experiments.

---

<p align="center">
  <strong>Key takeaway</strong><br />
  <em>Useful analytics is not just about finding patterns. It is about knowing which patterns are reliable enough to act on.</em>
</p>
