# cursor-plugins-test

A throwaway Cursor plugin marketplace used to test how Cursor handles skills that
**share a name across two installed plugins**. Every skill is a no-op marker — nothing
functional ships here.

## Plugins

| Plugin | Skills |
|---|---|
| `overlap-alpha` | `duplicate-skill` (🅰️ marker), `mirror-skill` (canonical) |
| `overlap-beta`  | `duplicate-skill` (🅱️ marker), `mirror-skill` (symlinked from alpha) |

## The two collision cases

1. **Same name, different descriptions** — `duplicate-skill` exists in both plugins
   with the identical skill name, but each description names its own source plugin
   (`overlap-alpha` vs `overlap-beta`). The source is recoverable from metadata.
2. **Same name, identical descriptions (symlinked)** — `mirror-skill` is a single
   physical file living in `overlap-alpha`; `overlap-beta` re-exports it via a directory
   symlink (`plugins/overlap-beta/skills/mirror-skill` →
   `../../overlap-alpha/skills/mirror-skill`). Both plugins present the exact same name
   **and** description, so nothing in the metadata distinguishes the source.

## Layout

```text
cursor-plugins-test/
├── .cursor-plugin/marketplace.json   # lists both plugins
└── plugins/
    ├── overlap-alpha/
    │   ├── .cursor-plugin/plugin.json
    │   ├── skills/duplicate-skill/SKILL.md
    │   ├── skills/mirror-skill/SKILL.md      # canonical
    │   └── assets/logo.svg
    └── overlap-beta/
        ├── .cursor-plugin/plugin.json
        ├── skills/duplicate-skill/SKILL.md
        ├── skills/mirror-skill -> ../../overlap-alpha/skills/mirror-skill   # symlink
        └── assets/logo.svg
```

## Install in Cursor

Add this repo as a team marketplace (Dashboard → Settings → Plugins → Add Marketplace →
**Import from Repo**), then install both `overlap-alpha` and `overlap-beta`. The point of
the test is to observe how Cursor resolves the two same-named skills — especially the
symlinked `mirror-skill`, whose name and description are identical across both plugins.
