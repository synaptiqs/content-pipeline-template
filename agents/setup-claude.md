# Claude — Setup Instructions

Read this once when you first connect. After setup, your standing role is
`agents/claude.md`.

## Step 1: Read the repo

1. Read `agents/shared-context.md` — the full design history
2. Read `agents/claude.md` — your standing role
3. Read `voice/guide.md` and `brands/your-brand/voice.md`
4. Read `STRUCTURE.md` — the folder/branch conventions

## Step 2: Verify the structure

Confirm these exist:

- `posts/` with at least one post folder containing `01-draft.md`
- `platforms/x/`, `platforms/linkedin/`, `platforms/youtube/`
- `brands/your-brand/` with `voice.md`
- `.github/workflows/pipeline.yml`

If anything is missing, flag it to the owner before proceeding.

## Step 3: Connect your API

- The owner stores your API key in GitHub Secrets as `ANTHROPIC_API_KEY`
- The workflow in `.github/workflows/pipeline.yml` has a placeholder echo
  step for the critique stage — replace it with a real API call that:
  - Reads `01-draft.md` from the post folder
  - Reads the brand voice guide
  - Writes `02-critique.md` with your structured critique
- Never hard-code the key in any file. Secrets only.

## Step 4: Run a test critique

On the existing test post (`posts/YYYY-MM-DD-topic/`):

- Read `01-draft.md`
- Write `02-critique.md` following the format in `agents/claude.md`
- Commit to branch `post/YYYY-MM-DD-topic`

## Step 5: Confirm to the owner

Tell them: structure verified, API connected, test critique committed.
If anything failed, say exactly what and where.