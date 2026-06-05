# LLM Wiki Method

This document explains the concept behind this template.

It is written for humans. AI agents should follow `AGENTS.md` for operating rules.

## The idea

Most document-based LLM workflows look like retrieval-augmented generation. You upload files, the system retrieves chunks at question time, and the LLM assembles an answer. That is useful, but the knowledge does not compound very much. Each subtle question can force the model to rediscover and reconnect the same fragments again.

The LLM Wiki method works differently.

Instead of only retrieving from raw documents at query time, the LLM incrementally builds and maintains a persistent markdown wiki. When you add a source, the agent reads it, extracts the important material, integrates it into existing pages, updates cross-references, flags contradictions, and records uncertainty.

The wiki becomes a compiled knowledge layer between you and the raw sources.

It can also become a coordination layer for agents. Instead of loading every available skill, plugin, MCP server, or subagent into every conversation, the project can maintain a small capability registry in the wiki. Agents consult that registry to decide which capabilities are relevant for the current task, which keeps context lean and makes tool choices auditable.

## Why the wiki matters

The useful artifact is not only the answer in chat. The useful artifact is the maintained wiki:

- summaries are already written
- entities and concepts already have pages
- contradictions have already been noticed
- open questions are visible
- decisions have rationale
- source-to-wiki traceability exists
- new questions can build on previous synthesis
- agents can coordinate through shared project memory instead of private chat context
- tool and subagent choices can be documented instead of improvised each time

The human curates sources, asks questions, reviews important changes, and decides what matters. The LLM handles the maintenance work that usually makes personal and team wikis decay.

## The core architecture

```txt
raw/       source material and evidence
wiki/      AI-maintained knowledge base
AGENTS.md schema, conventions, and operating instructions
target/    optional implementation or generated outputs
```

### `raw/`

`raw/` is the source-of-truth evidence layer. Put original material here: articles, papers, screenshots, transcripts, exports, source code, app screenshots, and notes.

Agents read `raw/`, but should not modify it unless explicitly instructed.

### `wiki/`

`wiki/` is the AI-maintained knowledge base. The agent creates and updates pages here as sources are ingested and questions are answered.

The wiki is the shared memory for future humans and agents.

The wiki can also include project-specific operating pages such as `wiki/capabilities.md`, where the project records which skills, plugins, MCP servers, subagents, or external tools are useful for which tasks.

### `target/`

`target/` is optional. Use it when the wiki drives implementation or output artifacts, such as a migrated app, generated report, analysis notebook, or slide deck.

### `AGENTS.md`

`AGENTS.md` is the schema. It tells the agent how to ingest sources, structure pages, update the index and log, mark uncertainty, and keep the wiki healthy.

## Core operations

### Ingest

Add a source to `raw/`, then ask the agent to ingest it. For larger collections, you can optionally describe sources in `raw/manifest.md`, but the method does not require a manifest.

The agent should:

1. read the source
2. write or update wiki pages
3. connect the source to existing concepts
4. mark contradictions and open questions
5. update `wiki/index.md`
6. append to `wiki/log.md`

### Query

Ask questions against the wiki. The agent should read `wiki/index.md`, open relevant pages, and answer from the maintained knowledge base.

If the answer is durable, file it back into the wiki as a new page or an update to an existing page.

### Lint

Periodically ask the agent to lint the wiki.

Useful checks include:

- contradictions between pages
- stale claims superseded by newer sources
- orphan pages with no inbound links
- important concepts without pages
- missing cross-references
- unsupported claims
- source gaps worth filling

### Build

If the project includes implementation, build from the wiki instead of private chat memory. After implementation, update the wiki with what changed, what was verified, and what remains unresolved.

### Route Capabilities

For projects with many possible tools, maintain `wiki/capabilities.md` as a lightweight routing table. It can list which skills, plugins, MCP servers, subagents, and external tools are relevant for common task types.

This helps agents avoid loading everything at once. The agent reads the registry, selects the smallest useful capability set for the task, and records meaningful tool use in `wiki/log.md` when it affects project knowledge.

### Coordinate Agents

Subagents can lose context when work is handed across several levels. The LLM Wiki pattern reduces that risk by making the wiki the handoff artifact.

Instead of relying on hidden or private chat state, the orchestrating agent points subagents to the relevant wiki pages and raw sources. Each subagent returns findings that can be filed back into the wiki. In larger projects, an AI Agent Council can use the same shared wiki to compare role-specific findings, resolve contradictions, and produce a better final answer.

The key rule is simple: if a finding, decision, assumption, or tool choice matters later, it should be written to the wiki and logged in `wiki/log.md`.

## How this differs from ordinary RAG

RAG retrieves relevant source chunks when a question is asked. The LLM Wiki method creates and maintains an intermediate knowledge artifact before and between questions.

In RAG, synthesis often happens repeatedly in chat.

In an LLM Wiki, synthesis is saved, linked, revised, and reused.

## What humans still do

Humans remain responsible for judgment:

- choose sources
- decide what questions matter
- review important synthesis
- resolve ambiguous intent
- approve high-impact decisions
- verify business-critical claims

The LLM reduces the bookkeeping burden. It does not remove the need for human curation.

## Where this works well

The method is useful when knowledge accumulates over time:

- personal goals and self-study
- research projects
- book or course companion wikis
- team knowledge bases
- competitive analysis
- due diligence
- application migration
- product requirements and implementation planning

It is less useful for one-off questions where no durable knowledge base is needed.