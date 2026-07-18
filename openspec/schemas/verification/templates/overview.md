---
schema-version: 1.2.0
document-version: 0
---

# Verification overview

<!-- Entry point.
     Test basis, scope, out of scope, reader map.
     Reference changes/artifacts by name; do not restate their content.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Test basis

<!-- ISTQB sense: the documents test design builds on. -->
| Change | Artifacts used |
|--------|----------------|
| `<{program}-requirements>` | operation-model (acceptance criteria) |
| `<{program}-backend / -frontend / -persistence / -game-ui / -ml, as present>` | `<artifacts>` |

## Scope

- Operations covered: `<requirements operation names>`

## Out of scope

- Derived per-contract test cases - generated from the detail-design contracts (29119-4 techniques), not designed here.
- Performance/SLO verification - targets live in the architecture crosscutting-concepts.
- `<project-specific exclusions>`

## Reader map

| Reader | Start with | Then |
|--------|-----------|------|
| QA | scenarios/index.md | environment.md |
| Engineer | scenarios/index.md | traceability.md |
| Product | traceability.md | scenarios/index.md |
