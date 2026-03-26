### Medicare Geographic Spending Disparities
Predicting unexplained county-level Medicare cost variation after geographic adjustment

#### Background

CMS adjusts Medicare payments for regional cost differences using GPCI and Wage Index.
Even after this adjustment, per-beneficiary spending varies considerably across U.S.
counties. This project builds a machine learning model to predict that remaining gap —
the spending residual — and identify which county-level factors drive it.

**Research question:** What demographic, socioeconomic, and healthcare supply factors
explain the variation in Medicare spending that CMS geographic adjustment does not
account for?

#### Data Sources

All datasets are publicly available.

- **Medicare Physician & Other Practitioners** (CMS, 2023) — [link](https://data.cms.gov/provider-summary-by-type-of-service/medicare-physician-other-practitioners/medicare-physician-other-practitioners-by-provider)
- **Hospital General Information** (CMS, 2023) — [link](https://data.cms.gov/provider-data/dataset/xubh-q36u)
- **ACS S1901, S2701, B17001** — median household income, health insurance coverage, poverty status (Census Bureau, 2022) — [link](https://data.census.gov)
- **Area Health Resources File (AHRF)** (HRSA, 2022–2023) — [link](https://data.hrsa.gov/topics/health-workforce/ahrf)

#### Results

- **Final model:** Ridge Regression
- **Test R²:** 0.2716 | **RMSE:** $34.86 | **MAE:** $19.53
- **R² gap (train − test):** 0.0908
- **Counties in model:** 3,018

**Key findings**

- The dominant driver of unexplained spending is utilization intensity
  (services per beneficiary), not healthcare supply shortage.
  This feature alone accounts for 62% of explained R² by permutation importance.
- Ridge outperformed Random Forest and XGBoost, suggesting the remaining signal
  after CMS geographic adjustment is largely linear. ML does not show a clear
  advantage over a well-specified regression here.
- The county risk tier framework revealed within-metro variation that aggregate
  analysis would miss. In the Philadelphia metro, seven counties share the same
  Medium risk label but operate through opposite mechanisms — access-barrier-driven
  low spending in Philadelphia city vs. supply-induced-demand-driven high spending
  in Montgomery County.

---

#### Limitations

- All findings are associational. No causal claims are made.
- Medicare spending is attributed to counties based on provider ZIP code,
  not beneficiary residence.
- Medicare data (2023) and ACS/AHRF data (2022) are from different years.
  Post-COVID spending pattern shifts may affect results.
- The model does not capture longer-term or preventive care effects.
