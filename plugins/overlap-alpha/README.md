# Overlap Alpha — skill reuse test

Test plugin **A** of a pair (`overlap-alpha` + `overlap-beta`). Ships the **canonical**
`mirror-skill`; `overlap-beta` reuses it (symlink in Cursor, dependency in Claude). No-op
marker only.

| Skill | Behavior |
|---|---|
| `mirror-skill` | replies with the **🪞 mirror** marker; addressed as `overlap-alpha:mirror-skill` in Claude |

See the repo root README for how the skill is shared across both plugins.
