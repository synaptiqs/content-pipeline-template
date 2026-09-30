# Content Pipeline Template

A multi-model content pipeline for running a brand's social media presence with AI.
Three models in a chain — one drafts, one critiques, one polishes — and a human
approves before anything publishes. The repo is the shared memory: every draft,
critique, and revision is a committed file, so the full history is auditable.

This is the public template. The working deployment (SynaptiqsHQ's private brain)
lives at https://github.com/synaptiqs/SynaptiqsHQ.

## Why this exists

Most AI content workflows are chat sessions that evaporate. This one treats
Git as the conversation. Models don't call each other — they read and write
files. That means:

- **Full audit trail.** Every decision is a commit. You can reconstruct why a
  post reads the way it does.
- **No context loss.** A new chat session reads the repo and picks up where
  the last one left off.
- **Parallel work.** Multiple brands, multiple platforms, multiple posts in
  flight — folders keep them from colliding.

## The architecture

```
Brief → Grok (draft) → Claude (critique) → Muse (polish) → Human approval → Metricool
```

| Stage | Model | Output |
|-------|-------|--------|
| Draft | Grok | `01-draft.md` |
| Critique | Claude | `02-critique.md` |
| Polish | Muse | `03-polish.md` (master) + platform adaptations |

## Three axes

- **Stages are branches.** One branch per post: `post/YYYY-MM-DD-topic`.
  Sequential, isolated, reviewable.
- **Platforms are folders.** `platforms/x`, `platforms/linkedin`,
  `platforms/youtube`. Parallel destinations for the same content — they
  never merge.
- **Brands are folders.** `brands/<slug>/` owns voice, briefs, posts, and
  platforms. Parallel, not nested. A post spanning brands references one
  brief from multiple folders.

## Quick start

1. Fork or copy this repo
2. Fill in `voice/guide.md` with your brand's voice
3. Copy `brands/_template/` to `brands/<your-brand>/` and write its voice
4. Add a brief to `briefs/`
5. Open a branch `post/YYYY-MM-DD-topic` and run the stage chain
6. Store API keys in GitHub Secrets — never in the repo
7. Wire your scheduler (Metricool or equivalent) to read `platforms/`

## Design decisions

- **Git as conversation.** Models read and write files; the repo is the memory.
- **Folders for platforms, branches for stages.** Platforms never merge;
  stages are sequential.
- **Folders for brands, parallel not nested.**
- **Secrets in GitHub Secrets only.**
- **Human approval gate.** Models draft, critique, polish. Humans publish.
- **Append-only history.** Conversations get dated files in `agents/history/`.

## Failure modes to watch

- **Context drift:** each model only sees files you feed it. Pass earlier
  reasoning forward explicitly.
- **Platform drift:** platform files must never diverge from the master
  `03-polish.md`. Date-stamp them.
- **Stale briefs:** one brief per post. If a topic splits, split the brief.
- **Workflow placeholders:** the skeleton Action echoes messages. Wire real
  API calls before expecting automation.

## License

Use freely for your own brands. Credit appreciated but not required.