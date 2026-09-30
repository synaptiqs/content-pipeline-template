# Roadmap: Deploying This Pipeline for a New Brand

Generic steps. Adjust per brand — the repo structure stays the same.

## Phase 0 — Decide (before touching the repo)

- [ ] Brand name and X handle
- [ ] Primary audience (who actually reads this)
- [ ] Platforms: X, LinkedIn, YouTube, others?
- [ ] Which models: draft / critique / polish assignments
- [ ] Publishing tool: Metricool, Buffer, native APIs, manual
- [ ] Cadence: posts per week per platform

## Phase 1 — Scaffold (one afternoon)

- [ ] Fork or copy this repo
- [ ] Rename `brands/_template/` to `brands/<handle>/`
- [ ] Fill in `brands/<handle>/voice.md` — tone, what works, what to avoid
- [ ] Update root `voice/guide.md` if the pipeline-wide tone differs
- [ ] Add platform folders only for platforms you'll actually use
- [ ] Store API keys in GitHub Secrets (never in files)

## Phase 2 — First post (validates everything)

- [ ] Write one brief in `briefs/` using the example format
- [ ] Open branch `post/YYYY-MM-DD-topic`
- [ ] Run draft → critique → polish, one commit per stage
- [ ] Adapt to each platform folder
- [ ] Open PR, review, merge to `main`
- [ ] Publish manually first — don't automate until the loop is trusted

## Phase 3 — Automate

- [ ] Wire the GitHub Action to call model APIs on file events
- [ ] Connect the scheduler to `platforms/` folders
- [ ] Add a review gate: nothing publishes without human approval
- [ ] Set up monitoring: failed workflow runs, stale branches

## Phase 4 — Scale

- [ ] Add a second brand by copying `_template/` again
- [ ] Shared briefs across brands: link, don't duplicate
- [ ] Track what works per brand in a simple log (briefs + results)
- [ ] Revisit voice guides monthly — drift is silent

## Failure modes to watch

- **Voice drift:** brand folders quietly diverging from the master guide
- **Stale platform files:** adaptations not updated when the master changes
- **Secrets in repo:** API keys committed by accident — rotate immediately
- **Over-automation:** publishing without review before the loop is proven
- **Branch sprawl:** old `post/` branches never deleted — clean monthly

## Success criteria

- One post goes brief → publish in under an hour with one human approval
- Every published post traces back to a brief, a voice guide, and a PR
- A new brand deploys from `_template/` in under a day