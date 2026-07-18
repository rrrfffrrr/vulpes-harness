# Changelog - verification schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: acceptance & verification design schema (ISTQB test-basis vocabulary, ISO/IEC/IEEE 29119-3 dynamic-level documentation types, Specification by Example + Gherkin, BABOK 10.1 acceptance criteria realized from the requirements operation-model) with 4 artifacts - `overview` -> `scenarios` -> `environment` -> `traceability`.
- Thin-by-design rule: per-contract test cases are derived from the detail-design contracts (29119-4 techniques) and are never written in these artifacts.
