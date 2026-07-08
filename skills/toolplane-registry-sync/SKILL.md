---
name: toolplane-registry-sync
description: Sync a GitHub-hosted skill registry into ToolPlane and verify imported Skill records.
author: ToolPlane
---

# ToolPlane Registry Sync

Use this skill when working on ToolPlane's GitHub-backed skill registry import
flow.

## Steps

1. Confirm the registry owner, repo, ref, and root path.
2. Verify the repository has either `registry.json` or skill folders under the
   root path.
3. Run the sync command:

   ```bash
   pnpm skills:sync:tp
   ```

4. Check the admin Skills Market page for created or updated skills.
5. Open an imported skill and confirm `SKILL.md` plus bundled files render.
6. If a skill failed, inspect its folder for missing `SKILL.md`, invalid paths,
   or files larger than ToolPlane's bundle limits.

## Environment

The sync command reads these optional variables:

- `TP_SKILLS_OWNER`
- `TP_SKILLS_REPO`
- `TP_SKILLS_REF`
- `TP_SKILLS_ROOT`
- `TP_SKILLS_SLUG_PREFIX`
- `GITHUB_TOKEN` or `TOOLPLANE_GITHUB_TOKEN`
