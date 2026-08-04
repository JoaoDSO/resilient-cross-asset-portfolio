# Executive summary

## Resilient Cross-Asset Portfolio under Defined Disruption Scenarios

Financial portfolios are usually optimised for expected return in normal
conditions. That is not enough when the client cares about resilience: a
portfolio can look attractive in calm periods while being highly exposed to a
specific disruption. This project builds a data-driven allocation pipeline that
asks a more practical question: which assets still look acceptable if a named
geopolitical shock occurs?

The selected disruption is a Taiwan Strait / TSMC supply shock. The model
curates 104 instruments across stocks, country ETFs and commodities, joins them
to macro-governance context, predicts forward 12-month returns, and then
re-predicts those returns after applying the scenario. The portfolio score
combines normal-case expected return, shocked expected return and a penalty for
the stressed 5% downside forecast.

Main findings:
- The refreshed data cache uses live yfinance prices for all 104 tickers and
  live yfinance fundamentals for all 104 rows.
- Split-conformal calibration lifts validation coverage to 90.1% for the
  nominal 90% prediction interval; test coverage is 81.5% on the live panel.
- The resilient portfolio gives up realised return in the test window
  (25.6% versus 34.5% for growth) but improves the Taiwan-scenario 5% tail
  forecast from -21.7% to -16.2%.
- SHAP attribution shows that the scenario mainly moves the features it was
  designed to stress: volatility, drawdown and political-stability context.

Recommendation:
Use the resilient allocation as a stress-aware overlay rather than as a claim
that it will beat a growth benchmark in every market. The client can tune the
alpha parameter to balance normal growth against stressed growth, and lambda to
control how strongly the allocation avoids downside under the Taiwan scenario.

Highlights:
- End-to-end reproducible pipeline: data, features, models, scenarios,
  allocation and explanation.
- Integrates at least three course topics: ensembles, uncertainty modelling,
  counterfactual scenarios, plus SHAP interpretability.
- Uses a concrete resilience objective tied to a named disruption rather than a
  generic risk score.
- Shows both model quality and portfolio trade-offs, including sensitivity to
  the main decision knobs.
- Produces a concrete portfolio trade-off: lower realised growth, better
  scenario downside.

Limitations:
- No actual Taiwan shock occurs in the test window, so realised backtesting and
  scenario resilience measure different objectives.
- Scenario magnitudes are expert-defined stress assumptions rather than
  observed causal effects.
- Test interval coverage after conformal calibration remains below the nominal
  target, so the interval should be interpreted as a conservative diagnostic
  rather than a production risk model.
- The universe is deliberately semiconductor-heavy, so results should not be
  read as a fully market-cap-weighted global allocation.
