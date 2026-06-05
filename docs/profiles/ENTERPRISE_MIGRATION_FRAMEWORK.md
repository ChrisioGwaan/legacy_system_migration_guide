---
title: "Wiki-Driven Enterprise Migration"
subtitle: "A Knowledge-Based SDLC and Multi-Agent Coordination Framework"
author: "Chrisio Gwaan GUAN"
date: "2026-06-02"
lang: en
fontsize: 11pt
geometry: margin=1in
---

# Attribution and License Notice {.unnumbered}

Concept, framework, and template direction by **Chrisio Gwaan GUAN**.

Copyright (c) 2026 Chrisio Gwaan GUAN.

The template materials are released under the MIT License. See `LICENSE` in the
repository root.

This notice records authorship and ownership intent for the wiki-driven
enterprise migration framework and associated template materials. It is not a
substitute for formal legal advice, registration, or licensing review.

# Abstract {.unnumbered}

Enterprise application migration is a socio-technical problem: teams must
recover the behaviour of a source system, preserve business intent, redesign
that behaviour for a target platform, and maintain evidence that the target
implementation remains faithful to the source. This document defines a
wiki-driven migration framework in which source evidence is stored under
`raw/`, interpreted migration knowledge is maintained under `wiki/`, schema and
operating rules are recorded in `AGENTS.md`, and target implementation work is
performed under `target/` or a linked target repository.

The framework is grounded in established concepts from software engineering,
requirements engineering, knowledge management, and artificial intelligence.
The wiki is treated as an externalized project knowledge base, a traceability
repository, and a coordination mechanism for human developers and AI agents.
The optional AI Agent Council pattern is framed as a role-based multi-agent
coordination model that uses shared project artifacts rather than private chat
history as its source of truth. The result is not a formal proof of migration
correctness; it is a practical governance and documentation framework designed
to reduce hallucination risk, preserve design rationale, support verification,
and make enterprise migration work auditable.

**Keywords:** enterprise migration, software migration, knowledge base,
requirements traceability, SDLC, multi-agent systems, design rationale,
knowledge management, human-in-the-loop AI, verification and validation.

# Introduction

Enterprise software migrations rarely fail only because code is difficult to
rewrite. They often fail because knowledge about the source system is fragmented
across screenshots, old code, workflow diagrams, user manuals, undocumented
business rules, access-control assumptions, and practitioner memory. This
creates a knowledge recovery problem before it becomes an implementation
problem.

The purpose of this template is to impose a disciplined knowledge lifecycle on
migration work. The template separates original evidence, interpreted
knowledge, schema rules, and implementation into distinct layers:

```txt
raw/    original source evidence
wiki/   structured migration knowledge and project memory
AGENTS.md schema and operating instructions
target/ target implementation or pointer to the target application
docs/   human-facing explanation of the method
```

This separation is important. Source evidence should not be rewritten to fit a
preferred design. The wiki should record what is known, what is inferred, what
is unclear, and how each source feature maps to the target system. The target
implementation should be built from this structured understanding rather than
from unstructured screenshots or private chat messages.

The framework therefore combines three practical ideas:

1. Evidence-first migration: source artifacts are collected and described
   before implementation starts.
2. Wiki-driven SDLC: the wiki supports discovery, planning, implementation,
   verification, and review.
3. Role-based agent coordination: multiple AI agents may participate, but all
   useful findings and decisions must be written back to the shared wiki.

## Primary Power Platform use case and generalization

The primary enterprise use case for this framework is migration from legacy
systems to Microsoft Power Platform, including Power Apps Code Apps, Dataverse,
Canvas Apps, and related Power Platform services. This context is common in
organizations that still depend on legacy applications whose source code is
hard to obtain, incomplete, encrypted, vendor-controlled, or restricted by
copyright and licensing constraints.

In such migrations, the first challenge is often source understanding rather
than direct code transformation. The team may need to infer application
behaviour from screenshots, database exports, configuration, workflow diagrams,
manual observations, and stakeholder knowledge. The wiki provides a controlled
place to distinguish confirmed evidence from inferred or unclear behaviour.

Although Power Platform is the primary use case, the framework is not limited
to Microsoft technologies. The same evidence-first, wiki-driven SDLC and
role-based AI Agent Council approach can be applied to migrations toward other
platform providers, cloud services, low-code environments, or pro-code frontend
and backend architectures.

