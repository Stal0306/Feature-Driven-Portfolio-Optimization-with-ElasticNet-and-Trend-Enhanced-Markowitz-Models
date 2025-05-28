# Predictability-Driven Portfolio Optimization

## Overview

This project presents an advanced portfolio optimization framework that combines **ElasticNet regression** for feature-based stock predictability with the **Markowitz model** for optimal allocation. Our aim is to improve portfolio robustness by identifying stocks whose returns are more predictable and incorporating these insights into allocation decisions.


## Problem Statement

Traditional models focus on maximizing return or minimizing risk. We shift the focus to identifying **which stocks are most predictable**, and **which features best predict their returns**. These insights are used to:

- Score stocks based on recent trends of key predictive features.
- Adjust Markowitz portfolio optimization to prioritize trend-favorable stocks.

---

## Methodology

### Feature Extraction — ElasticNet Regression

- Features used:  
  `MACD`, `Bollinger Band Distance`, `MAD`, `Turnover Ratio`, `Market Cap`, `Interest Rate`, `Month`.
- Target: Next-month return.
- ElasticNet was chosen for its balance between **sparsity (L1)** and **stability (L2)**.
- Implementation: `scikit-learn`, trained on monthly stock data from Yahoo Finance.

### Trend Scoring

- Top predictive features (1, 2, or 3 per stock) are monitored over the last 3 months.
- Favorable trends (↑ momentum, ↓ volatility) boost trend scores.
- Scores normalized to range `[0.5, 1.0]`.

### Portfolio Optimization — Extended Markowitz Model

Objective function:

```
minimize: xᵀΣx − λ_trend(trend_scoresᵀx)
subject to: xᵀ1 = 1, xᵀμ ≥ target_return
```

- Baseline model: Classical Markowitz (risk minimization).
- Comparisons: Top-1, Top-2, Top-3 predictive feature-embedded models.

---

## Results Summary

| Portfolio Type | Total Return | Monthly Volatility |
|----------------|--------------|---------------------|
| Pure Markowitz | 15.67%       | 3.16%               |
| Top-1 Feature  | 20.09%       | 4.01%               |
| Top-2 Feature  | 22.34%       | 4.19%               |
| Top-3 Feature  | **22.93%**   | 4.09%               |

**Insight:** Embedding trend scores improves returns while only modestly increasing volatility.

---

## Tools and Technologies

- **Python Libraries**: `scikit-learn`, `pandas`, `numpy`, `scipy`, `ta`, `yfinance`
- **API**: Yahoo Finance (stock data)
- **Optimization**: `scipy.optimize.minimize`

---

## File Structure

```plaintext
Project_3.ipynb         # Jupyter Notebook with code implementation
Math_441__Project_3_Final.pdf   # Project report (complete write-up)
README.md               # You're here!
```

---

## Dataset

- 50 stocks including AAPL, MSFT, NVDA, AMZN, TSLA, JPM, etc.
- Data range: **January 2020 – March 2025** for modeling, April 2024 – March 2025 for testing.

