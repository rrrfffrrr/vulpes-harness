---
schema-version: 1.2.1
document-version: 0
---

# ML overview

<!-- Entry point.
     Model inventory, reader map, conditional artifacts.
     Reference the ml-serving-view/components/ADRs by name/id; do not restate them.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Model inventory

| Model | Task (one line) | Inference location (ml-serving-view) | Consumed by |
|-------|-----------------|----------------------------------------|-------------|
| `<name>` | `<classify / rank / generate / ...>` | `<server / on-device / edge>` | `<METHOD /path / screen / job name>` |

## Reader map

| Reader | Start with | Then |
|--------|-----------|------|
| ML engineer | models.md | evaluation.md |
| Backend engineer | models.md | lifecycle.md |
| QA | evaluation.md | traceability.md |

## Conditional artifacts included

| Artifact | Included? | Reason |
|----------|-----------|--------|
| data | `<Yes/No>` | `<owned training data vs third-party/pretrained>` |
