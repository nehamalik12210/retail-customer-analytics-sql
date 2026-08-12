# Digital Payments / Retail Customer Analytics

SQL-driven customer segmentation, churn analysis, cohort retention, and revenue forecasting on the
real **UCI Online Retail II** dataset (805,549 transactions, 5,878 customers, Dec 2009–Dec 2011).

## What it does

- Loads and cleans the real Online Retail II Excel dataset (both sheets, missing customer IDs dropped,
  negative/refund amounts excluded)
- SQL (SQLite): monthly revenue trend, RFM scoring via window functions (`NTILE`), cohort retention
  via self-joins
- RFM segmentation (Champions / Loyal / At Risk / Hibernating / Lost), cross-checked against an
  independent KMeans clustering on log-transformed features
- Churn threshold chosen from a sensitivity sweep (30–180 days), not asserted
- Revenue forecasting: linear regression (trend + monthly seasonality) vs. a naive baseline, with
  residual autocorrelation check and bootstrap 95% prediction intervals
- Statistical tests throughout: significance of the growth trend, early-vs-late cohort retention

## Key results

- Revenue growth trend: **not statistically significant** (p=0.08) — real revenue is seasonal/noisy,
  not a clean upward line
- Churn rate: 50.9% at the chosen 90-day threshold
- Forecast: 4.7% MAPE, beats the naive baseline by **88.7%** (driven by capturing the real Nov/Dec
  holiday spike that a naive "last month" prediction misses entirely)
- Cohort retention differences (early vs. late signups): not statistically significant (p=0.14)


## Run it

**On Kaggle**: attach the Online Retail II dataset, run all cells.

**Locally**:
```bash
pip install -r requirements.txt
jupyter notebook customer_analysis.ipynb
```
Update the `path` variable in the data-loading cell to your local copy of `online_retail_II.xlsx`.
