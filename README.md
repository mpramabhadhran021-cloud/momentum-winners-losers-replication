# Momentum: Replicating Jegadeesh & Titman (1993)

A simple replication of Jegadeesh and Titman (1993), *Returns to Buying Winners and Selling Losers*.

The paper studies whether stocks that performed well in the past continue to perform well over the following few months. The authors find positive momentum returns for 3- to 12-month holding periods. citeturn0search0

## What I do

I use monthly Yahoo Finance data for a group of large US stocks from 1995–2024.

- `01_replication.ipynb` — main replication
- `02_extension.ipynb` — simple follow-up analysis

Because CRSP data are not freely available, this is **not an exact reproduction** of the original paper.

## Main replication

I follow the basic idea:

1. Calculate past 3-, 6-, 9-, and 12-month returns.
2. Rank stocks into portfolios.
3. Buy the winners and sell the losers.
4. Hold the portfolios for 3, 6, 9, or 12 months.
5. Use overlapping portfolios.
6. Calculate Newey-West t-statistics.
7. Compare the results with the original paper.

I use quintiles rather than deciles because the stock universe is much smaller than the original CRSP sample.

## What I find

For the 1995–2024 sample, the raw momentum result is much weaker than in the original paper. The 6-month formation / 6-month holding strategy is close to zero or negative in this sample.

I also check whether the result changes when I use terciles, quintiles, or deciles and whether winner and loser portfolios have different market betas.

## Extension

The second notebook asks whether momentum returns are especially weak during sharp market rebounds.

I:

- split the sample into five periods,
- identify large market-rebound months,
- compare momentum returns in those months with other months,
- check portfolio betas,
- and change the rebound thresholds as a simple robustness check.

This is an exploratory extension rather than a new momentum model.

## Limitations

- The original paper uses CRSP; I use Yahoo Finance.
- The stock universe is much smaller.
- The universe is based on currently available tickers, so survivorship bias is possible.
- I use quintiles for the main specification.
- I do not include transaction costs.
- The extension uses simple thresholds chosen for the analysis.

The results should therefore be viewed as a **student replication exercise**, not an exact reproduction.

## Reference

Jegadeesh, N. and Titman, S. (1993), *Returns to Buying Winners and Selling Losers: Implications for Stock Market Efficiency*, The Journal of Finance, 48(1), 65–91. citeturn0search0
