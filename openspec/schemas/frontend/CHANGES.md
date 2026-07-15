# Changelog - frontend schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header (this schema is new in 1.1.0 - no migrations yet).

## [1.1.0] - 2026-07-15

### Added

- Initial release: frontend (application UI - web, mobile, desktop) detail-design schema (IFML 1.0, UML 2.5.1 state machines, NN/g wireflows, Atomic Design + Open UI anatomy, five-state UI Stack, WCAG 2.2, DTCG tokens) with 6 artifacts - `overview` -> (`design-tokens`) -> `components` -> `screens` -> `flows` -> `traceability`; `design-tokens` conditional.
