# portfolio-optimization
Implemented and backtested a few risk-based strategies as well as a classical Markowitz risk-retrun strategy

### Data Generation

We would like to compare our backtests with the american market(S&P 500), for this we got market-weights, for the last approximately 21 years, for some stocks of the S&P500.
One challenge I had is to use yahoo-finance as a database for getting the stocks I got weights for. Here I really had to handle with bad data-quality. 
We needed to find senseful ways to keep as many stocks as we can such that we can replicate the american market in a realistic way and to test our strategies on a lot of stocks.

```ruby
import pandas as pd
import yfinance as yf

#path CSV
csv_file_path = '/content/Tickers.csv'

#CSV to df
df_tickers = pd.read_csv(csv_file_path)

#extract ticker list
tickers = df_tickers['Tickers'].tolist()

#start and end date
start_date = '2002-12-31'
end_date = '2024-01-31'

#initialice empy frame for our data
df_prices = pd.DataFrame()

#list for tickers without data
failed_tickers = []

#load historical data for all tickers
for ticker in tickers:
    try:
        #take historical data for current ticker
        data = yf.download(ticker, start=start_date, end=end_date, progress = False)
        #get closing price
        close_prices = data['Close']
        #column name
        close_prices.name = ticker
        #add closing prices to the frame
        if df_prices.empty:
            df_prices = close_prices
        else:
            df_prices = pd.merge(df_prices, close_prices, left_index=True, right_index=True, how='outer')
    except Exception as e:
        print(f"The following ticker don't exists: {ticker}: {e}")
        failed_tickers.append(ticker)

#show failed tickers
print("Tickers which couldnt be found in yfinance:", failed_tickers)
#show finale frame
print(df_prices)
```
