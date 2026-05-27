# SaaS Customer Health & Churn Risk Analysis

> **Business question:** Which customer segments carry 
> the highest churn risk, and what ARR is at stake 
> without intervention?

![Executive Summary](docs/screenshots/01_executive_summary.png)

---

## Key Findings

- **59% of total ARR** sits in At-Risk or Critical accounts
- Month-to-month customers churn at **42.7%** versus 
  just **2.8%** for two-year contracts — a 15× difference
- Fiber optic customers churn at **57.9%** — more than 
  3× the DSL rate of 17.6%
- Customers with zero add-ons in months 0-3 churn at 
  **52%** — suggesting onboarding drives retention more 
  than product features
- Reducing churn from 31% to 20% is worth **$554,178** 
  in additional lifetime value across the customer base

---

## Dashboard

![Churn Deep Dive](docs/screenshots/02_churn_deep_dive.png)
![At-Risk Register](docs/screenshots/03_at_risk_register.png)

---

## Tools & Skills Demonstrated

| Tool | Techniques |
|------|-----------|
| Excel | Power Query (M code), LET formulas, cohort retention matrix, SUMIFS/COUNTIFS, Data Tables for scenario analysis |
| Power BI | DAX measures (CALCULATE, DIVIDE, ALL), conditional formatting, drillthrough, bookmarks, slicers |
| GitHub | Version control, technical documentation, markdown |

---

## Project Structure

```
saas-churn-analytics/
├── data/
│   └── raw/          ← Original IBM Telco Churn dataset
├── excel/
│   └── saas_churn_model.xlsx
├── powerbi/
│   ├── saas_dashboard.pbix
│   └── dax_measures.md    ← Every DAX measure documented
├── docs/
│   └── screenshots/       ← Dashboard screenshots
```

---

## Excel Model Highlights

- **Power Query** — 14-step transformation pipeline 
  with named steps, null handling, and calculated columns
- **Cohort matrix** — churn rate by tenure band × 
  addon count, color-coded heatmap
- **8 SaaS KPIs** — MRR, ARR, NRR, LTV, churn rates, 
  health score
- **Scenario tables** — what-if analysis showing value 
  of churn reduction at different ARPU levels

![Excel Cohort](docs/screenshots/04_excel_cohort.png)

---

## How to Use

1. Download `data/raw/WA_Fn-UseC_-Telco-Customer-Churn.csv`
2. Open `excel/saas_churn_model.xlsx` — start on the 
   `_README` tab
3. Open `powerbi/saas_dashboard.pbix` in Power BI Desktop
4. Read `powerbi/dax_measures.md` for DAX documentation

---

## Data Source

IBM Telco Customer Churn dataset reframed to SaaS 
subscription context. Columns renamed to reflect SaaS 
terminology (tenure → months_subscribed, 
MonthlyCharges → mrr, etc).

Original source: https://www.kaggle.com/datasets/blastchar/telco-customer-churn
