# Developer Guide

This guide explains how to use this template well.

It is written for developers, researchers, and AI-agent users who want a reusable LLM-maintained wiki rather than one-off chat answers.

Business analysts can use the same workflow: add source material, optionally describe it in the manifest, ask the agent to ingest it, then review the generated wiki and open questions.

## 1. Copy the template

Create one copy of the template per project.

Good examples:

```txt
customer-research-wiki/
ai-agent-reading-notes/
legacy-crm-migration/
```

Avoid mixing unrelated projects in one wiki. A clear boundary keeps the index, log, and source evidence useful.

## 2. Review the schema

Read `AGENTS.md` before starting. It is the schema for the wiki: it tells the AI agent how to ingest sources, structure pages, update the index, update the log, and mark uncertainty.

Most developers and business analysts can use the default schema as-is. If your project needs different page categories, naming conventions, citation expectations, or ingest rules, update `AGENTS.md` before the first ingest.

## 3. Add source material

Put original material under `raw/`.

Possible folder shapes:

```txt
raw/articles/
raw/papers/
raw/transcripts/
raw/screenshots/
raw/exports/
raw/source-code/
raw/notes/
```

Keep source files as close to original as practical. If you clip a web page to markdown, keep the clipped markdown as source evidence rather than rewriting it into a polished summary.

## 4. Optionally update the source manifest

The original LLM Wiki concept does not require a manifest. For small projects, you can skip this step and let the agent inspect `raw/` directly.

Use `raw/manifest.md` when the source collection is large, messy, sensitive, partially external, or hard to understand from filenames alone.

For each important source, include:

- path
- source type
- date or version, if known
- author or origin, if known
- why it matters
- known limitations

The manifest helps future humans and agents understand the source collection before they read every file, but it is a convenience, not a gate.

## 5. Ask the agent to ingest

Use a prompt like this:

```txt
Read AGENTS.md, README.md, raw/manifest.md if useful, and the sources under raw/. Then ingest the sources, build or update the wiki, update wiki/index.md, append to wiki/log.md, and report open questions or missing evidence.
```

For careful projects, ingest one source at a time. For lower-risk projects, batch ingest is fine.

For more copy-paste prompts, see `docs/PROMPT_RECIPES.md`.

## 6. Review the first wiki

After the first ingest, review:

- `wiki/index.md`
- `wiki/log.md`
- source summary pages
- open questions
- contradictions or risk pages
- synthesis pages

Correct anything important early. The first wiki shape becomes the foundation for later work.

## 7. Query the wiki

Ask questions against the wiki, not only the raw sources.

Example prompts:

```txt
Using the wiki, compare the main arguments across these sources and file the comparison as a new wiki page.
```

```txt
Using the wiki, identify contradictions about pricing strategy. Update the relevant pages and log the result.
```

```txt
Using the wiki, propose the next three research questions and add them to the open questions page.
```

Good query results should not disappear into chat. If the answer is useful later, ask the agent to file it back into `wiki/`.

## 8. Lint the wiki periodically

Use a prompt like this:

```txt
Lint the wiki. Look for contradictions, stale claims, orphan pages, missing cross-links, duplicate pages, unsupported claims, and important concepts without their own pages. Update the wiki and append to wiki/log.md.
```

Linting keeps the wiki from becoming a pile of summaries.

## 9. Use `target/` when the wiki drives output

Use `target/` when the knowledge base drives implementation or deliverables.

Examples:

- a migrated app
- a prototype
- a generated report
- a slide deck
- a notebook
- an external repository pointer

Before changing `target/`, the agent should read the relevant wiki pages. After changing `target/`, the agent should update the wiki with what changed and how it was verified.

## 10. Keep the log useful

`wiki/log.md` should tell the story of the project.

Use entries like:

```md
## [2026-06-05] ingest | Example article

- Summary: Added source summary and updated related concept pages.
- Files changed: wiki/sources/example-article.md, wiki/concepts/example-topic.md, wiki/index.md
- Open questions: Need newer source for the market-size claim.
```

A consistent log makes handoff, auditing, and future AI sessions much easier.

## 11. Optional project profiles

The base template is general. Optional profiles under `docs/profiles/` show how to adapt it for implementation-heavy or migration-heavy projects.

When using this template for application migration, make sure the wiki captures:

- source app purpose
- screens and user flows
- data objects
- business logic
- workflows
- integrations
- roles and permissions
- assets
- target assumptions
- source-to-target traceability
- tests or verification notes

Do not implement the target app before the initial source-understanding wiki exists.

## 12. Healthy habits

- Keep `raw/` stable.
- Keep `wiki/index.md` current.
- Keep `wiki/log.md` append-only.
- Mark uncertainty instead of smoothing it over.
- File durable answers back into the wiki.
- Prefer small, reviewable wiki updates over huge opaque rewrites.
- Review `docs/PRIVACY_AND_SOURCE_HANDLING.md` before adding confidential sources.
- Update `AGENTS.md` deliberately; it is the schema future agents will follow.