# Game UI schema changelog

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
- `flows` is domain-split like the requirements scenarios: `flows/index.md` (domain index) + per-domain `flows/<domain>.md` (was single-file `flows.md`); a domain = a flow area (boot, gameplay, meta menus, settings).

### Fixed

- Template comments named the pre-1.2.0 WRITING-STYLE file; they now name `rules/writing.md`.

### Migration (from 1.2.0)

- Convert `flows.md` to the folder form: create `flows/index.md` (Domain | File | Scope) and move every flow into its domain's `flows/<domain>.md`.
- Replace the change folder's `README.md` and `README.ko.md` with fresh copies of the schema's `templates/README.md` and `templates/README.ko.md`.
- Recommended (SHOULD): retitle headings that trail a `Subject - explainer` dash suffix - the qualifier leads, the explanation opens the section body (rules/writing.md).

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: game-ui (game UI for PC, console, mobile, handheld) detail-design schema with 9 artifacts - `overview` -> (`design-tokens`) -> `widgets` -> `screens` / `hud` -> `flows` / `input` -> `settings` -> `traceability`; `design-tokens` conditional, subtitles/captions a conditional section of `hud`.
- Methodology: Fagerholt & Lorentzon diegesis/spatiality UI-layer design space (Chalmers 2009) with Andrews' diegetic/non-diegetic/spatial/meta terms (2010), Game UI Database screen-type vocabulary, SMPTE ST 2046-1 safe areas + Xbox Accessibility Guidelines 101 / Steam Deck legibility floors, Steam Input action sets/layers as the input model, Game Accessibility Guidelines + XAG v3.2 accessibility, Pinelle 2008 game-usability heuristics, IGDA Localization SIG text-expansion budgets, UML 2.5.1 state machines + wireflows (harness-shared).
- Boundary: the GDD `ux-ui` section keeps intent (flow map, key screens, input summary, onboarding); game-ui is the implementable spec below it. Application UIs (companion apps, web storefronts) stay in the frontend schema.
