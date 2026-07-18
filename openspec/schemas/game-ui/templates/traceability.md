---
schema-version: 1.2.0
document-version: 0
---

# Game UI traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     Include the Endpoint column only when a backend change exists.
     One value per cell - repeat the row per additional widget/option/endpoint link (WRITING-STYLE tables rule).
     Replace every example row.
     Delete guidance comments when done. -->

## GDD / requirement <-> screen / hud element <-> flow <-> widget <-> input <-> settings

| GDD section / requirement | Screen / hud element | Flow | Widget | Input context | Settings option | Endpoint (backend) |
|---------------------------|----------------------|------|--------|---------------|-----------------|---------------------|
| `<id / name>` | `<screen or element>` | `<flow>` | `<widget>` | `<context>` | `<option>` | `<METHOD /path or ->` |

## Gaps

- `<GDD/requirements items with no screen or hud element; screens no flow reaches; widgets nothing uses; hud elements missing an expected settings hook; conditional artifacts/sections excluded (overview's reason)>`
