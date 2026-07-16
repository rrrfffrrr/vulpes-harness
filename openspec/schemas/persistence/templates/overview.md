---
schema-version: 1.2.0
document-version: 0
---

# Persistence overview

<!-- Entry point.
     Store inventory, data domains, reader map.
     Reference architecture data-view/components/ADRs by name/id; do not restate them.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Store inventory

<!-- One row per store. Engine undecided or contested -> OPEN + candidates. -->
| Store | Engine (version intent) | Decided by | Owning components (data-view) |
|-------|-------------------------|------------|-------------------------------|
| `<name>` | `<PostgreSQL 16 / OPEN: MySQL vs PostgreSQL>` | `<ADR-NNN / OPEN>` | `<component names>` |

## Data domains

<!-- Which parts of the requirements object-model this design covers. -->
- `<domain - requirements object ids>`

## Reader map

| Reader | Start with | Then |
|--------|-----------|------|
| DBA | model.md | stores.md |
| Backend engineer | stores.md | migrations.md |
| Ops | migrations.md | traceability.md |
