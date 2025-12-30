# 📈 Portfolio Optimiser (Python) — Screening → Backtest → Frontier → Rebalanced Strategy Comparison

A modular portfolio research tool that:
1) downloads historical prices + volumes from Yahoo Finance (`yfinance`),
2) screens a user-supplied ticker universe for basic investability/data-quality,
3) runs a benchmark-relative backtest (Equal Weight),
4) simulates an efficient frontier “cloud” (Includes SciPy; random portfolios with constraints),
5) backtests multiple strategies with **monthly (configurable) rebalancing**, **turnover**, and **transaction-cost drag**.

> ⚠️ Educational project — not investment advice.

---

## ✅ What this project does (high level)

### Pipeline
- **Step 1 — Data Download:** pulls *Close* and *Volume* for tickers from `input/tickers.csv`
- **Step 2 — Screening:** removes tickers failing investability / data rules (price, liquidity, stale/zero returns)
- **Step 3 — Backtest (Equal Weight vs Benchmark):** rebalanced + cost-aware, includes turnover
- **Step 4 — Efficient Frontier (random cloud):** generates random portfolios with constraints and selects “best” points from the cloud and best possible mathemitacally with the contranints 
- **Step 5 — Strategy Backtests vs Benchmark:** backtests frontier strategies (rebalanced + cost-aware)

---

### How to run
1. Install requirements.txt
2. python main.py

### Outputs

**1. Raw**
   
	a. All of the closing share price of all stocks (raw_close.csv)

	b. All of the volume of stock trades (raw_volumes.csv)

**2. Screening**
   
	a. All of the closing share prices of the filtered stocks (close_fitered.csv)

	b. All of the volume of the filtered stock trades (volume_filtered.csv)

	c. The report of which stocks got filtered or not and why (universe_screening_report.csv)

<img width="894" height="505" alt="image" src="https://github.com/user-attachments/assets/f9aa1c51-50ca-4ed6-a616-42dd583e0bd5" />

**3. Backtest**
   
	a. The benchmark backtest prices (backtest_bechmark_close.csv)

	b. A backtest of all the filtered assets (backtest_daily_returns_assets_filtered.csv)

	c. A backtest comparison of the equal weighted and benchmark fitted for Power BI export (backtest_timeseries_equal_vs_benchmark.csv)

	d. A metric summary of the equal weighting and benchmark (frontier_optimal_weights.csv)

<img width="561" height="73" alt="image" src="https://github.com/user-attachments/assets/11d40470-efbf-4918-a263-2af0a13a3950" />

**4. Frontier**
   
   a. The different points used for the efficient frontier plot for the optimal weighting of portfolio (frontier_points.csv)
   
   b. The efficient frontier chart (efficient_frontier.png)
   
   c. The summary of the different method both scipy and efficient frontier (frontier_expected_summary.csv)
   
<img width="321" height="193" alt="image" src="https://github.com/user-attachments/assets/ba164a66-347e-4fb2-b843-5ad65ce66e85" />

   d. The optimal weights of the portfolio in order to achieve the desired strategy (frontier_optimal_weights.csv)
   
<img width="641" height="433" alt="image" src="https://github.com/user-attachments/assets/9f61dfb2-93d0-4379-8619-b6e83a6f62bc" />

**5. Strategies**

	a. A summery of the metrics of each strategy backtest (strategies_metrics_summary.csv)

<img width="561" height="217" alt="image" src="https://github.com/user-attachments/assets/99f6494e-ae63-4dac-9944-9e41abecaad3" />

	b. The timeseries of each strategy with the rebalance cost ready for power BI export (strategies_timeseries.csv)





