# Prompt Recipes

Use these prompts as starting points. Replace bracketed text with your project details.

## Initialize The Wiki

```txt
Read AGENTS.md, README.md, raw/manifest.md if useful, and the files under raw/. Build the initial wiki under wiki/, update wiki/index.md, append to wiki/log.md, and report missing source materials, assumptions, contradictions, and unclear areas.
```

## Ingest One Source

```txt
Read AGENTS.md, wiki/index.md, wiki/log.md, raw/manifest.md if useful, and [raw/path/to/source]. Ingest this source into the wiki. Create or update relevant source, concept, entity, question, and synthesis pages. Update wiki/index.md and wiki/log.md.
```

## Batch Ingest Sources

```txt
Read AGENTS.md, README.md, raw/manifest.md if useful, wiki/index.md, and wiki/log.md. Ingest the new sources under raw/ or the subset I specify. Keep source claims traceable, mark unclear details, update cross-links, update wiki/index.md, and append one log entry summarizing the batch.
```

## Ask A Question Against The Wiki

```txt
Using wiki/index.md first, find the relevant wiki pages and answer this question from the wiki: [question]. Distinguish source-derived claims from inferred claims and list any unresolved gaps.
```

## File A Useful Answer Back Into The Wiki

```txt
The answer we just discussed is durable. File it back into the wiki as either a new page or updates to existing pages. Add links from related pages, update wiki/index.md, and append to wiki/log.md.
```

## Compare Sources

```txt
Compare these sources using the wiki and raw evidence: [source/page list]. Create a comparison page in wiki/ that captures agreements, contradictions, open questions, and source-backed conclusions. Update wiki/index.md and wiki/log.md.
```

## Lint The Wiki

```txt
Lint the wiki. Look for contradictions, stale claims, orphan pages, missing cross-links, duplicate pages, unsupported claims, and important concepts without their own pages. Fix low-risk issues directly, record larger findings in a maintenance page, update wiki/index.md, and append to wiki/log.md.
```

## Prepare For Implementation

```txt
Before changing target/, read AGENTS.md, wiki/index.md, wiki/log.md, and all relevant wiki pages. Summarize the source-backed requirements, assumptions, open questions, and traceability for the requested implementation slice. Do not implement until unclear requirements are surfaced.
```

## Choose Capabilities For A Task

```txt
Read AGENTS.md and wiki/capabilities.md if it exists. For this task: [task], identify the smallest useful set of skills, plugins, MCP servers, subagents, or external tools. Explain what you will use and why. Do not load unrelated capabilities.
```

## Hand Off To A Subagent

```txt
Prepare a subagent handoff for this task: [task]. Include the relevant wiki pages, raw source paths, current assumptions, open questions, expected output, and where the result should be filed back into wiki/. After the subagent returns, update the wiki and append to wiki/log.md if the finding is durable.
```

## Run A Council Review

```txt
Use an AI Agent Council for this high-impact question: [question]. Each agent should read the same relevant wiki pages and raw sources, produce role-specific findings, then compare results through the wiki. Record the final synthesis, disagreements, and decision rationale in wiki/, and append to wiki/log.md.
```