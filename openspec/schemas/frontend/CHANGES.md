# Frontend schema changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.
`schema-version` records MUST items only; SHOULD items follow the Requirement keywords rule in `openspec/rules/writing.md` - deferrable, never dismissible.
On every migration, re-check every version's SHOULD items - including versions at or below the artifact's `schema-version` - and apply any still due.

## [1.2.1] - Unreleased

### Changed

- Version lockstep with the 1.2.1 harness release.
- Migration chain rule: SHOULD items follow the new Requirement keywords rule in rules/writing.md (RFC 2119: deferrable, never dismissible) - re-checked on every migration, even for versions already passed.
- Headings drop the `Subject - explainer` dash suffix (rules/writing.md Scannable structure): a qualifier leads, the explanation opens the section body; template titles follow.
- `flows` is domain-split like the requirements scenarios: `flows/index.md` (domain index) + per-domain `flows/<domain>.md` (was single-file `flows.md`); a domain = a user journey or feature area.

### Fixed

- Template comments named the pre-1.2.0 WRITING-STYLE file; they now name `rules/writing.md`.

### Migration (from 1.2.0)

- Convert `flows.md` to the folder form: create `flows/index.md` (Domain | File | Scope) and move every flow into its domain's `flows/<domain>.md`.
- Replace the change folder's `README.md` and `README.ko.md` with fresh copies of the schema's `templates/README.md` and `templates/README.ko.md`.
- Recommended (SHOULD): retitle headings that trail a `Subject - explainer` dash suffix - the qualifier leads, the explanation opens the section body (rules/writing.md).

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- `data` conditional artifact - the client data layer: per-resource freshness (RFC 9111 + RFC 5861 stale-while-revalidate vocabulary), the invalidation map, optimistic updates with rollback, client retry aligned to the backend error catalog's retryability, and an offline section (stale-if-error reads, write queueing, reconnect reconciliation).
- Error mapping in `screens`: when a backend change exists, the error state maps each applicable problem type from the backend conventions error catalog to screen behavior and exact copy; retryable types keep a retry affordance.
- `overview`'s conditional-artifacts table and the `traceability` gaps list now carry data.
- ROUTES conditional section in `flows` - when the platform addresses screens by URL or deep link: per screen the route pattern, params, auth guard, and deep-link entry behavior.
- LOCALIZATION POLICY conditional section in `overview` (target locales, IGDA Loc SIG expansion headroom, font fallback, CLDR date/number/currency formats, pseudo-localization) with a per-component TEXT BUDGET line in `components` when the policy exists.
- API CALL SEQUENCES conditional section in `flows` - when a flow drives backend calls whose order or failure behavior matters: client-perspective UML sequence diagrams (lifelines: screen, client data layer, backend surface; endpoints named verbatim).
  Backend-internal interaction stays in the backend schema's `sequences` - sequence diagrams are a per-schema expression tool, not a single-home artifact.
- Event->transition actions that call the backend name the endpoint verbatim (`METHOD /path`).
- Tables follow the new rules/writing.md one-value-per-cell rule (first normal form): `traceability` uses a singular Component column with one row per link; the `flows` routes table splits Deep-link entry into State restored + Back target + Fallback deviation.
- `flows` coverage is exhaustive by construction (event partitioning, McMenamin & Palmer): per screen, enumerate all four trigger kinds - user events per interactive component, arriving events (push, deep link, connectivity), temporal events (timers, expiry, polling), data events (fetch success/failure, revalidation, rollback) - and place each in the navigation map or the event->transition table, or mark it screen-local.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).
- Rules documents moved into `openspec/rules/`: prose rules are now `rules/writing.md` (was `openspec/WRITING-STYLE.md`), diagram rules `rules/diagrams.md` (was `openspec/DIAGRAM-STYLE.md`); schema and template references updated.

### Migration (from 1.1.1)

- Add a `data` row (`Yes/No` + one-line reason) to `overview.md`'s "Conditional artifacts included" table.
- When a backend change exists, add the "Error mapping" table (problem type -> screen behavior -> exact copy) to each screen in `screens.md` that displays backend data.
- If the app manages client-side server-state (caching, optimistic updates, offline), author `data.md` from the new template; otherwise no further rework.
- If the platform addresses screens by URL or deep link, add the "Routes" section to `flows.md`.
- If a flow drives backend calls whose order or failure behavior matters, add the "API call sequences" section to `flows.md` - moving any client-side sequences authored in the backend change's `sequences.md`.
- Re-shape `traceability.md` (singular Component, one row per link) and, when the Routes section exists, split the `flows.md` Deep-link entry column into State restored / Back target / Fallback deviation.
- Audit `flows.md` against the four trigger kinds (user / arriving / temporal / data events) per screen; add missing transitions or explicit screen-local marks.
- If the product ships more than one locale, add the "Localization policy" section to `overview.md` and text budgets to `components.md`.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header (this schema is new in 1.1.0 - no migrations yet).

## [1.1.0] - 2026-07-15

### Added

- Initial release: frontend (application UI - web, mobile, desktop) detail-design schema (IFML 1.0, UML 2.5.1 state machines, NN/g wireflows, Atomic Design + Open UI anatomy, five-state UI Stack, WCAG 2.2, DTCG tokens) with 6 artifacts - `overview` -> (`design-tokens`) -> `components` -> `screens` -> `flows` -> `traceability`; `design-tokens` conditional.
