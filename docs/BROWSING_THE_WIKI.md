# Browsing The Wiki

The AI writes and maintains the wiki. Your job is to read it, follow links, and steer. A plain text editor works, but a linked-markdown browser makes the wiki far easier to navigate, especially for non-technical users.

## Recommended: Obsidian

[Obsidian](https://obsidian.md) is a free markdown app that treats a folder of markdown files as a "vault." It is the most convenient way to browse this wiki.

1. Install Obsidian.
2. Choose "Open folder as vault" and select this repository, or just the `wiki/` folder.
3. Open `wiki/index.md` and follow the `[[wikilinks]]` between pages.

The intended loop: keep your AI tool open on one side and Obsidian on the other. The AI edits the wiki based on your conversation; you watch the pages, links, and graph update in real time.

## Graph view

Obsidian's graph view shows the shape of the wiki: which pages are hubs, what is connected, and which pages are orphans with no inbound links. Wiki pages in this template use `[[wikilinks]]`, so the graph fills in automatically as the AI cross-references pages.

## Dataview (optional)

Every generated wiki page carries YAML frontmatter (`type`, `status`, `created`, `updated`, `tags`). With the community plugin [Dataview](https://github.com/blacksmithgu/obsidian-dataview) you can run live queries over that frontmatter, for example:

- all pages with `status: unclear` (open questions to resolve)
- all pages of `type: decision` (a decision log)
- recently `updated` pages

Example Dataview query:

````txt
```dataview
table status, updated
from "wiki"
where status = "unclear"
sort updated desc
```
````

## Marp (optional)

If you want slide decks straight from wiki content, the Marp plugin renders markdown as slides. Useful for migration readouts or research summaries.

## Working with screenshots and images

AI tools cannot always read a markdown page and its embedded images in one pass. For screenshot-heavy projects, common in application migration, the reliable pattern is:

1. Ask the AI to read the page text first.
2. Then ask it to view specific referenced images for extra detail.

Keep original screenshots under `raw/` so they remain stable evidence.

## A note on scale

Reading `wiki/index.md` first, then opening relevant pages, works well up to roughly a hundred sources and a few hundred pages. Past that, add a markdown search tool, for example a local search engine the AI can shell out to, and record it as a row in `wiki/capabilities.md`.
