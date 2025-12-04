# portfolio-optimizer
A portfolio optimisation engine that downloads real financial data, computes returns and risk metrics, and identifies the Max Sharpe and Minimum Volatility portfolios. Automatically generates visualisations and export-ready allocation tables, making it ideal for analysts and finance students
# 📈 Portfolio Optimisation Tool  
*A Python-based portfolio optimiser using Modern Portfolio Theory, the Efficient Frontier, and real market data.*

This project builds an automated **portfolio optimisation engine** that:

- Downloads historical price data from Yahoo Finance  
- Computes annualised returns, volatility, and covariance  
- Generates thousands of random portfolios  
- Identifies the **Max Sharpe Portfolio**  
- Identifies the **Minimum Volatility Portfolio**  
- Compares against an **Equal Weight Benchmark**  
- Produces a full Excel/CSV allocation breakdown  
- Saves visualisations including the Efficient Frontier and allocation pie charts  

This tool is ideal for **investors, analysts, students, and quant enthusiasts** who want to explore portfolio construction using real market data.

---

## 🚀 Features

### ✔ 1. Automatic Data Download
Uses `yfinance` to fetch adjusted close prices for all tickers listed in your `tickers.csv`.

### ✔ 2. Cleans & Aligns Data
Handles missing data and ensures all tickers align correctly before optimisation.

### ✔ 3. Key Portfolio Outputs
The optimiser calculates:

- **Expected Return**
- **Volatility (Risk)**
- **Sharpe Ratio**
- **Optimal Asset Weights**
- **Total dollar allocation based on user investment amount**
- **Number of shares to buy for each asset**

### ✔ 4. Efficient Frontier Plotting
Automatically generates:

- Efficient frontier scatterplot  
- Max Sharpe portfolio highlight  
- Min Volatility portfolio highlight  

### ✔ 5. Exports Professional Outputs
The program saves:

| File | Description |
|------|-------------|
| `Portfolio_Optimisation_Results.csv` | Full allocation table with dollar amounts & share counts |
| `efficient_frontier.png` | Efficient frontier visualisation |
| `max_sharpe_allocation.png` | Pie chart for Max Sharpe |
| `min_vol_allocation.png` | Pie chart for Min Vol |
| `equal_weight_allocation.png` | Pie chart for Equal Weight portfolio |

---


