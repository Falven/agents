# Use PromQL Before Grafana Expressions

- Prefer datasource-native PromQL for rate, ratio, histogram, and label-aware aggregation logic.
- Apply `rate()` or `increase()` to counters before aggregating them.
- Use Grafana expressions for the final alert-specific steps: `Reduce`, `Threshold`, simple `Math`, or `Resample` when timestamps do not align.
- `Math` joins by labels, not by query order, so normalize labels before doing `$A / $B`.
- If the source query can express the alert clearly on its own, avoid rebuilding the same logic in Grafana expressions.
