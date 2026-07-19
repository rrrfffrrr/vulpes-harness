# Persistence schema changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.
`schema-version` records MUST items only; SHOULD items follow the Requirement keywords rule in `openspec/rules/writing.md` - deferrable, never dismissible.
On every migration, re-check every version's SHOULD items - including versions at or below the artifact's `schema-version` - and apply any still due.

## [1.2.1] - 2026-07-19

### Added

- `model.md` field-table Constraints vocabulary gains `identifier`: it marks the entity's identifying field(s) (composite: mark each), distinguishing them from merely-unique fields.
  Foreign-key fields stay out of the logical model - the relationship line owns the link, and its store realization (reference / embed / direction) lives in `stores.md`.

### Changed

- Version lockstep with the 1.2.1 harness release.
- Migration chain rule: SHOULD items follow the new Requirement keywords rule in rules/writing.md (RFC 2119: deferrable, never dismissible) - re-checked on every migration, even for versions already passed.
- Headings drop the `Subject - explainer` dash suffix (rules/writing.md Scannable structure): a qualifier leads, the explanation opens the section body; template titles follow.
- `stores` Units table holds one fact per column (rules/writing.md Tables): `Keys / partition` splits into `Key` (identity) and `Partition` (placement - partition/shard key, `-` where the unit is unpartitioned).
- `stores` Access-patterns table: `Notes` splits into `Cardinality` (result size) and `Frequency` (how often the pattern runs).

### Fixed

- Template comments named the pre-1.2.0 WRITING-STYLE file; they now name `rules/writing.md`.

### Migration (from 1.2.0)

- Replace the change folder's `README.md` and `README.ko.md` with fresh copies of the schema's `templates/README.md` and `templates/README.ko.md`.
- In each entity's field table in `model.md`, add `identifier` to the Constraints of the identifying field(s) (composite: mark each).
- In `stores.md`, split each Units table's `Keys / partition` column into `Key` and `Partition` (`-` where the unit is unpartitioned).
- In `stores.md`, split each Access-patterns table's `Notes` column into `Cardinality` and `Frequency`, moving any other note into prose.
- Delete field rows whose only fact is a foreign-key link the relationship diagram already carries; if such a row held extra facts (e.g. nullability of the link), move them to the entity's Integrity & cascade bullet.
- Recommended (SHOULD): retitle headings that trail a `Subject - explainer` dash suffix - the qualifier leads, the explanation opens the section body (rules/writing.md).

## [1.2.0] - 2026-07-18

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: persistence (data store) detail-design schema (ANSI/SPARC internal level below the architecture data-view, polyglot persistence per Sadalage & Fowler, access-pattern-driven store design, evolutionary database design per Ambler & Sadalage, Chen entity-relationship diagrams with crow's foot cardinality via mermaid erDiagram for the logical model) with 5 artifacts - `overview` -> `model` -> `stores` -> `migrations` -> `traceability`.
- Store blocks are keyed to the engine ADR; an undecided or contested engine is recorded as OPEN with candidates, and the block stays engine-portable.
