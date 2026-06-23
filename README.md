# VIX Volatility Forecasting with Basis Function Regression

Forecasting the CBOE VIX index using four basis function regression models, with hyperparameter tuning via validation set and long-range forecasts through 2028.

---

## Overview

The VIX ("fear index") measures implied volatility in S&P 500 options and is a core signal in risk management, derivatives pricing, and macro analysis. This project builds and compares four non-linear regression models to forecast VIX levels from historical annual data, selects the best-performing model via systematic hyperparameter tuning, and generates out-of-sample forecasts for 2026–2028.

---

## Models Compared

| Model | Description |
|---|---|
| Piecewise Constant | Step-function basis with k knots |
| **Piecewise Linear** | **Linear spline with k knots — best performer** |
| Radial Basis Function (RBF) | Gaussian kernels centred at k locations |
| Laplace Basis Function | Laplace kernels centred at k locations |

---

## Methodology

**Data split:** 80% train+validation / 20% test (train/val split 75/25 within trainval), `random_state=35`

**Hyperparameter tuning:** k searched across range 1–30 for each model; best k selected by lowest validation MSE

**Final evaluation:** Winning k re-fitted on full train+val set, evaluated on held-out test set

**Forecasting:** Optimal model extended to 2026–2028 via closed-form normal equations (β̂ = (ΦᵀΦ)⁻¹Φᵀy)

---

## Results

**Best model: Piecewise Linear Regression, k = 22**

| Model | Test MSE |
|---|---|
| Piecewise Constant | — |
| **Piecewise Linear** | **31.37** |
| Radial Basis Function | — |
| Laplace Basis Function | — |

**VIX Forecasts (Piecewise Linear, k = 22):**

| Year | Forecasted VIX |
|---|---|
| 2026 | *(model output)* |
| 2027 | *(model output)* |
| 2028 | *(model output)* |

> Note: Replace *(model output)* with actual printed values after running the notebook.

---

## Repo Structure

```
vix-forecasting/
├── vix-volatility-forecasting.ipynb  # Main notebook
├── vix.csv                           # Source data (CBOE VIX annual)
├── requirements.txt
└── README.md
```

---

## Skills Demonstrated

- Python (NumPy, Pandas, Scikit-learn, Matplotlib)
- Basis function regression and design matrix construction
- Train / validation / test split methodology
- Hyperparameter search and model selection
- Out-of-sample forecasting
- Financial time series (CBOE VIX)

---

## Requirements

```
numpy
pandas
scikit-learn
matplotlib
```

Install with:

```bash
pip install -r requirements.txt
```

---

## Context

Built as part of BUSS6002 — Data Analytics for Business at the University of Sydney (2025). The CBOE VIX index is a widely-used proxy for market-implied risk and appears in volatility trading, portfolio hedging, and risk model calibration across buy-side and sell-side finance.
