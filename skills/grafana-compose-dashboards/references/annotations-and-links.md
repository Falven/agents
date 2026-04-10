# Annotations and Links

- Treat annotations as dashboard-level annotation queries, not decoration. Add them when deploys, incidents, maintenance, or business events explain metric changes.
- Set annotation scope and visibility deliberately. Show only the event classes that help the dashboard's main task, and avoid noisy annotations that make trends harder to read.
- Use dashboard links for top-level navigation between related dashboards, runbooks, logs, traces, or external systems. Use tag-based dropdown links for sibling dashboard families, and set `keepTime` and `includeVars` when the target should preserve the current investigation context.
- Prefer an overview dashboard plus focused siblings when that keeps the operator's path clear. Link across dashboards instead of cloning the same panels into one overfull page.
- Use panel links when the whole panel should take the user to the next view. Prefer them for drill-down dashboards where the panel itself represents the navigation choice.
- Use data links when the click target depends on the hovered or selected series, field, or datapoint. Map variables explicitly so the destination gets the right label, value, or identifier instead of relying on ambiguous defaults.
- Keep dashboard links, panel links, and data links distinct in the plan. They solve different navigation problems and should not be treated as interchangeable.
- One-click behavior is constrained. Use it only where a single obvious destination exists; otherwise keep the interaction explicit so users can choose among multiple actions.
- Cross-link dashboards instead of cloning them when the only difference is scope, time, or variable context.
