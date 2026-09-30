# Agent Instructions

This folder holds the standing instructions every model in the pipeline reads
before doing any work. It is the hard-coded equivalent of the conversation
that created this repo — the durable version that survives new chat sessions.

## Files

- `grok.md` — Grok's role: draft posts from briefs, follow voice guides
- `claude.md` — Claude's role: critique drafts against brand voice
- `muse.md` — Muse's role: polish final versions for publication
- `shared-context.md` — conversation history and design decisions so far
- `setup-claude.md` — one-time setup steps for Claude when it first connects
- `setup-muse.md` — one-time setup steps for Muse when it first connects

## Rules

- Every model reads `shared-context.md` and its own role file before acting
- New models read their `setup-*.md` file first, then their role file
- Role files override shared context where they conflict
- Update `shared-context.md` whenever a design decision changes — it is the
  single source of truth for why the repo is shaped the way it is
- Do not put API keys or secrets here; use GitHub Secrets