# Assessment protocol

## Autonomous setup

The fixed objective is to identify the user's ideal presentation profile across the text and language criteria below. Speed, understanding, retention, and usability are measurements within this assessment, not goals for the user to select. Begin the test after the required preparation message. The agent chooses language, topics, difficulty, and duration using the rules in `SKILL.md`; there is no intake questionnaire.

Choose less familiar, demanding concepts when testing acquisition of new knowledge or the benefit of explanatory support. Choose common, easier material when testing efficient processing, navigation, or presentation of established concepts. Use varied subjects to reduce dependence on a single topic. These are design hypotheses about familiarity, not facts about this user. Keep difficulty and expected familiarity matched across A/B conditions so they do not become unintended manipulations.

Use existing performance evidence to choose difficulty. When needed, embed a brief objective calibration item that does not reveal the target facts. Use responses to adjust subsequent blocks, keeping each planned comparison stable. Do not ask the user to name subjects or describe what makes reading difficult. Preserve existing accessibility settings and needs already supplied; use accessible defaults otherwise. Do not infer a diagnosis or remove an accommodation from performance alone.

Tell the user briefly that the task records answers and interaction times, can be paused, and yields provisional guidance from a small sample. No countdown or speed pressure by default. The timer may be visible or hidden; keep that choice consistent across compared trials.

Use a very short practice item only when needed to learn the controls; exclude it from comparisons. Let the initial comparison block also establish task difficulty instead of requiring a separate baseline session. If a separate baseline is necessary, keep it brief and descriptive; it is not an adequate control if it always occurs first.

## Choose a feasible comparison

Choose the minimum work that can meaningfully distinguish the current alternatives. A practical first block can use two matched pairs of short passages, with one fact item and one causal-transfer item per passage, targeting roughly 8–10 minutes including controls and export. This is a planning example, not a validated duration or sample-size threshold. Calculate X from the actual block; shorten it when existing evidence makes fewer observations useful. Do not make a long test battery or a fixed passage quota the default.

Return a usable provisional profile after each completed block. Add a short targeted block only when its result could change a recommendation or resolve an important untested dimension. Stop repeating a comparison when it adds little useful evidence; use fresh-material confirmation for promising findings. Keep a coverage record so brevity does not become a false claim that every criterion was tested. Never promise that a short session establishes a perfect configuration or long-term retention.

Maintain a coverage plan for the presentation features below. Choose the next feature by unresolved evidence and likely information gained, while keeping the complete profile as the objective. A pilot is the first stage, not a substitute for assessing the other criteria. Plan conditions, outcome measures, practical differences worth acting on, and block size before seeing results. Measure reading time, comprehension, and transfer in each comparison, with delayed retention in follow-up sessions and usability ratings alongside performance. Any primary measure chosen for a specific statistical comparison is an agent design decision; it does not replace the other measurements or require a user goal choice. If no defensible numeric threshold exists, call the comparison exploratory rather than choosing one after the scores arrive. Use fixed blocks; review between blocks instead of stopping as soon as one condition leads.

| Feature | A focused comparison | What to hold steady or disclose |
|---|---|---|
| Vocabulary and syntax | Familiar wording vs precise technical wording with definitions | Tested concepts, accuracy, causal links; separate vocabulary from syntax when possible |
| Information density | Compact vs elaborated explanation | Same target propositions; report the added words and exposure time |
| Cohesion | Explicit causal links vs connections the reader must infer | Core facts and logical validity; never deliberately incoherent text |
| Example order | Principle then example vs example then principle | Same example, principle, and word count within each topic's candidate versions |
| Examples or analogy | Literal explanation vs one relevant example or analogy | Target propositions; note added content/time and analogy limits |
| Organization | Connected prose vs headings and grouped points | Same wording as far as feasible; preserve relationships |
| Tone | Direct conversational vs impersonal formal wording | Information, structure, terminology, and length |
| Information order | Main conclusion first vs supporting reasoning first | Same propositions and reasoning |
| Signaling | Plain presentation vs selective emphasis | Identical words; emphasize meaningful relationships |
| Narrative | Expository explanation vs relevant causal narrative | Match target facts; report unavoidable context and length differences |
| Learning supports | Explanation alone vs retrieval prompt or summary | A separate study-strategy experiment; added practice changes learning |
| Display | Readable layout alternatives permitted by the runtime | Accessibility, device, zoom; comfort is distinct from retention |

If multiple properties change together, name the comparison as a presentation package and attribute results only to that package. Do not claim which component caused the difference.

## Material construction and assignment

Create a small manifest before exposing the passages. Keep it in a task-owned location outside the reusable skill. Include:

