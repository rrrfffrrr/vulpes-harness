# Game UI schema changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.
`schema-version` records MUST items only; SHOULD items follow the Requirement keywords rule in `openspec/rules/writing.md` - deferrable, never dismissible.
On every migration, re-check every version's SHOULD items - including versions at or below the artifact's `schema-version` - and apply any still due.

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: game-ui (game UI for PC, console, mobile, handheld) detail-design schema with 9 artifacts - `overview` -> (`design-tokens`) -> `widgets` -> `screens` / `hud` -> `flows` / `input` -> `settings` -> `traceability`; `design-tokens` conditional, subtitles/captions a conditional section of `hud`.
- Methodology: Fagerholt & Lorentzon diegesis/spatiality UI-layer design space (Chalmers 2009) with Andrews' diegetic/non-diegetic/spatial/meta terms (2010), Game UI Database screen-type vocabulary, SMPTE ST 2046-1 safe areas + Xbox Accessibility Guidelines 101 / Steam Deck legibility floors, Steam Input action sets/layers as the input model, Game Accessibility Guidelines + XAG v3.2 accessibility, Pinelle 2008 game-usability heuristics, IGDA Localization SIG text-expansion budgets, UML 2.5.1 state machines + wireflows (harness-shared).
- Boundary: the GDD `ux-ui` section keeps intent (flow map, key screens, input summary, onboarding); game-ui is the implementable spec below it. Application UIs (companion apps, web storefronts) stay in the frontend schema.
