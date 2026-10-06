# Quant Lab Roadmap

A cv project and revision-friendly website and code library covering mathematical finance, from no-arbitrage and the binomial model through to Black-Scholes, backtesting and machine learning. Built alongside two university courses (an introductory mathematical finance course and an advanced stochastic finance course) and supplemented with textbooks.

**Goals**
- Produce clear theory notes, in my own words, that I and others can use for revision and show employers skills and knowledge.
- Show the theory in practice with small, focused coding projects.
- Demonstrate the maths *and* the engineering: tested code, honest results, reproducible notebooks.

**Time commitment:** about 3 hours per week, treated like an extra module. Dates are soft; align each milestone with lecture order.

---

## Structure

### Site sections

| Section | Purpose |
|---|---|
| **Home / Start Here** | What the site is, prerequisites, notation, reading list |
| **Theory** | Essential concepts, ordered like the courses, usable as a reference |
| **Applications** | Backtesting, trading strategies, machine learning |
| **Projects** | Index of all builds with status, each linked to its theory page |
| **About** | Who I am and how to contact me |

### Course-to-site mapping

| Site section | Course 1 (intro) | Course 2 (advanced) |
|---|---|---|
| Theory A: No-arbitrage and discrete time | No-arbitrage, FTAP, filtrations, martingales, binomial model | |
| Theory A: Portfolios and risk | Markowitz, CAPM, utility theory, VaR/ES | |
| Theory B: Stochastic calculus | | Brownian motion, SDEs, Markov processes, Itô |
| Theory B: Black-Scholes | | Girsanov, risk-neutral pricing, PDE vs SDE, Greeks, put-call parity |
| Theory B: Extensions | | American options, interest rates, credit risk |

A **Martingales hub page** links the discrete-time (course 1) and continuous-time (course 2) versions in one place.

### Repo layout

```
quant-lab/
├── README.md
├── ROADMAP.md
├── requirements.txt
├── src/quantlab/
│   ├── pricing/        # black_scholes, binomial, trinomial, monte_carlo
│   ├── data/           # loaders (yfinance, FRED)
│   ├── backtest/       # engine, metrics
│   ├── strategies/     # momentum, mean reversion, pairs
│   ├── risk/           # VaR, ES, portfolio optimisation
│   └── ml/             # features, models, walk-forward CV
├── notebooks/          # one short notebook per topic
├── tests/              # pytest
└── site/               # Quarto website (theory + application pages)
```

---

## Page template (every theory page)

1. **Motivation:** what problem does this solve?
2. **Prerequisites:** links to earlier pages.
3. **Definitions and key results:** own words, with an "Intuition" box after each theorem.
4. **Worked example:** one small numerical example.
5. **In practice:** link to the notebook or application page.
6. **Common pitfalls and limitations.**
7. **Sources:** textbook chapters used.

Pattern for every topic: **Theory page → Notebook → Application page.**

## Ground rules

- **No plagiarism.** Write from lecture notes and understanding, with the book closed. Use own examples and proof sketches. Cite all sources.
- **A milestone is only done when its site page is published.**
- Logic lives in `src/quantlab/`; notebooks stay short and self-contained.
- Every notebook runs top to bottom from a clean checkout.
- Every function has a docstring and type hints; key formulas are tested against code.
- Commit small and often, on `main`. Publish with `quarto publish gh-pages` from `site/`.
- Add a "Key results" summary at the end of each Theory part (one page of theorems and formulas for revision).

## Weekly rhythm (3 hours)

- **1 hour:** read, then write the theory page.
- **1.5 hours:** code and test the notebook or module.
- **30 minutes:** edit, proofread, commit, push, publish.

---

## Milestones

### Milestone 0: Foundations (weeks 1-2)
- [ ] Site skeleton live on GitHub Pages (Home, Start Here, About)
- [ ] "What is this site" page, prerequisites (probability, linear algebra, calculus, Python), notation page
- [ ] Page template and a stub for each Theory section
- [ ] Reading list (e.g. Shreve vols I and II, Hull, Björk, plus course texts)
- [ ] **First project:** download daily ETF prices with `yfinance`, compute returns, volatility and Sharpe ratio, and plot them (about 50 lines, one notebook)

**Done when:** the site is public and the notebook is linked from it.

### Milestone 1: No-arbitrage and the binomial model (weeks 3-6)
**Theory:** one-period model, arbitrage, equivalent martingale measures, FTAP, conditional expectation, filtrations, martingales, self-financing strategies, complete markets, binomial pricing and hedging.

**Projects**
- [ ] One-period arbitrage checker (linear programming, finds arbitrage or a risk-neutral measure)
- [ ] CRR binomial pricer for European and American options, showing the replicating portfolio at each node
- [ ] Trinomial tree, comparing convergence speed
- [ ] Tests: put-call parity; convergence as steps increase

