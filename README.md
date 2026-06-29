# cursor-plugins-test

A throwaway marketplace that tests how **Cursor** and **Claude Code** handle a single
skill (`mirror-skill`) shared across two plugins — using a different dedup mechanism per
ecosystem. Every skill is a no-op marker; nothing functional ships here.

## Plugins

| Plugin | Ships | Reuses |
|---|---|---|
| `overlap-alpha` | canonical `mirror-skill` | — |
| `overlap-beta`  | nothing of its own | `mirror-skill` from overlap-alpha |

## How `mirror-skill` is shared (two mechanisms)

`mirror-skill` is defined once, in `overlap-alpha`. `overlap-beta` reuses it differently
per ecosystem:

- **Cursor — filesystem symlink.** Cursor has no plugin-dependency feature, so
  overlap-beta exposes the skill via a symlink to alpha's copy. The symlink lives in a
  **custom `cursor-skills/` path** (not `skills/`), and overlap-beta's
  `.cursor-plugin/plugin.json` points at it with `"skills": ["./cursor-skills/mirror-skill"]`.
- **Claude Code — plugin dependency.** overlap-beta ships **no** `skills/` directory and
  declares `"dependencies": ["overlap-alpha"]` in `.claude-plugin/plugin.json`. Installing
  overlap-beta auto-installs overlap-alpha, and the skill is addressed as
  `overlap-alpha:mirror-skill`. No duplicate is loaded.

### Why the custom `cursor-skills/` path?

Claude **always** scans a plugin's `skills/` directory and offers no way to exclude a
skill. If the symlink lived at `overlap-beta/skills/mirror-skill`, Claude would load it as
`overlap-beta:mirror-skill` and defeat the dependency dedup. Putting the symlink in
`cursor-skills/` keeps it invisible to Claude's `skills/` scan while Cursor picks it up via
the explicit `skills` manifest path.

## Layout

```text
cursor-plugins-test/
├── .cursor-plugin/marketplace.json
├── .claude-plugin/marketplace.json
└── plugins/
    ├── overlap-alpha/
    │   ├── .cursor-plugin/plugin.json
    │   ├── .claude-plugin/plugin.json
    │   ├── skills/mirror-skill/SKILL.md      # canonical, scanned by both ecosystems
    │   └── assets/logo.svg
    └── overlap-beta/
        ├── .cursor-plugin/plugin.json        # "skills": ["./cursor-skills/mirror-skill"]
        ├── .claude-plugin/plugin.json        # "dependencies": ["overlap-alpha"], no skills/
        ├── cursor-skills/mirror-skill -> ../../overlap-alpha/skills/mirror-skill
        └── assets/logo.svg
```

## Install

**Cursor:** Dashboard → Settings → Plugins → Add Marketplace → Import from Repo, then
install both plugins.

**Claude Code:**
```
/plugin marketplace add /Users/sherif/code/sherifabdlnaby/cursor-plugins-test
/plugin install overlap-beta@cursor-plugins-test   # auto-pulls overlap-alpha
```

Observe how each ecosystem resolves the shared `mirror-skill`.
