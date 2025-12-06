# Market Risk Engine: VaR, CVaR & Stressed VaR (Monte Carlo Simulation)

This project computes **Value-at-Risk (VaR)**, **Expected Shortfall (CVaR)**, and **Stressed VaR** for a diversified portfolio using **Monte Carlo Simulation** and **historical stress scenarios**.

---

## 🚀 Project Overview

This risk engine uses 10 years of historical prices to estimate:

### ✔ Value-at-Risk (99%)  
Monte Carlo simulation of portfolio P&L distribution using:  
- Log returns  
- Mean vector & covariance matrix  
- 10,000 simulated scenarios

### ✔ Expected Shortfall (CVaR 99%)  
Tail-average loss beyond VaR threshold.

### ✔ Stressed VaR  
Default: 2007–2009 GFC window  
Fallback: Automatically selects worst volatility window using 252-day rolling covariance.

### ✔ Portfolio  
Equal-weight portfolio of:  
`SPY`, `BND`, `GLD`, `QQQ`, `VTI`

---

## 📊 Methodology

1. **Download price data (yFinance)**  
2. **Compute log returns**  
3. **Estimate mean (μ) and covariance (Σ)**  
4. **Simulate P&L distributions**  
5. **Compute VaR, CVaR, and Stress VaR**  
6. **Visualize distribution with risk thresholds**

---

## 🧮 Core Techniques Used

- Monte Carlo Simulation  
- Mean-variance estimation  
- Covariance modelling  
- Rolling volatility estimation  
- Tail-risk measurement  
- Stress testing  
- Data scraping with yFinance  
- Matplotlib for visualisation

---

## 📈 Output

- **VaR (99%)**
- **Expected Shortfall (CVaR 99%)**
- **Stressed VaR (GFC window or dynamic worst-vol window)**
- **Loss distribution plot** with VaR, ES, Stressed-VaR markers

---

## 🧠 Skills Demonstrated

- Quantitative risk modelling  
- Python for financial analytics  
- Portfolio risk estimation  
- Statistical simulation  
- Stress testing & tail risk  
- Data cleaning, indexing, covariance structures

---

## 🗂 Code

The complete code can be found in this repository.  
Below is a small excerpt of core functionalities:

```python
VaR = -np.percentile(scenario_returns, percentile)
ES = -scenario_returns[scenario_returns <= np.percentile(scenario_returns, percentile)].mean()
Stressed_VaR = -np.percentile(stress_returns, percentile)
