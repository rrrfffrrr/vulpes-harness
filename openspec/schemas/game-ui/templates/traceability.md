---
schema-version: 1.2.0
document-version: 0
---

# Game UI traceability matrix

<!-- All cross-artifact linking lives here, not in artifact prose.
     Include the Endpoint column only when a backend change exists.
     Replace every example row.
     Delete guidance comments when done. -->

## GDD / requirement <-> screen / hud element <-> flow <-> widget <-> input <-> settings

| GDD section / requirement | Screen / hud element | Flow | Widgets | Input context | Settings options | Endpoint (backend) |
|---------------------------|----------------------|------|---------|---------------|------------------|---------------------|
| `<id / name>` | `<screen or element>` | `<flow>` | `<widgets>` | `<context>` | `<options>` | `<METHOD path or ->` |

## Gaps

- `<GDD/requirements items with no screen or hud element; screens no flow reaches; widgets nothing uses; hud elements missing an expected settings hook; conditional artifacts/sections excluded (overview's reason)>`
