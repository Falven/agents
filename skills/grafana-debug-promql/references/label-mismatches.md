# Label Mismatches

Use this when labels, joins, or legends are the problem.

## Start with the Match Key

- Compare the label sets on both sides before using vector matching
- PromQL drops unmatched series by default in binary operations
- If the left side has `{job, instance}` and the right side has `{job}`, they will not match unless you aggregate or match on a smaller key

## Variable Filters

- Grafana multi-value or all-value Prometheus variables usually need regex matchers
- Use `instance=~"$instance"`, not `instance="$instance"`
- If a variable expands to `a|b|c`, exact match will return nothing

## Where the Labels Came From

- Some dashboards populate label variables from a separate selector metric, not from the metric being graphed
- Exported series can carry renamed labels such as `exported_namespace` or `exported_job`, which will not match the main metric's label names
- Dashboard variables like `$namespace`, `$controller`, or `$cluster` can be carried into the final query even when the plotted metric uses different labels
- If the join or filter depends on a label source, verify that source metric before changing the main expression

## Vector Matching Rules

- Use `on(label1, label2)` when only those labels should define equality
- Use `ignoring(label1, label2)` when some labels should be excluded from matching
- Use `group_left(...)` or `group_right(...)` only when one side has more series per match key
- The "one" side must still be unique on the chosen match labels, or Prometheus will reject the query

## Example

Bad:

```promql
rate(http_requests_total{code=~"5.."}[$__rate_interval])
/
rate(http_requests_total[$__rate_interval])
```

This often drops series because the numerator still has `code` and the denominator may not align the same way.

Better:

```promql
sum by (job) (rate(http_requests_total{code=~"5.."}[$__rate_interval]))
/
sum by (job) (rate(http_requests_total[$__rate_interval]))
```

If you truly need binary matching instead of pre-aggregation, make it explicit and verify uniqueness.

## Legend and Cardinality Signals

- If the legend explodes, the grouping is too broad for the panel
- Remove labels that the question does not need before visualizing or joining
- If series disappear after a binary expression, inspect the label sets before assuming the metric is missing
