# Asymmetric Volatility Modeling and Risk Forecasting: Evidence from the DAX Index

## Abstract
This project evaluates whether modeling volatility asymmetry (leverage effects) improves market risk forecasting.
Using daily DAX log returns, we estimate a symmetric GARCH(1,1) model and an asymmetric GJR-GARCH(1,1) model
under a rolling one-step-ahead forecasting framework. Forecast accuracy is assessed with RMSE and QLIKE loss,
and risk calibration is tested via 1% and 5% Value-at-Risk (VaR) backtesting using Kupiec and Christoffersen tests.
Overall, results support the practical relevance of asymmetric volatility modeling for downside risk estimation.

## Data
- Asset: DAX Index (Yahoo Finance ticker: ^GDAXI)
- Frequency: Daily
- Returns: Log returns
- Input file: `data/processed/dax_log_returns.csv`

## Methodology
1. **Stylized Facts**: Normality tests, ARCH effects, and volatility clustering
2. **Volatility Models**: GARCH(1,1) vs. GJR-GARCH(1,1) estimated by Maximum Likelihood
3. **Rolling Forecast**: Expanding window, one-step-ahead volatility forecasts
4. **Evaluation**:
   - Volatility forecast accuracy: RMSE, QLIKE
   - VaR backtesting at 1% and 5%: Kupiec (POF), Christoffersen (Independence), Conditional Coverage

## Key Findings
- GJR-GARCH achieves better out-of-sample performance than symmetric GARCH (especially in QLIKE loss).
- Asymmetric volatility modeling improves downside risk calibration in VaR backtests.
- Evidence is consistent with leverage effects in equity index returns.

## Repository Structure
- `notebooks/` — End-to-end analysis notebooks
- `data/raw/` — Raw inputs (if any)
- `data/processed/` — Processed returns used by the models
- `results/tables/` — Exported evaluation tables (metrics, backtests)
- `results/figures/` — Saved figures (plots used in the README/report)
- `src/` — Utility functions (optional)

## How to Run
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter lab
