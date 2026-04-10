# Empty Series and Missing Metrics

Use this when the metric exists, but some expected series vanish.

This is different from `no-data.md`: the query is not globally empty. A subset disappears because of filtering, aggregation, range functions, or binary math.

## Reduction Sequence

Check the same expression in this order:

1. raw metric
2. raw metric with one label filter
3. range function such as `rate()` or `increase()`
4. aggregation
5. ratio or other binary expression

If the subset disappears between two steps, debug that transition instead of rewriting the whole query.

## Series-Count Checks

- Count expected label combinations before and after each step
- Example: `count by (instance) (up{job=~"$job"})`
- If the count drops only after aggregation, the grouping is too aggressive
- If the count drops only after a binary expression, unmatched series are being discarded

## Missing Now vs Missing Entirely

- A series can be absent now because it went stale, even if it existed earlier in the selected range
- Use `absent(metric{instance="a"})` for a single evaluation-time check
- Use `absent_over_time(metric{instance="a"}[10m])` when you need to know whether it was missing across the range
- Widen the time range before concluding the target stopped existing

## Common Causes

- Exact-match variable filters where regex matchers were required
- `rate()` windows too short for a sparsely updated counter
- Aggregation that removed the label needed for a later join or legend
- Binary operations that dropped unmatched series by default
