# GPT-6 Prompt Guidance Reference

Source: OpenAI's “Using GPT-6 — Learn best practices, features, and migration guidance for GPT-6 Astra and the GPT-6 model family,” supplied by the user as pasted documentation on 2026-10-09. This summarizes that attachment; it is not a live documentation fetch.

Official guide: [Using GPT-6](https://developers.openai.com/api/docs/guides/latest-model/gpt-6-astra.md#prompting-best-practices).

The behavioral observations below concern GPT-6 Astra. OpenAI presents the prompting advice as a starting point across the GPT-6 family, to evaluate with the chosen model and workload. Example blocks here are condensed adaptations, not verbatim quotations or universal defaults.

## Initiative and follow-through

Astra stays coherent through long tasks but may ask questions or stop where users expect reasonable assumptions and continued work. Define when the agent should proceed, ask, and finish.

For workflows that need autonomy, adapt:

```text
Infer the user's intent and task scope from the instructions and conversation. Treat requests such as "can you", "I want to", and "help me" as requests to act. Carry authorized work through to the intended outcome rather than stopping at a plan or offer to continue.

Fill routine gaps with reasonable assumptions. Ask focused questions when missing information materially changes the result or prevents safe, correct progress. Continue independent, authorized work while awaiting an answer.

Before requesting approval, finish the authorized preparation needed to make the proposed action concrete and reviewable. Use authorization already established in the conversation. Require approval where the action's permissions or destructive or irreversible consequences demand it.

Keep warnings and approval steps tied to actual constraints or risks in the task.
```

Tune clarification behavior to the application. Greater autonomy does not expand the user's task or grant permissions. For workflows where clarification is valuable, keep focused questions rather than imposing blanket silence.

## Instruction following and skill conflicts

Astra follows instructions strongly and can be sensitive to guidance in skills and files such as `AGENTS.md`. Audit the instructions the model can access when it pauses unexpectedly, changes direction, or leaves work incomplete.

Make the priority of user intent over skill guidelines explicit within the application's instruction hierarchy. Preserve higher-priority rules and actual permission constraints.

```text
Prioritize explicit user instructions over conflicting skill guidelines, within system and developer constraints. Distinguish mandatory requirements from recommendations and your own interpretation.

If a skill causes a permission request, pause, unfinished work, or departure from user intent, name and link the exact SKILL.md, quote the relevant instruction, and explain how it applies. Identify whether the restriction is explicit or inferred.
```

Use this traceability to find the instruction causing a pause. Resolve the conflict at its source instead of piling new directives onto the prompt.

## Personality and writing style

Astra tends toward detailed, formatted responses and recurring phrases. Specify the application's desired length, structure, and tone.

For concise prose, adapt:

```text
State the main point early. Use short, connected paragraphs, familiar words, concrete examples, and active verbs. Include the detail needed to understand the result.

Use lists for parallel items, steps, or comparisons. Use tables and headings when they improve scanning. Match technical detail to the reader's background and include it when it explains the result or supports a decision.

State actions directly. Remove stock transitions, repeated summary closers, invented compound labels, and unprompted "X, not Y" contrasts.
```

When specific phrases recur, name the observed phrases to avoid. Keep formatting and terminology required by the product; prose preferences should not override schemas or output contracts.

## Subagent delegation

Astra may delegate less often than a workflow expects. If the harness supports subagents and the workflow authorizes them, specify when delegation is useful and any limits on concurrency or scope.

For workflows that favor parallel work, adapt:

```text
Use available collaboration tools to delegate independent tasks when doing so can save time or improve quality. Keep delegation within the authorized scope and the harness's limits.

Write inter-agent messages and final answers so a human can read them. Use proper grammar and spaces between words and numbers.
```

Tune this to the implementation. A prompt cannot create collaboration tools, and delegation is not a default requirement for every task.

## Testing and verification

Astra can test more broadly than a small coding task warrants. Set meaningful completion criteria and a stopping condition for verification.

```text
Run checks appropriate to the change and complete required validation. Add tests when they meaningfully verify behavior; avoid tests for reversible, low-impact changes that merely mirror the implementation.

Once relevant checks pass, broaden or repeat validation only when further changes, failures, or unresolved concerns justify it. Otherwise, finish the task.
```

Respect explicit user and repository testing requirements. When reviewing a prompt, look for instructions that require broad or repeated checks regardless of the change.

## API and harness context

Use these attachment-derived notes only when they affect the requested prompt. Verify current official documentation before implementing API changes.

- **Reasoning:** Preserve the existing effective effort where supported. Astra and GPT-6.1 Sol do not support `none`; start with `low` instead. For existing `minimal` requests, start with `low` and compare representative tasks. GPT-6.1 Sol supports `low`, `medium` (default), `high`, `xhigh`, and `max`. GPT-6 Sol and Luna support `none`; do not assume identical settings across the family.
- **Tool calling:** Use Responses for reasoning with tools. Astra and GPT-6.1 Sol require Responses for tool calling. GPT-6 Sol and Luna allow Chat Completions function calling only with `reasoning_effort: "none"`.
- **Async tools:** Mark a function or custom tool `async: true` and return its result with the original `call_id`. The application executes tools and tracks pending work; the model can work on independent parts while a tool runs.
- **Mid-turn steering:** The Responses API over WebSocket supports new user instructions while work is underway and retains completed work in a continuation. Prompt the agent to incorporate corrections and answer side questions while retaining the broader task unless redirected.
- **Reasoning updates:** In supported standard, single-agent requests, use `configuration_update` input items to change effort without rewriting the prompt prefix. Keep request-level `reasoning.effort` unchanged for caching; an update persists until another overrides it. Check compatibility before adopting this feature.

The attachment also covers sampling parameters, caching migration, residency, and service modes. Consult the official migration section for those implementation concerns rather than embedding them as agent behavior rules.
