# How to read these artifacts - game-ui

[English](README.md) | [한국어](README.ko.md)

**game-ui** schema (UI-layer taxonomy + safe areas/legibility floors + action-based input + Game Accessibility Guidelines/XAG + UML state machines + wireflows) artifacts - the implementable game-UI spec for PC, console, mobile, and handheld games, one level below architecture and the GDD.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - the system-wide UI vocabulary (UI layers, safe area & scale, legibility floors, widget states, localization budgets, accessibility target) and the reader map.

**Reading order:**

1. `overview.md` - platforms & devices / UI layers / safe area & scale / legibility / widget-state enum / localization / accessibility target / reader map
2. `design-tokens.md` - color / typography with fallbacks / dimension / motion / themes as tokens *(if present)*
3. `widgets.md` - shared widgets: anatomy, variants, states, per-device input behavior, text budgets
4. `screens.md` - per screen & modal: layout + safe area, screen states, data, per-device operation
5. `hud.md` - per HUD element: UI layer, placement, visibility, customization hooks, feedback channels *(+ subtitles section if present)*
6. `flows.md` - boot flow, navigation map, modal & pause conventions, statecharts; splits into `flows/<domain>.md` when it outgrows one sitting (the file stays as the index)
7. `input.md` - per-context action sets, bindings per device, glyphs, remapping, hot-swap
8. `settings.md` - the option inventory: type/range/default/effect/accessibility mapping per option
9. `traceability.md` - GDD/requirement <-> screen/hud <-> flow <-> widget <-> input <-> settings matrix

*design-tokens exists only when styling is token-based; the subtitles section only when the game has speech or important audio.*

---

Workflow: **require -> gdd -> architect -> game-ui -> propose -> apply**
Status: `openspec status --change <name>`
