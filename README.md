# MGSC 416 — Semester project

## Optimising cafe operations through demand forecasting and inventory planning

A data-driven approach to per-store demand, order-level baskets, unsold-unit cost (60% gross margin → COGS 40% of price), forecasting, and inventory optimisation.

### Dataset

- **[Coffee+Shop+Sales/Coffee Shop Sales.xlsx](Coffee+Shop+Sales/Coffee%20Shop%20Sales.xlsx)** — Maven Roasters line-level transactions (~149k rows, 2023). Sheet name: `Transactions`. Same-time stamps at the same store define one **order**; `transaction_id` is unique per line.
- **holidays.csv** — Canadian public holidays 2012–2026 (for feature engineering merges).

Legacy reference (previous coursework): **Cleaned_DataSet.csv** — smaller single-menu extract; older notebooks still refer to it.

### Main notebook

- **[notebooks/coffee_shop_inventory.ipynb](notebooks/coffee_shop_inventory.ipynb)** — canonical pipeline: load Excel, cleaning, `order_id`, COGS columns, order-level aggregates, calendar + holiday + product tags (Section 5), EDA (per store), **aggregation and correlation (Section 7)**, then stubs for forecasting, Gurobi optimisation, and sensitivity (Sections 8–10).

Run Jupyter with working directory `notebooks/` (or open from that folder) so paths resolve. Install Excel support: `pip install -r requirements.txt`.

### Notebook structure (coffee_shop_inventory.ipynb)

| Section | Topic | Status |
|---------|-------|--------|
| 1 | Introduction and business framing | Done |
| 2 | Data loading (Excel) | Done |
| 3 | Cleaning and validation (person 1) | Done |
| 4 | Order-level dataset | Done |
| 4.5 | Outlier checks (IQR, tails, SKU price CV) | Done |
| 5 | Feature engineering + holidays | Done |
| 6 | EDA visualisations (person 1) | Done |
| 7 | Aggregation and correlation | Done (daily demand by SKU, orders vs lines, feature correlation heatmap) |
| 8 | Forecasting | Stub (person 3) |
| 9 | Optimisation (gurobipy) | Stub (person 4) |
| 10 | Sensitivity and conclusion | Stub (person 5) |

### Outputs (generated)

Run **`notebooks/coffee_shop_inventory.ipynb`** to populate **`outputs/`** next to the project root. The folder holds figures (daily volume, revenue rolling mean, **hour × weekday revenue heatmaps** with lowest/highest cell labels and per-store range in the title, top products, category mix, basket size, AOV, outlier diagnostic plots) and large tables (`lines_clean.csv`, `lines_enriched.csv` after Section 5, `orders_clean.csv`, daily demand extracts). **All `outputs/*.csv` and `outputs/*.png` are gitignored**; clone the repo and re-run the notebook to recreate them locally.

### Legacy notebooks

**semestral_project_1.ipynb**, **semestral_project_2.ipynb**, **semestral_project 3.ipynb** — prior pipeline on **Cleaned_DataSet.csv**; reuse methodology for sections 8–9 when porting to the Excel-based line panel.

### Key figures (legacy CSV pipeline)

- `fig_revenue_by_item.png` — revenue breakdown by menu item
- `fig_day_of_week.png` — transaction volume by day of week
- `fig_weekly_revenue.png` — weekly revenue trend over 2023
- `fig_heatmap_day_month.png` — sales heatmap (day of week x month)
- `fig_boxplots.png` — spending distributions by season
- `fig_correlation_matrix.png` — feature correlations
- `fig_item_season.png` — item demand by season
- `fig_season_drink_food.png` — seasonal drink vs food split
- `fig_decomposition.png` — seasonal decomposition of weekly revenue
- `fig_sarima_forecast.png` — SARIMA revenue forecast vs actuals
- `fig_item_forecasts.png` — per-item SARIMAX demand forecasts
- `fig_ols_coefs.png` — OLS regression coefficients
- `fig_ols_diagnostics.png` — OLS residual diagnostics
- `fig_regularisation_cv.png` — Ridge/Lasso cross-validation curves
- `fig_coef_comparison.png` — OLS vs Ridge vs Lasso coefficient comparison

### Tools

Python 3.11+ · pandas · numpy · matplotlib · seaborn · openpyxl · statsmodels · scikit-learn · gurobipy

### Team

5 people — see notebook section headers for task assignments.
