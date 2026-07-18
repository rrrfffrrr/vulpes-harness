---
schema-version: 1.2.1
document-version: 0
---

# Model contracts

<!-- Model Cards at design altitude. One block per model.
     Inference-location invariant - never fork a contract per location.
     LLM prompt templates are project assets referenced by name only.
     Replace every `<...>` placeholder and example row; repeat the model block per model.
     Delete guidance comments when done. -->

## `<Model name>`

- **Intended use**: `<what it is for>`
- **Out-of-scope use**: `<what it must not be used for>`

### I/O contract

**Input**

| Field | Type | Constraints | Required |
|-------|------|-------------|----------|
| `<field>` | `<type>` | `<range/format>` | `<yes/no>` |

**Output**

| Field | Type | Semantics |
|-------|------|-----------|
| `<field / score>` | `<type>` | `<what the value means; what consumers may compare it against>` |

### Quality targets

- `<latency / memory / throughput - reference the ml-serving-view targets, do not restate>`

### Degradation & fallback

- Unavailable: `<fallback model / cached result / rule-based default / feature off + what the consumer observes>`
- Timeout: `<behavior + budget reference>`
- Low confidence: `<threshold + behavior>`

### Caveats

- `<known failure modes; factors (input subgroups, conditions) where quality varies>`
