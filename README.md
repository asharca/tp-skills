# tp-skills

ToolPlane skill registry. Each skill lives in `skills/<slug>/SKILL.md` and may
include references, scripts, or other supporting files beside it.

ToolPlane can sync this repository with:

```bash
pnpm skills:sync:tp
```

Default sync target:

```txt
asharca/tp-skills@main/skills
```

## Structure

```txt
registry.json
skills/
  my-skill/
    SKILL.md
    references/
    scripts/
```

`registry.json` is optional for ToolPlane, but keeping it explicit lets the
platform preserve slugs, categories, curation status, and scores.
