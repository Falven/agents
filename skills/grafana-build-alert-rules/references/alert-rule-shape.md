# Alert Rule Shape

## Core Model

- A Grafana-managed rule can have multiple queries and expressions, but it still has one condition.
- Keep one rule tied to one failure mode. Split unrelated symptoms into separate rules instead of stacking more logic into one condition.
- Make the condition readable in plain language, not just as ref IDs and operators.

## Alert Instances

- Time series input: each returned series is evaluated independently. After reduction, each series can become its own alert instance.
- Table input: each qualifying row can become its own alert instance. The row needs one numeric field to evaluate and stable non-numeric fields for labels.
- If the desired result is one fleet-wide alert, aggregate in PromQL or return one series before the condition step.

## Condition and Recovery

- `Threshold` is usually the cleanest final condition because it evaluates one number per series or row.
- Recovery threshold is hysteresis inside that same threshold condition. It is not a second condition.
- `Keep firing for` is separate from recovery threshold. It delays resolution after the condition stops matching.
- Pending period and evaluation interval still matter; short windows increase noise on sparse or bursty signals.

## Labels and Annotations

- Labels define alert identity, grouping, routing, and deduplication. Keep them stable.
- Annotations carry human context such as summary, runbook, and recent values.
- Avoid duplicate label keys and collisions between query labels, custom labels, and reserved Grafana labels such as `alertname` or `grafana_folder`.
- Prefer `$values` over `$value` when templates need ref-specific numbers or labels.
