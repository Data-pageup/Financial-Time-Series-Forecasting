
# Financial Time-Series Forecasting: TESLA Daily Return Prediction

## Overview

This project implements a complete machine learning pipeline for forecasting **TSLA daily returns** using ten years of market data (2015–2024). It includes full data processing, feature engineering, exploratory analysis, model development, benchmarking, statistical validation, and trading strategy backtesting.
The analysis shows that a rigorously validated **Linear Regression model outperforms LightGBM, XGBoost, CatBoost, ARIMA**, and other advanced approaches in out-of-sample accuracy and stability. 

---

## Key Features

* 116 engineered features across lagged returns, rolling statistics, technical indicators, volume patterns, market context, and calendar attributes.
* Daily OHLCV data for TSLA, NVDA, AMD, ORCL, GOOG, and XLK ETF.
* Extensive exploratory data analysis covering volatility regimes, volume spikes, return distributions, and inter-asset behavior.
* Benchmarking of Linear Regression, ARIMA, LightGBM, CatBoost, XGBoost, MA5, and Naive baselines.
* Statistical validation using the **Diebold–Mariano test**.
* Backtesting of signal-based trading strategies including cumulative return, Sharpe ratio, drawdown, and win rate.
* Production-compatible pipeline design with fast inference and retraining capability.
 
---

## Dataset

* **Period:** 2015–2024
* **Frequency:** Daily
* **Source:** Yahoo Finance
* **Train/Test Split:** 2015–2022 (train), 2023–2024 (test) 

---

## Methodology

### 1. Data Preparation

* Missing value check
* Removal of corrupted volume entries
* ADF stationarity tests confirming all return series are stationary

### 2. Feature Engineering

Feature categories:

* Lagged returns (1–10 days)
* Rolling means and volatility windows
* RSI, MACD, SMA (technical indicators)
* Volume-based features and spike detection
* Sector ETF context (XLK)
* Calendar features (DOW, month, quarter)
  Total: **116 features**. 

### 3. Model Development

Models tested:

* Baselines: Naive, MA5, Linear Regression
* Advanced: LightGBM, CatBoost, XGBoost, ARIMA(2,1,2)
* 5-fold time-series cross-validation
* Grid search tuning (for GB models)

### 4. Evaluation

* RMSE, MAE, directional accuracy
* Residual analysis and stability checks
* Diebold–Mariano significance test
* Backtesting with P&L, Sharpe ratio, max drawdown

---

## Results

### Model Performance

* **Best Model:** Linear Regression

  * RMSE: **0.0368**
  * MAE: **0.0269**
  * Statistically superior to LightGBM (DM p-value = 0.000081)
* Cross-validation stability: RMSE ≈ 0.0399 ± 0.0087
* LightGBM RMSE: 0.0397
* ARIMA RMSE: 0.0369 (fails to capture volatility spikes)


### Trading Outcome

* LR strategy cumulative return: **214.79%**
* Buy-and-hold benchmark: **286.13%**
* Win rate: ~47%
* Strong magnitude prediction, weak directional prediction


---

## Limitations

* Single-asset scope (TSLA only)
* Directional accuracy remains near-random despite good magnitude prediction
* No macroeconomic or regime-switching features
* Backtests assume zero transaction costs

---

## Future Work

* Multi-asset generalization (NVDA, AMD, GOOG, ORCL)
* Macro indicators (VIX, interest rates, yield curve)
* Regime detection (Markov switching)
* Position sizing based on predicted volatility
* Ensembles with uncertainty estimation




