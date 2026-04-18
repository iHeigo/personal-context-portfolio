# Personal Context System

Two complementary layers. One for who you are. One for what you know.

---

## The Problem

Every AI agent you use needs two things to be genuinely useful: it needs to know *who you are* (your role, goals, preferences, constraints) and it needs to know *what you know* (your accumulated research, meeting notes, domain expertise). Most people re-explain the first from scratch every session and lose the second entirely when a conversation closes.

This system solves both.

---

## Layer 1: Portfolio — Who You Are

A structured set of ten markdown files that together form a portable, AI-readable operating manual for anyone working with you. Not a resume. Not a profile. Context.

| File | What It Captures |
|------|-----------------|
| `identity.md` | Who you are — the one file an agent reads if it can only read one |
| `role-and-responsibilities.md` | What your weeks actually look like, not what your job title says |
| `current-projects.md` | Active workstreams, status, priority, what done looks like |
| `team-and-relationships.md` | Key people, how you interact, what they need from you |
| `tools-and-systems.md` | Your stack, your setup, what connects to what |
| `communication-style.md` | How you write, how you want things written for you |
| `goals-and-priorities.md` | What you're optimizing for and what you're deliberately ignoring |
| `preferences-and-constraints.md` | Hard rules, strong opinions, things any agent should respect |
| `domain-knowledge.md` | What you know that a general-purpose AI doesn't |
| `decision-log.md` | How you make decisions, with real examples |

**Update cadence:** Quarterly, or when something significant changes.
**How to build it:** See `portfolio/` — templates, examples, and the full interview protocol are there.

---

## Layer 2: Wiki — What You Know

A compounding knowledge base maintained entirely by the LLM. You drop raw sources (articles, transcripts, meeting notes, PDFs) into `raw/`. The LLM reads them, creates structured wiki pages in `wiki/`, and builds relationships between concepts automatically. The knowledge accumulates. Cross-references are already there when you need them. Nothing is re-derived from scratch on every query.

```
raw/    ← drop sources here (immutable — LLM reads, never writes)
wiki/   ← LLM-generated pages (entities, concepts, topics, syntheses)
index.md  ← catalog of all wiki pages, updated on every ingest
log.md    ← append-only record of ingests, queries, and lint passes
```

**Update cadence:** Continuous — any time you have a source worth keeping.
**How it works:** See `CLAUDE.md` for the ingest, query, and lint workflows.

---

## How They Connect

The portfolio is the identity layer. The wiki is the knowledge layer. Together they give any AI tool complete context: who it's working with *and* what that person has accumulated.

In practice: the LLM maintaining the wiki already knows from your portfolio who it's building this for — your domain, your goals, your communication style. The wiki's "about me" research (journal entries, retrospectives, goal reflections) can feed back into portfolio files like `current-projects.md` or `goals-and-priorities.md`. They're separate systems that inform each other.

---

## Repo Structure

```
/
├── README.md
├── GETTING-STARTED.md
├── CLAUDE.md               ← governs both layers (read this)
├── index.md                ← wiki index (LLM-maintained)
├── log.md                  ← wiki log (LLM-maintained)
├── raw/                    ← drop sources here
├── wiki/                   ← LLM-generated knowledge base
├── portfolio/
│   ├── templates/          ← ten empty templates with embedded interview protocols
│   ├── examples/           ← filled examples for knowledge-worker, executive, entrepreneur
│   └── interview-protocol/ ← full system prompt for the interviewer agent
└── wiring/                 ← guides for connecting both layers to AI tools
```

---

## Design Principles

**Markdown-first.** Every AI system on earth can read markdown. No databases, no embeddings infrastructure, no proprietary formats. Files that are human-readable and machine-readable.

**LLM writes, human curates.** The wiki's maintenance burden — updating cross-references, keeping summaries current, flagging contradictions — is entirely the LLM's job. Your job is sourcing, directing, and asking good questions.

**Portable across everything.** Works with Claude Code, Claude Projects, ChatGPT, any tool that reads files. No vendor lock-in.

**Modular by design.** The portfolio and wiki are independent systems. Use one, use both, wire them together. Pick what fits.

---

## License

MIT.
