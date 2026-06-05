# Prompt Recipes

Copy these prompts as starting points. Replace bracketed text with your project details.

Every recipe starts with "Read AGENTS.md ..." on purpose: that way the schema loads even if your AI tool does not auto-load it. See `docs/USING_WITH_AI_TOOLS.md`.

Each recipe lists when to use it and what you should get back.

## Initialize The Wiki

**When to use:** the first time you run a new project, after putting sources in `raw/`.
**What you get back:** an initial wiki, an updated index and log, and a list of gaps and open questions.

```txt
Read AGENTS.md, README.md, raw/manifest.md if useful, and the files under raw/. Build the initial wiki under wiki/, update wiki/index.md, append to wiki/log.md, and report missing source materials, assumptions, contradictions, and unclear areas.
```

*Tip:* add your sources to `raw/` before running this. If `raw/` is empty, the agent has nothing to build from.

## Resume Or Onboard A New Session

**When to use:** starting a fresh chat or a new agent on an existing project, to rebuild context without re-reading everything yourself.
**What you get back:** a summary of project state, recent activity, open questions, and a recommended next step. Nothing is changed.

```txt
You are picking up an existing LLM Wiki project. Read AGENTS.md, wiki/index.md, and wiki/log.md. Summarize the current state, what was done most recently, the main open questions, and the single best next action. Do not change any files yet.
```

*Example:* run this at the start of every session before asking for new work, so the agent acts from the wiki instead of guessing.

## Ingest One Source

**When to use:** you added a single new file to `raw/` and want it carefully integrated.
**What you get back:** new or updated source, concept, and entity pages, with the index and log updated.

```txt
Read AGENTS.md, wiki/index.md, wiki/log.md, raw/manifest.md if useful, and [raw/path/to/source]. Ingest this source into the wiki. Create or update relevant source, concept, entity, question, and synthesis pages. Update wiki/index.md and wiki/log.md.
```

*Example:* [raw/path/to/source] -> `raw/transcripts/2026-06-05-customer-call.md`

## Batch Ingest Sources

**When to use:** you dropped several files into `raw/` at once and want them processed together.
**What you get back:** wiki updates across all new sources and one summary log entry for the batch.

```txt
Read AGENTS.md, README.md, raw/manifest.md if useful, wiki/index.md, and wiki/log.md. Ingest the new sources under raw/ or the subset I specify. Keep source claims traceable, mark unclear details, update cross-links, update wiki/index.md, and append one log entry summarizing the batch.
```

*Example:* "...or the subset I specify" -> "only the files under `raw/papers/` added this week."

## Ask A Question Against The Wiki

**When to use:** you want an answer grounded in what has already been ingested.
**What you get back:** an answer from the wiki that separates source-backed facts from inference and lists gaps.

```txt
Using wiki/index.md first, find the relevant wiki pages and answer this question from the wiki: [question]. Distinguish source-derived claims from inferred claims and list any unresolved gaps.
```

*Example:* [question] -> "Which pricing model did the three vendor reports recommend, and where do they disagree?"

## File A Useful Answer Back Into The Wiki

**When to use:** a chat answer was valuable and you do not want it lost in history.
**What you get back:** a new or updated wiki page, new cross-links, and updated index and log.

```txt
The answer we just discussed is durable. File it back into the wiki as either a new page or updates to existing pages. Add links from related pages, update wiki/index.md, and append to wiki/log.md.
```

*Example:* use this right after a good "Ask A Question" result that you will need again later.

## Correct The Wiki

**When to use:** you reviewed a page and found something wrong or out of date.
**What you get back:** the corrected page, the old claim marked superseded, fixed cross-links, and a logged correction.

```txt
Read AGENTS.md and [wiki/path/to/page]. I reviewed it and found this is wrong: [incorrect claim]. The correct information is [correction], based on [evidence or source]. Update the page, mark the old claim as superseded or deprecated, fix any pages or cross-links that depended on it, and append a correction entry to wiki/log.md.
```

*Example:* [incorrect claim] -> "the page says approvals are single-step"; [correction] -> "approvals are two-step, manager then finance"; [evidence] -> `raw/screenshots/approval-flow.png`.

## Compare Sources

**When to use:** two or more sources cover the same topic and you want them reconciled.
**What you get back:** a comparison page capturing agreements, contradictions, and source-backed conclusions.

```txt
Compare these sources using the wiki and raw evidence: [source/page list]. Create a comparison page in wiki/ that captures agreements, contradictions, open questions, and source-backed conclusions. Update wiki/index.md and wiki/log.md.
```

*Example:* [source/page list] -> "the 2024 vendor report vs the 2026 internal audit note."

## Lint The Wiki

**When to use:** periodically, to keep the wiki from decaying into a pile of summaries.
**What you get back:** low-risk fixes applied directly and a maintenance page listing larger issues.

