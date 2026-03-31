# VIX–VXN Relative Spread: Regimes, Compression Dynamics, and Market Behavior
________________________________________
Executive Summary
This project studies how the relationship between VIX (S&P 500 volatility) and VXN (Nasdaq volatility) behaves during periods of market stress.
Instead of focusing on absolute levels, the analysis focuses on the relative spread between the two indices.
The main result is:
The level of the spread alone is not very informative.
What matters more is how fast it compresses, and under which market conditions that happens.
________________________________________
Research Question
Does extreme compression in the VXN–VIX spread carry useful information about short-term market behavior?
More specifically:
•	Does it provide directional signals? 
•	Or does it mainly affect the distribution of outcomes? 
________________________________________
Economic Motivation and Background
Volatility indices are not purely measures of expected volatility. They also reflect:
•	demand for protection 
•	risk premia 
•	changes in correlation across assets 
Index-level implied volatility tends to embed more systemic risk, while differences across indices may reflect shifts between:
•	idiosyncratic risk 
•	correlation-driven market stress 
This interpretation is consistent with several well-established findings:
•	Implied volatility reflects demand for hedging and insurance (Whaley, 2000) 
•	Index options embed a correlation component beyond single-name volatility (Driessen, Maenhout & Vilkov, 2009) 
•	Correlations tend to increase during market stress, particularly in downside regimes (Longin & Solnik, 2001) 
In this project, the VXN–VIX spread is treated as a proxy for dispersion vs systemic stress, acknowledging that it is not a direct measure of implied correlation.
The decision to study this spread is therefore not arbitrary, but grounded in the idea that relative volatility structures may contain information about how risk is distributed across the market.
________________________________________
Hypothesis
The working hypothesis is:
•	wider spreads → more dispersion (idiosyncratic behavior) 
•	tighter spreads → more uniform, systemic behavior 
Extreme compression may occur alongside:
•	elevated hedging demand 
•	increased cross-asset correlation 
•	short-term exhaustion of panic-driven positioning 
________________________________________
Methodology
Data
•	Source: Yahoo Finance (yfinance) 
•	Period: 2006–present 
•	Series: 
o	S&P 500 
o	VIX 
o	VXN 
________________________________________
Core Variable
spread_rel = (VXN - VIX) / VIX
A relative formulation is used to avoid distortions across different volatility regimes.
________________________________________
Event Definition
Events are defined when:
•	the spread falls below the 10th percentile 
•	percentiles are computed using past data only 
•	thresholds are explicitly shifted to avoid look-ahead bias 
•	a 21-day cooldown is applied to prevent clustering 
The percentile threshold is intentionally not optimized. It is used as a simple and consistent way to isolate extreme conditions while avoiding parameter overfitting.
________________________________________
Forward Metrics
For each event:
•	1d, 5d, 21d, 63d forward returns (SPX) 
•	hit rates 
•	comparison versus unconditional baseline 
________________________________________
Conditioning
The signal is evaluated under different contexts:
•	market regime (SPX relative to MA200) 
•	volatility regime (VIX levels) 
•	recent returns 
•	compression dynamics: 
o	magnitude 
o	short-term speed 
________________________________________
Methodological Notes
No Look-Ahead Bias
•	percentiles are computed using only past data 
•	thresholds are shifted 
•	forward returns are strictly forward 
________________________________________
Clustering Control
A 21-day cooldown is applied to avoid repeated signals from the same event.
________________________________________
Parameter Discipline
No parameters were tuned to maximize performance.
The objective is to understand behavior, not to construct a trading signal.
________________________________________
Results
1. Level Alone Is Weak
Extreme spread levels (e.g., p10) do not consistently produce strong directional outcomes.
Results are often close to baseline behavior.
________________________________________
2. Strong Dependence on Context
Results vary depending on:
•	market trend 
•	volatility regime 
•	recent price action 
This confirms that the signal is not standalone.
________________________________________
3. Dynamics Matter More Than Levels
The most consistent pattern appears when looking at compression dynamics:
Faster and stronger compression tends to carry more information than the level itself.
More favorable outcomes are typically observed when:
•	compression is large 
•	compression occurs quickly 
•	the broader regime is well defined 
________________________________________
4. Interpretation
This behavior is more consistent with:
•	shifts in positioning 
•	changes in correlation structure 
•	short-term unwinding of stress 
rather than a direct directional signal.
________________________________________
Limitations
•	The spread is a proxy, not implied correlation 
•	No option-level decomposition is used 
•	Results depend on: 
o	event definition 
o	window selection 
o	conditioning filters 
•	Overlapping forward returns reduce statistical independence 
If results vary significantly across samples, this reflects limited robustness rather than model failure.
________________________________________
Key Takeaway
This is not a directional signal.
It behaves as a regime-dependent filter that alters the distribution of outcomes.
________________________________________
Future Work
•	Incorporate implied correlation measures 
•	Extend across asset classes 
•	Analyze intraday behavior 
•	Connect more directly to dispersion frameworks