# Theoretical Foundations

## Knowledge management and organizational memory

In knowledge management, organizations distinguish between tacit knowledge
held by people and explicit knowledge that can be represented in documents,
models, and systems. Nonaka's theory of organizational knowledge creation
emphasizes the interaction between tacit and explicit knowledge and the role of
organizations in articulating and amplifying individual knowledge.

Enterprise migration depends on this conversion. A developer may know that a
field is required, that a status transition is exceptional, or that a workflow
step is rarely used but business-critical. If this knowledge remains tacit, it
is hard for other developers, reviewers, or AI agents to rely on it. The wiki
acts as an externalized organizational memory: it turns migration knowledge into
an explicit artifact that can be inspected, challenged, revised, and reused.

This does not make the wiki automatically correct. It makes the wiki a managed
knowledge artifact whose claims must be traced to source evidence or marked as
inferred or unclear.

## Requirements engineering and traceability

Requirements traceability is the ability to relate requirements, design
decisions, implementation artifacts, tests, and source evidence across the life
cycle of a system. Gotel and Finkelstein's analysis of the requirements
traceability problem is especially relevant to migration because source
requirements are often reconstructed from legacy artifacts rather than written
fresh.

In this template, traceability is applied in both directions:

- Forward traceability: source evidence leads to source understanding, target
  design, implementation, and verification.
- Backward traceability: a target feature can be traced back to the source
  evidence or decision that justified it.

This is why the wiki must record source-to-target mappings, open questions,
risks, implementation status, and verification notes. A migrated feature should
not be considered complete merely because code exists; it must be traceable.

## SDLC and iterative delivery

Software life cycle standards such as ISO/IEC/IEEE 12207 define software
development as a set of life cycle processes, activities, and tasks that may be
applied across acquisition, development, operation, maintenance, and retirement.
The wiki-driven process is compatible with this view: it gives migration teams
a repeatable process for discovery, design, implementation, verification, and
maintenance.

The framework is also compatible with agile delivery. The Agile Manifesto
values working software and responsiveness to change, but it does not imply
that documentation has no value. In this framework, documentation is not
treated as a static report produced after delivery. Instead, the wiki is a
working artifact that supports iterative delivery. Each migration slice should
move through analysis, planning, implementation, verification, and wiki sync.

## Knowledge-based agents and AI terminology

The phrase "knowledge-based agent" should be used carefully. In classical AI,
a knowledge-based agent reasons over a represented body of knowledge. An LLM
agent using this template is not necessarily a fully symbolic knowledge-based
agent. More precisely, the wiki acts as an external knowledge base that the
agent consults and updates as part of its work.

Similarly, the template can be described as utility-informed rather than as a
fully formal utility-based agent architecture. The process encourages agents to
prefer actions that increase traceability, reduce uncertainty, preserve source
behaviour, improve verification, and lower implementation risk. A formal
utility-based agent would require an explicit utility function, measurable
state variables, and decision rules. This template provides a governance model,
not a mathematical utility function.

## Multi-agent systems and shared-memory coordination

Multi-agent systems study how multiple agents coordinate, communicate, divide
work, and manage dependencies. The AI Agent Council pattern in this template is
a project-specific application of those ideas. It assigns specialized roles,
such as Source Analyst, Data Model Agent, UI Mapping Agent, Security Agent,
Implementation Agent, and QA Reviewer Agent.

The pattern is also related to blackboard architectures. In a blackboard system,
specialized knowledge sources contribute to a shared problem-solving space. The
template does not implement a formal blackboard control architecture, but it
uses a similar coordination principle: agents do not rely on private memory;
they read and write shared project artifacts.

## Constraint satisfaction, search, and planning

Migration can be analyzed as a constraint satisfaction and planning problem.
Source entities, fields, screens, workflows, roles, and integrations must be
mapped to target platform constructs while preserving business constraints.
Examples include required fields, relationships, status semantics, security
boundaries, side effects, audit requirements, and target-platform limitations.

This framing is conceptually useful, but the template should not claim to solve
a formal constraint satisfaction problem unless variables, domains, constraints,
and solving procedures are explicitly encoded. In its current form, the
template uses CSP and planning as analytical lenses for disciplined decision
making.

# Framework Definition

The wiki-driven enterprise migration framework has four repository areas plus an agent schema file.

