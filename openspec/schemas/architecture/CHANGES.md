# Changelog - architecture schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.

## [1.1.0] - Unreleased

### Added

- `schema-version` / `document-version` frontmatter on every template - artifacts now record the schema semver they were authored against and a per-document revision counter.
- Korean reading guide `templates/README.ko.md`; both guides carry an English/Korean switcher link.

### Changed

- Artifact renames (the change folder already namespaces them): `architecture-overview` -> `overview`, `design-traceability` -> `traceability`. Rework documents authored against 1.0.0 by renaming the two files; content structure is unchanged.
- Reading guide moved from `change-README.md` to `templates/README.md` (copied into the change folder name-preserving, alongside `README.ko.md`).

## [1.0.0] - 2026-06-22

### Added

- Initial release: 4+1 / arc42 / ISO 42010 / ADR architecture schema with 9 artifacts - `architecture-overview` -> `logical-view` -> (`process-view`, `data-view`, `ml-serving-view`) -> `deployment-view` -> `crosscutting-concepts` -> `adr` -> `design-traceability`; process/data/ml-serving views conditional.
