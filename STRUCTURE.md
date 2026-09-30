# Repository Structure

## Design decision: folders, not branches, for brands and platforms

Branches are for *work in progress* (draft → critique → polish).
Folders are for *brands* and *platforms* — things that run in parallel
and never merge.

Why: branches diverge and merge, which is expensive for content that
never merges. Folders are cheap, parallel, and each output is
independently reviewable. One branch per post keeps the stage chain
clean; brand and platform folders keep the destinations clean.

## Layout

```
content-pipeline-template/
├── README.md
├── ROADMAP.md              # Deployment steps for new brands
├── STRUCTURE.md            # This file
├── voice/
│   └── guide.md            # Pipeline-wide voice guide
├── briefs/                 # Topic briefs (input)
│   └── YYYY-MM-DD-topic.md
├── posts/                  # One folder per post
│   └── YYYY-MM-DD-topic/
│       ├── 01-draft.md     # Model A
│       ├── 02-critique.md  # Model B
│       └── 03-polish.md    # Model C (master)
├── platforms/              # Per-platform adaptations
│   ├── x/
│   ├── linkedin/
│   └── youtube/
├── brands/                 # One folder per brand
│   ├── README.md
│   ├── _template/          # Copy for new brands
│   └── <brand-handle>/
│       ├── voice.md
│       ├── briefs/
│       ├── posts/
│       └── platforms/
└── .github/workflows/
    └── pipeline.yml        # Stage triggers (skeleton)
```

## Stage chain (branches)

- `main` — approved, published content only
- `post/YYYY-MM-DD-topic` — working branch for one post
  - Model A commits `01-draft.md`
  - Model B commits `02-critique.md`
  - Model C commits `03-polish.md`
  - Human approves → merge to `main`

## Brand rules

- One folder per brand, named after the brand's handle (lowercase)
- Each brand owns its voice, briefs, posts, and platform files
- Shared pipeline logic stays at repo root
- A post spanning brands references the same brief from each folder
- Never duplicate content across brand folders — link it

## Platform rules

- `03-polish.md` is the master. Platform files are adaptations, never rewrites.
- X: ≤280 chars, hook-first, hashtags minimal
- LinkedIn: longer form, narrative, professional tone
- YouTube: full script, title, description, tags
- Scheduler reads from `platforms/` for publishing

## Voice layering

1. Root `voice/guide.md` — pipeline-wide defaults
2. `brands/<handle>/voice.md` — brand-specific override
3. Brand file wins where they conflict

## Failure modes to avoid

- Don't let platform files drift from the master — date-stamp them
- Don't put API keys in the repo; use GitHub Secrets
- One brief per post; if a topic splits, split the brief
- Don't nest brands inside posts — keep them parallel at top level