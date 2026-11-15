# Interactive administration and result transfer

Read the full active `visualize` skill before creating or updating a fragment. Its output, accessibility, design-system, resource, and state rules apply. The assessment requires passage text, question prompts, response controls, and a short completion instruction as functional test content; keep background research and report prose outside the test. Preserve host typography and control styles. Mark unsupported display experiments as untested rather than overriding the host's design rules.

## Interaction state

Use an explicit sequence: ready → reading → question → optional confidence/trial rating → next trial → completed. Include a short practice or objective calibration item only when needed. There is no intake screen or setup questionnaire. Pause can interrupt an active phase. Keep one current task visible. A visible elapsed timer is optional; pause/resume and explicit submission are required. No speed leaderboard, countdown, or automatic scoring of empty answers.

Keep the required quiet-space instruction and concrete session-duration estimate from `SKILL.md` visible on the initial screen. Let the user prepare before selecting Start; mounting the fragment must not start a test clock.

Persist the study/block/version, frozen assignment, phase, completed responses, draft, timing accumulators, and a monotonic revision counter. Restore only compatible state for that exact block. Listen for `openai:set_globals`; apply newer compatible snapshots without restarting clocks, regressing completed work, or saving back on a state event. Restore active work paused and require Resume.

Use `window.openai.setWidgetState({modelContent, privateContent}).catch(() => {})` after meaningful interactions when supported. Keep the whole snapshot under 16 KiB. `modelContent` can hold compact completion and score summaries; `privateContent` can hold the current UI and bounded recovery data. Neither is secure storage, and `modelContent` delivery is best-effort. Do not rely on either to send results or start an agent turn. Never persist on every timer tick or on load.

Choose a block size and visible response-length limits that keep its full recovery state within the cap. Measure serialized UTF-8 bytes with `TextEncoder`; shorten the next block or use an explicit export checkpoint before exceeding the cap. Never silently truncate answers or discard completed trials to make state fit. Show response limits before entry. A later block starts only after prior results have been exported and received; identify each block distinctly.

## Timing semantics

Use `performance.now()` for elapsed intervals within one page lifetime. Use UTC ISO timestamps for exposure dates and delayed intervals. Never subtract stored monotonic timestamps across a reload. Accumulate elapsed milliseconds and restart the monotonic origin only on explicit Resume.

For reading and each question, retain:

- `wall_ms`: elapsed phase time including known pauses, when measurable.
- `active_ms`: time while the content is visible and the phase is running.
- `paused_ms`: explicitly paused or document-hidden duration, when measurable.
- `pause_count`, `hidden_count`, and timing-quality flags such as `reload_gap`, `clock_gap`, or `timing_unavailable`.

Start the reading clock after the passage renders; stop when the user chooses to begin questions. Start a question clock when that item renders; stop on Submit or Skip, before confidence collection. Store first-response latency for discrete options and revision count if useful, but do not infer cognition from them. Input time includes reading, thought, and motor interaction.

On Pause or `visibilitychange` to hidden, close the current active interval, hide the stimulus/question, and retain the draft. Require Resume to reveal it and restart. Distinguish intentional pauses and hidden intervals. Visibility cannot establish attention; idle time or looking away is not detected. Do not use blur or pointer motion as a measure of comprehension.

If the page closes, sleeps, or reloads, mark uncertainty rather than manufacturing uninterrupted timing. Use wall-clock discrepancies only to flag a possible gap, not to estimate hidden reading. Preserve known intervals; use null for unknown totals. A restored draft may still support an accuracy result while its full response time is invalid. Never substitute zero for missing time. `setInterval` may refresh a display but must not be the clock.

No background telemetry, network requests, eye-tracking claims, or mouse/keystroke surveillance. Collect only interactions needed to interpret this assessment and tell the user what is recorded.

## Copy results: the primary completion action

At completion, show **Copy results** and exactly this short instruction:

> Paste this as your next reply so I can analyze your results.

The button copies a versioned JSON result packet containing all collected data for the block. Use the Clipboard API only from the user's click, if available. Report success only after it resolves. If unavailable or rejected, expose the same complete packet in a labeled, read-only textarea for manual selection and copying. Do not require clipboard permission to finish. A compact completion status can say that open responses await agent scoring.

