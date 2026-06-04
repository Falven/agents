# GPT-5.5 Prompt Guidance Reference

Source: https://developers.openai.com/api/docs/guides/prompt-guidance.md
Related source: https://developers.openai.com/api/docs/guides/latest-model.md
Source discovery: https://developers.openai.com/llms.txt -> https://developers.openai.com/api/docs/llms.txt -> prompt-guidance.md
Fetched: 2026-06-04
Last-Modified: Thu, 04 Jun 2026 15:05:55 GMT

This is the only bundled reference currently included in the generic `prompt-guidance` skill. It summarizes the official OpenAI GPT-5.5 Markdown guide and related latest-model notes without copying the full source.

## Core Shift

- Prompt GPT-5.5 with the desired outcome, constraints, available evidence, and final answer shape. Let the model choose the efficient path unless the path is part of the product contract.
- Start from the smallest prompt that preserves required behavior. Older prompt stacks often over-specify process because earlier models needed more scaffolding.
- Re-evaluate reasoning settings before escalating. The latest-model guide says GPT-5.5 defaults to `medium`; many tasks should test `low` or `medium` before `high` or `xhigh`.
- Use `text.verbosity` intentionally. Keep output length separate from reasoning quality.
- For tool-heavy Responses workflows, preserve preambles, assistant-item replay, and `phase` handling.

## Outcome-First Prompts

Write prompts around:

- role and context
- user-visible goal
- success criteria
- constraints and side-effect limits
- source, evidence, or data requirements
- output shape
- stop, retry, fallback, ask, or abstain rules

Prefer outcome and decision rules over rigid step lists. Keep `always`, `never`, `must`, and `only` for true invariants such as safety rules, required fields, or prohibited actions.

Minimal pattern:

```text
Goal: [user-visible outcome]
Success criteria: [what must be true before answering]
Constraints: [policy, source, safety, and side-effect limits]
Output: [format, length, and tone]
Stop rules: [when to answer, retry, ask, fallback, or abstain]
```

## Personality And Collaboration

Use personality instructions to shape how the assistant sounds: tone, warmth, formality, empathy, humor, and polish. Use collaboration instructions to shape how it works: when to ask, assume, proceed, verify, explain, and handle uncertainty.

Keep both short. They should not replace goals, success criteria, tool rules, or stopping conditions.

## Preambles And First Visible Token

For multi-step, tool-heavy, or long-running tasks, ask the model to start with a brief visible preamble before tool calls. The preamble should acknowledge the request and state the first step in one or two sentences.

Use this only where visible progress matters. Do not add preambles to tiny single-step answers where they add noise.

## Formatting And `text.verbosity`

Set formatting only where it improves comprehension or a product UI needs a stable shape. For normal prose, prefer clean paragraphs and light structure. Use headers, bullets, tables, JSON, or strict schemas only when the user or product contract needs them.

For concise answers, set `text.verbosity` to `low` and still specify any hard length limits. For rewrite, summary, or editing tasks, tell the model what to preserve before asking it to improve style: artifact type, length, structure, genre, claims, and audience.

## Grounding, Citations, And Retrieval Budgets

For grounded answers, define:

- which claims need source support
- what evidence is sufficient
- citation format
- what to do when evidence is missing
- when to stop retrieving

Retrieval budgets are search stopping rules. Start with the smallest search that can answer the core question. Search again only when the result does not answer the core request, a required fact is missing, the user asked for exhaustive coverage, a specific artifact must be read, or the answer would otherwise make an important unsupported factual claim.

Do not search again just to improve wording or cite nonessential details.

## Creative Drafting Guardrails

For slides, launch copy, leadership blurbs, talk tracks, summaries, and narrative framing, separate source-backed facts from creative wording.

- Source concrete product, customer, metric, roadmap, date, capability, and competitive claims.
- Do not invent names, metrics, roadmap status, customer outcomes, or product capabilities.
- If support is weak, use placeholders or labeled assumptions instead of unsupported specifics.

## Frontend And Coding Prompts

For frontend prompts, point the model at product context, user context, design-system constraints, first-screen usability, states, responsive behavior, accessibility, and visual defaults to avoid. The official guide points to the frontend prompt guide for detailed UI instructions.

For coding agents, include orchestration and validation expectations:

- inspect relevant code before editing
- reuse existing primitives
- keep changes scoped
- run targeted tests, type checks, lint checks, builds, or smoke tests when applicable
- explain when validation cannot run

## Validation Loops

Give the model tools and permission to verify outputs when verification is possible.

- Code: run the narrowest relevant validation after changes.
- Visual artifacts: render and inspect for layout, clipping, spacing, missing content, and consistency.
- Plans: make requirements traceable to implementation surfaces, data flow, validation, failure behavior, and open questions.

Avoid verification theater. The check should be capable of catching real defects.

## Responses API `phase` Handling

If an application uses `previous_response_id`, prior assistant state is preserved automatically. If it manually replays assistant output items into the next request, preserve each assistant item's original `phase` value unchanged.

Prompt guidance for manual replay:

```text
Preserve assistant phase values exactly. Use commentary for intermediate updates and final_answer for the completed answer. Do not add phase to user messages.
```

This matters most when a response includes preambles, repeated tool calls, or final answers after intermediate updates.

## Suggested Prompt Skeleton

Use this as a starting point for complex prompts and remove sections that do not change behavior:

```text
Role: [function, context, and job]

# Personality
[tone and collaboration style]

# Goal
[user-visible outcome]

# Success criteria
[what must be true before the final answer]

# Constraints
[policy, safety, evidence, and side-effect limits]

# Output
[sections, length, and tone]

# Stop rules
[when to retry, fallback, abstain, ask, or stop]
```
