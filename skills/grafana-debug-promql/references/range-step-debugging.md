# Range and Step Debugging

Use this when the same PromQL behaves differently inside Grafana.

## Query Type

- `Range` evaluates across the full dashboard time range and returns a time series
- `Instant` evaluates at one timestamp and is appropriate for current-value panels
- `Both` runs both query types and is useful when debugging panel behavior or confirming whether only one mode is broken

Example:

- A trend panel using `Instant` will only show one evaluation point
- A stat panel may still debug more clearly with `Both`, because you can compare the instant result with the range result Grafana is also capable of rendering

## Step and Alignment

- Grafana chooses a `step` based on time range, panel width, resolution, and `Min interval`
- Evaluation timestamps align to that step, not to arbitrary sample times
- If the step is too coarse, short spikes disappear
- If the step is much smaller than necessary, the query may return too many points and run slowly
- A short range window plus a coarse step can make `rate()` look empty or jagged even when raw samples exist

## Query Inspector

- Open Query Inspector and compare `expr`, `start`, `end`, and `step`
- Confirm the query datasource for each target; mixed Prometheus, Loki, and `__expr__` targets can be intentional in one dashboard family
- Confirm whether Grafana sent a range query, an instant query, or both
- Check whether the datasource returned the expected number of series
- If the inspector shows data but the panel still looks wrong, the problem may be panel reduction or transformation rather than PromQL

## Selector and Series-Count Checks

- Run the selector alone before debugging the full expression
- Use `count by (job) (up{job=~"$job"})` or a similar count to verify the expected series exist
- Compare series counts before and after each transformation
- If the series count drops only after binary math, switch to the label-matching references

## Common Fixes

- Switch `Instant` to `Range` for a time series panel
- Use `Both` while debugging a panel that mixes stat-style reduction with a time-series query
- Increase `Min interval` when Grafana is requesting too many points
- Decrease `Min interval` or narrow the time range when a coarse step hides short-lived behavior
