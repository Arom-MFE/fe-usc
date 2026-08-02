# fe-usc

Five quantitative finance projects, each a standalone Jupyter notebook. The work comes from my graduate financial engineering coursework at USC. Coverage runs from yield curve construction through Monte Carlo valuation of a variable annuity guarantee; every notebook opens with a contents table, states its model assumptions in markdown, derives the formulas it implements, and keeps every result in executed cells.

## Projects

| # | Project | Methods                                                                                                                                                                                                                                                       | Key result |
|---|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 01 | [Term Structure, Swaps, and Lattice Pricing](01-term-structure-swaps-and-trees/term_structure_swaps_and_trees.ipynb) | - SOFR curve bootstrapping under piecewise-constant, log-linear discount factor, and linear forward assumptions<br/>- Swap and forward-swap pricing<br/>- CRR binomial with conditional dividends<br/>- Double-barrier knockout<br/>- Trinomial tree | Par bonds reprice to exactly 100.00 at every quoted tenor under all three curves; the 70/130 knockout cuts the European put from 8.3406 to 4.5684 while early exercise holds the American at 9.1203 |
| 02 | [Monte Carlo Option Pricing](02-monte-carlo-option-pricing/monte_carlo_option_pricing.ipynb) | - Bump-and-revalue Greeks<br/>- Average-strike Asian call<br/>- Knockout put<br/>- Correlated two-asset baskets<br/>- Dynamic delta hedging<br/>- Least squares Monte Carlo<br/>- Time-varying rates and volatility | Weekly delta hedging of 100,000 sold calls averages a 782,038 replication cost against the 1,134,848 premium collected at 25% implied volatility; LSMC prices the American put at 15.3913 |
| 03 | [Credit Risk Models](03-credit-risk-models/credit_risk_models.ipynb) | - Merton structural model<br/>- CDS hazard bootstrapping and mark-to-market<br/>- Rating-transition valuation with a GFC stress<br/>- One-factor Gaussian tranche pricing<br/>- Vasicek loss distributions                                                                          | Merton calibration backs out asset value 226.07 and a 0.477% market spread; the seasoned 200bp CDS marks at 0.01223 per unit notional and the par binary spread is 2.833% |
| 04 | [Volatility, Market Risk, and Real Options](04-market-risk-and-real-options/market_risk_and_real_options.ipynb) | - GARCH(1,1) by maximum likelihood with normal and Student-t errors<br/>- Portfolio VaR and expected shortfall under Vasicek rates<br/>- PCA on the Treasury curve<br/>- Real options on a futures-calibrated trinomial tree                                                   | GARCH persistence lands at alpha + beta = 0.988; the first three PCs carry 98.3772% of Treasury curve variance, and the abandonment and expansion options price at 7.6228 and 7.9608 |
| 05 | [Variable Annuity Guarantee Pricing](05-annuity-guarantee-pricing/annuity_guarantee_pricing.ipynb) | - Seeded Monte Carlo of a 30-year withdrawal guarantee<br/>- Stochastic Vasicek rates correlated with equity returns<br/>- Annual mortality and fee income netted against guarantee shortfalls<br/>- Risk-neutral and real-world views                                                  | The 2% fee nets the insurer 4.6091 per 100 of premium against a 1.2590% breakeven; starting rates at 1% instead of 5% flips the value to -14.7196 |

## Repository layout

Each project is self-contained: one notebook, plus data only where a notebook reads any.

```
01-term-structure-swaps-and-trees/   term_structure_swaps_and_trees.ipynb
02-monte-carlo-option-pricing/       monte_carlo_option_pricing.ipynb
03-credit-risk-models/               credit_risk_models.ipynb
04-market-risk-and-real-options/     market_risk_and_real_options.ipynb   data/
05-annuity-guarantee-pricing/        annuity_guarantee_pricing.ipynb
requirements.txt
```

## Running the notebooks

- `pip install -r requirements.txt`. Versions are unpinned; the file covers everything the notebooks import, including QuantLib for 02 and arch for 04.
- Start each notebook from its own project directory. 04 reads its data with a relative path, so a kernel launched at the repo root will not find it.
- The Monte Carlo sections in 02, 03, and 05 are seeded, so the stored results reproduce exactly on a clean top-to-bottom rerun.