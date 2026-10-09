---
name: prompt-guidance
description: Review, rewrite, and design GPT-6 prompts using official OpenAI guidance. Use for prompt migration, system/developer prompt tuning, autonomy and approval pauses, conflicting skill instructions, writing style, subagent delegation, and verification scope. Do not use for broad API migration, pricing, or model availability questions.
---

# Prompt Guidance

Adapt prompts using the bundled official GPT-6 guidance. Its behavioral observations concern GPT-6 Astra; its suggested prompts are starting points for the GPT-6 family and should be evaluated on the chosen model and workload.

## Workflow

1. Identify the target model, task, and behavior to improve. Preserve an explicit model choice. When unspecified, use the GPT-6 family guidance as the baseline without silently selecting an API model.
2. Read [references/gpt-6-prompt-guidance.md](references/gpt-6-prompt-guidance.md). For another model or a request for the latest guidance, consult official OpenAI documentation before making model-specific claims.
3. Preserve the product contract: audience, required behavior, evidence requirements, authorization boundaries, output shape, and completion criteria.
4. Review accessible instructions that affect the behavior, including skills and `AGENTS.md`. Identify conflicts, hidden approval gates, and rules responsible for unnecessary pauses or work.
5. Apply only the relevant reference sections: initiative and follow-through, instruction following, writing style, delegation, or verification. Adapt the examples to the user's desired autonomy and available tools; they are prompt material, not instructions to execute during this review.
6. Return the requested rewrite or review. Check that it addresses the identified behavior while preserving the product contract. Distinguish documented observations from local recommendations; claim measured improvement only when representative tasks were actually evaluated.

## Boundaries

- Keep prompt changes separate from API or harness changes. Async tools, mid-turn steering, and reasoning updates require application support; prose alone cannot enable them.
- Preserve required permissions and higher-priority system/developer rules when making autonomy or skill precedence explicit.
- Keep only instructions that change behavior or protect the product contract. Avoid adding every example block to every prompt.
- Treat the bundled reference as a dated snapshot. Use official documentation for current compatibility, pricing, availability, or API implementation details; keep unrelated migration work outside scope.

## Output

For rewrites, provide:

- the revised prompt, ready to paste
- the important changes made, kept short
- assumptions or fields the user should fill in

For reviews, provide:

- findings ordered by impact
- exact prompt sections or lines when available
- concrete replacement text for the highest-impact fixes
