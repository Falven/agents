---
name: prompt-guidance-image-generation
description: Review, rewrite, and design prompts for OpenAI image generation and editing using bundled official guidance. Use for text-to-image prompts, surgical image edits, multi-image compositing, identity or character preservation, text inside images, photorealism, infographics, diagrams, ads, logos, UI mockups, product imagery, style transfer, model and quality tradeoffs, or iterative prompt refinement. Do not use merely to generate an image when prompt guidance is not needed.
---

# Prompt Guidance: Image Generation

Use this skill to turn an image request into a clear, production-ready prompt or to diagnose why an existing prompt drifts, misspells text, changes protected details, or produces the wrong composition.

Read [references/openai-image-generation-prompting-guide.md](references/openai-image-generation-prompting-guide.md) before rewriting or reviewing a prompt. It is a comprehensive, paraphrased snapshot of OpenAI's `gpt-image-2` prompting guide dated April 21, 2026.

## Workflow

1. Classify the task as generation, edit, localization, style transfer, identity-sensitive edit, multi-image composition, or iterative refinement.
2. Identify the deliverable and intended use: photograph, ad, logo, infographic, diagram, slide, UI mockup, product asset, illustration, comic, or other artifact.
3. Capture only the controls that affect the result:
   - scene or background
   - subject and action
   - composition, viewpoint, lighting, and medium
   - literal text and typography
   - elements to change
   - invariants to preserve
   - exclusions
4. Write the prompt in a stable order: intended use and scene, subject, key visual details, layout, then constraints. Use short labeled sections only when the request is complex.
5. For edits, say `change only X` and restate every critical invariant on each iteration. Include identity, geometry, layout, camera angle, lighting, labels, brand elements, and surrounding objects only when they truly must remain unchanged.
6. For multiple inputs, identify each image by index and role, then state what moves from which image, where it goes, and how lighting, perspective, scale, and shadows should match.
7. Put required in-image copy in quotes, require it verbatim and exactly once, specify placement and typography, and prohibit extra text. Prefer `medium` or `high` quality for dense or small text.
8. Keep quality cues targeted. Use concrete materials, textures, framing, and atmosphere; do not pile on vague superlatives or pretend camera specifications guarantee exact physical simulation.
9. Prefer one clean base prompt followed by small, single-change iterations. Reassert critical invariants if they begin to drift.
10. Return the ready-to-paste prompt first. Add suggested model, size, and quality only when the user needs API settings or the choice materially affects the result.

## Defaults

- Use a model-neutral prompt unless the user asks for API settings.
- When applying the bundled snapshot, treat `gpt-image-2` as its documented default for new production workflows.
- Start latency-sensitive or high-volume work at `quality="low"` and compare `medium` or `high` for dense text, detailed diagrams, close portraits, identity-sensitive edits, or high-resolution output.
- Use `1024x1024` when no orientation is implied. Choose portrait or landscape from the deliverable rather than adding an aspect ratio reflexively.

## Boundaries

- Do not invent current model availability, prices, parameter support, or limits. Refresh official OpenAI documentation when the user asks for the latest behavior.
- Do not copy every possible visual adjective into the prompt. Include only details that change the intended result.
- Do not weaken identity, label, geometry, or layout preservation requirements in editing tasks.
- Do not pass `input_fidelity` to `gpt-image-2` solely because some examples in the source notebook do so; the same source's model table says the parameter is disabled for that model. Verify the current API reference when this parameter matters.
- Do not broaden prompt guidance into API integration, asset pipelines, evaluation systems, or image generation unless requested.

## Output

For a rewrite, provide:

- the revised prompt, ready to paste
- suggested settings when relevant
- short assumptions only when they affect the image

For a review, provide:

- findings ordered by impact
- concrete replacement text
- one recommended revised prompt

## Reference Map

- [references/openai-image-generation-prompting-guide.md](references/openai-image-generation-prompting-guide.md) -> Model choices, size constraints, prompt fundamentals, generation and editing recipes, reusable templates, iteration guidance, and source caveats.
