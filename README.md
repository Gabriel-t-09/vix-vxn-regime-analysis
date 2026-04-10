# VIX–VXN Spread as a Risk Regime Signal

## Overview

This project investigates whether the relative spread between VXN (Nasdaq volatility) and VIX (S&P 500 volatility) contains usable information about market conditions.

The core idea is straightforward:

- The level of the spread is not informative.
- The dynamics of compression — how fast and how intense — may signal short-lived systemic stress.

Rather than predicting direction, the signal is used to characterize market regimes and improve tactical allocation.

---

## Key Result

When the VXN–VIX spread compresses both intensely and rapidly, and the market is in a favorable regime (above MA200):

- → The forward 21-day return distribution shifts positively
- → Hit rate: 87.5% (n=24, p=0.020)

Sub-period stability:

| Period | n | hit_21d | p-value |
|---|---|---|---|
| Full | 24 | 0.875 | 0.020 |
| 2010–2019 | 13 | 0.846 | 0.139 |
| post-2020 | 9 | 1.000 | — |

This effect is not replicated by VIX alone.

---

## Economic Intuition

VIX and VXN reflect demand for protection, not opinion.

In normal regimes:

- VXN > VIX, reflecting structurally higher volatility in growth assets

In systemic stress:

- dispersion collapses
- correlation rises
- hedging demand concentrates in index options

→ The spread compresses or inverts

Interpretation:

- High spread → idiosyncratic risk
- Compressed spread → systemic risk

---

## Methodology

### Data

- SPX (^GSPC)
- VIX (^VIX)
- VXN (^VXN)
- Source: Yahoo Finance
- Period: 2006–March 2026

All signals:

- computed using close at time t
- executed at next-day open (t+1)
- no look-ahead bias

---

## Core Variable

spread_rel = (VXN - VIX) / VIX

The spread is normalized by VIX to ensure comparability across different volatility regimes.

---

## Event Definition

An event occurs when:

spread_rel ≤ rolling 252-day 10th percentile (shifted by 1 day)

- Rolling window: 252 days
- Shift: prevents look-ahead bias
- Cooldown: 21 trading days

---

## Compression Dynamics

Two additional conditions define compression quality:

Intensity:

spread_rel(t) - spread_rel(t-21) ≤ rolling p10

Speed:

spread_rel(t) - spread_rel(t-3) ≤ rolling p10

If both conditions are satisfied: → strong_fast event

---

## Regime Filter

Market regime is defined as:

SPX > MA200 (shifted)

---

## Allocation Overlay

- Above MA200 → 1.0x exposure
- Below MA200 → 0.5x exposure
- strong_fast + above MA200 → 1.5x exposure for 21 trading days

---

## Results

### Signal Performance

- Baseline hit rate: 66.7%
- Spread (level only): 64.5%
- Spread (strong_fast): 87.5% (p=0.020)

---

## Comparison vs VIX

- VIX strong_fast: 62.1% (p=0.768)
- Spread strong_fast: 87.5% (p=0.020)

→ The spread captures distinct market conditions not visible in VIX alone.

---

## Portfolio Impact

**Buy & Hold:**

- CAGR: 8.67%
- Sharpe: 0.525
- Max DD: -57%

**MA200:**

- CAGR: 7.62%
- Sharpe: 0.603
- Max DD: -37%

**MA200 + Spread Overlay:**

- CAGR: 9.02%
- Sharpe: 0.667
- Max DD: -37%

→ Recovers the return lost by the MA200 filter
→ Maintains drawdown protection

---

## Interpretation

The spread behaves as a state variable:

- identifies acute systemic stress
- captures short-lived dislocations
- improves allocation timing

It does not predict direction.
It alters the distribution of outcomes.

---

## Limitations

- Signal identified through iterative exploration (not pre-specified)
- No out-of-sample validation
- Small sample size (n=24)
- Sensitivity to subperiods (notably post-2020)
- Limited data in bear market regimes
- Association does not imply causation

---

## Project Structure

notebook/
g1_vix_vxn_analysis.ipynb
images/
strategy_comparison.png

---

## Disclaimer

This project is for research and educational purposes only.
It does not constitute investment advice.
