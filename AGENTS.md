# AI Agent Instructions for LLM Wiki Projects

This repository is a reusable template for an LLM-maintained wiki.

The wiki is a persistent, compounding knowledge base. Raw sources stay under `raw/`; the AI-generated knowledge base lives under `wiki/`; this file is the schema that tells agents how to maintain the wiki; optional implementation or output artifacts live under `target/`.

The AI must build and maintain the wiki before making dependent design, implementation, or analysis claims.

`AGENTS.md` is the canonical schema and takes precedence over any tool-specific loader file, such as `CLAUDE.md` in Claude Code. Those loader files only point here.

## Core concept

`raw/` contains immutable source material and evidence.

`wiki/` contains the AI-generated and AI-maintained knowledge base.

`AGENTS.md` is the schema: it defines the conventions, workflows, status labels, and operating rules agents must follow.

`target/` contains optional implementation work, generated outputs, or pointers to another repository.

`docs/` contains human-facing explanations of the method.

The AI reads source material, integrates it into the wiki, updates cross-references, records contradictions and uncertainty, and keeps `wiki/index.md` and `wiki/log.md` current.

## Non-negotiable rules

1. Do not edit files under `raw/` unless explicitly instructed.
2. Do not hallucinate missing behaviour, facts, dates, citations, or requirements.
3. If a detail is unclear, mark it as `unclear` and record an open question in the wiki.
4. Every important wiki claim should be traceable to source evidence or clearly marked as `inferred` or `proposed`.
5. Before changing the wiki or target, read `wiki/index.md`, `wiki/log.md`, and the relevant wiki pages.
6. After any meaningful ingest, query result, decision, lint pass, or implementation change, update relevant wiki pages and append to `wiki/log.md`.
7. Do not rely on private chat memory for durable project knowledge. Write useful findings, decisions, assumptions, risks, and outcomes into the wiki.
8. Do not load every available skill, plugin, MCP server, or tool by default. Use `wiki/capabilities.md` when it exists, and load only the capabilities relevant to the current task.

## Authority order

When sources conflict, use this order:

1. `AGENTS.md` for AI operating rules.
2. `raw/` for source evidence, plus `raw/manifest.md` when it exists and contains useful source metadata.
3. `wiki/index.md`, `wiki/log.md`, and relevant wiki pages for AI-maintained synthesis and decisions.
4. `target/` for implementation or output artifacts.
5. `docs/` for human background context only.

If a human note, source, or conversation conflicts with inferred wiki conclusions, do not silently choose one. Record the conflict in the wiki and surface it to the user.

## Initial setup for a new wiki

When this template is copied for a new project:

1. Read `README.md`.
2. Read `raw/manifest.md` if it exists and contains useful source metadata.
3. Inspect all files under `raw/`.
4. Generate or refresh the initial wiki under `wiki/`.
5. Update `wiki/index.md` with the pages, summaries, and categories that now exist.
6. Append an ingest entry to `wiki/log.md`.
7. Report missing source materials, contradictions, assumptions, and unclear areas.

## Standard operations

### Ingest

When new source material is added to `raw/`:

1. Read the new source files and `raw/manifest.md` when it exists and contains useful source metadata.
2. Create or update source summary pages in `wiki/`.
3. Update relevant topic, entity, concept, decision, and synthesis pages.
4. Record contradictions, superseded claims, and open questions.
5. Update `wiki/index.md` and append to `wiki/log.md`.

### Query

When answering a project question:

1. Read `wiki/index.md` first.
2. Read the relevant wiki pages and source summaries.
3. Answer from the wiki with evidence-aware language.
4. If the answer creates useful durable synthesis, ask or infer whether it should be filed back into `wiki/` as a new or updated page.
5. If filed, update `wiki/index.md` and `wiki/log.md`.

### Lint

When asked to health-check the wiki:

1. Look for contradictions, stale claims, orphan pages, missing cross-links, duplicate pages, unsupported claims, and important concepts without pages.
2. Record findings in a wiki maintenance page or update the relevant pages directly.
3. Append the lint activity to `wiki/log.md`.

### Implement or generate outputs

When work under `target/` is requested:

