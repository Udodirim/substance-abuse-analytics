# 🧪 Global Substance Abuse Mortality Analytics

> **Portfolio Project** | Eden Mandate AI_Tools  
> Master's in AI and Data Science

## Overview
End-to-end analysis of global mortality attributable to substance abuse (drug, alcohol, tobacco)  
across 207 countries from 1990–2019, with a 5-year SARIMAX forecast through 2024.

## Dataset
- **Source:** Global Burden of Disease / Our World in Data  
- **Shape:** 6,210 rows × 8 columns  
- **Coverage:** 207 countries · 30 years (1990–2019)  
- **Measures:** 5 death categories (direct drug, direct alcohol, risk tobacco, risk drug, risk alcohol)

## Methodology

| Step | Description |
|---|---|
| Data Quality | Null checks, duplicate detection, negative value validation |
| Standardisation | Snake_case normalisation, date parsing, numeric coercion |
| Feature Engineering | Lag features (t-1, t-2), 3-year rolling mean, trend index |
| Modelling | SARIMAX (AIC grid), Prophet (annual-corrected), AutoTS (fast ensemble) |
| Evaluation | Hold-out test set (3 years) · MAE, RMSE, MAPE |
| Forecasting | 5-year horizon per measure with 80% confidence intervals |
| Exports | Power BI and Tableau ready CSVs |

## Key Results

See `model_evaluation.csv` for full metrics. Best model selected by lowest RMSE on the 3-year hold-out.

## Output Files

```
├── annual_totals.csv               # Global annual totals
├── country_year.csv                # Country × year breakdowns
├── measures_long.csv               # Tidy long format
├── fact_actual_forecast.csv        # Actuals + forecasts combined
├── forecast_by_measure_long.csv    # Forecasts in long format
├── forecast_by_measure_wide.csv    # Forecasts in wide format
├── kpi_all.csv                     # KPI summary table
├── model_evaluation.csv            # Model comparison (MAE/RMSE/MAPE)
├── model_report.json               # Full model selection report
└── tableau_ready/                  # Tableau-optimised exports
```

## Tech Stack
Python · pandas · statsmodels (SARIMAX) · Prophet · AutoTS · matplotlib · VS Code · GitHub

## Commit Structure
| Commit | Content |
|---|---|
| 1 | Data loading, quality checks, standardisation |
| 2 | KPIs and EDA visualisations |
| 3 | Feature engineering |
| 4 | Modelling, evaluation, forecasting |
| 5 | Export files |
| 6 | Quality report and findings |
| 7 | README |

---
*Built with integrity — real metrics, honest model reporting.*
