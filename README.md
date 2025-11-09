#### GARCH-Forecasted-vs-Historical-Volatility-in-Mean-Variance-Optimization

## Project Overview

Compares GARCH-forecasted volatility versus historical volatility in mean-variance portfolio optimization using S&P 500 stocks. Implements monthly rebalancing with rolling window estimation to evaluate whether sophisticated volatility forecasting improves risk-adjusted returns through Sharpe ratios and drawdown analysis.

---

## Methodology

**1. Expected Returns Estimation**
- Uses Bayes-Stein shrinkage estimator to calculate expected returns from 2-month rolling windows
- Shrinks individual stock returns toward grand mean to reduce estimation error

**2. Volatility Estimation**

*Historical Approach:*
- Calculates standard deviation of log returns over 2-month estimation window
- Uses past volatility directly for next month's optimization

*GARCH Approach:*
- Fits GARCH(1,1) model with 2 years of historical data (450+ observations) per stock
- Forecasts one-day-ahead volatility using rolling window estimation
- Averages daily GARCH forecasts across target month

**3. Portfolio Construction**
- Constructs correlation matrix from 2-month returns window
- Builds covariance matrix: Σ = D × R × D (where D is diagonal volatility matrix, R is correlation)
- Optimizes portfolio weights using mean-variance optimization with volatility-based position bounds
- Rebalances monthly using optimized weights

---

## Key Features

- **Bayes-Stein Expected Returns**: Reduces estimation error through shrinkage toward mean
- **Dual Volatility Framework**: Parallel implementation of historical vs GARCH-forecasted volatility
- **Rolling Window Backtesting**: Monthly rebalancing from 2012 onwards with expanding data
- **GARCH(1,1) Forecasting**: Uses rugarch in R with parallel processing for 46 stocks

Here are your two results sections:

---

## Results/Findings

**1. BT Library Backtesting (2012-2025)**

**https://pmorissette.github.io/bt/**

Both portfolios delivered strong performance with over 2000% total returns. GARCH-based optimization showed marginally better risk-adjusted performance:
- **Sharpe Ratio**: GARCH (1.36) vs Historical (1.27) - 7% improvement
- **Max Drawdown**: GARCH (-26.0%) vs Historical (-30.1%) - better downside protection
- **CAGR**: Nearly identical at ~25% for both strategies
- **Calmar Ratio**: GARCH (0.98) vs Historical (0.83) - superior risk-adjusted returns

GARCH portfolio demonstrated lower volatility (17.9% vs 19.1%) and less extreme tail risk, with best/worst days of +7.8%/-9.6% compared to +10.0%/-12.9% for historical approach.

**2. Daily Returns Backtesting (With Transaction Costs)**

After accounting for realistic transaction costs, both strategies maintained strong performance:
- **Annualized Return**: Historical (24.04%) slightly outperformed GARCH (23.80%)
- **Sharpe Ratio**: GARCH (1.33) vs Historical (1.26) - 5.6% improvement in risk-adjusted returns
- **Max Drawdown**: GARCH (-25.6%) vs Historical (-30.4%) - consistent downside protection
- **Volatility**: GARCH (17.9%) vs Historical (19.2%) - lower portfolio risk

GARCH forecasting provided marginal but consistent improvements in risk management metrics, though absolute return differences remained minimal after transaction costs.

---
- **Performance Metrics**: Sharpe ratio comparison, cumulative returns, and drawdown analysis
- **Volatility-Based Position Limits**: Dynamic bounds inversely proportional to stock volatility

---

