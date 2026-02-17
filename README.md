# Volatility Forecasting & VaR Backtesting (DAX)

This project provides a comprehensive empirical study of volatility modeling and market risk forecasting using daily DAX index returns.  
We benchmark symmetric and asymmetric GARCH-type models and evaluate their implications for Value-at-Risk (VaR) estimation and regulatory backtesting.

The objective is to assess whether modeling volatility asymmetry (leverage effects) improves out-of-sample forecast accuracy and risk calibration.

---

## Data

- Asset: DAX Index (^GDAXI)
- Frequency: Daily
- Transformation: Log returns
- Sample split: 80% in-sample (estimation), 20% out-of-sample (forecast evaluation)

Volatility proxy for evaluation: **squared returns**

---

## Methodological Framework

### Volatility Models
- GARCH(1,1)
- GJR-GARCH(1,1) (asymmetric specification)

### Estimation
- Maximum Likelihood Estimation (MLE)
- Gaussian innovations

### Forecasting Design
- Rolling one-step-ahead volatility forecasts
- Out-of-sample evaluation

### Forecast Evaluation Metrics
- RMSE (Root Mean Squared Error)
- QLIKE (Quasi-Likelihood Loss)

### Risk Metrics
- Parametric VaR (mean = 0)
- Confidence levels: 1% and 5%

### Backtesting Procedures
- Kupiec Proportion of Failures (POF) test
- Christoffersen Independence test
- Christoffersen Conditional Coverage test

---

## Empirical Findings

### Stylized Facts

- Strong excess kurtosis and rejection of normality (Jarque–Bera test).
- Significant ARCH effects detected.
- Clear volatility clustering in absolute returns.

### Model Comparison

- GJR-GARCH(1,1) outperformed symmetric GARCH in AIC and out-of-sample loss.
- RMSE and QLIKE metrics confirm the economic relevance of volatility asymmetry.
- Asymmetric volatility modeling improves forecast stability.

### Risk Implications

- At the 1% VaR level, GJR-GARCH produced fewer exceedances.
- Kupiec and Conditional Coverage tests indicate improved calibration under asymmetric modeling.
- Modeling leverage effects materially improves downside risk estimation.

### Conclusion

Accounting for asymmetry in volatility dynamics significantly enhances both volatility forecast accuracy and market risk calibration for equity index returns.

---

## Repository Structure
- `notebooks/` : end-to-end analysis notebooks
- `data/raw/` and `data/processed/` : raw prices and processed returns
- `results/tables/` : exported tables (metrics, backtests)
- `results/figures/` : saved figures (optional)

## Empirical Findings

### Stylized Facts
- Strong excess kurtosis and rejection of normality (Jarque–Bera test).
- Significant ARCH effects detected.
- Clear volatility clustering in absolute returns.

### Model Comparison
- GJR-GARCH(1,1) outperformed symmetric GARCH in AIC and out-of-sample loss.
- QLIKE and RMSE confirm the economic relevance of asymmetry (leverage effect).

### Risk Implications
- VaR backtesting indicates improved calibration under asymmetric volatility modeling.
- Conditional Coverage tests support the importance of dynamic volatility specification for market risk estimation.

### Conclusion
Modeling asymmetry in volatility dynamics materially improves risk forecasting accuracy for equity index returns.
  
## How to run
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter lab
