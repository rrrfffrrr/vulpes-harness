---
schema-version: 1.2.0
document-version: 0
---

# ML traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     Include the dataset column only when data.md exists.
     Replace every example row.
     Delete guidance comments when done. -->

## Operation <-> model <-> surfaces <-> gates

| Requirements operation | Model | Consumed by | Release gates | Dataset |
|------------------------|-------|-------------|---------------|---------|
| `<operation name>` | `<model>` | `<METHOD path / screen / job>` | `<gate names>` | `<dataset or ->` |

## Gaps

- `<models without release gates; models no surface consumes; operations whose inference step has no model; conditional artifacts excluded (overview's reason)>`
