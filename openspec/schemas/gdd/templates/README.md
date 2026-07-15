# How to read these artifacts - gdd

[English](README.md) | [한국어](README.ko.md)

**gdd** schema (Game Design Document) artifacts - how the intended game plays, looks, sounds, and ships. A living document; no implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - get the whole picture, then jump to the section you need.

**Reading order:**

1. `overview.md` - framing (genre / platform / pillars / USPs / MVP scope)
2. `gameplay.md` - core loop / states / win-lose
3. `mechanics.md` - systems / progression / economy
4. `world-narrative.md` - setting / characters / content structure *(if present)*
5. `art-direction.md` - visual direction
6. `audio-direction.md` - audio direction
7. `ux-ui.md` - screen flow / controls / accessibility
8. `tech.md` - engine / platforms / performance / save
9. `monetization.md` - business model / monetization *(if present)*
10. `production.md` - market / MoSCoW features / milestones (synthesis)

*world-narrative and monetization exist only when the game has that concern.*

---

Workflow: **require -> gdd -> propose -> apply**
Status: `openspec status --change <name>`
