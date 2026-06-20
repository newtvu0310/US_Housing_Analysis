# Housing Price Forecasting — SARIMAX with Market Exogenous Features

> End-to-end time-series analysis and forecasting of residential property prices using real transaction data and a SARIMAX model with automatically selected orders.

---

## Overview

This project builds a complete pipeline — from raw property sales data to a production-ready monthly price forecast — using Australian real estate transaction records sourced from Kaggle. Rather than treating price as a univariate series, the model incorporates **market composition signals** (bedroom mix, property type ratio, sales volume) as exogenous drivers, capturing how supply-side dynamics shape price trends.

---

## Why This Project Stands Out

- **Auto model selection** — uses `auto_arima` with AIC criterion across a full SARIMA grid (`max_p=3, max_q=3, max_P=2, max_Q=2`) to find the optimal order objectively, removing manual guesswork
- **Engineered exogenous features** — goes beyond univariate forecasting by building market-context variables from raw transactions: `avg_bedrooms`, `house_ratio` (house vs. unit share), `sales_count` — capturing demand mix and market activity
- **Seasonal awareness** — `m=12` seasonal component explicitly models annual property market cycles (spring/summer peak demand patterns)
- **Full production pipeline** — API data pull → cleaning → EDA → feature engineering → stationarity testing → model selection → forecast → evaluation, all in one reproducible notebook
- **Log-price transformation** — addresses right-skewed price distribution before modeling to improve residual normality

---

## Pipeline

**Step 1 — Data Acquisition**
- Downloaded via Kaggle API (`htagholdings/property-sales`) — reproducible with one command
- Dataset: residential property transactions with date, price, bedrooms, type, postcode

**Step 2 — Exploratory Data Analysis**
- Price distribution: histogram + KDE, boxplot by bedroom count
- Geographic analysis: median price by postcode
- Correlation heatmap: price vs. bedrooms
- Outlier handling: zero-bedroom entries replaced with `NaN` → dropped

**Step 3 — Time Series Feature Engineering**
- Resampled to **monthly frequency** using median price (robust to outliers)
- Built three exogenous variables per month:
  - `avg_bedrooms` — average bedroom size of transacted properties
  - `house_ratio` — share of houses vs. units sold (demand-mix signal)
  - `sales_count` — total transaction volume (market liquidity signal)
- Added 3-month centered rolling average for trend visualization

**Step 4 — Stationarity & Model Identification**
- ADF test on price series
- Log-price transformation applied to stabilize variance
- `auto_arima` searched full SARIMA(p,d,q)(P,D,Q)₁₂ space using AIC

**Step 5 — SARIMAX Modeling**
- Fitted with optimal order from auto_arima + exogenous features (X_train)
- 85/15 chronological train/test split (no data leakage)
- Forecast evaluated on held-out test period

**Step 6 — Evaluation**
- Metrics: RMSE, MAE, MAPE
- Visual: forecast vs. actual overlay on test window

---

## Tech Stack

| Library | Purpose |
|---------|---------|
| `pmdarima` | Auto ARIMA order selection |
| `statsmodels` | SARIMAX estimation, ACF/PACF, seasonal decomposition |
| `pandas` | Monthly resampling, feature engineering |
| `seaborn / matplotlib` | EDA visualizations, forecast charts |
| `scikit-learn` | Evaluation metrics (RMSE, MAE, MAPE) |
| `kaggle` | Programmatic dataset download |

---

## Dataset

- **Source:** [Kaggle — Property Sales](https://www.kaggle.com/datasets/htagholdings/property-sales)
- **Coverage:** Australian residential property transactions
- **Features:** `date`, `price`, `bedrooms`, `propertyType`, `postcode`
