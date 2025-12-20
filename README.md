# 📈 Portfolio Optimiser (Python) — Screening → Backtest → Frontier → Rebalanced Strategy Comparison

A modular portfolio research tool that:
1) downloads historical prices + volumes from Yahoo Finance (`yfinance`),
2) screens a user-supplied ticker universe for basic investability/data-quality,
3) runs a benchmark-relative backtest (Equal Weight),
4) simulates an efficient frontier “cloud” (no SciPy; random portfolios with constraints),
5) backtests multiple strategies with **monthly (configurable) rebalancing**, **turnover**, and **transaction-cost drag**.

> ⚠️ Educational project — not investment advice.

---

## ✅ What this project does (high level)

### Pipeline
- **Step 1 — Data Download:** pulls *Close* and *Volume* for tickers from `input/tickers.csv`
- **Step 2 — Screening:** removes tickers failing investability / data rules (price, liquidity, stale/zero returns)
- **Step 3 — Backtest (Equal Weight vs Benchmark):** rebalanced + cost-aware, includes turnover
- **Step 4 — Efficient Frontier (random cloud):** generates random portfolios with constraints and selects “best” points from the cloud  
- **Step 5 — Strategy Backtests vs Benchmark:** backtests frontier strategies (rebalanced + cost-aware)

---

## 📁 Project structure

Typical layout:

