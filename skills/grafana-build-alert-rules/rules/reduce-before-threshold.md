# Reduce Before Threshold

- Grafana-managed rules have one condition, even when the rule contains multiple queries and expressions.
- For time series input, reduce each series over the evaluation window before thresholding.
- For table input, each qualifying row can become its own alert instance; the numeric field is what the condition evaluates.
- Recovery threshold is hysteresis inside that one threshold condition, not a second condition.
- Prefer `Reduce -> Threshold` over classic condition when you need per-series alert instances.
