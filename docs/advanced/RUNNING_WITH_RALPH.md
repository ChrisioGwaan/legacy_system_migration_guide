# Running The Wiki With An Autonomous Loop (Ralph Orchestrator)

This document explains how to drive this LLM Wiki template with an autonomous loop runner, using [Ralph Orchestrator](https://github.com/mikeyobrien/ralph-orchestrator) as the example.

It is written for human readers. Operational rules for agents still come from `AGENTS.md`. Ralph Orchestrator is a third-party project; this page describes a pattern, not an endorsement or a dependency.

## Why combine them

Ralph Orchestrator implements the "Ralph Wiggum technique": keep an AI agent in a loop until the work is genuinely finished, with quality gates that reject incomplete output. It is an execution engine.

This template is a persistent, structured knowledge base with a schema, status labels, traceability, and a log. It is a memory and governance layer.

They solve opposite halves of the same problem:

> Ralph is the engine that keeps working. The wiki is the memory that keeps the engine from drifting, repeating work, or losing the thread between iterations.

A bare autonomous loop re-derives context on every pass and tends to repeat work or hallucinate. The wiki gives each iteration a durable place to read state from and write results to. In return, the loop gives the wiki something it does not ship on its own: an autonomous runner.

## Division of labour

| Ralph Orchestrator | This template |
| --- | --- |
| The loop and its iterations | `wiki/log.md` timeline plus the Resume/Onboard prompt as the per-iteration bootstrap |
| Runtime "Memories & Tasks" | `wiki/` as canonical durable memory; open questions and backlog as the task queue |
| Hat system (code-assist, debug, research, review) | AI Agent Council roles and the per-role prompts in `docs/PROMPT_RECIPES.md` |
| Backpressure (tests, lint, type checks) | Definition of Done plus the Traceability and QA recipe |
| `LOOP_COMPLETE` or iteration cap | A meaningful completion signal: no open questions and QA readiness met |
| Planning mode (requirements, design, plan) | Discovery to backlog to slice; file plans into `wiki/` pages, not loose files |
| Telegram human-in-the-loop | The "mark `unclear`, escalate, do not silently choose" rule |
| Backend (Claude Code, Codex, Gemini, ...) | `AGENTS.md` as the standing contract applied every iteration |
| High iteration count and cost | `wiki/capabilities.md` keeps each iteration context-lean |

## Wiring it up

1. Initialize the runner in the repository with your backend, for example `ralph init --backend claude`. With Claude Code, `CLAUDE.md` points to `AGENTS.md`, so the wiki guardrails govern every iteration automatically.
2. Use a per-iteration loop prompt that bootstraps from the wiki and defines completion:

```txt
Read AGENTS.md, wiki/index.md, and wiki/log.md. Choose the highest-priority open item: an open question, a backlog slice, or a QA gap. Complete it following AGENTS.md. Update the relevant wiki pages and append to wiki/log.md. If no open items remain and QA readiness is met, output LOOP_COMPLETE.
```

3. Map the runner's hats to the council role prompts in `docs/PROMPT_RECIPES.md`. For example: research to Source Analyst, code-assist to Implementation, review to QA Reviewer.
4. Make the Traceability and QA recipe a backpressure gate. A slice is not complete until it traces back to source evidence, passes tests under `target/`, and is synced to the wiki.
5. Keep `raw/` read-only to the loop. `AGENTS.md` already forbids editing evidence; an autonomous loop makes that rule more important, not less.

## Completion signal

A loop runner stops on a signal such as `LOOP_COMPLETE` or an iteration cap. Drive the first from wiki state rather than the agent's mood:

- no pages with `status: unclear` that block the current goal
- the backlog or open-questions list is empty for the current scope
- the Traceability and QA check reports no untraceable or untested items

This turns "the agent thinks it is done" into "the wiki shows it is done."

## Cautions

- **Source evidence under autonomy.** The biggest risk is an unattended loop touching `raw/`. Enforce immutability and review `wiki/log.md` and git diffs between runs. Because the wiki is markdown in git, every iteration is a reviewable diff.
- **Two memory systems.** Declare the wiki canonical, matching the authority order in `AGENTS.md`. Treat the runner's runtime memory as ephemeral; durable findings belong in the wiki.
- **Drift over many iterations.** Status labels, traceability, and QA backpressure counter this, but keep a human checkpoint for business-critical work, for example a review after each council pass or every N iterations.
- **Runaway cost.** Rely on the wiki completion signal and the iteration cap together, not either alone.

## Lighter alternatives

You do not need a separate orchestrator to loop. Some backends can loop on their own, for example Claude Code's `/loop`. A dedicated runner like Ralph Orchestrator adds multi-backend support, the hat system, backpressure quality gates, a dashboard, and human-in-the-loop messaging. Choose the lightest tool that fits the project.

## Capability registry note

For projects that use an autonomous runner, add a row to `wiki/capabilities.md` so the loop stays context-lean and the choice is auditable:

| Task type | Recommended capability | When to use | Required wiki context | Notes |
| --- | --- | --- | --- | --- |
| Autonomous loop | Autonomous loop runner (external) | Unattended implement, verify, and sync cycles | `wiki/index.md`, `wiki/log.md`, relevant pages | Optional. Wiki is canonical memory. Keep `raw/` read-only. |

## Important principle

The loop should make the wiki more complete and more traceable on every pass, not just produce more code.

> If an iteration changes the target but not the wiki, the loop is drifting. Every iteration should either update the wiki or record why no update was needed.

This is the same rule the rest of the template follows. The orchestrator simply applies it many times without getting bored.
