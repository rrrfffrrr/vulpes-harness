# Changelog - gdd schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - 2026-07-18

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
3. Recommended (SHOULD, not MUST): reflow artifact prose to `openspec/WRITING-STYLE.md`.

## [1.0.0] - 2026-06-22

### Added

- Initial release: Game Design Document schema with 10 artifacts - `overview` -> `gameplay` -> `mechanics` -> (`world-narrative`) -> `art-direction` -> `audio-direction` -> `ux-ui` -> `tech` -> (`monetization`) -> `production`; `world-narrative` and `monetization` conditional.
