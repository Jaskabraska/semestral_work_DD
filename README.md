# MGSC 416 — Semester project

## Optimising cafe operations through demand forecasting and inventory planning

A data-driven approach to reducing food waste and maximising profit for a small cafe, using transaction data, time series forecasting, and mathematical optimisation.

### Dataset

- **Cleaned_DataSet.csv** — 9,741 cafe transactions (Jan–Dec 2023) with item, quantity, price, and date
- **holidays.csv** — Canadian public holidays 2012–2026

### Notebook structure

| Section | Topic | Status |
|---------|-------|--------|
| 1 | Data loading and cleaning | Done |
| 2 | Feature engineering (temporal, holiday, item-derived) | Done |
| 3 | Descriptive analysis and visualisations | Done |
| 4 | Aggregation and correlation analysis | Done |
| 5 | Time series forecasting (SARIMAX per item) | Done |
| 6 | Regression models (OLS, Ridge, Lasso) | Done |
| 7 | Inventory optimisation (gurobipy) | To do |
| 8 | Results summary and sensitivity analysis | To do |

### Key figures

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

Python 3.11 · pandas · numpy · matplotlib · seaborn · statsmodels · scikit-learn · gurobipy

### Team

5 people — see notebook section headers for task assignments.
