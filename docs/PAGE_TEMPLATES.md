# Page Templates

These are starter shapes for pages an agent may create under `wiki/`. Adapt them to the domain in `AGENTS.md` when needed.

Every page begins with YAML frontmatter so humans and tools such as Obsidian Dataview can query it. The `status` values match the labels in `AGENTS.md`. Links between wiki pages use `[[wikilinks]]` so the Obsidian graph stays connected.

## Source Summary

```md
---
title: [Source title]
type: source
status: source-derived
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
tags: []
source: [raw/path]
related: []
---

# Source: [Title]

Source type: [article / transcript / screenshot / export / code / note]
Date/version: [known or unclear]

## Summary

## Key Claims

## Entities And Concepts Mentioned

## Evidence Notes

## Contradictions Or Tensions

## Open Questions

## Related Pages

- [[Related page name]]
```

## Concept Page

```md
---
title: [Concept]
type: concept
status: source-derived
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
tags: []
source: []
related: []
---

# [Concept]

## Definition

## Source-Backed Notes

## Related Concepts

- [[Related concept]]

## Contradictions Or Uncertainty

## Source Traceability

## Related Pages

- [[Related page name]]
```

## Entity Page

```md
---
title: [Entity name]
type: entity
status: source-derived
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
tags: []
source: []
related: []
---

# [Entity Name]

Entity type: [person / organization / system / object / place / data object]

## Description

## Attributes

## Relationships

## Evidence

## Open Questions

## Related Pages

- [[Related page name]]
```

## Decision Page

```md
---
title: [Decision title]
type: decision
status: proposed
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
tags: []
source: []
related: []
---

# Decision: [Short Title]

## Context

## Options Considered

## Decision

## Rationale

## Consequences

## Source Or Wiki Traceability

## Open Questions

## Related Pages

- [[Related page name]]
```

## Open Question

```md
---
title: [Question title]
type: question
status: unclear
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
tags: []
source: []
related: []
---

# Question: [Short Title]

## Question

## Why It Matters

## Relevant Sources Or Pages

- [[Relevant page]]

## Candidate Answers

## Resolution Notes
```

## Synthesis Page

```md
---
title: [Synthesis topic]
type: synthesis
status: inferred
created: [YYYY-MM-DD]
updated: [YYYY-MM-DD]
tags: []
source: []
related: []
---

# [Synthesis Topic]

## Thesis Or Summary

## Supporting Evidence

## Counterevidence Or Caveats

## Implications

## Open Questions

## Source Traceability

## Related Pages

- [[Related page name]]
```
