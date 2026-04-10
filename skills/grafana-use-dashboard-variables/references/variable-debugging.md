# Variable Debugging

Start by debugging the variable itself before changing panel queries.

Core checks:

- Use Preview of values in the variable editor to confirm the option list is what you think it is.
- Use Show dependencies to confirm chained variables refresh in the order you expect.
- Check how single-value, multi-value, `All`, and empty states expand into the final query text.
- If a variable preview looks wrong, inspect the selector metric inside the variable definition itself; the label source is often a different metric family than the panels it filters.
- If panels disagree, compare their variable usage, defaults, and formatter choices.
- If the dashboard uses hidden helper variables, do not skip them during debugging; they often bridge `cluster`, `instance`, or node-to-instance selection across panels.

Ad hoc filters:

- Ad hoc filters are injected automatically into queries for supported datasources.
- Do not look for a missing `$adhoc` interpolation string; the failure mode is usually datasource support, filter scope, or query shape.

Repeat-related failures:

- If repeated panels or rows are missing, confirm the repeat variable can actually return multiple values.
- If repeated titles are indistinguishable, add the repeated variable to the title.
- If layout breaks, check whether a horizontal repeat is trying to coexist with other panels on the same row.
- If repeated content looks copied from the wrong source, check the `Dashboard` datasource caveat and confirm the repeat still points at the intended source panel.
- If a carried link or sibling dashboard stops matching, compare the datasource variable names exactly (`ds` vs `datasource`) and any hidden bridge variables the target dashboard expects.

Simplify one variable at a time until the dashboard behaves predictably.