```text
project/
  main.py
  config.py
  data.py
  screening.py
  frontier.py
  backtest.py

  input/
    tickers.csv

  outputs/
    <run_id>/
      01_raw/
      02_screening/
      03_backtest/
      04_frontier/

🧰 Requirements

Python 3.10+ recommended

Packages:

numpy

pandas

yfinance

matplotlib (for frontier plot)

##**Install:**

pip install numpy pandas yfinance matplotlib

Configuration (important)

Open config.py. Key items:

Start date: backtest start

End date: the tool targets “yesterday” as last included date:

asof_date_inclusive = yesterday

yf_end_exclusive = today (because yfinance end= is exclusive)

Rebalancing frequency (applies in Step 3 + Step 5):

"M" = Monthly (recommended)

"Q" = Quarterly

"W" = Weekly

"A" = Annual

None = No rebalancing (buy-and-hold weights)

Transaction costs in bps (applies on rebalance dates only):

trading_cost_bps = 10.0 means 10 bps = 0.10% per unit of turnover

01_raw/

raw_close.csv — raw close prices for all requested tickers

raw_volume.csv — raw volumes for all requested tickers

02_screening/

universe_screening_report.csv — per-ticker screening results + reasons

close_filtered.csv — close prices for surviving tickers

volume_filtered.csv — volumes for surviving tickers

03_backtest/ (Equal Weight vs Benchmark)

backtest_daily_returns_assets_filtered.csv — daily returns of filtered universe

backtest_benchmark_close.csv — benchmark close series

backtest_timeseries_equal_vs_benchmark.csv — long format timeseries:

Date, Strategy, DailyReturn, Equity

Turnover, Cost, IsBenchmark

backtest_metrics_summary.csv — CAGR, AnnReturn, Vol, Sharpe, MaxDrawdown

04_frontier/

(Exact filenames depend on your frontier.py, but typically)

frontier_points.csv — random portfolio cloud points (ExpectedReturn/Vol/Sharpe)

frontier_optimal_weights.csv — weights for chosen strategies (e.g., MaxSharpe, MinVol, EqualWeight, TargetReturn_* if used)

frontier_expected_summary.csv — expected stats for those portfolios

efficient_frontier.png — scatter plot of the cloud + selected portfolios

05_strategies/ (multiple strategies vs benchmark)

strategies_timeseries.csv — long format timeseries per strategy:

DailyReturn, Equity, plus Turnover and Cost

strategies_metrics_summary.csv — performance metrics for each strategy vs benchmark

🧪 Screening (Step 2) explained

The screening is a basic “investability + data quality” filter.
Typical rules (from main.py):

adv_window = 60
Uses the last 60 trading days to estimate liquidity (ADV).

min_price = 0.01
Drops near-zero prices (often broken data / illiquid microcaps).

min_adv_dollars = 50_000
Drops tickers with low average dollar volume (illiquid).

max_zero_ret_frac = 0.20
Drops tickers with too many zero-return days (stale prices / bad series).

If a ticker is dropped, the screening report tells you why.

📉 Backtesting + rebalancing (Step 3 & 5)
What “monthly rebalancing” means

Weights drift as prices move. At each period-end (e.g., month-end trading day), the portfolio is reset to the target weights.

What is turnover?

Turnover measures how much you traded on rebalance dates.

We compute (on rebalance days):

turnover
=
∑
𝑖
∣
𝑤
𝑖
−
𝑤
drift
,
𝑖
∣
turnover=
i
∑
	​

∣w
i
	​

−w
drift,i
	​

∣

w = target weights

w_drift = weights just before rebalancing

Turnover is 0 on non-rebalance days.

How transaction costs are applied

If trading_cost_bps > 0, cost is applied only on rebalance days:

cost
=
turnover
×
bps
10000
cost=turnover×
10000
bps
	​


Portfolio value is reduced by that cost before rebalancing holdings.

✅ This cost drag is reflected in:

daily returns,

equity curve,

CAGR / Sharpe / drawdown metrics.

🧠 Efficient frontier (Step 4) explained (no SciPy)

This project does not use SciPy optimisation.

Instead:

It generates many random long-only portfolios (weights sum to 1),

Applies constraints like max_weight (e.g. 0.2),

Computes expected return / volatility / Sharpe using historical mean & covariance,

Selects:

MinVol: lowest volatility portfolio in the cloud

MaxSharpe: highest Sharpe portfolio in the cloud

EqualWeight: 1/N portfolio

TargetReturn (optional): lowest-vol portfolio near your target expected return

Because this is a random simulation, “optimal” portfolios are approximate and depend on num_portfolios and seed.

If your target-return portfolio is hard to match, increase:

num_portfolios (e.g., 50,000+), or

widen target_tolerance.

📌 Benchmark

By default, the benchmark used in backtests is the ASX 200 index ticker:

^AXJO

You can change it in main.py where Step 3/5 call:

benchmark_ticker="^AXJO"

benchmark_name="Benchmark"

📊 Power BI / SQL (using current outputs)

This project already exports tidy CSVs that are easy to ingest.

Power BI

In Power BI:

Get Data → Text/CSV

Load:

strategies_timeseries.csv (best for charts)

strategies_metrics_summary.csv (best for KPI cards/table)

Create visuals:

equity curve by Strategy

drawdown chart (derived)

turnover/cost over time

SQL (optional)

You can load the same CSVs into a database table (e.g., SQLite/Postgres/SQL Server) and query them:

strategies_timeseries.csv → strategy_returns

strategies_metrics_summary.csv → strategy_metrics

🛠 Troubleshooting
“No overlapping dates between strategy returns and benchmark returns”

Benchmark ticker might not have data for your date range.

Some tickers might have sparse/missing history.

“<2 tickers left after screening”

Relax screening thresholds:

lower min_adv_dollars

lower min_price

increase max_zero_ret_frac

Frontier looks inconsistent / “max sharpe not on the plot”

Ensure your frontier plot uses the same sharpe values as your selected portfolio.

If you select MaxSharpe from a separate run or different sample, you’ll see mismatches.

Increase num_portfolios for a denser cloud.

✅ Roadmap (future “industry” upgrades)

If you want to push further:

Walk-forward / out-of-sample testing (rolling train/test windows)

Shrinkage covariance (e.g. Ledoit–Wolf)

Deterministic optimiser (SciPy / cvxpy)

Sector constraints, max positions, rounding to shares, minimum trade sizes

Better data sources than yfinance
