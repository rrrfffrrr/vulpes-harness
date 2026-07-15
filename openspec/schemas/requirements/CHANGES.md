# Changelog - requirements schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.

## [1.1.0] - Unreleased

### Added

- `schema-version` / `document-version` frontmatter on every template - artifacts now record the schema semver they were authored against and a per-document revision counter.
- Korean reading guide `templates/README.ko.md`; both guides carry an English/Korean switcher link.
- Authoring principle: prose follows the new `openspec/WRITING-STYLE.md` - semantic line breaks, plain language, scannable structure, consistent terminology, findability, ISO 8601 dates.

### Changed

- Reading guide moved from `change-README.md` to `templates/README.md` (copied into the change folder name-preserving, alongside `README.ko.md`).

## [1.0.0] - 2026-06-22

### Added

- Initial release: KAOS/GORE + BABOK requirements schema with 7 artifacts - `business-requirements` -> `goal-model` -> `object-model`, `responsibility-model` -> `operation-model` -> `requirements-document` -> `traceability`.
