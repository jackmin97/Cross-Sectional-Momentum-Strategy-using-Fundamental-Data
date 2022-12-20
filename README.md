# Cross-Sectional-Momentum-Strategy-using-Fundamental-Data
In this notebook, we will consider the positive moves in fundamentals of the stocks, which is also a measure of strong past performance. We will create cross-sectional momentum strategy considering one of the fundamental factors. We will also combine fundamental momentum with price momentum to create and analyse cross-sectional momentum strategy.


### 1. Read price and volume data
We will read the pickle file, which stores the S&P 500 stocks price and volume data.

Filter stocks with high turnover

### 2. Read income statement data
We will read the CSV file, which stores the quarterly income statement data of filtered stocks.

### 3. Calculate the fundamental factor
We will use operating income growth as a fundamental factor to rank the stocks. Operating income growth is the change in the operating income this year compared to the same quarter last year.

We will create a new dataframe with the index as the unique values of the Publish date column of the quarterly_income_statement dataframe. We are creating this dataframe to store the value of operating income growth for each ticker.

We will run through the ticker column of quarterly_income_statement dataframe and calculate operating income growth for each ticker. We will store this in a fundamental_data dataframe which we created in the previous cell.

We need both operating income and stocks price to create a cross-sectional strategy. Therefore, we will keep only those tickers in the filtered_stocks_prices dataframe that have in fundamental_data dataframe.

We will create a new dataframe dates with index as filtered_stocks_prices index. We will then merge date dataframe with fundamental_data dataframe and then fill the NaN values with the forward fill method. We will use df.merge to do the same.

To make the number of rows in both filtered_stocks_prices and fundamental_data the same, we will keep only fundamental_data rows in the filtered_stocks prices dataframe.

### 4. Backtest CSMOM strategy
Now we have both price data and fundamental data in place, we will backtest cross-sectional momentum strategy. We will do this in two ways:

1. Fundamental momentum: We will rank the stocks based on the relative performance of the fundamental factor to generate trading signals.

2. Combined momentum: For the above strategy, we will calculate lookback returns and add skip period between the lookback and the holding days. We will recalculate the ranks by giving weight to both lookback returns rank and fundamental factor rank to generate trading signals.

### 4.1 Fundamental momentum strategy
Strategy logic:

1. Calculate the stock returns over the given holding period
2. Rank the stock returns based on the operating income growth
3. Long stocks with the highest 10 percentile operating income growth and short stocks with the lowest 10 percentile operating income growth
4. Include trading cost
5. Calculate the strategy returns

### 4.2 Combined momentum strategy
Strategy logic:

1. Calculate the stock returns over the given lookback and holding periods.
2. Rank the stocks based on the operating income growth and lookback returns.
3. Take a weighted average of both operating income growth and lookback returns ranks. We have assigned equal weights to both.
4. Long the highest 10 percentile stocks and short the lowest 10 percentile stocks.
5. Include the trading cost.
6. Calculate the strategy returns.

Combining price and fundamental momentum improves the strategy. The chart of the strategy shows that the strategy performed well and generated 87.48% returns for the same backtested period. The Sharpe ratio has also improved compared to the fundamental momentum strategy from 0.77 to 1.13. The strategy has a maximum drawdown of -7.69, which is approximately half of what has been observed for only fundamental momentum.
