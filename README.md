# Volatility Forecasting & VaR Backtesting (DAX)

This project benchmarks classical volatility models against each other and evaluates the implications for market risk forecasting (VaR).  
We use daily DAX returns and perform rolling one-step-ahead volatility forecasts, then compute 1% and 5% VaR and validate it with standard backtests.

## Data
- Instrument: DAX index (`^GDAXI`)
- Frequency: daily
- Sample start: 2014-01-01
- Data source: Yahoo Finance (via `yfinance`)

## Pipeline
1. **Data & Stylized Facts**
   - log-returns, heavy tails (Jarque–Bera)
   - volatility clustering (ACF of |returns|)
   - ARCH effects (ARCH LM test)

2. **Volatility Models (Econometrics)**
   - GARCH(1,1)
   - EGARCH(1,1)
   - GJR-GARCH(1,1) (captures asymmetry / leverage effect)
   - Model selection via AIC/BIC

3. **Out-of-sample Forecast Evaluation**
   - Rolling one-step-ahead forecasts
   - Variance proxy: squared returns
   - Metrics: RMSE, QLIKE

4. **VaR & Backtesting**
   - Normal VaR with mean=0
   - Levels: 1% and 5%
   - Tests: Kupiec (POF), Christoffersen (Independence), Conditional Coverage

## Repository Structure
- `notebooks/` : end-to-end analysis notebooks
- `data/raw/` and `data/processed/` : raw prices and processed returns
- `results/tables/` : exported tables (metrics, backtests)
- `results/figures/` : saved figures (optional)

## Key Findings

- GJR-GARCH(1,1) outperformed symmetric GARCH in both AIC/BIC and volatility forecast accuracy.
- RMSE and QLIKE metrics suggest asymmetric volatility effects are economically significant.
- At the 1% VaR level, GJR-GARCH produced fewer exceedances and passed Kupiec and Christoffersen tests more consistently.
- Results support the importance of modeling leverage effects in equity index risk forecasting.
  
## How to run
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter lab
