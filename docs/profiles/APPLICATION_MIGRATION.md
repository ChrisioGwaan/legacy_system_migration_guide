# Human Concepts Behind This Template

This document explains the ideas behind this LLM Wiki template for human readers, with special attention to the application migration profile.

It is not an operational instruction file for AI agents. AI agents should follow `AGENTS.md`, `README.md`, `raw/manifest.md` when present or useful, and the generated `wiki/`.

For the general method, start with `docs/LLM_WIKI_METHOD.md`. This page explains why the same method is useful for enterprise migration and implementation work.

## Why this template exists

Enterprise application migration is difficult because knowledge is usually scattered across many places:

* screenshots
* old source code
* database schemas
* workflow diagrams
* user manuals
* business rules
* permissions
* integrations
* developer memory
* undocumented behaviour

If an AI agent works only from chat history, it may forget context, duplicate analysis, miss constraints, or make unsupported assumptions.

This template solves that problem by creating a persistent migration knowledge base.

The main idea is:

> Convert scattered source evidence into a structured wiki, then use that wiki as the shared migration memory throughout the project.

## Core layers of knowledge

This template separates project knowledge into the same core layers as the LLM Wiki concept.

```txt
raw/      = original source evidence
wiki/     = structured AI-maintained knowledge
AGENTS.md = schema and operating rules
target/   = optional implementation or outputs
```

### `raw/`: source evidence

The `raw/` folder contains original material from the source application.

Examples:

* UI screenshots
* database screenshots
* workflow screenshots
* exported metadata
* source code
* documents
* meeting notes
* business process notes
* integration notes
* icons and assets

Files in `raw/` should be treated as evidence. They should not be rewritten by the AI unless explicitly requested.

### `wiki/`: migration knowledge base

The `wiki/` folder is generated from the raw evidence.

It explains:

* what the source app does
* which screens exist
* which data objects exist
* which workflows exist
* which roles and permissions exist
* what is known
* what is unclear
* what target design is proposed
* what has been implemented
* what has been tested

The wiki is not just documentation. It is the project memory.

### `target/`: implementation

The `target/` folder contains or points to the new application being built.

The target implementation should be designed and implemented from the wiki, not directly from unstructured screenshots or private chat history.

## The wiki as a knowledge base

In artificial intelligence, a knowledge base stores facts, relationships, rules, assumptions, and conclusions that an agent can use to make decisions.

In this template, the wiki acts as a practical software migration knowledge base.

Example:

```txt
Raw evidence:
- Screenshot of a user form
- Screenshot of a database table
- Screenshot of an approval workflow

Wiki knowledge:
- This screen allows a user to submit a request
- The request is stored in this data object
- The request has these statuses
- This role can approve it
- This workflow changes the status after approval

Target implementation:
- New form/page
- New database table
- New workflow or service logic
- New role permission rule
```

This helps both humans and AI agents understand the source system before changing or rebuilding it.

## Relation to AI concepts

This template can be understood through several common AI concepts.

## 1. Knowledge-based agent

A knowledge-based agent uses stored knowledge to reason and act.

In this template:

```txt
raw/ source files        = observations
wiki/ knowledge base     = structured memory
AGENTS.md rules          = behaviour rules
target/ implementation   = actions
tests/reviews            = feedback
```

The AI agent first observes the source materials, converts them into structured knowledge, and then uses that knowledge to guide migration work.

## 2. Utility-based agent

A utility-based agent chooses actions that produce the best expected outcome.

In migration work, the AI agent may choose between actions such as:

* analyse more screenshots
* ask for missing evidence
* design the data model
* build a UI slice
* review security
* update the wiki
* run tests
* refactor implementation

The best action is not always “write code now”.

A good migration agent should prefer actions that increase:

* source understanding
* traceability
* implementation correctness
* test confidence
* security confidence
* maintainability

And reduce:

* hallucination risk
* missing requirement risk
* duplicated work
* schema rework
* workflow mistakes
* stale documentation

Example:

```txt
Action A: Start coding immediately
Risk: high
Utility: low if source understanding is incomplete

Action B: Build the wiki first
Risk: lower
Utility: high because future design, coding, and testing become more reliable
```

This is why the template requires the wiki to be built before implementation.

## 3. Constraint satisfaction problem (CSP)

Application migration often behaves like a constraint satisfaction problem.

A migration must map source elements to target elements while satisfying constraints.

Examples:

```txt
Source screen       -> Target page/component
Source entity       -> Target table
Source field        -> Target column
Source role         -> Target permission model
Source workflow     -> Target automation/service
Source integration  -> Target API connector/service
```

But these mappings must satisfy constraints:

* required fields must remain required
* relationships must remain valid
* status values must preserve business meaning
* users must not gain excessive permissions
* workflows must preserve the correct order
* integrations must preserve side effects
* target platform limitations must be respected
* every target feature should trace back to source evidence

The wiki helps record these constraints so that future decisions remain consistent.

## 4. Search and planning

Migration can also be seen as a search and planning problem.

There are many possible migration paths:

```txt
Path A: data model first, then UI, then workflows
Path B: UI first, then data model, then integrations
Path C: one complete feature slice at a time
Path D: rebuild everything at once
```

A good migration process uses heuristics to choose a safe path.

Useful heuristics include:

* understand the source before coding
* model core data before building dependent UI
* migrate small slices instead of the whole app at once
* verify behaviour against source evidence
* update the wiki after each implementation change

The wiki helps the agent plan migration slices and avoid blind exploration.

## 5. Multi-agent coordination

For large enterprise migrations, one AI agent may not be enough.

Different agents can focus on different concerns:

* source analysis
* data modelling
* UI mapping
* workflow mapping
* security
* implementation
* testing

However, multiple agents can easily conflict if they rely on private chat memory.

This template solves that by making the wiki the shared source of truth.

Agents may have different roles, but they must all read from and write back to the same migration knowledge base.

## Why not use chat history only?

Chat history is useful, but it is not enough for enterprise migration.

Problems with chat-only migration:

* important details can be buried in long conversations
* different agents may not share the same context
* decisions may not be recorded clearly
* assumptions may become invisible
* implementation may drift from source evidence
* later contributors cannot easily understand why decisions were made

The wiki solves these problems by making knowledge explicit and persistent.

## The core method

The method is simple:

```txt
1. Collect source evidence
2. Store it under raw/
3. Optionally describe it in raw/manifest.md
4. Let the AI build the initial wiki
5. Use the wiki to design the target system
6. Build the target system slice by slice
7. Update the wiki after every change
8. Test target behaviour against source evidence
```

## What makes this useful for companies

This template is useful for company teams because it creates a repeatable migration process.

Instead of every migration depending on one developer’s memory, the project has:

* a clear source evidence folder
* a generated knowledge base
* a wiki log
* traceability between source and target
* explicit open questions
* explicit risks
* reusable AI agent instructions
* optional multi-agent collaboration

This makes the migration easier to review, hand over, audit, and continue.

## Important principle

The wiki is not a final report written after the migration.

The wiki is the working memory of the migration.

It connects:

```txt
source evidence
        ↓
source understanding
        ↓
target design
        ↓
implementation
        ↓
testing
        ↓
review
        ↓
future maintenance
```

If the implementation changes but the wiki does not, the migration memory becomes stale.

A stale wiki makes future AI work less reliable.

Therefore:

> Every meaningful implementation change should either update the wiki or explicitly state why no wiki update was needed.
