---
name: research
description: Investigate a question against high-trust primary sources and capture the findings as a Markdown file in the repo. Use when the user wants a topic researched, docs or API facts gathered, or reading legwork delegated to background agents.
---

Spin up **subagents** to do the research, so you keep working while they read.

Their job:

1. Investigate the question against **primary sources** (official docs, source code, specs, first-party APIs), not a secondary write-up of them. Follow every claim back to the source that owns it.
2. Once the subagents return, compile findings and either output them to the user, or if specified, to a single Markdown file, citing each claim's source.
3. If writing to a Markdown file, save it where the repo already keeps such notes; match the existing convention, and if there is none, put it somewhere sensible and say where.
