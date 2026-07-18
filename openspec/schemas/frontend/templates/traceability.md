---
schema-version: 1.2.0
document-version: 0
---

# Frontend traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     Include the Endpoint column only when a backend change exists.
     One value per cell - repeat the row per additional component/endpoint link (rules/writing.md tables rule).
     Replace every example row.
     Delete guidance comments when done. -->

## Requirement <-> screen <-> flow <-> component

| Requirement (goal / operation) | Screen | Flow | Component | Endpoint (backend) |
|--------------------------------|--------|------|-----------|---------------------|
| `<id / name>` | `<screen>` | `<flow>` | `<component>` | `<METHOD /path or ->` |

## Gaps

- `<requirements with no screen; screens no flow reaches; components no screen uses; data.md resources no screen displays (when data exists); conditional artifacts excluded (overview's reason)>`
