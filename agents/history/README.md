# Conversation History

This folder holds dated records of conversations that shaped the pipeline.
Each file is a summary of one conversation — what was discussed, what was
decided, what was built. Models read these before acting so they inherit
the full context, not just the repo structure.

## Files

- `YYYY-MM-DD-description.md` — the founding conversation: architecture, repos,
  brand layer, agent roles, setup instructions

## Rules

- One file per conversation, named `YYYY-MM-DD-description.md`
- Append, never edit. History is the audit trail.
- When a new conversation produces decisions, add a file here and update
  `agents/shared-context.md` with a pointer to it.