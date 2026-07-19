# Requirements schema changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.
`schema-version` records MUST items only; SHOULD items follow the Requirement keywords rule in `openspec/rules/writing.md` - deferrable, never dismissible.
On every migration, re-check every version's SHOULD items - including versions at or below the artifact's `schema-version` - and apply any still due.

## [1.2.1] - 2026-07-19

### Changed

- Version lockstep with the 1.2.1 harness release.
- Migration chain rule: SHOULD items follow the new Requirement keywords rule in rules/writing.md (RFC 2119: deferrable, never dismissible) - re-checked on every migration, even for versions already passed.
- Headings drop the `Subject - explainer` dash suffix (rules/writing.md Scannable structure): a qualifier leads, the explanation opens the section body; template titles follow.

### Fixed

- Template comments named the pre-1.2.0 WRITING-STYLE file; they now name `rules/writing.md`.

### Migration (from 1.2.0)

- Replace the change folder's `README.md` and `README.ko.md` with fresh copies of the schema's `templates/README.md` and `templates/README.ko.md`.
- Recommended (SHOULD): retitle headings that trail a `Subject - explainer` dash suffix - the qualifier leads, the explanation opens the section body (rules/writing.md).

## [1.2.0] - 2026-07-18

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Acceptance criteria per operation in `operation-model` (BABOK v3 technique 10.1): the measurable pass/fail conditions stakeholders accept the operation by. The new `verification` schema realizes them as cross-layer scenarios.
- `scenarios` artifact - domain-split operational scenarios (ISO/IEC/IEEE 29148 operational scenarios information item, 9.3.17/9.4.17; KAOS behavior scenarios; BABOK v3 10.42 Sequence Diagrams / 10.47 Use Cases and Scenarios).
  `scenarios/index.md` is the domain index (domains mirror the goal model's top-level goals); each domain's `scenarios/<domain>.md` holds agent-interaction sequence diagrams: trigger (agent or schedule), lifelines = responsibility-model agents, messages = operation-model operations, outcome = the satisfied goal, plus obstacle variants.
  Coverage is exhaustive by construction (event partitioning, McMenamin & Palmer): each domain file opens with its full EVENT LIST (agent actions, temporal events incl. missed-expected-event probes, arriving environment events) and every event maps to one scenario or an explicit "no response"; scenario steps get a Cockburn-style extension sweep; every operation appears in at least one scenario.
  `requirements-document`'s Behavior section restates the flows; `traceability` gains an operation -> scenario table.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).
- Tables follow the new rules/writing.md one-value-per-cell rule (first normal form): the `traceability` BR table uses a singular Goal column with one row per BR-goal link.
- Classification markers lead the line: goal-model leaves start with `[Requirement]`/`[Expectation]` before the goal id, and business-requirements headings start with `[Goal]`/`[Constraint]` before the BR id - a marker never trails the free text.
- Rules documents moved into `openspec/rules/`: prose rules are now `rules/writing.md` (was `openspec/WRITING-STYLE.md`), diagram rules `rules/diagrams.md` (was `openspec/DIAGRAM-STYLE.md`); schema and template references updated.

### Migration (from 1.1.1)

- Add an "Acceptance criteria" list (measurable, pass/fail) to every operation in `operation-model.md`; derive them from the operation's post-condition and the goal it operationalizes, and confirm them with stakeholders before relying on them.
- Re-shape the `traceability.md` BR table: singular Goal column, one row per BR-goal link.
- Move each goal-model leaf's trailing `[Requirement]`/`[Expectation]` marker to the front of the line (before the goal id), and each business-requirements heading's `[Goal]`/`[Constraint]` marker to the front (before the BR id).
- Author `scenarios/index.md` (domain index) plus one `scenarios/<domain>.md` per top-level goal from the existing models; cover every operation with at least one scenario; add the operation -> scenario table to `traceability.md` and restate the flows in `requirements-document.md`'s Behavior section.

## [1.1.1] - 2026-07-15

### Added

- Migration guidance: the chain rule in this header and a Migration section under 1.1.0.

## [1.1.0] - 2026-07-15

### Added

- `schema-version` / `document-version` frontmatter on every template - artifacts now record the schema semver they were authored against and a per-document revision counter.
- Korean reading guide `templates/README.ko.md`; both guides carry an English/Korean switcher link.
- Authoring principle: prose follows the new `openspec/WRITING-STYLE.md` - semantic line breaks, plain language, scannable structure, consistent terminology, findability, ISO 8601 dates.

### Changed

- Reading guide moved from `change-README.md` to `templates/README.md` (copied into the change folder name-preserving, alongside `README.ko.md`).

### Migration (from 1.0.0)

1. Add the version frontmatter to every artifact in the change: `schema-version: 1.1.0`, `document-version: 0`.
2. Replace the change folder's `README.md` with a copy of the schema's `templates/README.md`, and copy `templates/README.ko.md` to `README.ko.md`.
3. Recommended (SHOULD, not MUST): reflow artifact prose to `openspec/WRITING-STYLE.md` (now `openspec/rules/writing.md`).

## [1.0.0] - 2026-06-22

### Added

- Initial release: KAOS/GORE + BABOK requirements schema with 7 artifacts - `business-requirements` -> `goal-model` -> `object-model`, `responsibility-model` -> `operation-model` -> `requirements-document` -> `traceability`.
