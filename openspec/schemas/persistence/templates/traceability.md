---
schema-version: 1.2.0
document-version: 0
---

# Persistence traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     Replace every example row.
     Delete guidance comments when done. -->

## Object <-> entity <-> store <-> access pattern

| Requirements object / invariant | Entity (model.md) | Store / native unit | Access patterns |
|---------------------------------|-------------------|---------------------|-----------------|
| `<id>` | `<entity>` | `<store: unit>` | `<patterns>` |

## Gaps

- `<entities with no store; structures serving no access pattern; retention invariants without an enforcing mechanism; stores whose engine is OPEN (what the pending decision blocks)>`
