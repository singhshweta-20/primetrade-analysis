# Trader Performance vs Market Sentiment
### PrimeTrade.ai — Data Science Intern Assignment

Analysis of how Bitcoin Fear/Greed sentiment relates to trader behavior
and performance on Hyperliquid.

---

## Setup

1. Clone the repo
   git clone https://github.com/singhshweta-20/primetrade-analysis
   cd primetrade-analysis

2. Install dependencies
   pip install -r requirements.txt

3. Download datasets and place in /data
   - Fear/Greed index: https://drive.google.com/file/d/1PgQC0tO8XN-wqkNyghWc_-mnrYv_nhSf
   - Hyperliquid trades: https://drive.google.com/file/d/1IAfLZwu6rJzyWKgBToqwSmmVYU6VbjVs

4. Run the notebook
   jupyter notebook notebooks/analysis.ipynb

---

## Project Structure

primetrade-analysis/
├── data/                        # raw datasets (not pushed to git)
├── notebooks/
│   └── analysis.ipynb           # main analysis notebook
├── charts/                      # output charts and tables
├── README.md
└── requirements.txt

---

## Datasets

| Dataset | Records | Date Range |
|---------|---------|------------|
| Bitcoin Fear/Greed Index | 2,644 daily records | Feb 2018 – May 2025 |
| Hyperliquid Trader Data | 211,224 trades | May 2023 – May 2025 |

Usable overlap: May 2023 – May 2025 (732 sentiment days, 32 unique traders)

---

## Analysis Summary

### Methodology

Filtered trades to core directions (Open/Close Long/Short), kept only
closed trades with realized PnL (84,626 trades). Built daily per-trader
metrics — PnL, win rate, trade size, long/short ratio — then joined with
sentiment. Collapsed 5 sentiment classes to 3 (Fear/Neutral/Greed).

Traders segmented by trading frequency, performance consistency, and
position size. No leverage column in data — trade size used as proxy.

---

### Insights

**1. Fear days are more profitable — consistently**
Traders made 53% more on Fear days ($826 median) than Greed days ($540).
Win rate also higher (87% vs 84%). Market panic creates cleaner entry
points for the traders in this dataset.

**2. Traders fade the market, not follow it**
On Fear days: smaller positions ($1,801), more long-biased (48.3%).
On Greed days: larger positions ($2,047), more short-biased (44.9%).
Nobody here is momentum trading.

**3. Size matters more than frequency on Fear days**
Medium-sized traders ($1,710–$4,856) made $4,005 on Fear vs $739 on
Greed — a 5.4x gap. Fewer, better-sized trades beat high frequency on
the days that matter most.

---

### Strategy Recommendations

**Strategy 1 — Fear days: go long, size medium, be selective**
When sentiment hits Fear or Extreme Fear, go contrarian — long bias,
medium position sizes, don't overtrade. Every segment shows a PnL
premium on these days.

**Strategy 2 — Greed days: pull back and fade**
Greed days have the worst median PnL. Reduce size, lean short or neutral,
don't chase the move.

> Note: 32 traders in dataset — patterns are clear but sample is small.
> No leverage data available for direct analysis.

---

## Output Files

| File | Description |
|------|-------------|
| charts/01_performance_by_sentiment.png | PnL, win rate, loss rate by sentiment |
| charts/02_behavior_by_sentiment.png | Trade size, volume, frequency, L/S ratio |
| charts/03_segments_vs_sentiment.png | All 3 segments vs sentiment |
| charts/05_strategy_evidence.png | Strategy recommendation evidence |
| charts/table_01_performance_by_sentiment.csv | Q1 stats table |
| charts/table_02_behavior_by_sentiment.csv | Q2 stats table |
| charts/table_03_freq_segment.csv | Segment 1 stats |
| charts/table_03_winner_segment.csv | Segment 2 stats |
| charts/table_03_size_segment.csv | Segment 3 stats |
| charts/table_04_trader_stats.csv | Per-trader overall stats |