# Changelog - backend schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- `jobs` conditional artifact - contracts for time-triggered/background work outside the request/event surface: trigger (POSIX cron vocabulary), run identity (Spring Batch JobInstance semantics), overlap policy (Kubernetes CronJob terms), restart/rerun (Jakarta Batch), input scope, effects vs event publish, failure, backfill.
- `overview`'s conditional-artifacts table, the `sequences` critical-path list, and the `traceability` interface column now carry jobs.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).

### Migration (from 1.1.1)

- Add a `jobs` row (`Yes/No` + one-line reason) to `overview.md`'s "Conditional artifacts included" table.
- If the system runs time-triggered or background work outside its request/event surface, author `jobs.md` from the new template and add those jobs to the `traceability.md` interface column; otherwise no further rework.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header (this schema is new in 1.1.0 - no migrations yet).

## [1.1.0] - 2026-07-15

### Added

- Initial release: backend detail-design schema (OpenAPI 3.2 + JSON Schema 2020-12, RFC 9110/9457/9111, BCP 14, UML 2.5.1 sequences, C4 Component) with 8 artifacts - `overview` -> `conventions`, `components` -> `endpoints` -> `sequences`, (`events`, `webhooks`) -> `traceability`; `events` and `webhooks` conditional.
