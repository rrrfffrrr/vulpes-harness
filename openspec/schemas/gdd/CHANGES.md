# GDD schema changelog

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

### Migration (from 1.2.0)

- Replace the change folder's `README.md` and `README.ko.md` with fresh copies of the schema's `templates/README.md` and `templates/README.ko.md`.
- Recommended (SHOULD): retitle headings that trail a `Subject - explainer` dash suffix - the qualifier leads, the explanation opens the section body (rules/writing.md).

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.

### Changed

- Version lockstep with the 1.2.0 harness release (adds the game-ui schema) - no changes to this schema's artifacts; no migration needed.
- Rules documents moved into `openspec/rules/`: prose rules are now `rules/writing.md` (was `openspec/WRITING-STYLE.md`), diagram rules `rules/diagrams.md` (was `openspec/DIAGRAM-STYLE.md`); schema and template references updated.

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

- Initial release: Game Design Document schema with 10 artifacts - `overview` -> `gameplay` -> `mechanics` -> (`world-narrative`) -> `art-direction` -> `audio-direction` -> `ux-ui` -> `tech` -> (`monetization`) -> `production`; `world-narrative` and `monetization` conditional.
