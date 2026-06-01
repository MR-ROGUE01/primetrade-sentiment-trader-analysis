# Bitcoin Market Sentiment × Trader Performance Analysis
### Primetrade.ai Data Science Assignment

---

## Overview

This project explores the relationship between **Bitcoin market sentiment** (Fear & Greed Index) and **real trader performance** on the Hyperliquid derivatives platform. The goal is to uncover actionable patterns that can inform smarter trading strategies.

---

## Datasets

| Dataset | Source | Size | Description |
|---|---|---|---|
| `se.csv` | Hyperliquid | ~211,000 rows | Historical trader data — accounts, coins, PnL, fees, direction, leverage |
| `fear_greed_index.csv` | Alternative.me | ~2,700 rows | Daily Fear & Greed Index (0–100) with classification labels (2018–2025) |

---

## Project Structure

```
📁 root
├── 01.ipynb                  # Main analysis notebook
├── se.csv                    # Trader data
├── fear_greed_index.csv      # Sentiment data
└── README.md
```

---

## How to Run

```bash
# 1. Install dependencies
pip install pandas numpy matplotlib seaborn scipy

# 2. Place both CSV files in the same folder as the notebook

# 3. Open and run all cells
jupyter notebook 01.ipynb
```

---

## Analysis Sections

The notebook is structured in 9 sections:

1. **Load & Inspect Data** — Shape, dtypes, nulls, duplicates
2. **Data Preparation** — Date parsing, merging datasets, isolating closed trades
3. **Sentiment Overview** — Distribution of sentiment categories + index over time
4. **Distribution Analysis** — PnL and trade size distributions by sentiment
5. **Performance by Sentiment** — Avg PnL, win rate, trade count per sentiment group
6. **Correlation Analysis** — Pearson correlation between Fear & Greed value and daily PnL
7. **Trading Activity** — Top coins, most active accounts, win/loss ratio
8. **Statistical Test** — Kruskal-Wallis test for significance across sentiment groups
9. **Conclusions & Strategy Recommendations**

---

## Key Findings

**1. Fear is the best time to trade — counterintuitively**

| Sentiment | Avg PnL | Win Rate | Trades |
|---|---|---|---|
| **Fear** | **$126.41** | **88.6%** | 26,481 |
| Extreme Fear | $95.25 | 80.0% | 9,358 |
| Neutral | $68.32 | 83.0% | 15,843 |
| Greed | $69.17 | 76.1% | 19,320 |
| Extreme Greed | $46.23 | 87.4% | 13,683 |

Traders in this dataset earn the most and win most often during **Fear** — not Greed. This suggests experienced traders enter selectively during fear, buying dips with high conviction.

**2. Greed = overtrading**
Greed periods show the lowest win rate (76.1%), consistent with FOMO-driven entries reducing trade quality.

**3. Statistically significant result**
Kruskal-Wallis test: **H = 738.43, p < 0.000001** — the PnL differences across sentiment groups are not random.

**4. Weak negative correlation with index value**
Pearson **r = −0.25, p < 0.000001** — as the greed index rises, aggregate daily PnL slightly decreases. Effect is real but small (r² ≈ 6.3%).

**5. HYPE dominates trading activity**
~32% of all trades are in Hyperliquid's own token (HYPE), followed by BTC and ETH.

**6. High baseline win rate: 83.5%**
Even in the worst sentiment condition (Greed), win rate stays above 76% — this dataset skews toward skilled or systematic traders.

---

## Strategy Recommendation

> Use the Fear & Greed Index as a **contrarian signal**, not a momentum signal:
> - **Increase aggression during Fear / Extreme Fear** — historically the best risk/reward environment
> - **Reduce position sizing during Greed / Extreme Greed** — win rates and PnL both drop
> - Trade selectively: fewer, higher-conviction entries appear to drive the Fear outperformance

---

## Tools & Libraries

- Python 3.10+
- pandas, numpy
- matplotlib, seaborn
- scipy (Pearson correlation, Kruskal-Wallis test)
