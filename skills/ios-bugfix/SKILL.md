---
name: ios-bugfix
description: Fix iOS app bugs in isolated worktrees, verify them in Simulator with agent-device, and return a short proof clip.
metadata:
  inspiration: https://github.com/mattpocock/skills/blob/main/skills/engineering/diagnosing-bugs/SKILL.md
---

# iOS Bug Fix

Build a **tight feedback loop** around the user's exact symptom. Keep the fix and its proof together.

## Phase 1: Isolate

Read the project instructions, relevant glossary/ADRs, and existing build and test commands.

Reuse a suitable worktree or create one from the intended base. Prefer the host's managed worktree tools; use their returned path. Preserve the user's existing changes.

Bind the worktree to an explicit simulator UDID, app bundle, build directory, and automation session. Concurrent fixes need separate simulators and account/data state. For React Native, also bind the Metro port and project root. Confirm the running app comes from this checkout.

Use the installed `agent-device` CLI for simulator interaction; consult its help for syntax. Its implicit sessions are worktree-scoped; explicit session names must be unique. Keep the simulator and build cache warm. If tooling is unavailable, report the missing prerequisite and continue independent diagnosis.

## Phase 2: Build a feedback loop

Choose the account role, fixture, and starting screen that reproduce the bug. Reuse the project's account profiles and navigation flows. Assert the account identity before reusing a signed-in session.

**Credentials stay out of the conversation.** Use account aliases and vault references. Enter credentials through the project's trusted login helper or pipe vault output directly into `agent-device fill --text-stdin --no-record`, bound to the assigned session and verified login field. Never retrieve a password into one tool response to paste into another. Ask for missing account configuration, not the password; continue work that does not require login.

`--no-record` suppresses action scripts, not video. XCTest logs and `.xcresult` can still contain typed values. Use test accounts and keep raw authentication artifacts private. An unrestricted coding agent remains trusted.

Navigate through accessibility identifiers or fresh element references. Batch known steps, wait for observable conditions, and use screenshots when the tree cannot establish the target or result. Reuse existing deep links where they preserve the relevant bug path.

Build the smallest **red-capable** check: an existing test, replayable UI flow, or temporary harness that asserts the user's exact symptom. Run it before editing when practical. A successful launch or tap is not a pass.

Done when you can name the executed check, show its failure, and state what would make it pass. If reproduction is unavailable, state that limit; keep a hypothesis distinct from a verified fix.

## Phase 3: Fix + verify

Trace the relevant callers. State falsifiable hypotheses, test one variable at a time, and fix the cause. Remove temporary instrumentation afterward.

Use the existing build path and preserve incremental state within this worktree. Rebuild changed native code; reload the correct Metro bundle for applicable JS-only changes. Reuse prepared test products only while their source and configuration are unchanged.

Run the relevant existing tests and required repository checks. Add permanent tests only within the task's scope and repository policy.

Run the original check against the changed build, with the same account and fixture. Assert the expected outcome; explain any change to the check. Preserve failed attempts instead of retrying them into an unexplained pass.

## Phase 4: Capture proof

Record the passing verification itself. Start after login and navigation unless those steps are the bug being tested. Aim for 10–30 seconds showing the trigger and result.

Use `agent-device record start/stop` for the assigned session, or native `simctl` recording with an explicit UDID and H.264. Stop and finalize the owned recorder even if the check fails. Verify the video plays and contains the relevant action and result. Keep timing intact for performance bugs.

The assertion is the test result; the clip is evidence. Report a recording failure separately from a functional pass. Inspect the clip and selected output for secrets and personal data before sharing.

## Phase 5: Report

Return:

- The trigger, cause, and change.
- The exact checks run and their outcomes, including whether the old failure was reproduced.
- The clip, tested revision/build, simulator/runtime, and account alias.
- Material behavior left untested.

Preserve the worktree for follow-up and keep the evidence outside it before cleanup.

When a PR is requested, use the repository's template and publish the tested state. Attach the sanitized clip with `gh pr create --body-file ... --attach ...` when supported. A failed attachment can still create the PR: check the returned URL and repair the attachment on that PR. Verify the uploaded clip before declaring completion. Reuse existing verification unless subsequent changes invalidate it.
