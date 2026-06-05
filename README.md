# LLM Wiki Template

This repository is a reusable starter template for building a persistent knowledge base with an LLM.

The method is simple: curated source material goes into `raw/`, AI agents maintain a structured markdown wiki under `wiki/`, and `AGENTS.md` acts as the schema that tells the agent how the wiki should be maintained. Optional implementation or generated outputs live under `target/`.

The wiki is not a one-time summary. It is a compounding artifact that gets richer as new sources are ingested, questions are answered, contradictions are found, and decisions are made.

## Attribution and license

This template is a concrete implementation of the "LLM Wiki" idea, inspired by [Andrej Karpathy's "LLM Wiki" note](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

Template design, schema (`AGENTS.md`), enterprise-migration framework, AI Agent Council pattern, and capability routing by **Chrisio Gwaan GUAN**.

Copyright (c) 2026 Chrisio Gwaan GUAN.

This template is released under the MIT License. See [LICENSE](LICENSE).

## Purpose and scope

This template can be used for any project where knowledge accumulates over time and should be organized instead of rediscovered from scratch.

Example uses include:

- personal knowledge bases
- research projects
- book, course, or podcast notes
- competitive analysis and due diligence
- team knowledge bases
- application migration projects
- product discovery and requirements analysis
- implementation projects that need durable design rationale

For the concept explanation, read `docs/LLM_WIKI_METHOD.md`.

For step-by-step usage, read `docs/DEVELOPER_GUIDE.md`.

For all human-facing guides, see `docs/README.md`.

## Repository layout

```txt
raw/     immutable source material and evidence
wiki/    AI-generated knowledge base, index, and log
target/  optional implementation, generated outputs, or external repo notes
docs/    human-facing explanations and guides
AGENTS.md schema and operating instructions for AI wiki maintenance
CLAUDE.md thin loader so Claude Code reads AGENTS.md (see docs/USING_WITH_AI_TOOLS.md)
```

The starter wiki includes `wiki/capabilities.md`, a lightweight registry for routing agents to only the skills, plugins, MCP servers, subagents, or external tools that are useful for the current project.

## Before starting a project

Create a new copy of this template for each knowledge project.

Example:

```txt
research-ai-agents/
book-companion-notes/
customer-discovery-wiki/
migration-app-a/
```

Do not mix unrelated projects in one wiki. Each project should have its own `raw/`, `wiki/`, schema instructions, and optional `target/` context.

## Quick start

1. Copy the template for a new project.
2. Add source material under `raw/`.
3. Optional: update `raw/manifest.md` if a source inventory would help humans or agents understand the collection.
4. If the project needs special wiki conventions, adjust `AGENTS.md`; otherwise use the default schema.
5. Update `wiki/capabilities.md` if the project has known skills, plugins, MCP servers, subagents, or external tools the agent should prefer.
6. Ask the AI agent to ingest the sources and build the initial wiki.
7. Review `wiki/index.md`, `wiki/log.md`, open questions, and unclear areas.
8. Ask questions against the wiki; file durable answers back into `wiki/` when useful.
9. Periodically ask the agent to lint the wiki for contradictions, stale claims, missing links, and orphan pages.
10. If the project has implementation work, build it under `target/` or document the linked target repository there.

Tip: browse `wiki/` in Obsidian to follow links and see the graph. See `docs/BROWSING_THE_WIKI.md`.

## Source materials

Before asking AI agents to build the wiki, add useful source materials under `raw/`.

Useful materials include:

- articles, papers, reports, and copied web pages
- books, chapter notes, course notes, and transcripts
- screenshots, images, diagrams, and assets
- meeting notes, interviews, and decision notes
- spreadsheets, CSV exports, and data files
- source code, exported packages, or technical docs
- app UI screenshots, database screenshots, workflow screenshots, and role or permission screenshots for migration projects
- human notes explaining unclear behaviour or context

For small projects, adding files under `raw/` may be enough. For larger or messier collections, use the optional `raw/manifest.md` to describe important sources, dates, origins, limitations, and known gaps.

## Standard LLM Wiki process

The AI must understand and update the wiki before making dependent design or implementation claims.

1. Developers or researchers place source material into `raw/`.
2. If useful, developers describe the source collection in `raw/manifest.md`.
3. AI agents inspect `raw/` and generate or update pages under `wiki/`.
4. The team reviews missing information, assumptions, risks, contradictions, and open questions.
5. Queries, comparisons, decisions, and analyses are filed back into the wiki when they are durable.
6. Periodic lint passes keep the wiki healthy.
7. Optional implementation or output work happens under `target/` and is kept synchronized with the wiki.

## AI agent expectations

Before wiki or target work, agents must read:

- `AGENTS.md`
- `README.md`
- `raw/manifest.md` if present or useful
- `wiki/index.md`
- `wiki/log.md`
- relevant generated wiki pages

Agents should mark unclear details as `unclear`, avoid unsupported assumptions, and keep the wiki in sync with meaningful work.

## Human learning materials

For the human-facing explanation of this template, see:

- `docs/LLM_WIKI_METHOD.md` - explains the general LLM Wiki concept and why it differs from ordinary RAG
- `docs/DEVELOPER_GUIDE.md` - gives step-by-step instructions for using this template well
- `docs/PROMPT_RECIPES.md` - provides copy-paste prompts for common BA/developer workflows
- `docs/PAGE_TEMPLATES.md` - provides starter page shapes the agent can use in `wiki/`
- `docs/SCHEMA_CUSTOMIZATION.md` - explains how to adapt `AGENTS.md` for a domain
- `docs/PRIVACY_AND_SOURCE_HANDLING.md` - covers source handling, sensitive data, and Git hygiene
- `docs/USING_WITH_AI_TOOLS.md` - how to make any AI tool load the `AGENTS.md` schema
- `docs/BROWSING_THE_WIKI.md` - browsing the wiki in Obsidian with graph view and Dataview

Optional profiles and advanced material live under:

- `docs/profiles/` - examples for migration or implementation-heavy projects
- `docs/advanced/` - advanced coordination patterns such as multi-agent councils and autonomous loop orchestration
