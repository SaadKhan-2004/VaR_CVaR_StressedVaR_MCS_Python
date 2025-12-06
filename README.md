# 🧮 Market Risk Engine: VaR, CVaR & Stressed VaR (Python, Monte Carlo Simulation)

This project implements a complete **Market Risk Measurement Engine** that computes:

- **Value-at-Risk (VaR)**
- **Expected Shortfall (CVaR)**
- **Stressed VaR**  
- **Loss Distribution Simulation (Monte Carlo)**

using **10 years of historical data** and a **diversified 5-asset portfolio**.

---

## 📌 Project Summary

This project builds a 1-day portfolio risk engine using:

- **10 years (~2,500 days) of historical price data**
- **5-asset portfolio** — SPY, BND, GLD, QQQ, VTI  
- **10,000 Monte Carlo simulations**
- Multivariate **mean–variance modelling**
- A **dynamic stress-testing module**

It quantifies market risk during **normal** and **stress** conditions using VaR, CVaR, and Stressed VaR.

---

## 📊 Final Output (Actual Results)

| Metric | Value (99% Confidence) | Interpretation |
|--------|-------------------------|----------------|
| **VaR** | **$17,417** | Max loss expected 99% of the time under normal conditions |
| **CVaR / ES** | **$20,396** | Average loss in the worst 1% scenarios (≈ **17% deeper** loss than VaR) |
| **Stressed VaR** | **$30,421** | Tail risk under crisis-like volatility; **~75% higher** than normal VaR |

### 🔍 Key Insights
- **Stressed VaR increased from $17,417 → $30,421**  
  → **~75% jump**, indicating much higher downside risk in stressed markets.
- **CVaR exceeded VaR by ~17%**, capturing heavy-tail loss severity.
- Stressed VaR reflects conditions similar to the **2007–2009 financial crisis**.

---

## 🛠️ Methodology

### 1. **Data Collection**
- 10 years of daily closing prices downloaded via `yfinance`
- Assets: *SPY, BND, GLD, QQQ, VTI*  
- Log returns computed using:  
  \[
  r_t = \ln\left(\frac{P_t}{P_{t-1}}\right)
  \]

### 2. **Portfolio Construction**
- Equal weights across 5 assets  
- Portfolio mean (μ) and variance estimated using:  
  \[
  \mu_p = w^T\mu
  \]
  \[
  \sigma_p = \sqrt{w^T \Sigma w}
  \]

### 3. **Monte Carlo Simulation**
- 10,000 scenarios simulated using:  
  \[
  R = \mu_p + \sigma_p Z
  \]
  where \(Z \sim N(0,1)\)

### 4. **Risk Metrics**

#### ✔ **Value-at-Risk (VaR)**
Loss at the 99th percentile:  
\[
\text{VaR}_{0.99} = -\text{Percentile}(R, 1\%)
\]

#### ✔ **Expected Shortfall (CVaR)**
Average loss beyond VaR:  
\[
\text{CVaR} = -E[R \mid R \leq \text{VaR}]
\]

#### ✔ **Stressed VaR**
Two-stage logic:
1. Use 2007–2009 GFC window if available  
2. Otherwise, identify the **worst 252-day rolling volatility window** and compute stressed covariance matrix

---

## 📉 Loss Distribution Plot

A histogram of simulated losses with VaR, CVaR, and Stressed VaR markers.

