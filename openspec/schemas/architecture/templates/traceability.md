---
schema-version: 1.2.1
document-version: 0
---

# Design traceability matrix

<!-- BABOK RTM for the requirements->architecture link.
     All design linking lives here, not in view prose.
     One value per cell - repeat the row per additional view/ADR link (rules/writing.md tables rule).
     Replace every example row.
     Delete guidance comments when done. -->

## Requirements -> architecture component

| Requirements (goal / operation / agent id) | Architecture component (logical-view) | View | ADR |
|--------------------------------------------|---------------------------------------|------|-----|
| `<requirements id>` | `<component>` | `<view>` | `<ADR-NNN>` |

## Role coverage

<!-- Every role in the overview view map has at least one view to read.
     One row per role-view pair; roles with no view to read go to Gaps. -->
| Role | View read |
|------|-----------|
| `<role>` | `<view>` |

## Gaps

- `<requirements operations with no architecture component; uncovered stakeholders; ADRs still 'proposed'>`
