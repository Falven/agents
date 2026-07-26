# OpenAI Image Generation Prompting Guide

## Contents

- [Scope and provenance](#scope-and-provenance)
- [Core operating model](#core-operating-model)
- [Model and output settings](#model-and-output-settings)
- [Prompt anatomy](#prompt-anatomy)
- [Prompting fundamentals](#prompting-fundamentals)
- [Text-to-image recipes](#text-to-image-recipes)
- [Image-editing recipes](#image-editing-recipes)
- [Additional production recipes](#additional-production-recipes)
- [Reusable prompt templates](#reusable-prompt-templates)
- [Iteration and review](#iteration-and-review)
- [Freshness and source caveats](#freshness-and-source-caveats)

## Scope and provenance

Official guide: https://developers.openai.com/cookbook/examples/multimodal/image-gen-models-prompting-guide

Source notebook: https://github.com/openai/openai-cookbook/blob/main/examples/multimodal/image-gen-models-prompting-guide.ipynb

Snapshot:

- Guide date: April 21, 2026
- Fetched: July 25, 2026
- Cookbook `main` commit at fetch: `e65bbfc454036e38e27c863c13ff3b3996daed87`

This reference comprehensively paraphrases the official guide's recommendations, parameter table, examples, and production lessons. It omits notebook setup code and generated sample images because they do not change prompt-writing behavior.

## Core operating model

The guide presents GPT image models as production tools for:

- photorealism with natural lighting, materials, and color
- quality and latency tradeoffs
- facial, identity, and character preservation
- legible text and structured layouts
- infographics, diagrams, slides, and multi-panel compositions
- style control and transfer
- real-world knowledge and scene reasoning
- iterative generation and editing

Its central control strategy is simple:

1. State the intended artifact and use.
2. Describe the scene and subject concretely.
3. Specify composition, medium, lighting, and material cues that matter.
4. Separate requested changes from protected invariants.
5. Iterate with small changes instead of continually expanding one prompt.

## Model and output settings

The source snapshot recommends:

| Model | Quality values | Input fidelity | Size behavior | Best fit |
| --- | --- | --- | --- | --- |
| `gpt-image-2` | `low`, `medium`, `high` | Listed as disabled because output is high fidelity by default | Any valid resolution under the constraints below | Default for new production work, high-quality generation and edits, text-heavy images, photorealism, compositing, and identity-sensitive work |
| `gpt-image-1.5` | `low`, `medium`, `high` | `low`, `high` | `1024x1024`, `1024x1536`, `1536x1024`, `auto` | Existing validated workflows during migration |
| `gpt-image-1` | `low`, `medium`, `high` | `low`, `high` | `1024x1024`, `1024x1536`, `1536x1024`, `auto` | Short-term legacy compatibility |
| `gpt-image-1-mini` | `low`, `medium`, `high` | `low`, `high` | `1024x1024`, `1024x1536`, `1536x1024`, `auto` | Lower-stakes batches, rapid ideation, previews, and throughput-sensitive drafts |

### Choosing a model

- Default new production workflows to `gpt-image-2`.
- Prefer `gpt-image-2` for customer-facing assets, photorealism, editing-heavy work, text in images, brand-sensitive creative, and cases where first-pass quality reduces review or retries.
- Try `gpt-image-2` at low quality when speed and unit economics dominate. The guide reports that this can compete well with `gpt-image-1-mini`.
- Use `gpt-image-1-mini` when large exploratory batches and cost matter more than maximum fidelity.
- Keep `gpt-image-1.5` or `gpt-image-1` only while validating migrations or preserving an older, regression-tested workflow.
- During migration, compare the existing prompt unchanged first. Retune after measuring image quality, latency, and retry rates on the real workload.

### Choosing quality

- Start at `low` for high-volume, latency-sensitive, preview, or exploratory generation.
- Compare `medium` or `high` for small or dense text, detailed infographics, close-up portraits, identity-sensitive edits, and high-resolution output.
- Prefer `high` for dense scientific diagrams, slides, chart labels, legends, axes, footnotes, or course material.
- Treat quality as an empirical production choice, not an automatic synonym for better prompt writing.

### `gpt-image-2` size constraints

A requested `size` must satisfy all of these:

- each edge is a multiple of 16
- the longest edge is less than 3840 pixels
- the long-to-short edge ratio is no more than 3:1
- total pixels are at least 655,360
- total pixels are no more than 8,294,400

The guide treats output above `2560x1440` (3,686,400 pixels) as experimental because results become more variable.

Useful sizes:

| Use | Size | Note |
| --- | --- | --- |
| Square | `1024x1024` | General-purpose default |
| Portrait | `1024x1536` | Standard portrait |
| Landscape | `1536x1024` | Standard landscape |
| Widescreen / QHD | `2560x1440` | Recommended upper reliability boundary |
| Near-UHD | `3824x2144` | Valid rounded-down alternative when the strict `<3840` edge rule applies; still experimental |

Choose the canvas from the artifact:

- portrait for posters, people, packaging, mobile UI, and vertical comics
- landscape for slides, charts, workflow diagrams, environments, and deck assets
- square for general-purpose assets without a directional layout

## Prompt anatomy

Use the smallest set of fields that controls the result:

```text
Deliverable and use:
[What is being made and for whom or where it will appear]

Scene or background:
[Environment, context, time, atmosphere]

Subject:
[Who or what, appearance, scale, pose, gaze, action]

Composition:
[Framing, angle, placement, negative space, hierarchy]

Visual treatment:
[Medium, materials, texture, lighting, palette]

Text:
[Exact quoted copy, typography, placement, frequency]

Change:
[For edits, the only requested differences]

Preserve:
[Identity, geometry, layout, labels, lighting, camera, surroundings]

Exclude:
[Unwanted text, watermarks, logos, objects, or stylistic drift]
```

Do not fill every field by default. Omit sections that do not change the desired result.

## Prompting fundamentals

### Structure and intended use

- Keep a consistent order: background or scene, subject, key details, then constraints.
- Name the intended use—ad, UI mockup, infographic, slide, catalog image—to establish the expected polish and visual logic.
- Use short labels or line breaks for complex requests. Simple requests can remain a sentence or short paragraph.
- Choose the format that is easiest to maintain. Plain prose, labeled instructions, tag-like blocks, and JSON-like prompts can all work when the intent and constraints are clear.

### Specificity and quality cues

- Describe concrete shapes, materials, textures, colors, and media.
- Add only targeted quality cues such as film grain, textured brushwork, fabric wear, paper fibers, or macro detail.
- Say `photorealistic` directly when realism is the goal. Phrases such as real photograph, professional photography, or phone photo can also set the mode.
- Use lens and camera language mainly to shape framing and overall look. Do not expect exact optical simulation from detailed hardware specifications.

### Composition and atmosphere

- Specify framing: close-up, medium, full-body, wide, top-down.
- Specify viewpoint: eye-level, low-angle, overhead, three-quarter.
- Specify lighting and mood: soft diffuse light, golden hour, high contrast, dusk, overcast.
- State placement when layout matters: subject centered, logo top-right, negative space on the left.
- Give extra information about scale, atmosphere, and color for wide, low-light, rainy, neon, or cinematic scenes so mood does not replace surface realism.

### People, pose, and action

- State whether the full body and feet must be visible.
- Describe subject scale relative to nearby objects.
- Control gaze explicitly: toward an object, away from camera, at camera.
- Describe physical interaction: how hands grip, where weight rests, what the person is doing.
- For identity-sensitive edits, lock face, features, skin tone, body shape, pose, expression, hair, and proportions as needed.

### Change versus preserve

- State exclusions and invariants explicitly.
- Use `change only [target]` and `keep everything else the same` for surgical edits.
- Repeat the preserve list in every iteration because conversational shorthand can allow drift.
- When precision matters, name saturation, contrast, layout, arrows, labels, camera angle, surrounding objects, geometry, and brand elements individually.
- Avoid impossible blanket preservation requirements; protect only what genuinely matters.

### Text inside images

- Put literal copy in quotes or all caps.
- Require verbatim rendering with no extra characters.
- State whether the copy appears once or multiple times.
- Describe font family or class, weight, size, color, contrast, placement, alignment, and spacing.
- Spell unusual brand names or difficult words letter by letter when character accuracy matters.
- Prefer `medium` or `high` for small text, dense panels, or multiple font styles.
- Iterate with small wording or layout changes if typography is imperfect.

### Multi-image inputs

- Refer to every input by index and role, such as `Image 1: base room` and `Image 2: chair reference`.
- State which element comes from which image.
- State the insertion location and protected base-image elements.
- Require matched perspective, scale, lighting, color temperature, occlusion, contact shadows, and surface interaction.

### Iteration

- Start from a clean base prompt.
- Make one change per follow-up where possible.
- Use contextual references such as `the subject` or `same style as before` for noncritical details.
- Restate critical details whenever they drift.
- Diagnose the smallest failing control—composition, identity, text, lighting, or an invariant—rather than rewriting unrelated sections.

## Text-to-image recipes

### Infographics

Prompt as structured explanation:

- define the audience and learning goal
- list the systems, steps, labels, or relationships that must appear
- specify reading order, arrows, hierarchy, and white space
- request a consistent visual language
- use high quality for dense layouts or heavy text

### Image localization

Treat translation as a preserve-everything-except-text edit:

- name the target language
- require accurate, verbatim translation
- preserve typography style, placement, spacing, hierarchy, logos, icons, and imagery
- allow reflow only when the translated copy cannot fit otherwise
- prohibit extra words and unrelated visual changes

### Natural photorealism

Describe a real moment rather than a studio concept:

- use the word `photorealistic`
- specify candid action, framing, viewpoint, and natural light
- include authentic surface details such as pores, wrinkles, worn fabric, weathering, and imperfections
- request natural color and restrained processing
- prohibit glamorization, heavy retouching, movie-poster grading, or staged polish when those conflict with realism

### World-knowledge scenes

- Give an exact place and time when cultural or historical context matters.
- Request period-appropriate clothing, objects, staging, and environment.
- Do not depend on inference for facts that must be exact; spell out required details and verify factual accuracy separately.

### Logos

- Define brand name, personality, audience, and use.
- Request an original, non-infringing mark.
- Favor a strong silhouette, clean vector-like shapes, balanced negative space, and readability at small and large sizes.
- Prefer flat design and minimal strokes; avoid gradients unless they serve the concept.
- Ask for a single centered mark on a plain background with generous padding and no watermark.
- Use the API's variation count only when multiple alternatives are actually wanted.

### Advertisements

Write a creative brief:

- brand positioning
- audience and cultural context
- campaign concept and desired energy
- scene and composition
- exact quoted tagline
- typography and placement
- prohibited extra copy, watermarks, and unrelated logos

Leave taste-driven art direction to the model inside those boundaries instead of specifying every decorative choice.

### Story-to-comic

- Define canvas orientation and panel count.
- Give one concrete visual beat per panel.
- Make each beat action-focused and sequential.
- Specify equal or intentional panel sizing.
- Keep character, setting, and visual style consistent across panels.
- Add speech or captions only when required, with exact quoted copy.

### UI mockups

- Describe the product as if it already exists.
- Name the screen, device, users, and primary tasks.
- List the real interface sections and content.
- Control hierarchy, spacing, typography, navigation, and density.
- Ask for a usable shipped interface, not concept art.
- Use a device frame only when the presentation requires one.

### Scientific and educational visuals

- Define the audience, lesson objective, and visual format.
- List every required component, label, molecule, stage, or relationship.
- Specify arrows, reading order, icon consistency, label legibility, and white space.
- Prohibit scientifically irrelevant elements and decorative clutter.
- Use high quality for dense labels or production course material.
- Verify scientific accuracy independently; image quality is not evidence of correctness.

### Slides, diagrams, charts, and productivity artifacts

Prompt as an artifact specification:

- name the exact deliverable and canvas
- provide the real title, copy, labels, numbers, sources, axes, legends, and footnotes
- define hierarchy, spacing, typography, and visual language
- use landscape for deck-style output
- use high quality for small type and dense data
- prohibit clip art, stock-photo treatment, excessive gradients, shadows, and decorative clutter when a professional minimal artifact is required

Do not ask the model to invent business metrics or citations. Supply real data or mark placeholders clearly.

## Image-editing recipes

### Style transfer

- Identify the style reference and the content image.
- List the style properties to preserve: palette, texture, brushwork, grain, line quality, or rendering method.
- State the new subject or scene.
- Lock background, framing, and element count when needed.
- Prohibit extra elements that are not part of the transfer.

### Virtual clothing try-on

- Lock identity, face, skin tone, body shape, pose, expression, hair, and proportions.
- Change only the garments.
- Require realistic draping, folds, occlusion, fit, and contact with the body.
- Match original lighting, shadows, and color temperature.
- Preserve background, camera angle, framing, and image quality.
- Prohibit accessories, copy, logos, or watermarks unless supplied.

### Sketch to rendered image

- Preserve the sketch's layout, proportions, perspective, and intent.
- Add plausible materials, lighting, and environmental detail.
- Name the target rendering mode, such as photorealistic, product render, or watercolor.
- Prohibit new objects or text when faithful interpretation matters.

### Product extraction and mockups

- Request a centered product on a plain opaque background.
- Require a crisp silhouette without halos or fringe.
- Preserve geometry, branding, and label legibility exactly.
- Allow only light polishing and an optional subtle contact shadow.
- Prohibit restyling.
- For `gpt-image-2` in the source snapshot, use an opaque result and remove the background downstream when transparency is needed.

### Marketing creatives with exact copy

- Supply the product or subject reference.
- Describe the placement context, such as a billboard or ad.
- Quote exact copy and require it once with no extra characters.
- Specify high-contrast typography, placement, and kerning.
- Prohibit watermarks and unrelated logos.
- Refine text or layout in small iterations when legibility is imperfect.

### Lighting, weather, season, and time changes

- Change only environmental conditions.
- Specify lighting direction and quality, shadows, atmosphere, precipitation, sky, and ground wetness as needed.
- Preserve identity, geometry, camera angle, object placement, and scene composition.
- Require the result to remain recognizably the same photograph.

### Object removal

- Name the single object to remove.
- Say `do not change anything else`.
- Add explicit invariants only if prior attempts drift.
- Inspect the filled background, nearby anatomy, shadows, reflections, and occluded geometry for artifacts.

### Inserting a person into a scene

- Lock identity and any required appearance details.
- Describe action, pose, gaze, location, and scale within the new scene.
- Match natural lighting, color, perspective, surface contact, and environmental effects.
- Request grounded photographic realism when a cinematic or poster-like result would be wrong.

### Multi-image compositing

- Index and describe every source image.
- Name the transplanted element and destination.
- Preserve the base scene, background, framing, and unrelated subjects.
- Match lighting, perspective, scale, color, occlusion, reflections, and shadows.
- Review boundaries around hair, hands, transparent materials, and contact points.

## Additional production recipes

### Interior design swaps

- Replace one named furnishing or finish.
- Preserve room geometry, camera angle, surrounding objects, lighting, and floor shadows.
- Match material texture and realistic contact shadows.
- Avoid turning a swap into a full redesign.

### Physical card and paper-product mockups

- Describe the physical construction: layers, folds, paper fibers, cut edges, and depth.
- Specify tactile materials, studio lighting, and photographed-product composition.
- Quote the only allowed card copy.
- Prohibit trademarks, logos, and watermarks unless intentionally supplied.

### Collectible and merchandise concepts

- Keep the character or product original and non-infringing.
- Describe materials, wear, proportions, packaging, label print, and retail presentation.
- Use premium product-photography cues.
- Quote the only allowed packaging copy.
- Generate variants when comparing character, material, or package directions.

### Children's book character consistency

Use a two-stage workflow:

1. Create a character anchor that establishes facial features, proportions, outfit, palette, demeanor, and illustration style.
2. Reuse that anchor for later scenes while changing only environment, pose, and narrative action.

Every continuation should:

- identify the same character reference
- repeat fixed outfit, features, proportions, and palette
- preserve the illustration medium and tone
- prohibit redesign, text, and watermarks

## Reusable prompt templates

### General generation

```text
Create [deliverable] for [audience or use].

Scene:
[background, setting, time, atmosphere]

Subject:
[appearance, scale, pose, gaze, action]

Composition:
[framing, angle, placement, negative space]

Visual treatment:
[medium, materials, textures, lighting, palette]

Constraints:
- [required element]
- [required element]
- No [unwanted element]
```

### Surgical edit

```text
Change only [target change].

Preserve exactly:
- [identity or subject details]
- [geometry and layout]
- [camera angle and framing]
- [lighting, shadows, and color]
- [labels, text, logos, or surrounding objects]

Do not add [unwanted elements]. Keep everything else unchanged.
```

### Multi-image composition

```text
Image 1: [base scene and protected elements]
Image 2: [source element]

Place [element from Image 2] at [location in Image 1].
Match Image 1's perspective, scale, lighting, color temperature, occlusion, and shadows.
Preserve [base-scene invariants]. Do not change anything else.
```

### Exact text

```text
Create [artifact].

Text (EXACT, verbatim, once, no extra characters):
"[COPY]"

Typography:
[font class, weight, size, color, contrast, alignment, placement]

No other text, watermarks, or unrelated logos.
```

### Identity-sensitive edit

```text
Change only [garment, background, or scene].

Preserve the person's exact identity:
- face and facial features
- skin tone
- body shape and proportions
- hairstyle and expression
- [pose, when required]

Integrate the change with realistic perspective, lighting, shadows, color temperature, and occlusion.
Preserve [background/camera/framing] and add no [accessories/text/logos/watermarks].
```

## Iteration and review

Review the result against the prompt:

- Is the intended artifact recognizable?
- Are all required subjects and relationships present?
- Does composition match framing, angle, hierarchy, and placement?
- Is literal copy exact, legible, and present the right number of times?
- Are identity, geometry, labels, layout, and other invariants preserved?
- Are lighting, scale, perspective, occlusion, and shadows physically coherent?
- Did any prohibited text, logo, watermark, object, or style appear?
- Is factual, scientific, or numerical content accurate when checked against a real source?

Refine by changing only the failed control. Examples:

- `Move the headline higher; keep all other layout unchanged.`
- `Make the light warmer; preserve subject, pose, camera, and background.`
- `Remove the extra tree; do not alter the remaining scene.`
- `Restore the original label exactly; change nothing else.`

## Freshness and source caveats

- Model availability, pricing, parameter names, and limits can change. Use the current official API reference for implementation claims.
- The guide's model table labels the setting as `outputQuality`, while its Python examples pass `quality`. Follow the schema of the API or SDK actually in use.
- The same snapshot says `input_fidelity` is disabled for `gpt-image-2`, but several edit examples still pass `input_fidelity="high"` to that model. Treat this as a source inconsistency. Do not copy the parameter into a `gpt-image-2` call without checking current official documentation.
- The size table mentions `3840x2160` as a familiar UHD target while also requiring the longest edge to be strictly less than 3840. Use a valid rounded-down size such as `3824x2144` if the strict rule applies.
- Image generation can render plausible but incorrect facts, labels, numbers, or diagrams. Review important factual content independently.