Provide the same export for an incomplete session, labeled partial. Do not navigate away, reset, or erase results after copying. Copying does not send a message. The user pastes the packet as the next reply. No automatic `sendFollowUpMessage` is needed for this workflow.

Keep the full packet in memory independently of the compact widget summary. Do not truncate exports to fit the widget-state cap. Keep blocks small enough for a practical chat paste; if a large export needs numbered parts, preserve complete records, include part count and block ID, and instruct the agent to wait for every part before aggregation.

## Result contract, version 1

Use these fields or a lossless equivalent. Keep the schema consistent within a study. Null means unknown or not collected. Use stable IDs rather than relying on array order. Do not include a person's name, medical history, or unrelated conversation text.

| Record | Required content |
|---|---|
| Packet | `schema_version`, `study_id`, `block_id`, `manifest_version`, `revision`, `status` (complete/partial), start/end UTC, fixed assessment objective, timing/feedback policies, trial order, environment/accommodation notes actually supplied |
| Context | Agent-selected language, basis for language choice, selected topics and estimated duration; distinguish design assumptions, volunteered information, and objective calibration results; unknown personal attributes remain null |
| Condition | Feature, A/B definitions, package changes if any, and primary outcome planned before exposure |
| Trial | `trial_id`, `pair_id`, role (practice/calibration/baseline/comparison/confirmation), domain, condition, sequence, expected familiarity and separate knowledge evidence if available, passage ID, word count, target-objective IDs, exposure UTC, reading timing, optional ratings with scale definitions, completion status |
| Response | `item_id`, `trial_id`, attempt ID, immediate/delayed phase, item type, actual prompt and option-ID/text mapping, submitted answer or text, first/final choice and revisions if collected, Submit/Skip status, question timing, optional confidence and its separate duration |
| Score | Per-item `points`, `max_points`, `scoring_status` (objective/pending_agent/pending_rubric/unscorable), and key/rubric version; points are null until scored; include objective numerator and denominator separately |
| Delayed trial | Original trial ID, actual delayed-test UTC and elapsed hours, prior retrieval dates and feedback delivered by the assessment, delayed-form ID |
| Data completeness | Excluded or abandoned trials and reasons; timing-quality flags; reload/recovery events; packet part information if split |

Assessment packets must support per-question scoring and timing, not merely aggregate accuracy or words per minute. Include submitted free text verbatim and all final discrete choices. If intermediate choice data, ratings, pause events, or latencies were collected, export them too. Avoid collecting raw events when aggregate counts and durations answer the question.

Keep the generated manifest and rubrics accessible to the agent in the same chat's task-owned files. Include the manifest identifier and path as a locator, not as proof of access. For a fresh chat without the manifest, request the original manifest or mark affected responses unscorable. Do not reconstruct a missing key by guessing. Include question wording in the packet so responses remain interpretable; include rubric/key material only when the feedback policy allows it. Pasting a local path does not give another environment access to that file.

Use client-side objective scoring or mark points pending agent scoring according to the feedback policy. Recompute scores against the manifest on receipt. Keep future delayed questions and their keys out of the initial fragment so they are first presented at the intended time.

## Verification before presenting a generated assessment

Use available local execution or preview tools to check behavior; do not invent a successful browser check. A simulated run is implementation validation, not user evidence. Verify:

- The selected condition and order match the manifest; practice does not enter comparison scores.
- Reading ends before response timing starts; confidence is separate; pause hides content and stops active time.
- Submit commits one item once; Skip is distinct; incomplete text and required choices behave clearly; no answer key or correctness appears early.
- A reload restores completed answers and the draft paused, with timing uncertainty marked; older state cannot overwrite newer work.
- Completion and partial completion export all collected records; **Copy results** has a working manual fallback; copied JSON round-trips and its objective totals match the individual items.
- State byte size stays below the cap with maximum permitted input; identifiers and queried elements exist; no undefined JavaScript identifiers or external API calls are introduced.
- Controls work by keyboard, labels are meaningful, timer ticks do not flood live announcements, and the UI fits the supported widths and themes.

Run the lightest checks that establish these behaviors. If browser inspection or host APIs are unavailable, state exactly which checks remain unverified and keep the manual export available. Keep generated personal data and simulated assessment artifacts outside the reusable skill directory.
