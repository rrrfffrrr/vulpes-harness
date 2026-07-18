# Changelog - persistence schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: persistence (data store) detail-design schema (ANSI/SPARC internal level below the architecture data-view, polyglot persistence per Sadalage & Fowler, access-pattern-driven store design, evolutionary database design per Ambler & Sadalage, Chen entity-relationship diagrams with crow's foot cardinality via mermaid erDiagram for the logical model) with 5 artifacts - `overview` -> `model` -> `stores` -> `migrations` -> `traceability`.
- Store blocks are keyed to the engine ADR; an undecided or contested engine is recorded as OPEN with candidates, and the block stays engine-portable.
