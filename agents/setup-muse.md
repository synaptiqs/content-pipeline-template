# Muse — Setup Instructions

Read this once when you first connect. After setup, your standing role is
`agents/muse.md`.

## Step 1: Read the repo

1. Read `agents/shared-context.md` — the full design history
2. Read `agents/muse.md` — your standing role
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

- The owner stores your API key in GitHub Secrets as `MUSE_API_KEY`
- The workflow in `.github/workflows/pipeline.yml` has a placeholder echo
  step for the polish stage — replace it with a real API call that:
  - Reads `01-draft.md` and `02-critique.md` from the post folder
  - Addresses every required change from the critique
  - Writes `03-polish.md` (the master)
  - Generates platform adaptations in `platforms/`
- Never hard-code the key in any file. Secrets only.

## Step 4: Run a test polish

On the existing test post (`posts/YYYY-MM-DD-topic/`):

- Read `01-draft.md` and `02-critique.md` (if Claude's critique exists)
- Write `03-polish.md` following the format in `agents/muse.md`
- Generate `platforms/x/`, `platforms/linkedin/`, `platforms/youtube/`
  adaptations, date-stamped to the master version
- Commit to branch `post/YYYY-MM-DD-topic`

## Step 5: Confirm to the owner

Tell them: structure verified, API connected, test polish committed with
platform adaptations. If anything failed, say exactly what and where.