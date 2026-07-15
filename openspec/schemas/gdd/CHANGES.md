# Changelog - gdd schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.

## [1.1.0] - Unreleased

### Added

- `schema-version` / `document-version` frontmatter on every template - artifacts now record the schema semver they were authored against and a per-document revision counter.
- Korean reading guide `templates/README.ko.md`; both guides carry an English/Korean switcher link.
- Authoring principle: artifact prose uses semantic line breaks (sembr.org) - one sentence per line.

### Changed

- Reading guide moved from `change-README.md` to `templates/README.md` (copied into the change folder name-preserving, alongside `README.ko.md`).

## [1.0.0] - 2026-06-22

### Added

- Initial release: Game Design Document schema with 10 artifacts - `overview` -> `gameplay` -> `mechanics` -> (`world-narrative`) -> `art-direction` -> `audio-direction` -> `ux-ui` -> `tech` -> (`monetization`) -> `production`; `world-narrative` and `monetization` conditional.
