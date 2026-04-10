# No Data

Use this when the whole query is empty.

## Fast Path

1. Validate the raw selector before debugging math or panel options.
2. Check Grafana query type: `Both`, `Range`, or `Instant`.
3. Open Query Inspector and inspect the exact expression, time range, and `step`.
4. Fix short `rate()` or `increase()` windows before changing labels or joins.
5. Distinguish "selector matches nothing" from "series is stale right now."

## Validate the Selector First

- Start with the bare metric: `http_requests_total`
- Add one filter at a time: `http_requests_total{job=~"$job"}`
- For multi-value or all-value Grafana variables, use regex matchers like `job=~"$job"`, not exact matchers like `job="$job"`
- If the raw selector is empty, the problem is upstream of aggregation or binary expressions

## Check the Grafana Query Type

- `Range` is for trend panels and returns samples across the selected time range
- `Instant` is for one evaluation timestamp and is often right for stat panels
- `Both` is useful while debugging because it exposes whether only one query mode is broken
- If a time series panel uses `Instant`, one point may look like no trend; if a stat panel is wired to range data, the panel may reduce in a surprising way

## Use Query Inspector

- Compare the expression Grafana sent with the query you think it sent
- Check `start`, `end`, and `step`
- Check whether the datasource returned zero series or whether the panel failed after data came back
- If the inspector shows zero series, stay in selector and window debugging

## Fix Empty `rate()` and `increase()` Windows

- `rate(http_requests_total[1m])` is often too short on a 60s scrape interval
- Prefer `rate(http_requests_total[$__rate_interval])` in Grafana panels
- A rate window usually needs several scrapes to produce stable data
- If the window is shorter than the scrape interval or only barely longer, the result can be empty or misleading

## Absent vs Stale

- `absent(metric{...})` answers "does this selector match anything at this evaluation time?"
- `absent_over_time(metric{...}[10m])` answers "was this selector absent across the whole range?"
- A series can exist historically and still be missing now because it went stale after Prometheus lookback
- If a selector worked earlier in the time range but is empty now, widen the range or test a range function before rewriting the query

## Typical Fixes

- Replace `job="$job"` with `job=~"$job"` for multi-value dashboard variables
- Replace `rate(counter[1m])` with `rate(counter[$__rate_interval])`
- Switch the panel query from `Instant` to `Range`, or use `Both` while debugging
- Remove binary math and aggregations until a raw selector returns data
