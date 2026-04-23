# Medicare Provider Cost & Utilization Analysis

A Python-based data analysis project examining Medicare claims data across 
Cardiology, Internal Medicine, and Family Practice specialties for 2022–2023.

## Project Summary

| Metric | Value |
|---|---|
| Total rows analyzed | 19,416,074 |
| Rows after specialty filter | 4,027,496 |
| States / territories covered | 60 |
| Providers analyzed (min. 100 services) | 327,133 |
| Outlier providers flagged (ratio ≥ 10x) | 5,229 |
| Years covered | 2022, 2023 |

## Data Source

CMS Medicare Physician & Other Practitioners — by Provider and Service  
https://data.cms.gov/provider-summary-by-type-of-service/medicare-physician-other-practitioners/medicare-physician-other-practitioners-by-provider-and-service

## Analysis Structure

**1. Load & Filter**  
Loaded two years of CMS claims data (~19M rows), filtered to three specialties 
using pandas, and tagged each row with its year before combining into a single 
DataFrame.

**2. State-Level Benchmarking**  
Aggregated average Medicare payment, submitted charges, total services, and 
beneficiary counts by state, specialty, and year. Calculated charge-to-payment 
ratio as a billing intensity signal.

**3. Year-over-Year Trend**  
Pivoted state-level data to compare 2022 vs. 2023 payments and volume side by 
side. Key finding: Cardiology payments declined across multiple states while 
Primary Care payments modestly increased — consistent with 2023 Medicare 
physician fee schedule adjustments.

**4. Provider-Level Outlier Detection**  
Identified 5,229 providers (out of 327,133 analyzed) with charge-to-payment 
ratios ≥ 10x and minimum 100 services — a standard signal used in claims 
analysis to flag billing anomalies. Geographic clustering was observed in NJ 
and TX among top outliers.

## Key Findings

- DC, NV, and FL ranked highest for average Cardiology Medicare payments in 2023
- Cardiology payments declined nationally 2022→2023 while Internal Medicine 
  and Family Practice saw modest increases
- 1.6% of providers (5,229) exceeded a 10x charge-to-payment ratio with 
  meaningful service volume
- Top outlier: one TX Internal Medicine provider averaged $4,606 in submitted 
  charges against $39 in Medicare payment (117x ratio) across 1,979 services

## Outputs

| File | Description |
|---|---|
| `output_state_summary.csv` | Avg payment, charges, volume by state/specialty/year |
| `output_trend_yoy.csv` | Year-over-year payment and volume change by state/specialty |
| `output_outliers.csv` | 5,229 flagged providers with ratio ≥ 10x |
| `chart1_cardiology_payment_by_state.png` | Top 20 states by Cardiology payment (2023) |
| `chart2_payment_trend_by_specialty.png` | National payment trend by specialty |
| `chart3_outlier_distribution.png` | Charge-to-payment ratio distribution |

## Tools & Libraries

- Python 3.14
- pandas — data loading, filtering, aggregation, pivoting
- matplotlib — visualization
- Jupyter Notebook (VS Code) — interactive development

## Skills Demonstrated

- Working with large datasets (19M+ rows) in pandas
- GroupBy aggregation and pivot tables
- Year-over-year trend analysis
- Outlier detection using ratio-based thresholds
- Data export and chart generation