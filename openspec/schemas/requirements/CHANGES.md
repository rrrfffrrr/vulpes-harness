# Changelog - requirements schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- Acceptance criteria per operation in `operation-model` (BABOK v3 technique 10.1): the measurable pass/fail conditions stakeholders accept the operation by. The new `verification` schema realizes them as cross-layer scenarios.
- `scenarios` artifact - domain-split operational scenarios (ISO/IEC/IEEE 29148 operational scenarios information item, 9.3.17/9.4.17; KAOS behavior scenarios; BABOK v3 10.42 Sequence Diagrams / 10.47 Use Cases and Scenarios).
  `scenarios/index.md` is the domain index (domains mirror the goal model's top-level goals); each domain's `scenarios/<domain>.md` holds agent-interaction sequence diagrams: trigger (agent or schedule), lifelines = responsibility-model agents, messages = operation-model operations, outcome = the satisfied goal, plus obstacle variants.
  Coverage is exhaustive by construction (event partitioning, McMenamin & Palmer): each domain file opens with its full EVENT LIST (agent actions, temporal events incl. missed-expected-event probes, arriving environment events) and every event maps to one scenario or an explicit "no response"; scenario steps get a Cockburn-style extension sweep; every operation appears in at least one scenario.
  `requirements-document`'s Behavior section restates the flows; `traceability` gains an operation -> scenario table.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema).
- Tables follow the new WRITING-STYLE one-value-per-cell rule (first normal form): the `traceability` BR table uses a singular Goal column with one row per BR-goal link.
- Classification markers lead the line: goal-model leaves start with `[Requirement]`/`[Expectation]` before the goal id, and business-requirements headings start with `[Goal]`/`[Constraint]` before the BR id - a marker never trails the free text.

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
3. Recommended (SHOULD, not MUST): reflow artifact prose to `openspec/WRITING-STYLE.md`.

## [1.0.0] - 2026-06-22

### Added

- Initial release: KAOS/GORE + BABOK requirements schema with 7 artifacts - `business-requirements` -> `goal-model` -> `object-model`, `responsibility-model` -> `operation-model` -> `requirements-document` -> `traceability`.
