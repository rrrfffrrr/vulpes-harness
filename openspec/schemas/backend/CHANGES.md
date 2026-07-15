# Changelog - backend schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema) - no changes to this schema's artifacts; no migration needed.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header (this schema is new in 1.1.0 - no migrations yet).

## [1.1.0] - 2026-07-15

### Added

- Initial release: backend detail-design schema (OpenAPI 3.2 + JSON Schema 2020-12, RFC 9110/9457/9111, BCP 14, UML 2.5.1 sequences, C4 Component) with 8 artifacts - `overview` -> `conventions`, `components` -> `endpoints` -> `sequences`, (`events`, `webhooks`) -> `traceability`; `events` and `webhooks` conditional.
