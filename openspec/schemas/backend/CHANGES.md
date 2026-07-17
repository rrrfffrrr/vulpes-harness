# Changelog - backend schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- `jobs` conditional artifact - contracts for time-triggered/background work outside the request/event surface: trigger (POSIX cron vocabulary), run identity (Spring Batch JobInstance semantics), overlap policy (Kubernetes CronJob terms), restart/rerun (Jakarta Batch), input scope, effects vs event publish, failure, backfill.
- `overview`'s conditional-artifacts table, the `sequences` critical-path list, and the `traceability` interface column now carry jobs.

- `configuration` conditional artifact - the named catalog of config keys and feature flags (12-factor III): name, type, default, reading component, effect; flag lifecycle; secrets by name only. Per-environment values stay with ops.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).
- `sequences` is scoped to the backend boundary: lifelines are components.md components plus stores/brokers, and the client is at most one boundary lifeline.
  Client-side behavior (screen logic, client cache, UI retries) moves to the frontend schema's `flows` "API call sequences" section - sequence diagrams are a per-schema expression tool, not a single-home artifact.
- Tables follow the new WRITING-STYLE one-value-per-cell rule (first normal form): `traceability` splits the overloaded interface column into Kind + Interface (the Interface cell holds only `METHOD /path` or a name - no bracketed annotations), Component is singular, and rows repeat per link; the `conventions` error catalog splits Retryable into Retryable + Backoff.
- `sequences` coverage is exhaustive by construction (trigger closure - event partitioning applied to the interface catalogs): every state-changing trigger (unsafe endpoint, consumed channel, job) is shown in a flow or explicitly single-component; every outbound effect appears in its trigger's flow; `traceability` gains the matching gap (multi-component state-changing interfaces no sequence shows).

### Migration (from 1.1.1)

- Add `jobs` and `configuration` rows (`Yes/No` + one-line reason) to `overview.md`'s "Conditional artifacts included" table.
- If `sequences.md` diagrams client-side behavior (screen logic, client cache, UI retries), move those parts to the frontend change's `flows.md` "API call sequences" section and keep the client as a single boundary lifeline here.
- Re-shape `traceability.md`: add the Kind column, strip everything but `METHOD /path`/the name from the Interface cell, make Component singular, and repeat rows per link.
- Audit `sequences.md` against trigger closure: walk endpoints/events/jobs item by item, add flows for uncovered multi-component state-changing triggers (or mark them single-component), and list remaining holes in the traceability gaps.
- Split the `conventions.md` error-catalog Retryable column into Retryable (`yes/no`) + Backoff.
- If the system runs time-triggered or background work outside its request/event surface, author `jobs.md` from the new template and add those jobs to the `traceability.md` interface column; otherwise no further rework.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header (this schema is new in 1.1.0 - no migrations yet).

## [1.1.0] - 2026-07-15

### Added

- Initial release: backend detail-design schema (OpenAPI 3.2 + JSON Schema 2020-12, RFC 9110/9457/9111, BCP 14, UML 2.5.1 sequences, C4 Component) with 8 artifacts - `overview` -> `conventions`, `components` -> `endpoints` -> `sequences`, (`events`, `webhooks`) -> `traceability`; `events` and `webhooks` conditional.
