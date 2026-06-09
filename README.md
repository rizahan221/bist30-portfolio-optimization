# BIST 30 Portfolio Optimization
### Optimal Portfolio Allocation in Borsa Istanbul (BIST 30): A Markowitz Mean-Variance and Monte Carlo Simulation Approach

**Author:** Rizahan Akgün  
**Advisor:** Derya Çoksak  
**Institution:** Yeditepe University, Department of Mathematics  
**Course:** MATH 491 — Senior Project, 2026

---

## Overview

This repository contains the full Jupyter Notebook implementation for the senior thesis on optimal portfolio allocation using BIST 30 stocks. The study applies Markowitz Mean-Variance optimization and Monte Carlo simulation to construct and evaluate three optimal portfolios against the BIST 30 benchmark index.

---

## Methodology

- **Training window:** January 2015 – December 2024 (10 years)
- **Backtesting window:** January 2025 – May 2026 (out-of-sample)
- **Universe:** 30 highly liquid BIST 30 constituents
- **Risk-free rate:** 18% (time-weighted avg. TCMB repo rate, training period)
- **Weight constraint:** Maximum 10% per asset (no short-selling)

### Three optimization objectives:
| Portfolio | Objective |
|---|---|
| Maximum Sharpe | Maximize excess return per unit of total risk |
| Minimum Variance | Minimize portfolio variance |
| Maximum Sortino | Maximize excess return per unit of downside deviation |

---

## What the Code Does

1. Downloads historical price data from Yahoo Finance (`yfinance`)
2. Computes log returns, expected return vector **μ**, and covariance matrix **Σ**
3. Runs 50,000 Monte Carlo simulations to map the Efficient Frontier
4. Solves exact QP optimization via SLSQP algorithm (SciPy)
5. Conducts out-of-sample backtest against XU030.IS benchmark
6. **COVID Robustness Check** — compares Pre-COVID (2015–2019) vs Full Window (2015–2024) weights using L1 turnover metric
7. **MAR Sensitivity Analysis** — runs Sortino optimization at MAR = 0%, 18%, 40% to demonstrate convergence artifact
8. **Estimation Error Sensitivity** — 500 return perturbations at ±1 standard error to assess weight fragility

---

## Requirements

```
python >= 3.9
yfinance
pandas
numpy
matplotlib
seaborn
scipy
```

Install with:
```bash
pip install yfinance pandas numpy matplotlib seaborn scipy
```

---

## Usage

Open the notebook directly in Jupyter or view it rendered on GitHub:

```
bist30_optimization.ipynb
```

The notebook is self-contained — run all cells top to bottom. All figures are saved to the working directory upon execution:
- `efficient_frontier_final.png`
- `correlation_heatmap_final.png`
- `weight_distribution_final.png`
- `cumulative_returns.png`
- `sortino_mar_divergence.png`
- `sensitivity_analysis.png`

> **Note:** The notebook requires an internet connection to download price data from Yahoo Finance. Runtime is approximately 5–10 minutes due to the 50,000-iteration Monte Carlo simulation and 500-perturbation sensitivity analysis.

---

## Key Results

| Strategy | ROI (2025–2026) | vs. Benchmark |
|---|---|---|
| Max Sharpe | 46.61% | −3.83% |
| Min Variance | **55.65%** | **+5.21%** |
| Max Sortino | 46.81% | −3.63% |
| BIST 30 Benchmark | 50.44% | — |

The Minimum Variance portfolio outperformed all strategies despite carrying the lowest in-sample Sharpe Ratio, consistent with the thesis finding that variance minimization offers more robust performance in high-inflation, high-interest-rate emerging market environments.

---

## License

This project is shared for academic purposes.  
Please cite the thesis if you use this code in your own work.
