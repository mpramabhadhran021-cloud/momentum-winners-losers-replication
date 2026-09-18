# Momentum in US Equities: Replicating Jegadeesh & Titman (1993)

A master's-level portfolio project that (1) replicates the core result of Jegadeesh, N. and
Titman, S. (1993), *"Returns to Buying Winners and Selling Losers: Implications for Stock
Market Efficiency,"* Journal of Finance 48(1), 65-91, and (2) adds a small, manageable
extension that grows directly out of the original paper's own robustness analysis.

## What's here

| File | Purpose |
|---|---|
| `01_replication.ipynb` | Reproduces the paper's headline relative-strength ("momentum") result on ~90-115 large-cap US stocks, 1995-2024, using free Yahoo Finance data. |
| `02_extension.ipynb` | Extension: tests whether the strategy still suffers sharp, concentrated losses during market rebounds — the same "crash" mechanism J&T document in their own 1927-1940 back-test (their Section VII) — using modern data. |
| `data/` | Created automatically by Notebook 1; holds a cached CSV of the downloaded monthly prices so Notebook 2 doesn't need to re-download. |
| `requirements.txt` | Python dependencies. |

## How to run

```bash
pip install -r requirements.txt
jupyter notebook
```

1. Run `01_replication.ipynb` **top to bottom first**. It needs an active internet connection
   to download monthly price data via `yfinance`; the result is cached to
   `data/monthly_adj_close.csv` so it only needs to be downloaded once.
2. Run `02_extension.ipynb`. It reads the cached CSV from step 1 and does not need internet
   access on its own.

## One-paragraph summary

The original paper shows that buying stocks with strong returns over the past 3-12 months and
selling stocks with weak returns over the same window earns significant positive returns over
the following 3-12 months, and that this is not explained by systematic (market) risk. Notebook
1 reproduces this using a smaller, free, large-cap-only universe (quintiles instead of deciles,
given the smaller cross-section), following the same overlapping-portfolio construction and
using Newey-West significance tests. On raw returns, the momentum effect does not replicate in
this sample — every formation/holding combination comes out flat-to-negative. Notebook 2 shows
why: momentum was positive in 1994-2000 but negative in 2000-2012, driven largely by a handful
of sharp market-rebound months (2001, 2002, 2009) where the higher-beta loser portfolio gets
hurt badly. That crash pattern is the same mechanism J&T themselves document in their own
1927-1940 back-test — this project's extension checks whether it still shows up in a modern,
independent sample, and finds that it does.

## Key limitations (see the notebooks for full discussion)

- **Survivorship bias**: the universe is currently-listed, large-cap stocks only, which J&T's
  own results suggest *understates* the momentum effect.
- **Quintiles, not deciles**, due to a much smaller cross-section than the original CRSP
  universe. Tested directly in Notebook 1 (Section 9b) and ruled out as the reason the raw
  result comes out negative.
- **Yahoo Finance adjusted close** is a free proxy for CRSP total returns, not an exact match.
- No transaction-cost analysis and no skip-week (Panel B) variant — left out to keep the
  project a manageable, single-strategy, single-universe exercise appropriate for a master's
  application portfolio.
- The raw momentum return did not replicate at the full-sample level; only the risk-adjusted
  (CAPM alpha/beta) picture points the same direction as the original paper, and even that is
  not statistically significant in this small sample. See Notebook 1, Section 11 for the full,
  honest discussion of this.

## Citation

Jegadeesh, N. and Titman, S. (1993). Returns to Buying Winners and Selling Losers:
Implications for Stock Market Efficiency. *The Journal of Finance*, 48(1), 65-91.
