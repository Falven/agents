---
name: grafana-debug-dashboards
description: Debug Grafana dashboards end to end. Use when panels show no data, misleading units, wrong time windows, broken variables, slow queries, or unreadable layouts and the problem is not yet isolated, so you need a systematic inspect-and-fix workflow across panels and dashboard settings.
---

# Grafana Debug Dashboards

Debug the dashboard as a system, not as isolated screenshots. First split the fault into raw query result, transformed result, or display semantics. Only then change queries or panel options.

Official dashboards may be row-based, use mixed or inherited datasources, and mix metrics, logs, and annotations by design; keep those structures intact while isolating the fault.

## When to Apply

Use this skill when:

- A panel is empty, misleading, slow, or inconsistent and the fault is not yet isolated.
- Multiple panels or dashboards disagree and you need to separate time, variable, transformation, and presentation causes.
- A dashboard "looks wrong" but it is not clear whether the source data, transform chain, or display config is responsible.

Do not use this as a general Grafana authoring guide. Once the failure is isolated to a specific query, datasource, or panel build-out task, switch to a narrower skill or direct implementation work.

## Debug Surface Map

Work top to bottom. Do not skip to cosmetics before the earlier surfaces are clean.

| Priority | Surface | Use for |
| --- | --- | --- |
| 1 | Inspect and Explore | Establish whether the panel is wrong in raw query output, transformed data, or rendered display. |
| 2 | Time and resolution | Empty ranges, gaps, hidden spikes, refresh drift, or query-step mismatch. |
| 3 | Variables and links | Wrong dashboard context, bad multi-select expansion, broken repetition, or link propagation bugs. |
| 4 | Transformations and field config | Correct query data that becomes wrong after joins, reductions, overrides, or display settings. |
| 5 | Performance checks | Slow dashboards, repeated expensive panels, oversized ranges, or duplicate queries. |
| 6 | Panel semantics | Misleading units, mappings, thresholds, null handling, or stacking. |

## How to Use

1. Reproduce the failure with the same time range, timezone, refresh state, variables, and link entry path.
2. Read [references/inspect-workflow.md](references/inspect-workflow.md) first. Treat Inspect plus Explore as the canonical loop.
3. If the raw query is wrong, load [references/time-range-and-resolution.md](references/time-range-and-resolution.md), [references/variables-and-links.md](references/variables-and-links.md), or [references/performance-checks.md](references/performance-checks.md), whichever matches the failure.
4. If the raw query is right but the panel is wrong, load [references/transformations-and-field-config.md](references/transformations-and-field-config.md) first, then [references/panel-semantics.md](references/panel-semantics.md) if the fault is still only presentation.
5. Verify one change at a time. After every change, re-run Inspect and confirm whether raw, transformed, and formatted outputs now agree.

## Reference Map

- [references/inspect-workflow.md](references/inspect-workflow.md) -> canonical Inspect and Explore loop.
- [references/time-range-and-resolution.md](references/time-range-and-resolution.md) -> dashboard time, panel overrides, interval, and Prometheus step checks.
- [references/variables-and-links.md](references/variables-and-links.md) -> variable expansion, chaining, URL context, links, and ad hoc filters.
- [references/transformations-and-field-config.md](references/transformations-and-field-config.md) -> transform order, debug/disable, Table view, and meaning-changing display config.
- [references/performance-checks.md](references/performance-checks.md) -> Stats and Query inspection, data-volume reduction, and duplicate-query reuse.
- [references/panel-semantics.md](references/panel-semantics.md) -> units, mappings, thresholds, null handling, and stacking.

## Output

Return the isolated fault domain, the smallest verified fix, and the exact Grafana checks used to verify it.
