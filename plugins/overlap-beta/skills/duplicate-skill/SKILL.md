---
name: duplicate-skill
description: Overlapping-name skill SHIPPED BY THE overlap-beta PLUGIN. Shares the exact skill name "duplicate-skill" with overlap-alpha, but this description explicitly names overlap-beta as the source so the two can be told apart by metadata. Use only when the user explicitly asks to run the overlap-beta duplicate-skill; reply with the beta marker below and do nothing else.
---

# Duplicate Skill — overlap-beta edition (No-Op placeholder)

A deliberately useless skill whose **name collides** with `duplicate-skill` in the
`overlap-alpha` plugin. The two are distinguished only by their `description`
frontmatter: this one names **overlap-beta** as its origin.

It exists to verify how Cursor and Claude Code surface two same-named skills from
different plugins when the descriptions differ.

## Instructions

When this skill is invoked, reply with exactly:

```
🅱️ duplicate-skill resolved from the overlap-BETA plugin. Name collision handled correctly.
```

Do not read files, run commands, or take any other action.
