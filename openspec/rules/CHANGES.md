# Rules changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version; the folder is replaced whole on update, so this file is the installed copy's version marker.
Document rework a rule change requires is recorded as a Migration section in each affected schema's `CHANGES.md` - never here.

## [1.2.1] - Unreleased

### Added

- writing.md Tables: the category test - a column is a category of fact, a compound identifier is one value; a column splits only when two categories share it.
- writing.md Requirement keywords: SHOULD semantics defined once here (RFC 2119 / RFC 8174: deferrable, never dismissible); schema changelogs reference it.
- writing.md Line breaks: a worked example of sentence-end and clause breaks.

### Changed

- Headings drop the `Subject - explainer` dash suffix (writing.md Scannable structure); diagrams.md and structure.md headings follow.
- structure.md Split on growth: sequence-heavy artifacts split into an index file plus per-domain files; the domains mirror the requirements scenarios domains.

## [1.2.0] - 2026-07-18

### Added

- Rules folder: `writing.md` (was root-level `openspec/WRITING-STYLE.md`), `diagrams.md` (was `openspec/DIAGRAM-STYLE.md`), and the new `structure.md` (boundary, place, growth, naming, index).
