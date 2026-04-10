# PromQL Aggregation and Labels

Choose the final comparison labels first, then aggregate to exactly that shape.

- Keep the labels the panel must compare on.
- Drop labels that only add noise or cardinality.
- Use `sum by (...)` to preserve comparison dimensions.
- Use `sum without (...)` only when the labels to drop are clearer than the labels to keep.
- Align numerator and denominator label sets before division.
- On counters, aggregate after `rate()` so reset detection still works.

Check:

- which labels appear in the legend
- whether the panel wants one line, a few grouped lines, or a fleet-wide total

Examples:

- Fleet-wide request rate: `sum(rate(http_requests_total[$__rate_interval]))`
- Per-service request rate: `sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Per-service error ratio: `sum by (service) (rate(http_requests_total{status=~"5.."}[$__rate_interval])) / sum by (service) (rate(http_requests_total[$__rate_interval]))`
