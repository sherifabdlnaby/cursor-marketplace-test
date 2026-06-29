# Overlap Beta — skill reuse test

Test plugin **B** of a pair (`overlap-alpha` + `overlap-beta`). It ships **no skill of its
own** and reuses `mirror-skill` from `overlap-alpha`, via a different mechanism per
ecosystem. No-op markers only.

| Ecosystem | Mechanism |
|---|---|
| Cursor | symlink `cursor-skills/mirror-skill` → `../../overlap-alpha/skills/mirror-skill`, surfaced by `"skills": ["./cursor-skills/mirror-skill"]` |
| Claude Code | `"dependencies": ["overlap-alpha"]` — installing this plugin auto-installs overlap-alpha; skill is `overlap-alpha:mirror-skill` |

The symlink is deliberately kept out of `skills/` so Claude's mandatory `skills/` scan
doesn't load a duplicate. See the repo root README for the full rationale.
