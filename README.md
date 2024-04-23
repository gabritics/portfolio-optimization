# portfolio-optimization
Implemented and backtested a few risk-based strategies as well as a classical Markowitz risk-retrun strategy

### Description

We compareed our backtests with the american market(S&P 500), for this we got market-weights, for the last approximately 21 years, for some stocks of the S&P500.
One challenge I had is to use yahoo-finance as a database for getting the stocks we got weights for. Here we really had to handle with bad data-quality. 
We needed to find senseful ways to keep as many stocks as we can such that we can replicate the american market in a realistic way and to test our strategies on a lot of stocks.
So we replicated the market, calculated some stats as well as for our different investment strategies, and compared the stats.

### How to build

We worked with a Colab Python Jupyter Notebook.
process: get Market weights and corresponding stockprices for the benchmark-> do the data cleaning(Find out how to handle with NaN's etc) -> caculate the returns, stats and replicate the graph, to validate that everything works -> code the different strategies (e.g. Equally weighted) and compare with the benchmark-> Backtest the different strategies by defininig a sliding window over time -> being creative from here, play with the numbers, the sliding windows, the volatility we accept...

### Replicated market
![alt text](SPX.png)

### Lehman brothers and covid crisis as top two max drawdowns
![alt text](MaxDrawDown.png)

### Replicated market key risk indicators 
| Performance Measure | Value (%) |
| ------------- | ------------- |
| Annualized Return | 9.0  |
| Annualized Volatility | 18.6  |
| Max Drawdown | -54  |
| Max Drawdown | -1.7  |
| Sharpe Ratio | 0.48  |

### Risk Based strategies (Static, only one Portfolio each)
## Equally Weighted Portfolio (EW)
This portfolio is calculated every trading day. It will assign the same weight to all the stocks currently available that day. It is the most rudimentary of the risk-based approaches. It aims to spread the risk out among as many stocks as possible without going into complex and costly variance analysis.

$\Large w_{EW}= \frac{\mathbb{1} \textbf{1}}{\textbf{1}^t \mathbb{1} \textbf{1}}$

$\textbf{1}$: is a vector of ones(with the stocks available at the date of optimization)

$\mathbb{1}$: Identity Matrix

![alt text](EW.png)
| Performance Measure | Value (%) |
| ------------- | ------------- |
| Annualized Return | 6.45  |
| Annualized Volatility | 21.56|
| Max Drawdown | -69.28  |
| Max Drawdown | -1.98  |
| Sharpe Ratio | 0.3  |

## Equally Risk Based portfolio (ERB)
The $\Lambda$ matrix has been calculated with the whole price dataset. The weights thus obtained have then been tested on the whole historical data. The $\Lambda^{-1}$ matrix is of diagonal structure. For each stock, the inverse of the standard deviation is present on the diagonal. It is then normalized by being divided by the sum for all stocks of the inverse standard deviation. This portfolio aims to reduce risk by penalizing standard deviation : the higher the standard deviation, the lower the weight used in the portfolio.

$\Large w_{ERB}=\frac{\Lambda^{-1}\textbf{1}}{\textbf{1}^t \Lambda^{-1} \textbf{1}}$

$\Lambda$: Diagonal matrix with standard deviation on the diagonal

![alt text](ERB.png)

| Performance Measure | Value (%) |
| ------------- | ------------- |
| Annualized Return | 6.32  |
| Annualized Volatility | 18.06|
| Max Drawdown | -58.40  |
| Max Drawdown | -1.65  |
| Sharpe Ratio | 0.35  |

## Inverse Variance Portfolio(IV)
The weights thus obtained have then been tested on the whole historical data. Note that the $\Lambda$ matrix here is the same as the one for the ERB portfolio. The $(\Lambda^{2})^{-1}$ matrix is of diagonal structure. For each stock, the inverse of the variance is present on the diagonal. It is then normalized by being divided by the sum for all stocks of the inverse variance. This portfolio aims to reduce risk by penalizing variance : the higher the variance, the lower the weight used in the portfolio. 

$\Large w_{IV}=\frac{(\Lambda^2)^{-1}\textbf{1}}{\textbf{1}^t (\Lambda^2)^{-1} \textbf{1}}$

![alt text](IV.png)

| Performance Measure | Value (%) |
| ------------- | ------------- |
| Annualized Return | 5.47  |
| Annualized Volatility | 13.36|
| Max Drawdown | -44.90  |
| Max Drawdown | -1.21  |
| Sharpe Ratio | 0.41  |


```ruby

```
