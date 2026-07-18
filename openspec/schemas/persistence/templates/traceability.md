---
schema-version: 1.2.0
document-version: 0
---

# Persistence traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     One value per cell - repeat the row per additional store/pattern link (rules/writing.md tables rule).
     Replace every example row.
     Delete guidance comments when done. -->

## Object <-> entity <-> store <-> access pattern

| Requirements object / invariant | Entity (model.md) | Store / native unit | Access pattern |
|---------------------------------|-------------------|---------------------|----------------|
| `<id>` | `<entity>` | `<store: unit>` | `<pattern>` |

## Gaps

- `<entities with no store; structures serving no access pattern; retention invariants without an enforcing mechanism; stores whose engine is OPEN (what the pending decision blocks)>`
