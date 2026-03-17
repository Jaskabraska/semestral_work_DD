---
name:  Semestral Project Plan
overview:  plan for the MGSC 416 semester project using only the two CSV files (no weather), with purely date-derived features, GitHub setup, and task division for 5 people.
todos: []
isProject: false
---

# MGSC 416 Semester Project Plan (updated)

## Project folder and GitHub

- **Folder:** `c:\Users\jachy\Desktop\Vysoká\2025-erasmus\Classes\Data-driven models\semestral_work_DD\`
- **Files:** [Cleaned_DataSet.csv](c:\Users\jachy\Desktop\Vysoká\2025-erasmus\Classes\Data-driven models\semestral_work_DD\Cleaned_DataSet.csv) (9,741 rows), [holidays.csv](c:\Users\jachy\Desktop\Vysoká\2025-erasmus\Classes\Data-driven models\semestral_work_DD\holidays.csv) (Canadian holidays 2012-2026)
- **GitHub:** `https://github.com/Jaskabraska/semestral_work_DD.git` -- will initialise git repo and push initial commit with the two CSVs and the notebook
- **Environment:** Anaconda Python 3.13.9 (matching HW4), using pandas, numpy, gurobipy, matplotlib/seaborn
- **Notebook style:** follows HW4 pattern -- markdown cells with explanations/formulations, then code cells

---

## Data issues to fix first

1. **"unknown" (337 rows) and "error" (283 rows)** -- 620 rows with invalid item names, drop them
2. **1,166 rows where Quantity x Price Per Unit != Total Spent** -- recalculate Total Spent as Qty x Price
3. **Inconsistent prices per item** -- investigate and document (could be size variants)

---

## Feature engineering (no external data -- all derived from dates + holidays.csv)

**Temporal features from Transaction Date:**
- `day_of_week` (0=Mon ... 6=Sun)
- `day_name` (Monday, Tuesday, ...)
- `is_weekend` (1 if Saturday/Sunday, 0 otherwise)
- `month` (1-12)
- `season` (Winter: Dec-Feb, Spring: Mar-May, Summer: Jun-Aug, Autumn: Sep-Nov)
- `week_number` (1-52)
- `is_month_start` / `is_month_end`

**From holidays.csv merge:**
- `is_holiday` (1 if the date matches a holiday, 0 otherwise)
- `days_to_next_holiday` (integer distance to nearest upcoming holiday)

**Item-derived features:**
- `item_category`: "drinks" (coffee, tea, juice, smoothie) vs "food" (cake, cookie, sandwich, salad)
- `is_hot_drink`: 1 for coffee/tea, 0 otherwise -- allows testing season x drink-type interaction without weather data

---

## Notebook structure (single Jupyter Notebook)

The notebook will be divided into clearly labelled sections matching the report structure:

### Section 1 -- Data loading and cleaning (Person 1)
- Load both CSVs
- Drop "unknown" and "error" rows
- Fix Total Spent mismatches
- Document price inconsistencies

### Section 2 -- Feature engineering (Person 2)
- Create all temporal features from Transaction Date
- Merge holidays.csv to create is_holiday and days_to_next_holiday
- Create item_category and is_hot_drink
- Export the enriched dataset as `enriched_dataset.csv`

### Section 3 -- Descriptive analysis and visualisations (Person 1)
- Summary statistics (mean/median/std per item, per day of week, per season)
- Bar charts: revenue by item, transactions by day of week
- Line chart: weekly revenue over time
- Heatmap: sales by day_of_week x month
- Box plots: spending distribution by season, weekday vs weekend

### Section 4 -- Aggregation and correlation (Person 2)
- Aggregate to daily level: daily total transactions, daily revenue, daily demand per item
- Correlation matrix of all numeric + encoded features
- Test key hypotheses: weekend effect, holiday effect, season x drink-type interaction

### Section 5 -- Time series forecasting (Person 3)
- Weekly demand per item time series
- Seasonal decomposition (trend, seasonality, residual)
- ARIMA or dynamic regression model for demand forecasting
- Train/test split (e.g. first 10 months train, last 2 months test - need to be stratisfied)
- Evaluate with RMSE, MAE

### Section 6 -- Regression models (Person 3)
- Predict daily revenue using: day_of_week, is_weekend, season, month, is_holiday, item mix
- Compare OLS regression vs regularised (Ridge/Lasso)
- Report R-squared, coefficient interpretation

### Section 7 -- Optimisation (Person 4)
- **Problem:** daily inventory planning for the cafe -- decide how many units of each item to prepare
- **Inputs:** demand forecasts from Section 5, assumed cost per item, selling prices from data
- **Formulation:** LP/IP using gurobipy (matching course tools from HW4)
  - Decision variables: quantity to prepare for each item
  - Objective: maximise expected profit (revenue - cost - waste cost)
  - Constraints: budget, capacity, minimum service level
- Solve and present optimal inventory plan for weekday vs weekend, by season

### Section 8 -- Results summary and sensitivity (Person 5)
- Compile key findings from all sections
- Sensitivity analysis on optimisation (vary budget, demand uncertainty)
- Prepare figures/tables for the appendices

---

## Work division for 5 people

| Person | Sections | Deliverables |
|--------|----------|-------------|
| 1 | Sections 1 + 3 | Data cleaning, summary stats, all visualisations, Data Overview page of report |
| 2 | Sections 2 + 4 | Feature engineering, aggregation, correlation analysis, assist with Data Overview |
| 3 | Sections 5 + 6 | Time series forecasting, regression models, Methodology page (prediction part) |
| 4 | Section 7 | Optimisation model in gurobipy, Methodology page (optimisation part) |
| 5 | Section 8 + report + deck | Results/