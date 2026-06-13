# 📈 NVIDIA Stock Price Forecast | June 8–12, 2026

> A short-term stock price prediction project using an ensemble ML model — built as part of a data science course.

**Team:** BUSLIK &nbsp;|&nbsp; **Author:** Anastasiya Vikhrova

---

## 🤔 What is this?

I tried to predict NVIDIA's (NVDA) closing price for each day of the week **June 8–12, 2026** using two models combined together. The prediction was made *before* the week started, and then compared to what actually happened.

---

## ⚙️ How it works

I used an **ensemble of 2 models** (their outputs are blended based on past accuracy):

**1. GBM-Regime** (Geometric Brownian Motion + KMeans clustering)
- Detects whether the market is in a Bull / Sideways / Bear regime using 20-day rolling volatility, returns, and VIX
- Runs 10,000 Monte Carlo simulations using regime-specific parameters
- Returns the median predicted price

**2. Momentum**
- Looks at price changes over the last 5 and 10 days (weighted 70/30)
- Projects the trend forward with exponential decay so it fades over time

Weights between the two models are set automatically using **inverse-MAE from walk-forward validation** — no manual tuning.

**Data used:** NVDA daily close + `^VIX` (fear index), last 6 months, via `yfinance`

---

## 📊 Results

| Date | Day | 🔮 Predicted | ✅ Actual | Δ |
|------|-----|-------------|----------|---|
| Jun 8 | Mon | $204.26 | $208.64 | +$4.38 |
| Jun 9 | Tue | $203.72 | $208.19 | +$4.47 |
| Jun 10 | Wed | $203.29 | $200.42 | –$2.87 |
| Jun 11 | Thu | $202.91 | $204.87 | +$1.96 |
| Jun 12 | Fri | $202.62 | $205.19 | +$2.57 |

---

## 💬 Conclusion

The model got the **general range right** — NVDA did stay in the low $200s all week, which matched the prediction. The direction (slow consolidation, no big moves) was also correct.

Where it missed: actual prices were **$2–4 higher than predicted** on most days. The model detected a "Sideways" regime after the June 5 market drop and played it conservatively — but the market bounced back a bit stronger than expected. Wednesday was the exception, where the real price actually dipped below the forecast.

**What could make it better:** adding news sentiment, options flow data, or volume signals — pure price + VIX isn't enough to catch sentiment-driven rebounds after a sector shock.

---

## 🧰 Libraries

```
yfinance · numpy · pandas · matplotlib · scikit-learn · statsmodels
```