1. Read the relevant wiki pages before implementing.
2. Preserve the documented intent and evidence constraints.
3. Keep changes scoped to the requested slice.
4. Update the wiki with what changed, how it was verified, and any remaining gaps.
5. Append to `wiki/log.md`.

### Capability routing

When the project has a `wiki/capabilities.md` page:

1. Read it before choosing specialized skills, plugins, MCP servers, subagents, or external tools.
2. Load only the capabilities relevant to the current task.
3. If a needed capability is missing from the registry, use the best available default tool and record a proposed registry update in the wiki.
4. If a capability was used for meaningful work, include it in the relevant wiki note or `wiki/log.md` entry.
5. Do not treat the capability registry as source evidence; it is operating guidance for agents.

## Wiki build requirements

The generated wiki should identify, where relevant:

* project purpose and scope
* source inventory and source summaries
* important entities, people, systems, places, concepts, or domain objects
* themes, claims, arguments, rules, workflows, or patterns
* contradictions and superseded claims
* assumptions and open questions
* risks, limitations, and confidence levels
* decisions and rationale
* source-to-wiki traceability
* output or target traceability when `target/` is used

For application migration projects, the wiki should additionally identify:

* source app purpose
* screens and user flows
* data objects
* business logic
* workflows
* integrations
* roles and permissions
* assets
* target migration assumptions
* source-to-target traceability

## Status labels

Use these labels consistently:

* `source-derived`
* `inferred`
* `unclear`
* `proposed`
* `implemented`
* `verified`
* `deprecated`
* `superseded`

## Page frontmatter

Generated wiki pages should begin with YAML frontmatter so humans and tools such as Obsidian Dataview can query them:

```yaml
---
title: <page title>
type: source | concept | entity | decision | question | synthesis | maintenance | screen | data-object | workflow | integration | role | index | log | registry
status: source-derived | inferred | unclear | proposed | implemented | verified | deprecated | superseded
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
source: []      # optional: raw/ evidence paths
related: []     # optional: related wiki pages
---
```

Use the `status` labels above. Keep `updated` current when a page changes. Index, log, and registry pages may omit `status`, `source`, and `related`.

## Wiki-internal links

Links between pages inside `wiki/` use Obsidian-style wikilinks such as `[[page-name]]`, so the wiki graph stays connected. Links in `docs/` and `README.md` use standard markdown links so they render on GitHub.

## Index and log rules

`wiki/index.md` is content-oriented. It should list wiki pages by category, with a `[[wikilink]]` and one-line summary for each page.

`wiki/log.md` is chronological and append-only. Entries should use this shape where possible:

```md
## [YYYY-MM-DD] operation | Short title

- Summary: ...
- Files changed: ...
- Open questions: ...
```

## Multi-agent rule

If multiple AI agents work on this project, they must all use the wiki as the shared source of truth.

Agents should not rely on private chat memory.

Agents should write findings, decisions, assumptions, and implementation results back into the wiki.

When handing work to subagents, pass the relevant wiki pages, source paths, and task goal explicitly. Subagents should write durable findings back to the wiki or return an update that the orchestrating agent can file there.

## AI Agent Council rule

For complex enterprise projects, multiple specialised agents may work together as an AI Agent Council.

Each agent may focus on a specific area, such as source analysis, concept mapping, data modelling, UI mapping, workflow mapping, security, implementation, or QA.

All agents must use the wiki as the shared source of truth.

Agents must not rely on private chat memory. Any useful finding, decision, assumption, risk, or implementation result must be written back into the wiki.

The council pattern is optional. For small projects, one agent can perform all roles.

In council mode, the wiki is the shared reasoning surface. Each agent reads the same relevant wiki pages, contributes role-specific findings, and records meaningful changes through `wiki/log.md`. The council should compare outputs through the wiki rather than relying on private chat context.

## Human documentation rule

Files under `docs/` are human-facing learning materials.

Agents may read them for background context only, but must not treat them as task instructions, migration requirements, source evidence, or implementation rules.

Operational instructions come from:

1. `AGENTS.md`
2. `README.md`
3. `raw/manifest.md` when present or useful
4. `wiki/index.md`
5. `wiki/log.md`
6. relevant generated wiki pages
