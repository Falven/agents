# Matching, Range, and Cardinality

Use this when a ratio or binary expression fails because matching rules, range choice, and cardinality are all part of the same problem.

This is different from:

- `label-mismatches.md`, which is the primary reference for pure label and vector-matching issues
- `range-step-debugging.md`, which is about Grafana query mechanics
- `performance-cardinality.md`, which is about panel cost and scale

## Compound Failure Pattern

These queries usually fail in one of three ways at the same time:

- label sets do not align, so unmatched series drop
- the selected range is too short, so one side of the ratio is empty or unstable
- high-cardinality labels leak through, making the result noisy or expensive

## Safer Shape for Ratios

Prefer this pattern:

```promql
sum by (job) (rate(http_requests_total{code=~"5.."}[$__rate_interval]))
/
sum by (job) (rate(http_requests_total[$__rate_interval]))
```

Why:

- `rate()` happens before aggregation
- both sides are grouped by the same labels
- `$__rate_interval` scales with Grafana's time range and scrape interval assumptions

## Matching Rules

- Unmatched series disappear by default in binary operations
- Use `on(...)` or `ignoring(...)` only when you can explain the intended match key
- Use `group_left` or `group_right` only when one side is intentionally more granular
- The lower-cardinality side must still be unique on the match labels

## Range and Scrape Checks

- Sparse counters often need longer windows
- If the range is too short for the scrape interval, a ratio can vanish because one side has no usable samples
- When a ratio flips between empty and non-empty as you change the time range, suspect the window before suspecting the panel

## Cardinality Checks

- Remove labels that do not matter before dividing or joining
- If a legend explodes, the result is too granular for the question
- If the query is expensive and semantically noisy, aggregate earlier
