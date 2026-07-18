---
schema-version: 1.2.1
document-version: 0
---

# Data view

<!-- CONDITIONAL - omit if no persistent state.
     Solution-level schema, not the conceptual object-model.
     Derive entities from requirements object-model by name.
     Honor invariants.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Stakeholders & concerns

- `<roles (e.g. DBA, backend)>`. Concerns: `<concerns this view frames>`

## Logical data model

<!-- Entities -> tables/collections with key fields + logical types. -->
| Table | Key fields (logical) | From object-model |
|-------|----------------------|-------------------|
| `<table>` | `<fields>` | `<entity>` |

## Ownership

- `<component>` -> `<data it owns>`

## Integrity & relationships

- `<keys, relationships, integrity rules>`

## Indexing & partitioning

- `<access-pattern-driven indexing/partitioning>`

## Retention & migration

<!-- Honor requirements data-minimization/retention invariants. -->
- `<retention/deletion policy; migration/versioning approach>`
