---
schema-version: 1.2.1
document-version: 0
---

# Evaluation design

<!-- Pass/fail release gates per model; named datasets and slices.
     A model version that misses a gate does not ship.
     Replace every `<...>` placeholder and example row; repeat the model block per model.
     Delete guidance comments when done. -->

## `<Model name>`

### Release gates

| Metric | Threshold (gate) | Eval dataset | Slices measured |
|--------|------------------|--------------|-----------------|
| `<metric>` | `<pass/fail threshold>` | `<named dataset>` | `<subgroups/conditions>` |

### Regression policy

- `<what a new version must not regress vs the shipping version - named slices, named metrics>`

### Monitoring signals

- `<drift/quality indicator watched in production + paging threshold; reference architecture observability conventions>`