```txt
Lint the wiki. Look for contradictions, stale claims, orphan pages, missing cross-links, duplicate pages, unsupported claims, and important concepts without their own pages. Fix low-risk issues directly, record larger findings in a maintenance page, update wiki/index.md, and append to wiki/log.md.
```

*Tip:* run this every several ingests, or before a review or handoff.

## Traceability And QA Check

**When to use:** before calling work "done," especially in implementation or migration projects.
**What you get back:** a QA page listing claims or features that lack traceable evidence or tests.

```txt
Read AGENTS.md, wiki/index.md, and the relevant wiki pages. Run a traceability and QA check: for each [target feature or key claim], confirm it links back to a source page or raw evidence. List anything asserted or implemented without traceable support, and any target slice without tests or verification notes. Record findings in a wiki maintenance or QA page and append to wiki/log.md.
```

*Example:* [target feature or key claim] -> "each migrated screen under `target/`."

## Prepare For Implementation

**When to use:** before changing anything in `target/`, to surface unknowns first.
**What you get back:** a source-backed summary of requirements, assumptions, and open questions for the slice. No code yet.

```txt
Before changing target/, read AGENTS.md, wiki/index.md, wiki/log.md, and all relevant wiki pages. Summarize the source-backed requirements, assumptions, open questions, and traceability for the requested implementation slice. Do not implement until unclear requirements are surfaced.
```

*Example:* "the requested implementation slice" -> "the request-submission form and its approval status field."

## Choose Capabilities For A Task

**When to use:** a task might need special tools and you want the agent to stay context-lean.
**What you get back:** the smallest useful set of tools or subagents, with reasons.

```txt
Read AGENTS.md and wiki/capabilities.md if it exists. For this task: [task], identify the smallest useful set of skills, plugins, MCP servers, subagents, or external tools. Explain what you will use and why. Do not load unrelated capabilities.
```

*Example:* [task] -> "extract the data model from 30 database screenshots."

## Hand Off To A Subagent

**When to use:** you want to delegate a scoped piece of work without losing context.
**What you get back:** a clean handoff package and, after the subagent returns, a wiki update.

```txt
Prepare a subagent handoff for this task: [task]. Include the relevant wiki pages, raw source paths, current assumptions, open questions, expected output, and where the result should be filed back into wiki/. After the subagent returns, update the wiki and append to wiki/log.md if the finding is durable.
```

*Example:* [task] -> "analyze the security and permission screenshots and produce a role matrix."

## Run A Council Review

**When to use:** a high-impact question deserves several specialized perspectives at once.
**What you get back:** a synthesis page recording role findings, disagreements, and decision rationale.

```txt
Use an AI Agent Council for this high-impact question: [question]. Each agent should read the same relevant wiki pages and raw sources, produce role-specific findings, then compare results through the wiki. Record the final synthesis, disagreements, and decision rationale in wiki/, and append to wiki/log.md.
```

*Example:* [question] -> "is the proposed data model safe to build against, or are there unresolved data risks?"

## Council Role Prompts

**When to use:** running the council one role at a time. See `docs/advanced/AI_AGENT_COUNCIL.md` for the full pattern.
**What you get back:** role-specific wiki pages from each agent, all written back to the shared wiki.

Use these one at a time. Every role reads the wiki first and writes findings back to it.

```txt
Orchestrator: Read AGENTS.md, wiki/index.md, and wiki/log.md. Report current status, the next migration slice, blockers, and which role should act next. Do not implement.
```

```txt
Source Analyst: Read AGENTS.md and the relevant raw sources. Produce or update the source inventory, screen catalogue, data object catalogue, and open questions in wiki/. Mark unclear evidence.
```

```txt
Data Model Agent: Read AGENTS.md and the relevant source and screen pages. Produce or update source data model notes, a target data model mapping, data constraints, and data risks in wiki/.
```

```txt
UI Mapping Agent: Read AGENTS.md and the relevant screen evidence. Map source screens to target pages or components, capture user flows, and record uncertain UI behaviour in wiki/.
```

```txt
Workflow And Integration Agent: Read AGENTS.md and the relevant workflow evidence. Catalogue source workflows and integrations, map them to target mechanisms, and record side effects and open questions in wiki/.
```

```txt
Security Agent: Read AGENTS.md and the relevant role and permission evidence. Produce a role mapping and permission matrix, flag overly broad target permissions, and record security risks in wiki/.
```

```txt
Implementation Agent: Read AGENTS.md and the relevant wiki pages before coding. Implement one slice under target/, preserve source behaviour, then update implementation status, traceability, and test notes in wiki/ and append to wiki/log.md.
```

```txt
QA Reviewer Agent: Read AGENTS.md, the relevant wiki pages, and target/. Check source-to-target traceability and test coverage, flag incomplete slices and stale pages, and record a readiness assessment in wiki/.
```
