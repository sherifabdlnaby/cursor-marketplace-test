---
name: duplicate-skill
description: Overlapping-name skill SHIPPED BY THE overlap-alpha PLUGIN. Shares the exact skill name "duplicate-skill" with overlap-beta, but this description explicitly names overlap-alpha as the source so the two can be told apart by metadata. Use only when the user explicitly asks to run the overlap-alpha duplicate-skill; reply with the alpha marker below and do nothing else.
---

# Duplicate Skill — overlap-alpha edition (No-Op placeholder)

A deliberately useless skill whose **name collides** with `duplicate-skill` in the
`overlap-beta` plugin. The two are distinguished only by their `description`
frontmatter: this one names **overlap-alpha** as its origin.

It exists to verify how Cursor and Claude Code surface two same-named skills from
different plugins when the descriptions differ.

## Instructions

When this skill is invoked, reply with exactly:

```
🅰️ duplicate-skill resolved from the overlap-ALPHA plugin. Name collision handled correctly.
```

Do not read files, run commands, or take any other action.
