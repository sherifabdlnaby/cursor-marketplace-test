# Overlap Beta — skill collision test

Test plugin **B** of a pair (`overlap-alpha` + `overlap-beta`) used to exercise how
Cursor handles skills that share a name across plugins. No-op markers only.

| Skill | Behavior |
|---|---|
| `duplicate-skill` | replies with the **🅱️ beta** marker; description names overlap-beta as source |
| `mirror-skill` | replies with the **🪞 mirror** marker; a symlink to overlap-alpha's canonical copy (identical name and description) |

`skills/mirror-skill` here is a directory symlink → `../../overlap-alpha/skills/mirror-skill`.
See the repo root README for the full description of the two collision cases.
