# Brands

Each brand gets its own folder. Brands are parallel to posts and platforms —
not nested inside them.

## Layout

```
brands/
├── README.md
├── _template/             # Copy this for every new brand
│   ├── voice.md
│   ├── briefs/
│   ├── posts/
│   └── platforms/
└── <brand-handle>/        # One per brand
    ├── voice.md
    ├── briefs/
    ├── posts/
    └── platforms/
```

## Rules

- One folder per brand, named after the brand's X handle (lowercase)
- Each brand owns its voice, briefs, posts, and platform files
- Shared pipeline logic (workflows, STRUCTURE.md) stays at repo root
- A post spanning brands references the same brief from each brand folder
- Never duplicate content across brand folders — link it

## Adding a new brand

1. Copy `_template/` to `brands/<new-handle>/`
2. Fill in `voice.md` with the brand's tone and audience
3. Add the first brief to `briefs/`
4. Open a branch `post/YYYY-MM-DD-topic` and run the stage chain
5. Adapt to platforms under `platforms/`

## Failure modes

- Don't nest brands inside posts — keep them parallel
- Don't share one voice.md across brands with different audiences
- Don't let brand folders drift from the shared stage conventions