---
name: toolplane-skill-author
description: Create or refine ToolPlane-compatible agent skills with clear triggers, instructions, and supporting files.
author: ToolPlane
---

# ToolPlane Skill Author

Use this skill when the user wants to create, review, or improve an agent skill
that will be stored in a ToolPlane skill registry.

## Workflow

1. Clarify the skill's trigger: when should an agent load it?
2. Keep `SKILL.md` focused on procedural instructions, not marketing copy.
3. Add frontmatter with `name`, `description`, and optional `author`.
4. Put large examples, scripts, schemas, or references in sibling files.
5. Make the first version small enough to test with a real task.

## Quality Bar

- The description should be specific enough for automatic skill selection.
- Instructions should tell the agent what to do, what to avoid, and what output
  shape to produce.
- Supporting files should be referenced by path from `SKILL.md`.
- Avoid secrets, personal data, or environment-specific paths.

## ToolPlane Compatibility

ToolPlane imports the whole skill folder. `SKILL.md` is stored as the primary
content, and sibling files are bundled as extra files.

See `references/checklist.md` for a compact review checklist.
