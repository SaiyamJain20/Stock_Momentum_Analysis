# 📈 Stock Momentum Analysis & Portfolio Allocation Tool

A quantitative investment tool that applies price momentum strategies on S&P 500 stocks. The system uses Yahoo Finance data to compute historical returns, rank stocks by momentum metrics, and recommend portfolio allocations for investors.

## Overview

This project implements a quantitative investment strategy based on price momentum analysis of S&P 500 stocks. The tool uses live Yahoo Finance data to calculate historical returns, rank stocks by momentum metrics, and recommend portfolio allocations for a user-specified investment amount.


## Features

### Data Collection
- Pulls real-time stock data from the Yahoo Finance API
- Retrieves historical price data (up to 50 years)
- Gathers key metrics like current price and market capitalization

### Momentum Analysis
- Calculates price returns across multiple timeframes:
  - **1-year**
  - **6-month**
  - **3-month**
  - **1-month**
- Converts raw returns into percentile rankings
- Computes a composite **High-Quality Momentum (HQM) Score**

### Portfolio Allocation
- Accepts user input for total portfolio value
- Filters top momentum stocks
- Allocates equal weight across selected stocks
- Calculates the optimal number of shares to purchase for each


## Installation

Clone the repository and install dependencies:

```bash
pip install numpy pandas requests scipy yfinance
````

Ensure you have the required data file:

* `sp_500_stocks.csv` — Contains ticker symbols for S\&P 500 companies.


## Usage

1. Open and run the Jupyter notebook.
2. Execute the cells sequentially.
3. When prompted, input your total portfolio value.
4. Review the generated DataFrames:

   * `final_dataframe1`: Basic stock data with allocation recommendations
   * `hqm_dataframe`: Complete momentum analysis with HQM scores and allocations


## How It Works

### Step 1: Data Collection

* Iterates through each S\&P 500 stock, retrieving:

  * Current price
  * Market capitalization
  * Historical prices (up to 50 years)

### Step 2: Return Calculation

* Computes percentage returns for each stock:

  * **1-Year Return** = (Current Price / Price 252 trading days ago) - 1
  * **6-Month Return** = (Current Price / Price 126 trading days ago) - 1
  * **3-Month Return** = (Current Price / Price 63 trading days ago) - 1
  * **1-Month Return** = (Current Price / Price 21 trading days ago) - 1

### Step 3: Percentile Ranking

* Converts each return metric to a **percentile score (0-1)** relative to all stocks in the universe.

### Step 4: HQM Score Calculation

* Calculates the **HQM Score** as the arithmetic mean of all percentile scores for each stock.

### Step 5: Stock Selection

* Ranks stocks by HQM Score.
* Selects the **top 50 stocks** for inclusion in the portfolio.

### Step 6: Portfolio Allocation

* Divides the total portfolio value equally among the 50 stocks.
* Determines the number of shares to buy based on current stock prices.


## Results Interpretation

The final output includes:

* **Ticker**: Stock symbol
* **Price**: Current price
* **Number of Shares to Buy**: Recommended allocation
* **Return Metrics**: 1-year, 6-month, 3-month, and 1-month returns
* **Percentile Rankings**: Ranking of each stock relative to others
* **HQM Score**: Composite momentum score (higher is better)


## Dependencies

* `numpy` — Numerical calculations
* `pandas` — Data manipulation and analysis
* `requests` — API communication
* `scipy` — Statistical operations
* `yfinance` — Fetching financial data from Yahoo Finance


## Limitations

* Relies on Yahoo Finance data accuracy and availability.
* Historical performance does not guarantee future returns.
* Does not consider trading costs, taxes, or liquidity.
* Momentum strategies may underperform during market regime shifts.


## Future Enhancements

* Incorporate risk-adjusted return metrics (e.g. Sharpe ratio)
* Implement sector-based constraints
* Integrate fundamental data filters (P/E ratio, debt levels, etc.)
* Add backtesting capabilities
* Create portfolio performance visualizations