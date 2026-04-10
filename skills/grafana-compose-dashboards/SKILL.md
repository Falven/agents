---
name: grafana-compose-dashboards
description: Compose Grafana dashboards from working panels. Use when arranging panels into a coherent dashboard, choosing time defaults, refresh cadence, placement of already-defined variables, annotations, and links, and service-overview or drill-down layouts after the underlying queries already work.
---

# Grafana Compose Dashboards

Compose Grafana dashboards that answer one operational question cleanly. Start from already-working panels and organize them into a layout that supports scanning, comparison, drill-down, and handoff.

## When to Apply

Reference this skill when:

- Arranging already-working panels into a coherent Grafana dashboard
- Choosing dashboard-level time defaults and refresh behavior
- Deciding between rows, tabs, repeat behavior, and panel grouping
- Placing existing variables, annotations, and links into a usable navigation flow
- Reviewing a service overview or drill-down dashboard before it is considered done

Do not use this skill to write panel queries, fix broken visualizations, or design variable definitions from scratch.

## Version Note

Grafana's documentation is currently in transition around dynamic dashboards and layout guidance. This skill assumes the current model: dynamic dashboards are GA and on by default as of April 8, 2026, while composition still centers on explicit choices about layout mode, grouping, time defaults, annotations, and links.

## Workflow

1. Define the dashboard's audience and the first-screen question it must answer.
2. Pick the layout mode and grouping plan before placing panels. If the question fans out, prefer an overview dashboard plus focused sibling dashboards over one oversized page.
3. Choose the default time range, timezone behavior, and refresh cadence that match the data.
4. Add annotations and links only where they reduce operator navigation cost.
5. Review the finished dashboard for scannability, coherence, and unnecessary repetition.

## Upstream Pattern

Current Grafana dashboard families in this workspace lean on three layout shapes: flat row headers as separators, collapsed row containers for detail, and hybrids that keep the summary visible while hiding lower-priority sections. Related families such as Tempo and Loki often split an overview dashboard from focused siblings and use dropdown dashboard links that preserve the current variables and time window.

## Reference Map

- `references/layout-and-scannability.md` -> choose `Custom` vs `Auto grid`, rows vs tabs, and repeat behavior.
- `references/time-range-and-refresh.md` -> choose sensible defaults for time and refresh behavior.
- `references/annotations-and-links.md` -> separate annotation scope from dashboard, panel, and data-link navigation.
- `references/dashboard-review-checklist.md` -> final review before declaring the dashboard done.

## Output

Return:

- `layout mode`
- `grouping plan`
- `default time range`
- `refresh choice`
- `annotation plan`
- `link plan`

If the dashboard still needs panel query or visualization work, name the next Grafana skill to use after composition.
