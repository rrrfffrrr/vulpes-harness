# Verification schema changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.
`schema-version` records MUST items only; SHOULD items follow the Requirement keywords rule in `openspec/rules/writing.md` - deferrable, never dismissible.
On every migration, re-check every version's SHOULD items - including versions at or below the artifact's `schema-version` - and apply any still due.

## [1.2.1] - 2026-07-19

### Changed

- Version lockstep with the 1.2.1 harness release.
- Migration chain rule: SHOULD items follow the new Requirement keywords rule in rules/writing.md (RFC 2119: deferrable, never dismissible) - re-checked on every migration, even for versions already passed.
- Headings drop the `Subject - explainer` dash suffix (rules/writing.md Scannable structure): a qualifier leads, the explanation opens the section body; template titles follow.
- `scenarios` is domain-split like the requirements scenarios: `scenarios/index.md` (domain index) + per-domain `scenarios/<domain>.md` (was single-file `scenarios.md`); domains mirror the requirements scenarios domains.
- `environment` test data requirements table holds one fact per column (rules/writing.md Tables): `Data set / state` splits into `Data set` (records that must exist) and `State` (condition those records are in); `Notes` becomes `Resetting` (how runs stay isolated).
- `environment` test environment requirements: the `Real vs stubbed` item splits into `Real components` and `Stubbed systems`, one fact per item.

### Fixed

- Template comments named the pre-1.2.0 WRITING-STYLE file; they now name `rules/writing.md`.

### Migration (from 1.2.0)

- Convert `scenarios.md` to the folder form: create `scenarios/index.md` (Domain | File | Scope) and move every scenario into its domain's `scenarios/<domain>.md`.
- In `environment.md`, split the test-data table's `Data set / state` column into `Data set` and `State`, and rename `Notes` to `Resetting`, keeping only reset/isolation facts there (move anything else into prose or its own column).
- In `environment.md`, split the `Real vs stubbed` item into `Real components` and `Stubbed systems`.
- Replace the change folder's `README.md` and `README.ko.md` with fresh copies of the schema's `templates/README.md` and `templates/README.ko.md`.
- Recommended (SHOULD): retitle headings that trail a `Subject - explainer` dash suffix - the qualifier leads, the explanation opens the section body (rules/writing.md).

## [1.2.0] - 2026-07-18

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: acceptance & verification design schema (ISTQB test-basis vocabulary, ISO/IEC/IEEE 29119-3 dynamic-level documentation types, Specification by Example + Gherkin, BABOK 10.1 acceptance criteria realized from the requirements operation-model) with 4 artifacts - `overview` -> `scenarios` -> `environment` -> `traceability`.
- Thin-by-design rule: per-contract test cases are derived from the detail-design contracts (29119-4 techniques) and are never written in these artifacts.
