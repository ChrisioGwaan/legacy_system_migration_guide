# Schema Customization

`AGENTS.md` is the schema for this template. It tells AI agents how to operate on `raw/`, `wiki/`, and optional `target/` content.

Most projects can start with the default schema. Customize it when the domain needs different page categories, evidence rules, status labels, or workflows.

## What To Customize

- page categories the wiki should use
- naming conventions for generated files
- status labels and confidence labels
- citation or source traceability expectations
- ingest workflow for special source types
- query filing rules
- lint checks
- rules for optional `target/` implementation work
- task-to-capability routing rules for skills, plugins, MCP servers, subagents, or external tools

## Safe Customization Pattern

1. Keep the non-negotiable rules intact unless you have a strong reason.
2. Add domain-specific requirements under the relevant section.
3. Prefer short, testable rules over broad prose.
4. Give examples of desired page names and page shapes.
5. After changing `AGENTS.md`, ask the agent to summarize the new rules before doing wiki work.

## Example Additions

For a book wiki:

```md
Generated wiki pages should include character pages, location pages, theme pages, chapter summaries, timeline notes, and unresolved plot questions.
```

For customer research:

```md
Generated wiki pages should distinguish direct customer quotes from inferred themes. Preserve speaker, company, date, and source transcript path where available.
```

For application migration:

```md
Generated wiki pages should capture source screens, data objects, workflows, roles, integrations, target mappings, and verification notes.
```

For capability routing:

```md
When a task requires specialized tools, read `wiki/capabilities.md` first. Load only the capabilities listed for that task type. If no match exists, use the minimum necessary default tools and propose an update to the capability registry.
```

## Capability Registry

For larger projects, keep a project-specific capability registry at `wiki/capabilities.md`.

Use it to record:

- task type
- recommended skills or plugins
- recommended MCP servers or tools
- useful subagent roles
- required wiki pages to read before acting
- notes about when not to use a capability

The registry should be short and practical. Its purpose is to save context by routing agents to the right capabilities, not to document every tool in the environment.

## Do Not Put Source Facts In The Schema

Use `AGENTS.md` for operating rules, not source content. Put source material in `raw/` and source-derived synthesis in `wiki/`.