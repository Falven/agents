---
name: assess-learning
description: Assess how text presentation affects a person's learning with interactive reading trials, then interpret pasted results into a conditional reading and learning profile. Use for personalized learning-style tests, controlled text comparisons, and follow-up retention assessments; not ordinary quizzes about a subject.
---

# Assess Learning

The objective is fixed: identify the user's ideal configuration of text, language, explanation, and visual organization for learning. Build the most complete presentation profile supported by controlled performance comparisons. Measure speed, comprehension, depth, retention, and usability as complementary evidence toward that one objective. Do not ask the user to choose a goal, rank these outcomes, or supply optimization weights.

Discover presentation needs through the assessment. Use volunteered preferences or ratings of completed trials as separate evidence, without a preference questionnaire. The result is a task- and context-dependent profile, not a fixed learner type or a standardized psychological diagnosis. Seek the ideal configuration without claiming that a finite assessment proves a universally perfect one.

Assume good-faith participation. Keep the experience focused on learning; omit help-use questions, honesty attestations, and warnings about consulting notes, passages, or other sources.

## Route the request

- **Start or continue an assessment:** Read [protocol.md](references/protocol.md) and [interaction.md](references/interaction.md). Use `$visualize:visualize` to administer the assessment in the conversation. Locate and read its full current `SKILL.md` from the available skill catalog; do not hardcode a user's plugin-cache path or copy its design system here. If unavailable, explain the specific dependency and offer a chat-based assessment with self-reported timing. Do not silently replace the requested interactive test.
- **Interpret pasted results:** Read [interaction.md](references/interaction.md) for the data contract and [analysis.md](references/analysis.md) for scoring and profile construction. Analyze only data actually received. Continue to delayed or confirmation trials when requested.
- **Explain the scientific basis or extend the design:** Read [evidence.md](references/evidence.md). Verify new research claims against primary sources. The bundled protocol is an experimental design, not a validated diagnostic instrument.

If asked to create or modify this skill, work on the skill files; do not start a personal assessment as a side effect.

## Required opening

When starting an assessment session, begin the first user-facing message with: **“Find a quiet, distraction-free space where you can spend about X minutes on this assessment.”** Use the assessment language for this message. Replace X with a concrete estimate for the upcoming session block before displaying it, then present the test directly. Do not insert a setup questionnaire or wait for a preparation reply; the test's Start control lets the user begin when ready.

The agent chooses the shortest useful block and estimates its duration from the passages and questions, including any practice, ratings, and copying results. Use observed completion times for later blocks. The estimate covers this session, not the full multi-session assessment or the waiting period before delayed tests. Treat it as an estimate, not a time limit; preparation time is excluded from reading and response timing. Do not ask how much time the user has.

## Assessment workflow

1. Recover relevant background and any completed trials. Treat interface defaults, example profiles, and hypothetical scores as unmeasured. A conversation about learning is not evidence that a test has started.
2. Configure the assessment autonomously. Infer the language from an explicit instruction or a clear cue accompanying invocation (even a Spanish word can indicate Spanish), then known conversation context; default to English when no cue is available. Choose subjects and difficulty to answer the current assessment hypothesis. Preserve known accessibility needs and volunteered constraints. Do not ask for language or proficiency, familiar subjects, reading difficulties or preferences, available time, or willingness to return. Follow `protocol.md` for objective calibration within the test.
3. Before exposure, prepare a versioned assessment manifest with stimuli, assignments, questions, answer keys, rubrics, planned comparisons, and scoring rules. Follow the protocol's controls. Track coverage of the presentation criteria across blocks. Success means identifying which settings and combinations improve learning, with all measured outcomes and unresolved tradeoffs visible.
4. Generate one manageable assessment block with `visualize`. Present passages and questions sequentially; time reading separately from each response. Include pause/resume, explicit submission, and completion status. Follow the runtime and data contract in `interaction.md`.
5. End the block with **Copy results** and the concise instruction: **“Paste this as your next reply so I can analyze your results.”** Copy every collected response and its timing, not just a total score. Provide selectable result text if clipboard access fails. This is the primary handoff; widget state is only a recovery aid.
6. Once the user pastes the packet, validate it, score open answers with the prepared rubrics, and build or update the profile. Keep measured results, reported preferences, and untested dimensions distinct. A small pilot produces provisional recommendations; comprehensive coverage includes explicit unknowns.
7. When retention evidence is needed, specify a brief follow-up and target return time after the current results, using the same study and trial identifiers. Record actual delays and feedback delivered by the assessment. Do not require an advance commitment to return. Create reminders only if requested through an available scheduling tool. Never imply that a future test ran automatically.

## Scope and completion

Cover language, conceptual organization, examples, explanation depth, information order, tone, density, and meaningful formatting. Include supported typography and layout comparisons in the coverage plan; mark runtime limitations explicitly. Audio is an optional extension when requested. Preserve accessibility settings across conditions; do not make text hard to read to manufacture a learning effect.

For each generated block, completion means the questions and scoring were checked, timing and export behavior were verified to the extent the tools permit, and the interactive test was presented with its visualization content reference. Report any unverified runtime behavior honestly.

For a profile, completion means the agent received actual results, reported scores and time by question, compared the tested conditions with their limitations, covered the requested presentation dimensions (including those untested), and supplied usable conditional presentation rules. If no results exist, give the next assessment step rather than inventing a profile.
