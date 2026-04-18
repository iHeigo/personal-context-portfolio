# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

Two complementary systems in one repo:

1. **Portfolio** (`portfolio/`) — a structured set of markdown files representing who the user is. Static context injected into AI system prompts. Updated quarterly.
2. **Wiki** (`raw/` + `wiki/`) — a compounding knowledge base you maintain by ingesting sources. Dynamic, grows continuously. You write all of it; the user only reads it.

Read both layers before doing anything. The portfolio tells you who you're working with. The wiki tells you what they've accumulated.

---

## Portfolio Layer

### Structure

```
portfolio/
├── templates/          ← empty templates with embedded interview protocols
├── examples/           ← filled examples for reference
└── interview-protocol/
    └── agent-system-prompt.md  ← full interviewer agent system prompt
```

The user's actual filled-in portfolio files may live directly under `portfolio/` (not in `templates/` or `examples/`).

### When to update portfolio files

- When the user says a project, role, priority, or relationship has changed
- During a quarterly review ("let's update the portfolio")
- When the wiki surfaces information that contradicts or extends a portfolio file

### How to update

Read the existing file first. Make targeted edits — don't rewrite unless the user asks. After updating, append an entry to `log.md`:

```
## [YYYY-MM-DD] portfolio-update | <filename>
Updated: <one-line description of what changed and why>
```

---

## Wiki Layer

### Structure

```
raw/        ← immutable source documents. Never modify these.
wiki/       ← your domain. You create and maintain all pages here.
index.md    ← catalog of all wiki pages. Update on every operation.
log.md      ← append-only. Every ingest, query, lint pass gets an entry.
```

### Wiki page conventions

Every wiki page should have:
- A `# Title` at the top
- A one-paragraph summary immediately below
- `## Connections` section listing related pages as `[[wiki/page-name]]` links
- `## Sources` section listing which raw files this page draws from

Use subdirectories in `wiki/` to organize by type: `wiki/entities/`, `wiki/concepts/`, `wiki/topics/`, `wiki/syntheses/`.

### Operations

#### Ingest

When the user drops a source into `raw/` and says to ingest it:

1. Read the source fully.
2. Discuss key takeaways with the user if they want to stay involved; otherwise proceed.
3. Write a summary page in `wiki/topics/` or wherever fits.
4. Create or update entity pages (`wiki/entities/`) for people, organizations, products mentioned.
5. Create or update concept pages (`wiki/concepts/`) for ideas or frameworks introduced.
6. Wire cross-references between new and existing pages.
7. Update `index.md` — add new pages to the catalog, update source counts.
8. Append to `log.md`:

```
## [YYYY-MM-DD] ingest | <source title>
File: raw/<filename>
Pages created: <list>
Pages updated: <list>
Key takeaways: <2-3 bullet points>
```

A single source typically touches 5-15 wiki pages.

#### Query

When the user asks a question:

1. Read `index.md` to find relevant pages.
2. Read those pages and follow their `## Connections` links as needed.
3. Synthesize an answer with citations to wiki pages.
4. If the answer is substantive and reusable, offer to file it as a new wiki page in `wiki/syntheses/`.
5. Append to `log.md`:

```
## [YYYY-MM-DD] query | <brief question summary>
Answer filed: wiki/syntheses/<filename> (or: not filed)
```

#### Lint

When the user asks for a wiki health check:

1. Scan all pages for: contradictions between pages, stale claims superseded by newer sources, orphan pages (no inbound links), concepts mentioned but lacking their own page, missing cross-references.
2. Report findings grouped by type.
3. Ask the user which issues to fix, then fix them.
4. Suggest new sources or questions that would fill identified gaps.
5. Append to `log.md`:

```
## [YYYY-MM-DD] lint
Issues found: <count>
Issues fixed: <count>
Suggestions: <list>
```

---

## Index and Log Conventions

**`index.md`** — content-oriented. One row per wiki page. Keep the categories clean: Entities, Concepts, Topics, Syntheses, Sources. Update on every ingest or lint pass.

**`log.md`** — chronological, append-only. Most recent entry first. Every entry starts with `## [YYYY-MM-DD] <operation> | <title>`. Never edit old entries.

---

## What Not to Do

- Never modify files in `raw/`. They are immutable source of truth.
- Never write portfolio files from scratch unprompted. Edit existing ones with targeted changes only.
- Never let wiki pages become stale without flagging it. If you know a page's claim has been superseded, note it inline.
- Don't let `index.md` drift out of sync. Update it on every operation that touches wiki pages.
