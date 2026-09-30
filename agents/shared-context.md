# Shared Context — Pipeline Design Decisions

Last updated: YYYY-MM-DD. Read this before any stage work.
All models (Grok, Claude, Muse) share this file. It is the durable record
of the conversation that created this repo — it survives new chat sessions.

## The problem

[Owner] runs multiple brands on social media (starting with [brand] on X).
They want AI models to draft, critique, and polish content, with a human
approval gate before publishing. Publishing goes through Metricool.

## The architecture

Three models in a chain:

1. **Grok** drafts from a brief
2. **Claude** critiques against the brand voice
3. **Muse** polishes into a final master + platform adaptations

Git is the conversation. Models don't talk to each other — they read and
write files. Every draft, critique, and revision is preserved as history.

## Design decisions

### Folders for platforms, branches for stages

Branches diverge and merge — expensive for content that never merges.
Folders are cheap and parallel. One branch per post
(`post/YYYY-MM-DD-topic`) keeps the stage chain isolated. Platform folders
(`platforms/x`, `platforms/linkedin`, `platforms/youtube`) hold adaptations
of the master `03-polish.md`.

### Folders for brands, not nested

`brands/<slug>/` owns voice, briefs, posts, and platforms for one brand.
Brands are parallel to posts and platforms — never nested inside them.
A post spanning brands references the same brief from each brand folder;
it never duplicates content. New brand = copy `brands/_template/`, fill
`voice.md`, add a brief, run the chain.

### Voice is layered

`voice/guide.md` is pipeline-wide. Each brand's `voice.md` extends
it and overrides where brand-specific. Models read both before acting.

### Secrets in GitHub Secrets only

API keys never go in the repo. The workflow skeleton in
`.github/workflows/pipeline.yml` has placeholder echo steps waiting for
real API calls wired to secrets.

### Human approval gate

Models draft, critique, and polish. [Owner] approves. Metricool publishes.
No model posts directly to any social platform.

### Append-only conversation history

`agents/history/` holds dated records of every conversation that shaped
the pipeline. New conversations get a new file; nothing is edited away.
See `agents/history/YYYY-MM-DD-description.md` for the founding record.

## Repos

- **Working pipeline:** [link to your deployment repo]
- **This template:** https://github.com/synaptiqs/content-pipeline-template

## Open items (as of YYYY-MM-DD)

- [ ] Wire Claude API into the critique stage
- [ ] Wire Muse API into the polish stage
- [ ] Add remaining brands beyond [brand]
- [ ] Connect Metricool to `platforms/` for scheduling
- [ ] Add analytics feedback loop (performance → briefs)

## Pointers to detailed history

- Founding conversation: `agents/history/YYYY-MM-DD-description.md`