- Study, block, and manifest version identifiers; fixed assessment objective; feature coverage plan; chosen feature; A/B definitions; planned outcomes and analysis; feedback and timing policies; scoring treatment of skipped, not-reached, and defective items. Report attempted and scheduled denominators separately, and specify before exposure whether skips count as zero in the scheduled score.
- Practice/baseline/comparison roles, domain, learning objectives and target propositions, passage text and word count, source or clearly identified fictional system, and expected difficulty.
- Matched-pair identifier, sequence position, assigned condition, and recorded random assignment or seed plus realized order.
- Question IDs, wording, options if applicable, type (fact, explanation, inference, transfer), target objective, key or rubric, maximum points, and immediate/delayed form.
- Delayed schedule and objectives reserved for delayed-only testing when relevant.

For each candidate topic, draft both conditions against the same proposition checklist. Show the learner only one version. Within a pair, randomly assign two distinct, matched topics to A and B; balance AB and BA order across pairs. Keep domains and prior-knowledge bands balanced across conditions. Freeze the realized assignment before exposure and preserve it on reload.

Do not show the same material twice in different formats and interpret the second reading as an independent comparison. New topics reduce content carryover but introduce topic differences. Counterbalancing cannot prove generated passages equivalent. Repeat across topics and report the remaining confound.

Match concept count, inferential demands, target facts, assessment difficulty, and length when length is not the manipulated variable. Check that every scored answer is supported by the material and that transfer questions require a new application rather than outside trivia. Check alternative correct interpretations, plausible distractors, and inadvertent cues in headings or option wording. Generated materials and rubrics are not normed tests. Fictional systems can reduce prior knowledge but limit generalization; mark them clearly and validate later on real material.

Record expected topic familiarity separately from measured knowledge. Use existing context or a brief non-target objective item only when knowledge calibration is necessary; otherwise leave actual familiarity unknown. Do not pretest the very facts the passage is meant to teach. Record any material substitution before exposure; never remove a low-scoring trial after seeing its result. No self-report familiarity survey is required.

## Trial sequence

1. **Ready:** Show neutral trial identification and Start. Do not reveal the passage or future quiz. Avoid labels such as “optimized version.”
2. **Read:** On Start, reveal the passage and begin reading time after it renders. Use self-paced exposure by default. The user ends reading explicitly. Hide the source when testing starts.
3. **Respond:** Present one question at a time. Use a consistent battery across conditions, such as one fact item, one short causal explanation, and one inference or transfer item. Match question types and points across paired passages. Include a genuine new-application item to support claims about depth.
4. **Confidence:** After committing an answer, optionally collect 0–100% confidence that it is fully correct; time this separately. Missing confidence is null, not an implicit midpoint.
5. **Experience:** Include a brief rating of the completed trial only when it informs the comparison. Ask about that specific experience, not general reading preferences or difficulties. Keep ratings separate from performance and omit redundant ratings to reduce burden.
6. **Continue or finish block:** Offer a break. Commit completed results and provide a complete partial export if the user stops early.

Use a predefined, criterion-based rubric for open responses: required factual or causal elements, partial credit, errors that invalidate an element, and acceptable paraphrases. Score each element once. Reward conceptual accuracy rather than matching vocabulary, prose length, or spelling unless language accuracy is explicitly the target. A simple 0/1/2 rubric can mean incorrect/missing, one of two required elements, both elements; define the actual elements for each question before exposure.

Default to one committed response per item, allowing changes before Submit. Record changes as a count and first/final choice for discrete options; do not capture keystroke streams. Explicit Skip produces a missing-response status, distinguishable from an incorrect submitted answer. Lock completed trials to avoid accidental retakes; a retake is a new labeled attempt.

Keep passage visibility, question format, and feedback policy consistent across conditions through the test interface.

## Delayed retention and confirmation

The agent selects a practical target such as 48 hours for a brief retention check and states it after the current assessment; do not ask the user to choose a schedule or commit before starting. Add a later check only when it resolves an important remaining question. Honor volunteered scheduling constraints. Record the actual exposure-to-test interval for every trial; compare similar delays. These intervals are options, not universal optima.

Keep answer keys and corrective feedback out of the visible immediate-test flow until the planned delayed outcomes are collected. Delay question-specific feedback and revealing profile examples that disclose the tested content. If the user requests feedback sooner, provide it and mark later retention as occurring after feedback. Always preserve the user's ability to stop.

Per-item scores can also disclose correctness. When delayed testing is planned, default to pending agent scoring in the copied packet, score internally after receipt, and defer the per-question score report until the delay is complete. If scores appear in an export or interim report, record that disclosure as feedback and apply the same policy across conditions. The agent can still provide a provisional presentation profile without revealing individual answers.

Immediate retrieval changes later memory even without feedback. Standardize immediate testing across conditions. Report “retention after immediate testing,” or reserve comparable objectives for delayed-only testing when the design requires it. A 48-hour test also affects a later one-week test; record both. Parallel delayed items should test the same constructs without simply repeating recognized options, with comparable scoring and no source access.

Record feedback and repeated testing delivered by the assessment itself. Missing delayed data means retention is unknown.

Use fresh topics to confirm candidates after exploratory selection. Confirm combinations separately: two individually promising features may interact. Reassess when the user's expertise or reading contexts change. Respect session limits and stopping requests; a short session yields a provisional profile with the remaining coverage identified.
