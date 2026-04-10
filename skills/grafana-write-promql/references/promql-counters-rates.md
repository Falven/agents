# PromQL Counters and Rates

- `rate(counter[$__rate_interval])` is the default for dashboard trends, slow-moving counters, and alert-style logic. It gives a stable per-second rate.
- `irate(counter[$__rate_interval])` is for volatile counters when you intentionally want the last-two-samples view. It is much spikier.
- `increase(counter[$__rate_interval])` is human-readable sugar for total change over the window. Use it for panels that ask "how many happened in this interval?"
- Prefer `$__rate_interval` in Grafana instead of hard-coding `[5m]`.
- Keep the counter lookback window on `$__rate_interval` even if the panel sampling interval comes from a different step variable such as `$resolution`.
- Do not apply `rate()`, `irate()`, or `increase()` to gauges.
- A common dashboard trap is treating `workqueue_depth` like a counter; it is a gauge, so aggregate it directly instead of wrapping it in `rate()`.

## Order of Operations

- Do `rate()` before aggregation so Prometheus can detect counter resets correctly.
- Good: `sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Bad: `rate(sum by (service) (http_requests_total)[$__rate_interval:])`
- Good: `sum by (name) (workqueue_depth{job="kube-controller-manager"})`
- Bad: `sum(rate(workqueue_depth{job="kube-controller-manager"}[$__rate_interval]))`
- For error ratios, divide two counter-based rates with aligned label sets.

Common patterns:

- Request rate: `sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Error ratio: `sum by (service) (rate(http_requests_total{status=~"5.."}[$__rate_interval])) / sum by (service) (rate(http_requests_total[$__rate_interval]))`
- Requests in the displayed window: `sum by (service) (increase(http_requests_total[$__rate_interval]))`
- Volatile per-second packets: `sum by (instance) (irate(node_network_receive_packets_total[$__rate_interval]))`
