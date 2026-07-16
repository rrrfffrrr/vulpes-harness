---
schema-version: 1.2.0
document-version: 0
---

# Logical data model (detail)

<!-- Store-agnostic. Deepens architecture data-view entities to full field level.
     Logical types only - store-native mapping lives in stores.md.
     Replace every `<...>` placeholder and example row; repeat the entity block per entity.
     Delete guidance comments when done. -->

## `<Entity name>`

(data-view: `<entity>`; traces to: requirements object `<id>`)

| Field | Type (logical) | Constraints | Null |
|-------|----------------|-------------|------|
| `<field>` | `<string / integer / decimal / timestamp / ...>` | `<unique / range / format / ...>` | `<yes/no>` |

- **Relationships**: `<entity -> entity, cardinality, cascade intent>`
- **Retention & PII**: `<class + retention window>` (invariant `<id>`)
