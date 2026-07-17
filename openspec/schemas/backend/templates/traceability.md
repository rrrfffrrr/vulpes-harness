---
schema-version: 1.2.0
document-version: 0
---

# Backend traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     One value per cell - repeat the row per additional interface/component/sequence link (WRITING-STYLE tables rule).
     Replace every example row.
     Delete guidance comments when done. -->

## Operation <-> interface <-> component <-> sequence

| Requirements operation | Kind | Interface | Component | Sequence |
|------------------------|------|-----------|-----------|----------|
| `<operation name>` | `<endpoint / channel / webhook / job>` | `<METHOD /path or name>` | `<component>` | `<flow name>` |

## Gaps

- `<operations with no interface; interfaces tracing to no operation; components no flow exercises; multi-component state-changing interfaces no sequence shows; conditional artifacts excluded (overview's reason)>`
