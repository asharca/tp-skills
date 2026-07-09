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

## Included Skills

- `mineru-ocr` — Use an attached OcrPlane OCR MCP deployment.
- `ocrplane-cli` — Use the `ocrplane` CLI for sandbox/local document OCR.

## Automatic Sync

After deploying ToolPlane with the tp-skills registry webhook route, create a
GitHub repository webhook for this repo:

```txt
Payload URL: https://<toolplane-host>/api/v1/skill-registries/tp-skills/webhook
Content type: application/json
Secret: the value of TP_SKILLS_WEBHOOK_SECRET
Events: push
```

ToolPlane will verify GitHub's `X-Hub-Signature-256` header and sync this
registry whenever `main` receives a push.

For GitHub API rate limits, configure exactly one token variable in ToolPlane:

```txt
GITHUB_TOKEN=...
```

or:

```txt
TOOLPLANE_GITHUB_TOKEN=...
```

Do not set both. If both are present, ToolPlane uses `GITHUB_TOKEN`.
