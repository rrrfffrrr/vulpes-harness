# Data View

<!-- CONDITIONAL — omit if no persistent state. Solution-level schema, not the conceptual
     object-model. Derive entities from planning object-model by name. Honor invariants.
     Replace every <...> and example row. Delete guidance comments when done. -->

## Stakeholders & Concerns

- <roles (e.g. DBA, backend)>. 관심사: <concerns this view frames>

## Logical Data Model

<!-- Entities -> tables/collections with key fields + logical types. -->
| Table | Key fields (logical) | From object-model |
|-------|----------------------|-------------------|
| <table> | <fields> | <entity> |

## Ownership

- <component> → <data it owns>

## Integrity & Relationships

- <keys, relationships, integrity rules>

## Indexing & Partitioning

- <access-pattern-driven indexing/partitioning>

## Retention & Migration

<!-- Honor planning data-minimization/retention invariants. -->
- <retention/deletion policy; migration/versioning approach>