| Template layer | Academic construct | Enterprise purpose |
| --- | --- | --- |
| `raw/` | Evidence repository | Stores original source artifacts without reinterpretation. |
| `wiki/` | External knowledge base, traceability repository, design rationale store | Converts source evidence into structured migration knowledge. |
| `target/` | Implementation artifact layer | Contains or points to the target system being built. |
| `docs/` | Method documentation | Explains the framework for human readers without replacing operational rules. |
| `AGENTS.md` | Schema and operating rules | Defines how agents ingest, update, index, log, and maintain the wiki. |

The framework's central rule is:

> Implementation should not begin until enough source evidence has been
> collected, described, and converted into an initial wiki.

This does not mean that every detail must be known before any migration work
starts. It means that unknowns must be explicit. Unknown or unsupported
behaviour should be marked as `unclear`, not silently filled in by the agent.

# Wiki-Driven SDLC

The SDLC workflow can be described as a recurring loop:

```txt
collect evidence
  -> build or update wiki
  -> identify gaps, risks, and assumptions
  -> design target mapping
  -> plan migration slice
  -> implement target feature
  -> verify against source evidence
  -> sync wiki
  -> select next slice
```

This loop supports both governance and agility. Governance comes from
traceability, explicit assumptions, and verification records. Agility comes from
implementing one migration slice at a time rather than attempting a single
large rewrite.

A migration slice is done only when:

1. The target feature is implemented.
2. The feature is linked to source evidence.
3. Relevant wiki pages are updated.
4. Traceability is updated.
5. Tests or verification notes are recorded.
6. Open questions are updated.
7. `wiki/log.md` has a new entry.

This definition of done prevents a common migration failure mode: source
understanding, implementation, and documentation drifting apart.

# AI Agent Council Pattern

The AI Agent Council is an optional role-based coordination pattern for complex
enterprise migrations. It should be understood as a governance pattern, not as a
claim that the agents form a formally verified multi-agent system.

The council pattern is useful when a migration has multiple concerns:

- source analysis
- data modeling
- UI mapping
- workflow and integration mapping
- security and permission analysis
- implementation
- QA and traceability review

Each role contributes to the shared wiki. The wiki is the coordination
mechanism and the durable source of truth. Private chat memory is not
authoritative because it is hard to audit, hand over, or reuse.

| Council role | Primary concern | Wiki output |
| --- | --- | --- |
| Orchestrator | Process coordination and prioritization | Current status, next slice, blockers |
| Source Analyst | Source system understanding | Source inventory, screen catalog, open questions |
| Data Model Agent | Entities, fields, constraints, relationships | Data mapping, data risks, assumptions |
| UI Mapping Agent | Screens, flows, controls, user experience | Screen mapping, UI backlog |
| Workflow and Integration Agent | Process logic and side effects | Workflow catalog, integration mapping |
| Security Agent | Roles, permissions, sensitive data | Permission matrix, security risks |
| Implementation Agent | Target build work | Implementation status, changed artifacts |
| QA Reviewer Agent | Completeness and verification | Traceability gaps, test status, readiness notes |

The council pattern is especially relevant for enterprise contexts because
migration quality depends on separation of concerns. A single agent can perform
all roles for a small app, but large migrations benefit from explicit role
boundaries and review responsibilities.

# Academic Correctness of Key Terms

The following terminology should be used with precision.

| Term | Correct use in this template | Overclaim to avoid |
| --- | --- | --- |
| Knowledge base | The wiki is an external repository of structured migration knowledge. | Claiming the LLM itself is a symbolic knowledge-based agent. |
| Utility-based reasoning | The process prefers actions that reduce risk and improve traceability. | Claiming a formal utility function exists when it is not defined. |
| Constraint satisfaction | Migration mappings can be analyzed as constraints over source and target elements. | Claiming formal CSP solving without encoded variables and constraints. |
| Multi-agent system | The council is inspired by role-based multi-agent coordination. | Claiming formal autonomous agent negotiation or protocol compliance. |
| Blackboard architecture | The wiki resembles a shared problem-solving space. | Claiming the template implements a formal blackboard control cycle. |
| Requirements traceability | Source evidence, requirements, design, implementation, and tests are linked. | Treating traceability as optional documentation after implementation. |
| Design rationale | Decisions, assumptions, and trade-offs are recorded for future review. | Recording only final decisions without why they were made. |

