# Volatility Forecasting & VaR Backtesting (DAX)

## Overview

This project performs an empirical comparison of symmetric and asymmetric GARCH-type models for volatility forecasting and Value-at-Risk (VaR) backtesting using daily DAX index returns.

The main objective is to evaluate whether modeling volatility asymmetry (leverage effects) improves out-of-sample volatility forecasts and market risk estimation.

Models estimated:
- GARCH(1,1)
- GJR-GARCH(1,1)

Forecasting framework:
- Rolling one-step-ahead volatility forecasts
- Out-of-sample evaluation
- 1% and 5% VaR backtesting


---

## Data

- Asset: DAX Index (^GDAXI)
- Frequency: Daily
- Returns: Log returns
- Sample split: 80% training / 20% test (rolling forecast)

Processed returns file:
```
data/processed/dax_log_returns.csv
```


---

## Methodology

### 1. Stylized Facts

- Jarque–Bera test for normality
- ARCH effect detection
- Volatility clustering analysis


### 2. Volatility Modeling

Both models are estimated using Maximum Likelihood Estimation.

Forecast evaluation metrics:
- RMSE (volatility forecast accuracy)
- QLIKE loss function (robust to noise in realized variance)


### 3. Rolling Forecast Framework

- Expanding window estimation
- One-step-ahead sigma forecast
- Out-of-sample comparison


### 4. VaR Estimation & Backtesting

- Parametric Normal VaR (mean = 0)
- Confidence levels: 1% and 5%
- Backtests:
  - Kupiec (POF)
  - Christoffersen (Independence)
  - Conditional Coverage


---

## Empirical Findings

### Stylized Facts

- Strong excess kurtosis and rejection of normality.
- Significant ARCH effects detected.
- Clear volatility clustering in absolute returns.


### Model Comparison

- GJR-GARCH(1,1) outperformed symmetric GARCH in AIC and out-of-sample loss.
- RMSE and QLIKE indicate improved forecast accuracy under asymmetry.
- Asymmetric modeling enhances volatility forecast stability.


### Risk Implications

- At the 1% VaR level, GJR-GARCH produced fewer exceedances.
- Kupiec and Conditional Coverage tests indicate improved calibration.
- Modeling leverage effects materially improves downside risk estimation.


---

## Conclusion

Accounting for asymmetry in volatility dynamics significantly enhances both volatility forecasting performance and market risk measurement accuracy for equity index returns.


---

## Repository Structure

```
notebooks/        End-to-end analysis notebooks
data/raw/         Raw price data
data/processed/   Processed log returns
results/tables/   Exported evaluation tables
results/figures/  Saved figures (optional)
src/              Modularized utilities
```


---

## How to Run

Create environment:

```
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Launch Jupyter:

```
jupyter lab
```

Run notebooks in order:

1. 01_data_and_stylized_facts.ipynb  
2. 02_garch_models.ipynb  
3. 03_rolling_forecast.ipynb  
4. 04_var_backtesting.ipynb
