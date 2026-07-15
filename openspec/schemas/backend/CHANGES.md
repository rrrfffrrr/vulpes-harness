# Changelog - backend schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.

## [1.1.0] - Unreleased

### Added

- Initial release: backend detail-design schema (OpenAPI 3.2 + JSON Schema 2020-12, RFC 9110/9457/9111, BCP 14, UML 2.5.1 sequences, C4 Component) with 8 artifacts - `overview` -> `conventions`, `components` -> `endpoints` -> `sequences`, (`events`, `webhooks`) -> `traceability`; `events` and `webhooks` conditional.