# Application to Enterprise Migration

The framework is intended for migrations where the source and target platforms
may differ substantially. For example, a source system may be a low-code
application with captured screens, entities, workflows, and roles, while the
target may be a modern platform with a different data model, UI framework, or
workflow engine.

In the motivating Power Platform scenario, target artifacts may include
Dataverse tables and relationships, Power Apps Code Apps, Canvas Apps,
connectors, environment configuration, and supporting automation. In other
organizations, the target may instead be a different platform provider or a
custom pro-code application with separate frontend, backend, data, and
integration layers.

In such contexts, direct implementation from screenshots is risky. Screenshots
show interface state, but they may not explain validation rules, permissions,
workflow side effects, or data ownership. The wiki acts as an intermediate
representation between evidence and implementation. It forces the team to ask:

- What is confirmed by source evidence?
- What is inferred?
- What remains unclear?
- Which target artifact implements this source behaviour?
- How was it verified?

This makes the migration more auditable and easier to continue across multiple
developers, reviewers, and AI agents.

# Limitations and Risks

The framework reduces several risks but does not eliminate them.

First, the wiki is only as good as the available source evidence and the care
with which that evidence is interpreted. Missing evidence must remain visible.

Second, AI agents can still hallucinate or overgeneralize. The template reduces
this risk by requiring evidence, status labels, open questions, and wiki sync.

Third, documentation can become stale. The SDLC rule that every implementation
change must update the wiki or explicitly state why no update was required is a
control against this risk.

Fourth, the framework is not a replacement for domain experts. Human review is
still required for business-critical workflows, security assumptions,
regulatory constraints, and ambiguous source behaviour.

Finally, the current template does not formalize all concepts mathematically.
It is a practical framework informed by academic concepts, not a complete
formal method.

# Future Work

The framework could be extended in several ways:

- A machine-readable traceability matrix linking source artifacts, wiki pages,
  target files, tests, and verification evidence.
- A stricter machine-readable schema for optional source manifests.
- Confidence labels for each wiki claim.
- Automated stale-documentation checks that compare implementation changes with
  wiki updates.
- Role-specific prompts or agent profiles for the AI Agent Council.
- Metrics for migration readiness, traceability coverage, unresolved risk, and
  verification completeness.
- A more formal utility model for prioritizing migration slices.

# Conclusion

The wiki-driven enterprise migration framework applies academic ideas from
knowledge management, requirements traceability, SDLC governance, design
rationale, and multi-agent coordination to a practical enterprise migration
template. Its core contribution is not a new AI theory. Its contribution is a
disciplined operating model: preserve source evidence, convert it into explicit
migration knowledge, coordinate agents through shared artifacts, implement in
verified slices, and keep the wiki synchronized with the target system.

This makes the template suitable for enterprise migration work where
correctness, auditability, continuity, and controlled use of AI agents matter.

# References {.unnumbered}

Agile Alliance. (2001). *Manifesto for Agile Software Development*.
https://agilemanifesto.org/

Burge, J. E. (2008). Design rationale: Researching under uncertainty. *AI EDAM*,
22(4), 311-324. https://doi.org/10.1017/S0890060408000319

Gotel, O., & Finkelstein, A. (1994). An analysis of the requirements
traceability problem. *Proceedings of the First International Conference on
Requirements Engineering*, 94-101. https://discovery.ucl.ac.uk/id/eprint/749/

ISO. (2018). *ISO/IEC/IEEE 29148:2018 Systems and software engineering - Life
cycle processes - Requirements engineering*. https://www.iso.org/standard/72089.html

ISO. (2026). *ISO/IEC/IEEE 12207:2026 Systems and software engineering -
Software life cycle processes*. https://www.iso.org/standard/90219.html

Nii, H. P. (1986). Blackboard application systems, blackboard systems and a
knowledge engineering perspective. *AI Magazine*, 7(3), 82.
https://doi.org/10.1609/aimag.v7i3.550

Nonaka, I. (1994). A dynamic theory of organizational knowledge creation.
*Organization Science*, 5(1), 14-37. https://doi.org/10.1287/orsc.5.1.14

Wooldridge, M., & Jennings, N. R. (1995). Intelligent agents: Theory and
practice. *The Knowledge Engineering Review*, 10(2), 115-152.
https://doi.org/10.1017/S0269888900008122
