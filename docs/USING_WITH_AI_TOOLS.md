# Using This Template With AI Tools

The schema that controls AI behaviour in this template is `AGENTS.md`. The only trick is making sure your AI tool actually reads it. Different tools auto-load different files at the start of a session.

## Which file your tool reads automatically

| Tool | Auto-loaded instruction file | What to do here |
| --- | --- | --- |
| Claude Code | `CLAUDE.md` | Already provided. It points to `AGENTS.md`. |
| OpenAI Codex and many agents | `AGENTS.md` | Works out of the box; `AGENTS.md` is the canonical schema. |
| Cursor | `.cursor/rules` or `AGENTS.md` | Add a rule that says "Read AGENTS.md and follow it," or rely on `AGENTS.md`. |
| Gemini CLI | `GEMINI.md` | Copy `CLAUDE.md` to `GEMINI.md`; the same content works. |
| Anything else | varies | Use the universal fallback below. |

## Universal fallback

If you are unsure whether your tool loaded the schema, start your first message with:

```txt
Read AGENTS.md and follow it.
```

Every prompt in `docs/PROMPT_RECIPES.md` already begins with "Read AGENTS.md ...", so the recipes work in any tool even when nothing is auto-loaded.

## Why `AGENTS.md` is canonical

Keeping one schema avoids drift. `CLAUDE.md` (and any `GEMINI.md` you create) should stay thin: a pointer to `AGENTS.md`, nothing more. Put real operating rules only in `AGENTS.md` so there is a single source of truth.

## Making an equivalent for a new tool

1. Find which file your tool auto-loads at the start of a session.
2. Create that file at the repository root.
3. Paste the contents of `CLAUDE.md` into it. It already points to `AGENTS.md`.
