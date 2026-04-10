# Layout and Scannability

- Put the highest-value summary panels in the first screen. The dashboard should answer its main question before the user scrolls.
- Keep the first screen compact: a summary band up top, then lower-priority rows collapsed or moved to sibling dashboards.
- Group panels by question, usually overview first, diagnosis second, and drill-down last.
- Use flat row headers as separators when a section needs visual structure but not a collapsed container.
- Use collapsed row containers when the row is a detail bundle. Keep nested child panels inside the row so the section can disappear cleanly.
- Use hybrids when the summary should stay visible but deeper sections should collapse.
- Choose `Custom` layout when panel sizes and positions need deliberate placement for comparison or narrative flow. Choose `Auto grid` when the dashboard benefits from faster assembly and uniform sizing more than exact placement.
- Use tabs only when the groups are meaningfully separate views, not just a long page split into buckets.
- Repeat panels or rows only when a repeated variable view is the core task. Repetition is useful for symmetrical comparisons, but it becomes noise when the user still has to scan every instance manually.
- Keep related panels aligned so operators can compare them without hunting across different widths or unrelated sections.
- Treat placeholder markdown blocks and blank row titles as layout debt inside a populated dashboard.
- Avoid long dashboards whose critical information sits below the fold. Prefer fewer panels with clearer intent over a wall of partially useful charts.
