# Changelog - architecture schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.
`schema-version` records MUST items only; a SHOULD item stays due until its effect is in the document or a weighed skip is recorded ([RFC 2119](https://www.rfc-editor.org/rfc/rfc2119)).
On every migration, re-check every version's SHOULD items - including versions at or below the artifact's `schema-version` - and apply any still due.

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.

### Changed

- Migration chain rule: a SHOULD item stays due until applied or a weighed skip is recorded (RFC 2119) - re-checked on every migration, even for versions already passed.
- `ml-serving-view` demarcation against the new `ml` detail schema: the view keeps the model lifecycle APPROACH (versioning/update/rollback intent); concrete procedures and release gates live in the ml detail schema when one exists. Existing documents stay valid at architecture altitude - no migration needed.
- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).
- Tables follow the new rules/writing.md one-value-per-cell rule (first normal form): `traceability` uses singular View/ADR columns with one row per link and a role-coverage row per role-view pair; the `logical-view` interface table splits Inputs -> Outputs into Inputs + Outputs with a singular Consumer column; the `overview` reader map splits Views to read into Start with + Then.
- Rules documents moved into `openspec/rules/`: prose rules are now `rules/writing.md` (was `openspec/WRITING-STYLE.md`), diagram rules `rules/diagrams.md` (was `openspec/DIAGRAM-STYLE.md`); schema and template references updated.

### Migration (from 1.1.1)

- Re-shape `traceability.md` (singular View/ADR, one row per link; role coverage one row per role-view pair - drop the Covered? column, uncovered roles go to Gaps), the `logical-view.md` interface table (Consumer singular with one row per consumer; separate Inputs and Outputs columns), and the `overview.md` reader map (Views to read splits into Start with + Then).

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header and a Migration section under 1.1.0.

## [1.1.0] - 2026-07-15

### Added

- `schema-version` / `document-version` frontmatter on every template - artifacts now record the schema semver they were authored against and a per-document revision counter.
- Korean reading guide `templates/README.ko.md`; both guides carry an English/Korean switcher link.
- Authoring principle: prose follows the new `openspec/WRITING-STYLE.md` - semantic line breaks, plain language, scannable structure, consistent terminology, findability, ISO 8601 dates.

### Changed

- Artifact renames (the change folder already namespaces them): `architecture-overview` -> `overview`, `design-traceability` -> `traceability`.
  Rework documents authored against 1.0.0 by renaming the two files; content structure is unchanged.
- Reading guide moved from `change-README.md` to `templates/README.md` (copied into the change folder name-preserving, alongside `README.ko.md`).

### Migration (from 1.0.0)

1. Rename `architecture-overview.md` to `overview.md` and `design-traceability.md` to `traceability.md` in the change folder.
   Until renamed, `openspec status` reports `overview` and `traceability` as missing - do not create duplicates.
2. Add the version frontmatter to every artifact in the change: `schema-version: 1.1.0`, `document-version: 0`.
3. Replace the change folder's `README.md` with a copy of the schema's `templates/README.md`, and copy `templates/README.ko.md` to `README.ko.md`.
4. Recommended (SHOULD, not MUST): reflow artifact prose to `openspec/WRITING-STYLE.md` (now `openspec/rules/writing.md`).

## [1.0.0] - 2026-06-22

### Added

- Initial release: 4+1 / arc42 / ISO 42010 / ADR architecture schema with 9 artifacts - `architecture-overview` -> `logical-view` -> (`process-view`, `data-view`, `ml-serving-view`) -> `deployment-view` -> `crosscutting-concepts` -> `adr` -> `design-traceability`; process/data/ml-serving views conditional.
