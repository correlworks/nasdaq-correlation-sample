# Correlworks Nasdaq Large-Cap Correlation Sample

A sample export containing correlation-distribution summaries for 59 Nasdaq large-cap stocks, shared by Correlworks. Explore how correlation distributions differ across stocks rather than treating different tickers as proof of diversification.

## Files

- `correlworks_nasdaq_largecap_correlation_distributions.csv`: 59 stock records, 26 columns.

## Fields

- `ticker`, `name`: stock identifiers.
- `total_pairs`: number of observations represented by the distribution in the supplied export; not the number of pairs among these 59 stocks.
- `weak_share_pct`: supplied weak-correlation percentage. Numerically matches the sum of the six bins labelled -0.3 through 0.3, divided by `total_pairs`, rounded to one decimal place. Exact boundary conventions require source-methodology confirmation.
- `skewness`, `kurtosis`: supplied summary statistics; the kurtosis convention is not documented in the export.
- `bin_*`: 20 labelled intervals spanning -1.0 to 1.0. Each row's bin counts sum to `total_pairs`.

## Important limitations

This is a static sample, not a live market feed, pairwise correlation matrix, or investment recommendation. The original file does not document its observation dates, calculation window, sampling frequency, price/return basis, adjustment policy, comparison universe, or bin-generation method. Those details have not been independently verified. Do not interpret the publication date as the data's market as-of date or infer portfolio risk from these summaries alone. AMD and leveraged ETFs are not included. The supplied values are preserved without recalculation.

## Usage

```python
import pandas as pd

df = pd.read_csv("correlworks_nasdaq_largecap_correlation_distributions.csv")
print(df[["ticker", "weak_share_pct", "total_pairs"]].head())
bins = [c for c in df.columns if c.startswith("bin_")]
assert (df[bins].sum(axis=1) == df["total_pairs"]).all()
```

## Licensing and contact

A reuse license has not yet been specified by the owner. Public availability does not imply a CC0 dedication or a grant of unrestricted reuse rights. Contact Correlworks at founder@correlworks.com for methodology, licensing, or collaboration inquiries.
