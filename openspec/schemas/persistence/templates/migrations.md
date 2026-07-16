---
schema-version: 1.2.0
document-version: 0
---

# Migration & versioning

<!-- Evolutionary database design - plans and rules, no migration scripts.
     Replace every `<...>` placeholder.
     Delete guidance comments when done. -->

## Policy

- **Versioning & ordering**: `<how migrations are numbered and applied>`
- **Compatibility window**: `<which schema versions must coexist with running code>`

## Breaking changes - expand-contract

<!-- What qualifies as breaking, and the parallel-change rule for shipping it. -->
- `<qualifies as breaking: ...>`
- Expand -> dual-write -> backfill -> cut over reads -> contract: `<project-specific rules per step>`

## Seed / reference data

- `<what ships with the schema and how it is versioned>`

## Backfills

- `<how historical data is transformed - backend jobs.md name when one exists>`
