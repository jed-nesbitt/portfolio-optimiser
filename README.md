# portfolio-optimizer

A Python + Power BI portfolio optimisation project that downloads real market data, simulates thousands of portfolios (Modern Portfolio Theory), and outputs **Max Sharpe / Min Vol / Max Return / Equal Weight** strategies with export-ready tables and a Power BI dashboard.

---

## 📈 Portfolio Optimisation Tool

A Python-based portfolio optimiser using **Modern Portfolio Theory**, the **Efficient Frontier**, and real market data.

This project builds an automated portfolio optimisation engine that:

- Downloads historical price data from Yahoo Finance
- Computes annualised returns, volatility, and covariance
- Generates thousands of random portfolios
- Identifies:
  - **Max Sharpe Portfolio**
  - **Minimum Volatility Portfolio**
  - **Maximum Return Portfolio**
  - **Equal Weight baseline**
- Backtests each strategy (constant weights) to produce equity curves
- Exports clean CSVs for Power BI + saves charts (frontier + allocation pies)

This tool is ideal for investors, analysts, students, and quant enthusiasts who want to explore portfolio construction using real market data.

---

## 🚀 Features

✅ **1. Automatic Data Download**  
Uses `yfinance` to fetch adjusted close prices for all tickers listed in `tickers.csv`.

✅ **2. Data Cleaning & Alignment**  
Forward/back fills missing values and ensures tickers align correctly before optimisation.

✅ **3. Portfolio Optimisation (Monte Carlo)**  
Simulates thousands of random weight portfolios to approximate the efficient frontier.

✅ **4. Strategy Outputs**  
For each strategy, the tool produces:
- expected return
- volatility
- Sharpe ratio
- optimal weights
- dollar allocation (based on your investment amount)
- shares to buy (based on latest price)

✅ **5. Visualisations**  
Automatically generates:
- Efficient frontier scatterplot (Sharpe as colour)
- Allocation pie charts for key strategies

✅ **6. Power BI Dashboard Exports**  
Exports tidy tables designed for Power BI (long-form tables + metrics + frontier points).

---

## 📦 Files generated

### Core outputs
| File | Description |
|---|---|
| `Portfolio_Optimisation_Results.csv` | Human-friendly allocation table with weights, $ amounts, and shares |
| `efficient_frontier.png` | Efficient frontier scatter plot with optimal portfolios highlighted |
| `max_sharpe_allocation.png` | Allocation pie chart (Max Sharpe) |
| `min_vol_allocation.png` | Allocation pie chart (Min Volatility) |
| `max_return_allocation.png` | Allocation pie chart (Max Return) |
| `equal_weight_allocation.png` | Allocation pie chart (Equal Weight) |

### Power BI exports (`powerbi_exports/`)
| File | Description |
|---|---|
| `pb_allocations_long.csv` | Allocations by **Ticker × Strategy** (Weight, DollarAlloc, Shares) |
| `pb_portfolio_timeseries.csv` | DailyReturn + EquityCurve + EquityCurve_$ by **Date × Strategy** |
| `pb_metrics.csv` | Realised metrics by strategy (CAGR, Vol, Sharpe, MaxDrawdown) |
| `pb_frontier_points.csv` | Efficient frontier cloud (Volatility, ExpectedReturn, Sharpe) |
| `pb_ticker_map.csv` | Ticker → Company mapping |

---

## 🧠 Key definitions (what the dashboard shows)

- **CAGR**: annualised growth rate of the strategy’s equity curve  
- **Vol**: annualised volatility (risk) from daily returns  
- **Sharpe**: risk-adjusted return vs risk-free rate  
- **Max Drawdown**: worst peak-to-trough decline of the equity curve

---

## 🛠️ How to run

### 1) Install dependencies
```bash
pip install numpy pandas matplotlib yfinance

⚠️ Disclaimer

This project is for educational purposes only and does not constitute financial advice. Past performance does not guarantee future results.

Author
Jed Nesbitt

::contentReference[oaicite:0]{index=0}