**Done when:** the Martingales page exists and the binomial notebook runs from a clean checkout.

### Milestone 2: Portfolio theory and risk (weeks 7-10)
**Theory:** mean-variance, efficient frontier, tangency portfolio and capital market line, CAPM, utility theory and risk aversion, VaR and Expected Shortfall.

**Projects**
- [ ] Efficient frontier on 10-20 ETFs (long-only and unconstrained) with the tangency portfolio
- [ ] Beta estimation by regression and a CAPM test on real data (discuss why it is weak or rejected)
- [ ] VaR and ES three ways (historical, parametric, Monte Carlo) plus a VaR backtest counting exceedances

**Done when:** the Risk page explains why ES is preferred to VaR (coherence, subadditivity), with plots.

### Milestone 3: Backtesting pipeline and metrics (weeks 11-14)
Core of the portfolio, so give it time.

- [ ] Own backtester in `src/quantlab/backtest/` (data → signal → positions → returns → metrics)
- [ ] Transaction costs and a one-day signal lag to avoid look-ahead bias
- [ ] **Metrics page:** for each of total/annualised return, volatility, Sharpe, Sortino, max drawdown, Calmar, turnover and hit rate, give the formula, what it measures, what it means and when it misleads
- [ ] First strategy: momentum, benchmarked against buy-and-hold
- [ ] "How backtests lie" page: look-ahead bias, survivorship bias, overfitting, data snooping

**Done when:** one command runs the momentum backtest and produces a tearsheet whose figures appear on the site.

### Milestone 4: Brownian motion and SDEs (weeks 15-19)
**Theory:** random walk to Brownian motion, quadratic variation, Itô integral and lemma, geometric Brownian motion, SDEs, Markov processes.

**Projects**
- [ ] Simulate Brownian paths and verify quadratic variation numerically
- [ ] Euler-Maruyama and Milstein schemes for GBM, with strong error against the exact solution
- [ ] Compare simulated GBM to real returns (fat tails, volatility clustering)

**Done when:** the Itô's lemma page has a numerical check alongside the derivation.

### Milestone 5: Black-Scholes and Greeks (weeks 20-25)
**Theory:** risk-neutral valuation, Girsanov (intuition first, then statement), martingale representation, BS PDE derived both ways, Greeks, put-call parity and symmetry.

**Projects**
- [ ] Closed-form BS pricer and Greeks, validated against finite differences
- [ ] Implied volatility solver (Newton-Raphson with bisection fallback)
- [ ] Monte Carlo pricer with confidence intervals and antithetic variates, validated against BS
- [ ] **Delta-hedging simulation:** hedge a short call along simulated paths and plot hedging error against rebalancing frequency (flagship demo; polish it)
- [ ] Implied volatility smile from a few real option quotes

**Done when:** the BS page has the full derivation, the hedging experiment and a limitations section (constant volatility, no jumps).

### Milestone 6: More strategies (weeks 26-30)
- [ ] Mean reversion, with the Ornstein-Uhlenbeck process as the theory link (reused later for Vasicek)
- [ ] Pairs trading: Engle-Granger cointegration tests, hedge ratios, z-score entry and exit rules
- [ ] All strategies in the backtester, compared in one results table net of costs

**Done when:** a comparison page includes an honest "what worked, what didn't, and why".

### Milestone 7: Machine learning (weeks 31-36)
- [ ] Feature engineering (returns, volatility, volume signals)
- [ ] Models: ridge/lasso, random forests, gradient boosting
- [ ] Walk-forward validation, with a page on why random splits leak information
- [ ] Turn predictions into positions and run them through the backtester
- [ ] Compare against momentum and buy-and-hold after costs and report honestly

**Done when:** the ML page includes feature importance and a clear failure-mode discussion.

### Milestone 8: Advanced extensions (summer, or as time allows)
Pick two or three:
- [ ] **American options and optimal stopping:** Snell envelope, Longstaff-Schwartz Monte Carlo
- [ ] **Interest rates:** Vasicek, CIR and Hull-White; simulation, bond pricing, calibration to a yield curve
- [ ] **Credit risk:** Merton structural model, linking default probability to option pricing
- [ ] **GARCH** volatility modelling and a VaR comparison
- [ ] **Capstone:** polish the README, results summary, repo tidy-up, and a "what I learned / next steps" page

---

## Scope control

Milestones 0-3 alone make a strong portfolio. Any milestone can be cut to its first one or two projects. A finished, published page beats three half-written ones.

## Progress log

| Date | Milestone | Notes |
|---|---|---|
| | | |
