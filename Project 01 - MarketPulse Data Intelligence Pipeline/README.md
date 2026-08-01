# MarketPulse — Multi-Source Data Intelligence Pipeline

An automated data pipeline that collects live financial/market data from a public API and cross-references it with scraped news headlines to detect correlation patterns and flag anomalies in real time. The system reconciles mismatched timestamps and formats between two independent live sources using Pandas, computes rolling averages and volatility metrics, and applies rule-based logic to surface actionable signals — all structured around the CRISP-DM methodology.

## Project Overview

Sudden stock price movements are often linked to news events, but the relationship isn't always obvious in real time. This project investigates whether spikes in news headline volume coincide with significant price changes for a given stock (IBM), using a fully transparent, rule-based approach rather than a black-box model.

## Data Sources

- **Price data:** Daily OHLCV (open, high, low, close, volume) data for IBM, pulled from the Alpha Vantage API (last 100 trading days).
- **News data:** Headline data from Yahoo Finance's public RSS feed for the IBM ticker.

## Methodology (CRISP-DM)

1. **Business Understanding** — Can news activity help explain sudden price swings?
2. **Data Understanding** — Explored both sources independently, noting their differing time coverage.
3. **Data Preparation** — Reconciled the two sources by date, filling in zero-headline days rather than dropping them.
4. **Modeling** — Calculated 5-day rolling averages, volatility, and daily percent price change; applied a rule-based anomaly flag (price move > 3% AND headline count > 2).
5. **Evaluation** — Reported findings honestly, including cases where no anomalies were detected.
6. **Recommendations** — Suggested extending the news collection window for more robust future analysis.

## Tech Stack

- Python
- Pandas
- REST APIs (Alpha Vantage)
- RSS Feed Parsing (feedparser)
- Jupyter Notebook

## Files in This Folder

| File | Description |
|---|---|
| `MarketPulse_Analysis.ipynb` | Full analysis notebook, structured using CRISP-DM |
| `price_data_raw.csv` | Raw daily price data (OHLCV) from Alpha Vantage |
| `headlines_raw.csv` | Raw scraped headlines from Yahoo Finance RSS feed |
| `merged_data.csv` | Price and headline data merged on date |
| `final_analysis.csv` | Final dataset with rolling stats, volatility, and anomaly flags |

## Key Skills Demonstrated

- Data integration from heterogeneous, live sources
- Time-series alignment and reconciliation
- Rolling statistics and rule-based anomaly detection
- Business-driven analytical framing (CRISP-DM)
- Transparent, honest reporting of findings (including negative/null results)

## Notes & Limitations

The news data reflects only a limited recent window (a few days), while price data spans 100 trading days. This is acknowledged directly in the notebook's Data Understanding and Evaluation sections, and is suggested as an area for future improvement (e.g., accumulating headlines daily over a longer period via a scheduled script).
