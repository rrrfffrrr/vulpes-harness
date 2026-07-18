# How to read these artifacts - frontend

[English](README.md) | [한국어](README.ko.md)

**frontend** schema (IFML + UML state machines + wireflows + Atomic Design/Open UI anatomy + UI Stack + WCAG 2.2) artifacts - the implementable UI spec for web, mobile, and desktop apps, one level below architecture.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - the system-wide UI vocabulary (breakpoints, interaction states, accessibility target) and the reader map.

**Reading order:**

1. `overview.md` - platforms / breakpoints / interaction-state enum / accessibility target / reader map
2. `design-tokens.md` - color / typography / dimension / motion / themes as tokens *(if present)*
3. `components.md` - shared components: anatomy, variants, states, behavior, content rules
4. `screens.md` - per screen: layout + breakpoint behavior, the five UI Stack states, data, forms with exact error copy
5. `data.md` - client data layer: freshness, invalidation map, optimistic updates, offline *(if present)*
6. `flows/index.md` - domain index; `flows/<domain>.md` - navigation map, event->transition tables, API call sequences, statecharts for complex interactions
7. `traceability.md` - requirement <-> screen <-> flow <-> component matrix

*design-tokens exists only when styling is token-based; data only when the app manages client-side server-state.*

---

Workflow: **require -> architect -> frontend -> propose -> apply**
Status: `openspec status --change <name>`
