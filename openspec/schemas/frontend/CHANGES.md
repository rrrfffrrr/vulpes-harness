# Changelog - frontend schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- `data` conditional artifact - the client data layer: per-resource freshness (RFC 9111 + RFC 5861 stale-while-revalidate vocabulary), the invalidation map, optimistic updates with rollback, client retry aligned to the backend error catalog's retryability, and an offline section (stale-if-error reads, write queueing, reconnect reconciliation).
- Error mapping in `screens`: when a backend change exists, the error state maps each applicable problem type from the backend conventions error catalog to screen behavior and exact copy; retryable types keep a retry affordance.
- `overview`'s conditional-artifacts table and the `traceability` gaps list now carry data.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).

### Migration (from 1.1.1)

- Add a `data` row (`Yes/No` + one-line reason) to `overview.md`'s "Conditional artifacts included" table.
- When a backend change exists, add the "Error mapping" table (problem type -> screen behavior -> exact copy) to each screen in `screens.md` that displays backend data.
- If the app manages client-side server-state (caching, optimistic updates, offline), author `data.md` from the new template; otherwise no further rework.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header (this schema is new in 1.1.0 - no migrations yet).

## [1.1.0] - 2026-07-15

### Added

- Initial release: frontend (application UI - web, mobile, desktop) detail-design schema (IFML 1.0, UML 2.5.1 state machines, NN/g wireflows, Atomic Design + Open UI anatomy, five-state UI Stack, WCAG 2.2, DTCG tokens) with 6 artifacts - `overview` -> (`design-tokens`) -> `components` -> `screens` -> `flows` -> `traceability`; `design-tokens` conditional.
