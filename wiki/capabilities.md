---
title: Agent Capability Registry
type: registry
created: 2026-06-06
updated: 2026-06-06
tags: []
---

# Agent Capability Registry

Status: starter template

Use this page to route agents to the smallest useful set of skills, plugins, MCP servers, subagents, or external tools for the current project.

Do not list every available capability. List only capabilities that are useful for this project.

## How Agents Should Use This Page

1. Read this page before loading specialized capabilities.
2. Choose only the capabilities relevant to the current task.
3. If no entry matches, use the minimum necessary default tools.
4. If a new capability becomes repeatedly useful, propose adding it here.
5. Record meaningful capability use in `wiki/log.md` when it affects project knowledge, decisions, or implementation.

## Capability Table

| Task type | Recommended capability | When to use | Required wiki context | Notes |
| --- | --- | --- | --- | --- |
| Source ingest | Default file/search tools | Reading and summarizing files under `raw/` | `wiki/index.md`, `wiki/log.md`, `raw/manifest.md` if useful | Add domain-specific tools only when sources require them. |
| Wiki query | Default file/search tools | Answering from existing wiki pages | `wiki/index.md`, relevant wiki pages | File durable answers back into the wiki. |
| Wiki lint | Default file/search tools | Checking contradictions, stale claims, orphan pages, missing links | `wiki/index.md`, `wiki/log.md` | Create or update maintenance notes when useful. |
| Implementation | Project-specific build/test tools | Changing files under `target/` or linked implementation repos | Relevant wiki pages, decisions, open questions | Update wiki and log after meaningful changes. |

## Project-Specific Additions

Add rows here as the project learns which capabilities are useful.

Examples:

- A PDF conversion tool for source PDFs.
- An image viewing tool for screenshot-heavy research.
- A database MCP for schema inspection.
- A browser MCP for live web verification.
- A specialist subagent for source analysis, security review, or QA.
- An autonomous loop runner such as Ralph Orchestrator for unattended implement and QA cycles (see `docs/advanced/RUNNING_WITH_RALPH.md`).