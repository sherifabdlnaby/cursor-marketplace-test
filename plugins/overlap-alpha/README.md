# Overlap Alpha — skill collision test

Test plugin **A** of a pair (`overlap-alpha` + `overlap-beta`) used to exercise how
Cursor handles skills that share a name across plugins. No-op markers only.

| Skill | Behavior |
|---|---|
| `duplicate-skill` | replies with the **🅰️ alpha** marker; description names overlap-alpha as source |
| `mirror-skill` | replies with the **🪞 mirror** marker; canonical copy that overlap-beta symlinks to |

See the repo root README for the full description of the two collision cases.
