# Conversation: YYYY-MM-DD — Pipeline Founding

**Participants:** [Owner], [Model]
**Duration:** [start] to [end]
**Outcome:** Repo created, scaffold committed, agent instructions written.

---

## What [Owner] asked for

1. [Request one]
2. [Request two]
3. [Request three]

## What was built

- `agents/` — role files, shared-context.md, setup files, history/
- `brands/` — README, _template/, your-brand/ (voice.md + subfolders)
- `briefs/example-brief.md` — sample topic
- `voice/guide.md` — pipeline-wide voice guide
- `pipeline/README.md` — stage definitions
- `STRUCTURE.md` — full design documentation
- `posts/YYYY-MM-DD-topic/01-draft.md` — test draft on branch
  `post/YYYY-MM-DD-topic`
- `platforms/x|linkedin|youtube/` — test adaptations
- `.github/workflows/pipeline.yml` — skeleton with echo placeholders

## Design decisions made

1. **Git as conversation.** Models don't call each other. They commit files.
   The repo is the memory. This means every decision is auditable.
2. **Folders for platforms, branches for stages.** Platforms never merge;
   stages are sequential and isolated per post.
3. **Folders for brands, parallel not nested.** A post spanning brands
   references one brief from multiple brand folders.
4. **Voice is layered.** Pipeline-wide guide + per-brand override.
5. **Secrets in GitHub Secrets only.** No keys in the repo, ever.
6. **Human approval gate.** Models draft/critique/polish; owner approves;
   Metricool publishes. No model posts directly.
7. **Append-only history.** Conversations get dated files; nothing is edited
   away.

## Open items

- [ ] Wire Claude API into critique stage (replace echo in pipeline.yml)
- [ ] Wire Muse API into polish stage
- [ ] Add remaining brands beyond your-brand
- [ ] Connect Metricool to platforms/ folders
- [ ] Analytics feedback loop (performance data → briefs)

## Notes for future models reading this

- [Owner] is [who they are]. Their content is about [topics].
- Their X handle is @[handle]. The brand handle is @[brand].
- They value [qualities].
- [Scheduler] is their publishing tool.
- They are exploring multi-brand operations; [brand] is brand one.