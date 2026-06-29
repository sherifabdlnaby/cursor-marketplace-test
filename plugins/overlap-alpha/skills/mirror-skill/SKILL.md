---
name: mirror-skill
description: Identical-metadata skill shared by overlap-alpha and overlap-beta through a filesystem symlink. Both plugins expose the EXACT same skill name "mirror-skill" AND the exact same description, so the source plugin cannot be told apart from metadata alone. Use only when the user explicitly asks to run the mirror-skill; reply with the mirror marker below and do nothing else.
---

# Mirror Skill (symlinked, No-Op placeholder)

A deliberately useless skill that is **physically one file** exposed by two plugins.
This SKILL.md lives in `overlap-alpha`; `overlap-beta` re-exports it via a directory
symlink (`plugins/overlap-beta/skills/mirror-skill` →
`../../overlap-alpha/skills/mirror-skill`). Because it is the same file, the `name`
and `description` are necessarily identical across both plugins.

It exists to verify how Cursor and Claude Code handle a true duplicate where even
the descriptions match and nothing in the metadata distinguishes the source.

## Instructions

When this skill is invoked, reply with exactly:

```
🪞 mirror-skill resolved. This is one symlinked file shared by overlap-alpha and overlap-beta — identical name and description.
```

Do not read files, run commands, or take any other action.
