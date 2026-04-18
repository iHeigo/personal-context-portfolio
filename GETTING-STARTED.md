# Getting Started

Two systems. Build them in order — portfolio first, then wiki.

---

## Step 1: Build Your Portfolio

Your portfolio is the foundation. It tells the wiki who it's being built for.

### Option A: Use the Web App

A purpose-built interviewer agent handles the whole process.

1. Go to [app URL].
2. Sign in with your email (magic link, no password needed).
3. The agent interviews you across all ten files in sequence.
4. Download your complete portfolio as a zip when done.
5. Drop the files into `portfolio/` in this repo.

The whole thing takes 30-60 minutes in one sitting. Most people spread it across a few sessions.

### Option B: Do It Yourself

1. Open any template file from `portfolio/templates/`.
2. Paste the entire file to Claude or ChatGPT.
3. Say "let's do this one."
4. Your AI build partner reads the embedded interview protocol and starts asking questions.
5. When it has enough, it drafts the file. Read it and correct what's wrong.
6. Save the final version into `portfolio/` (or a subdirectory of your choosing).
7. Repeat for the remaining templates.

**Recommended order:** Start with `identity.md` and `role-and-responsibilities.md` — everything else builds on those two.

**Full sequence:**
1. `identity.md`
2. `role-and-responsibilities.md`
3. `current-projects.md`
4. `team-and-relationships.md`
5. `tools-and-systems.md`
6. `communication-style.md`
7. `goals-and-priorities.md`
8. `preferences-and-constraints.md`
9. `domain-knowledge.md`
10. `decision-log.md`

**Tips:**
- Be specific, not aspirational. Your agents need ground truth, not how you wish you worked.
- Don't skip the reaction pass. When your build partner drafts a file, read it and correct what it got wrong. That's where the real signal is.
- Short is better than long. One page per file, not five. Dense context beats sprawling context.

---

## Step 2: Set Up the Wiki

Open a new Claude Code session in this repo and say:

> "Read CLAUDE.md, then read my portfolio files in portfolio/. You are my LLM wiki agent. Confirm you understand the ingest, query, and lint workflows, and tell me what you need to ingest the first source."

Then drop your first source into `raw/` and say "ingest this."

That's it. The LLM reads the source, creates wiki pages, updates the index, and appends to the log. Drop in another source when you have one.

**What makes a good first source:**
- Something you've already read and found valuable
- An article, transcript, meeting notes, or research paper
- Text-based (PDFs work; images need the LLM to handle them separately)

**After the first ingest:** Open Obsidian on this folder. The graph view shows you what got created and how it connects.

---

## Step 3: Wire It In

The wiki and portfolio are most useful when they're accessible to your other AI tools — not just Claude Code sessions on this repo.

See the `wiring/` directory for:
- **`mcp-resource.md`** — expose both layers as MCP resources (most automated)
- **`system-prompt-patterns.md`** — copy-paste patterns for Claude, ChatGPT, Gemini
- **`claude-projects.md`** — use your portfolio in Claude Projects
- **`api-layer.md`** — build an API layer if you want programmatic access

Start with whichever tool you use most.

---

## Ongoing Maintenance

**Portfolio:** Review quarterly or when something significant changes (new job, new projects, major priority shift). Ask Claude Code: "Help me update current-projects.md — here's what's changed."

**Wiki:** Add sources whenever you read something worth keeping. Run a lint pass monthly: "Health-check the wiki — look for contradictions, orphan pages, stale claims, and missing cross-references."

**Log:** Use `grep "^## \[" log.md | tail -10` to see recent activity.
