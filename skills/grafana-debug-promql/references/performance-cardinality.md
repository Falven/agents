# Performance and Cardinality

Use this when the panel is slow, returns too many series, or returns too many points.

## Start with Query Inspector

- Check total query time
- Check the exact `step` Grafana requested
- Check returned series count
- Check whether the problem is too many series, too many points, or both

## Too Many Points

- Shorten the dashboard time range
- Increase Grafana `Min interval`
- Lower panel resolution if Grafana is oversampling relative to the question
- Avoid tiny steps for long time ranges unless the investigation truly needs that detail

## Too Many Series

- Tighten selectors before optimizing anything else
- Aggregate away labels the panel does not need
- Prefer `sum by (service)` or `sum by (job)` when the question is operational, not per-pod
- Avoid joins that duplicate a high-cardinality side across many output series

## Concrete Remedies

- Replace per-instance or per-pod legends with service-level aggregation
- Narrow the time range during debugging, then widen only after the query shape is correct
- Use recording rules for expensive expressions reused across dashboards
- Fix cardinality in the query shape before trying to hide it with panel options

## `Min interval` and Resolution

- Raising `Min interval` reduces returned points and often removes panel overload
- If important short-lived behavior disappears after raising it, narrow the time range instead of immediately dropping back to a tiny step
- The right fix depends on whether the bottleneck is query cost, point count, or result cardinality
