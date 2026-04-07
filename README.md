# VIX–VXN Spread as a Risk Regime Filter

This project investigates whether the relative spread between VXN and VIX carries useful information about market behavior.

The focus is not on predicting direction, but on understanding whether the spread helps identify when taking risk is more or less favorable.

---

## Research Question

Does extreme compression in the VXN–VIX spread carry useful information about future market behavior?

More specifically:

- Does the spread level matter?
- Do compression dynamics matter more?
- Can the signal be used in a practical allocation framework?

---

## Economic Intuition

Volatility indices reflect more than expected volatility. They embed:

- demand for protection  
- risk premia  
- changes in correlation  

Index volatility tends to capture systemic risk, while differences between indices can reflect shifts between:

- idiosyncratic risk  
- correlation-driven stress  

The VXN–VIX spread is therefore treated as a proxy for dispersion vs systemic stress.

---

## Methodology

- Data: Yahoo Finance (SPX, VIX, VXN)  
- Period: 2006–present  

### Core variable

`spread_rel = (VXN - VIX) / VIX`

### Event definition

An event occurs when:

- the relative spread falls below its rolling 252-day 10th percentile  
- the threshold is shifted (no look-ahead)  
- a 21-day cooldown is applied  

### Evaluation

- forward returns (5d, 21d, 63d)  
- hit rates  
- comparison vs baseline  
- conditioning by:
  - market regime (MA200)
  - compression dynamics (magnitude and speed)
  - local positioning

---

## Main Findings

1. **Spread level alone is weak**
2. **Market regime matters**
3. **Compression dynamics carry more information than static levels**

The signal is not a reliable standalone directional predictor.

---

## Practical Result

The signal performs poorly as a standalone strategy.

However, it becomes more useful as a **risk overlay**.

A simple allocation rule:

- 1.5x exposure when the signal is active  
- 0.5x otherwise  

produces, in this simple implementation:

- similar long-term returns  
- materially lower drawdowns  
- better Sharpe and Sortino  
- significantly improved drawdown-adjusted performance  

---

## Interpretation

The VIX–VXN spread behaves as a:

> **state-dependent risk filter**

Its value lies in improving **risk allocation**, not predicting direction.

---

## Files

- `notebook/g1_vix_vxn_analysis.ipynb`
- `images/equity_regime_overlay.png`
- `images/drawdown_regime_overlay.png`

---

## Disclaimer

This project is for research and educational purposes only. It is not investment advice.
