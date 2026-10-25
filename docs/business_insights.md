# Business insights

Total: 3,900 customers · $233,081 revenue · $59.76 average purchase · 3.75 average rating. All numbers below were recomputed from the cleaned data.

**Read this first:** most group differences in this dataset are small (often under $2 on a $60 average). The strongest signals are structural (who discounts and subscribes), and those look like a data artifact, so treat conclusions as hypotheses to test, not proof.

---

## 1. Revenue is driven by the number of male customers, not by higher spend

- **Evidence:** Male $157,890 (67.7%) vs Female $75,191. Men are 2,652 of 3,900 customers (68%). Average spend: $59.54 (men), $60.25 (women).
- **Interpretation:** Women spend slightly more per person; the revenue gap is a reach gap.
- **Recommendation:** Prioritise acquisition among women (targeted campaigns, assortment, channels they use). Growing that segment to parity would add revenue without raising basket size.
- **Caveat:** No acquisition-channel data, so cause of the imbalance is unknown.

## 2. Discounts and subscriptions exist only among male customers

- **Evidence:** 0 of 1,248 women used a discount or subscribed. Among 2,652 men: 1,677 (63.2%) used a discount and 1,053 (39.7%) subscribe. All 1,053 subscribers also used a discount.
- **Interpretation:** The offers may never have reached women, or the fields were generated or recorded differently by gender.
- **Recommendation:** Confirm with the data provider first. If real, test discount and subscription offers on women, since the gap is a large untapped group.
- **Caveat:** A clean 0% and a perfect nesting (subscriber ⊂ discount user ⊂ male) is unusual in real retail data. It also means the overall figure of "43% used a discount" is really 63% of men and 0% of women.

## 3. Discounts do not raise spend

- **Evidence:** Among men (the only group with discounts), discount users average $59.28 vs $59.98 without. Overall: $59.28 vs $60.13.
- **Interpretation:** Discounts are given to 63% of men without increasing basket size, which suggests margin is being given away.
- **Recommendation:** Run holdout tests: pause discounts on the most-discounted items (Hat 50.0%, Sneakers 49.7%, Coat 49.1%) for one cycle and compare sales and margin.
- **Caveat:** Data has no margin or price-before-discount, and discount use is not randomly assigned, so this is an association.

## 4. Subscribers do not spend or rate differently

- **Evidence:** $59.49 vs $59.87 average (all customers); $59.49 vs $59.57 among men only. Ratings 3.747 vs 3.751. Revenue: subscribers $62,645 (26.9%), non-subscribers $170,436.
- **Interpretation:** The subscription is not changing per-purchase behaviour. Its value, if any, lies in retention or frequency, which this data can't show.
- **Recommendation:** Redesign benefits around spend or frequency (shipping thresholds, early access) and measure repeat rate, not sign-ups alone.
- **Caveat:** No time data, so retention can't be measured.

## 5. Loyalty is high and the "Loyal" label is too broad

- **Evidence:** Loyal (11+ purchases) 3,116 (79.9%), Returning (2–10) 701 (18.0%), New (1) 83 (2.1%). Previous purchases average 25 (range 1–50).
- **Interpretation:** With four in five customers "Loyal", the tier can't guide targeting.
- **Recommendation:** Re-cut tiers, for example 1–10 / 11–25 / 26+, and apply the same definition in SQL and Power BI.
- **Caveat:** `previous_purchases` is a count, not a recency or value measure.

## 6. Subscription rises modestly with loyalty

- **Evidence:** Subscribed share: New 18.1% (15 of 83), Returning 24.1%, Loyal 27.9%. Repeat buyers (>5 purchases) 27.6% vs 27.0% overall.
- **Interpretation:** A mild gradient, mostly visible between New and the others.
- **Recommendation:** Offer subscription at the second or third purchase, when customers are moving from New to Returning.
- **Caveat:** The New group is very small; the gradient is also confounded by finding 2.

## 7. Clothing carries the business; Outerwear is small

- **Evidence:** Clothing $104,264 (44.7%), Accessories $74,200 (31.8%), Footwear $36,093 (15.5%), Outerwear $18,524 (7.9%). Customers: 1,737 / 1,240 / 599 / 324. Average order: Footwear $60.26, Clothing $60.03, Accessories $59.84, Outerwear $57.17.
- **Interpretation:** Category revenue follows how many customers buy it, not price.
- **Recommendation:** Protect Clothing availability, cross-sell Accessories into Clothing baskets, and review Outerwear range and timing (lowest order value and volume).
- **Caveat:** One item per customer row; no basket data.

## 8. Ratings are tightly bunched; Jeans and Shirt trail

- **Evidence:** Range 3.62–3.86. Top: Gloves 3.86, Sandals 3.84, Boots 3.82, Hat 3.80. Bottom: Shirt 3.62, Jeans 3.65. Jeans has the fewest orders (124) of any product; Shirt has 169, which is typical.
- **Interpretation:** Product quality perception is fairly uniform, with Jeans and Shirt as relative weak spots.
- **Recommendation:** Collect fit and quality feedback on Jeans and Shirt; use top-rated products in promotions.
- **Caveat:** 37 ratings were imputed; a 0.2-point gap on about 150 reviews per product is not strong evidence.

## 9. Seasonality is mild; Fall is strongest

- **Evidence:** Fall $60,018 (25.7%, $61.56 average order), Spring $58,679, Winter $58,607, Summer $55,777 (23.9%, $58.41).
- **Interpretation:** Demand is steady year-round with a small Fall lift in order value.
- **Recommendation:** Keep inventory and campaigns evenly spread; give Fall a modest push on higher-value items.
- **Caveat:** `Season` is a label, not a date, so true trends and holiday peaks can't be seen.

## 10. Age, shipping, payment and frequency are nearly flat

- **Evidence:** Age-group revenue: Young Adult 26.7%, Middle_aged 25.4%, Adult 24.0%, Senior 23.9%. Shipping averages $58.46–$60.73. Payment methods: PayPal 677, Credit Card 671, Cash 670, Debit Card 636, Venmo 634, Bank Transfer 612 customers; average spend $58.95–$60.92. Purchase frequency groups hold 539–584 customers each.
- **Interpretation:** None of these split customers into meaningfully different groups. Offer a broad range of payment and shipping options rather than optimising for one.
- **Recommendation:** Use the scarce segmentation effort on gender, loyalty and category instead.
- **Caveat:** No significance tests were run.

---

## Overall limitations

- One row per customer, no dates: no trends, retention or seasonality by date.
- No online/offline channel field (requested in the brief, so not analysed).
- No cost, margin or pre-discount price.
- Likely synthetic or heavily sampled data (very even distributions, finding 2), so results may not transfer to a real retailer.

## Future analysis

Generate or obtain transaction dates; add channel; test discount lift with an experiment; build a star schema; run significance tests (chi-square for subscription by segment, t-tests for spend differences).
