# DAX Measures Documentation

All measures live in the `_measures` table in saas_dashboard.pbix

---

### Total MRR
**Formula:**
```dax
Total MRR = 
CALCULATE(
  SUM(fact_customers[mrr]),
  fact_customers[is_churned] = FALSE
)
```
**Business meaning:** Monthly recurring revenue from active 
customers only. Excludes churned customers.
**Used on:** Executive Summary — primary KPI card.

---

### Churned MRR
**Formula:**
```dax
Churned MRR = 
CALCULATE(
  SUM(fact_customers[mrr]),
  fact_customers[is_churned] = TRUE
)
```
**Business meaning:** MRR belonging to customers who have 
already left. Used to calculate churn rate.
**Used on:** Executive Summary, churn rate calculation.

---

### Total ARR
**Formula:**
```dax
Total ARR = [Total MRR] * 12
```
**Business meaning:** Annualised recurring revenue.
**Used on:** Executive Summary KPI card.

---

### MRR Churn Rate %
**Formula:**
```dax
MRR Churn Rate % = 
DIVIDE(
  [Churned MRR],
  [Total MRR] + [Churned MRR],
  0
)
```
**Business meaning:** Percentage of total MRR base that 
has churned. Healthy SaaS benchmark is below 2% monthly.
**Used on:** Executive Summary KPI card.

---

### Customer Churn Rate %
**Formula:**
```dax
Customer Churn Rate % = 
DIVIDE(
  CALCULATE(
    COUNTROWS(fact_customers),
    fact_customers[is_churned] = TRUE
  ),
  COUNTROWS(fact_customers),
  0
)
```
**Business meaning:** Percentage of all customers who 
have churned. Different from MRR churn because 
high-paying customers may churn at different rates.
**Used on:** Churn Deep Dive charts.

---

### ARR at Risk
**Formula:**
```dax
ARR at Risk = 
CALCULATE(
  SUM(fact_customers[mrr]),
  fact_customers[is_churned] = FALSE,
  fact_customers[health_band] IN {"At-Risk", "Critical"}
) * 12
```
**Business meaning:** Annual revenue from customers in 
At-Risk or Critical health bands who have not yet churned.
**Used on:** Executive Summary, At-Risk Register.

---

### ARR at Risk %
**Formula:**
```dax
ARR at Risk % = 
DIVIDE(
  CALCULATE(
    SUM(fact_customers[mrr]),
    fact_customers[is_churned] = FALSE,
    fact_customers[health_band] IN {"At-Risk","Critical"},
    ALL(fact_customers[health_band])
  ),
  CALCULATE(
    SUM(fact_customers[mrr]),
    fact_customers[is_churned] = FALSE,
    ALL(fact_customers[health_band])
  ),
  0
)
```
**Business meaning:** At-risk ARR as a percentage of 
total ARR. Uses ALL() to ignore page-level filters.
**Used on:** At-Risk Register headline card.

---

### Avg Health Score
**Formula:**
```dax
Avg Health Score = 
CALCULATE(
  AVERAGE(fact_customers[health_score_raw]),
  fact_customers[is_churned] = FALSE
)
```
**Business meaning:** Average composite health score 
across all active customers. Score is 0-100 where 
higher = healthier customer.
**Used on:** Executive Summary KPI card.

---

### Last Refreshed
**Formula:**
```dax
Last Refreshed = 
"Data as of: " & FORMAT(NOW(), "DD MMM YYYY")
```
**Business meaning:** Shows when the data was last 
loaded. Appears on every dashboard page.
**Used on:** All 3 pages, bottom right corner.
