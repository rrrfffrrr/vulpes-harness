---
schema-version: 1.2.0
document-version: 0
---

# Object model

<!-- The conceptual structure the goals refer to.
     Conceptual / requirements-level (what exists + its rules),
     not solution design or a database schema.
     Replace every `<...>` placeholder, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Objects (entities)

- **`<Entity>`** - `<what it represents>`

## Relationships

<!-- Cardinality lives ONLY here. -->
- `<Entity A>` **`<cardinality>`** `<Entity B>` - `<relationship meaning>`

## Attributes

- **`<Entity>`**: `<attribute - meaning>`, `<attribute - meaning>`

## Invariants

<!-- Rules that must always hold and are NOT expressible as a cardinality. -->
- INV1: `<rule that must always hold>`

## Glossary

- **`<term>`**: `<definition>`
