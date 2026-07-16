---
name: opsx-game-ui
version: "1.2.0"
description: Game UI detail design from an architecture change and the GDD - screens, HUD, widgets, input, settings, flows. No implementation.
---

Design the game UI in detail - the implementable game-UI spec for PC, console, mobile, and handheld games, one level below architecture and the GDD, and separate from development. This uses the `game-ui` schema (the Fagerholt & Lorentzon UI-layer design space with Andrews' diegetic/non-diegetic/spatial/meta terms, Game UI Database screen-type vocabulary, SMPTE ST 2046-1 safe areas + XAG 101/Steam Deck legibility floors, Steam Input-style action sets, Game Accessibility Guidelines + XAG v3.2, UML 2.5.1 state machines + wireflows). It produces:

**Core artifacts (always):**

- overview.md (platforms/devices, UI-layer vocabulary, safe area & scale, legibility floors, widget-state enum, localization policy, accessibility target, reader map)
- widgets.md (shared widgets: anatomy, variants, states, per-device input behavior, text budgets, glyph slots)
- screens.md (per screen & modal: layout + safe area, screen states, widgets, data, per-device operation, emitted event names)
- hud.md (per HUD element: UI layer, placement, data, visibility, customization hooks, feedback channels; conditional subtitles/captions section)
- flows.md (boot flow, navigation map, modal & pause conventions, event->transition tables, statecharts)
- input.md (per-context action sets with bindings per device, glyph policy, remapping, hot-swap, menu navigation model)
- settings.md (the option inventory: type/range/default/effect/platforms/accessibility mapping per option)
- traceability.md (GDD/requirement <-> screen/hud <-> flow <-> widget <-> input <-> settings matrix)

**Conditional artifact (only when the product has that concern):**

- design-tokens.md - token-based styling (DTCG: color/typography with fallbacks/dimension/motion/themes)

This pipeline answers WHAT EVERY SCREEN AND HUD ELEMENT SHOWS AND HOW THE GAME UI BEHAVES per state, input device, and setting; the GDD's ux-ui section already answered intent (flow map, key screens, input summary, onboarding). There is **no implementation/apply step** and the change stays open - you can keep adding screens and refining widgets over time.

---

**Input**: The argument after `/opsx:game-ui` is a description OR the program name. An architecture or GDD change to build on may be named too (e.g. `--from tycoon-architecture`).

**Steps**

1. **Identify the source changes.** Game-UI detail design builds on the architecture change (technology stack) and the GDD change (ux-ui intent). If the user named them, use those. Otherwise list `openspec/changes/*-architecture/` and `openspec/changes/*-gdd/` and ask which to build on. If one is genuinely missing, proceed from what the user gives, but say so.

2. **Decide whether the CONDITIONAL artifact applies - recommend, then confirm.**
   - Auto-recommend: include **design-tokens** if styling is token-based (a centralized stylesheet, theming, or multi-platform styling exists or is planned).
   - Also recommend whether hud.md needs its **subtitles/captions section** (the game has speech or important audio).
   - Present the recommendation (include yes/no + one-line reason each) and **ask the user to confirm or adjust** before creating the change. Core artifacts are not negotiable.

3. **Determine the change name - `{program}-game-ui`.** The game-ui schema has no apply step and is a **project-level singleton** - normally one game-UI detail design per program.
   - If a `*-game-ui` change already exists, that is this project's game-UI design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source architecture/GDD program); the user may give a different fixed name. The change name is then `{program}-game-ui`.
   - To keep multiple parallel game-UI designs, the user gives distinct program names -> `{a}-game-ui`, `{b}-game-ui`.

4. **Create the game-ui change**

   ```bash
   openspec new change "{program}-game-ui" --schema game-ui
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/game-ui/templates/README.md` to `openspec/changes/{program}-game-ui/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/game-ui/templates/README.ko.md` to `openspec/changes/{program}-game-ui/README.ko.md`. These static guides are identical for every game-ui change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-game-ui" --json
   ```

   Build in dependency order: `overview -> (design-tokens) -> widgets -> screens -> hud -> flows -> input -> settings -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-game-ui" --json`
   - Read the relevant source architecture/GDD files AND any completed dependency game-ui files for context.
   - **If the user excluded design-tokens in step 2: do NOT create the file.** Leave it absent - an omitted artifact simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-game-ui" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-game-ui"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the system-wide UI vocabulary, declared ONCE: the four UI layers in this game's terms, safe-area/scale/aspect-ratio policy (ultrawide behavior is a recorded project decision), per-platform legibility floors, the widget-state enum, localization budgets (30-40% expansion headroom unless justified otherwise), the accessibility target (GAG tier + XAG numbers; CVAA/EAA note only when the game has chat or purchasing), the platform-cert placeholder (NDA docs are project inputs).
- **design-tokens** - DTCG vocabulary (name/$type/$value): semantic color roles, the font set with per-script fallback chains, spacing, named easing + duration tokens (reducible per the accessibility target), themes as token-value collections (default/high-contrast/colorblind). Widgets consume tokens by name.
- **widgets** - shared widgets only: anatomy (named parts), variants/sizes with concrete dimensions, behavior per applicable widget state, operation per device class (pointer / gamepad focus + cardinal navigation / touch), text budgets with localization headroom, glyph slots, narration/text-scaling behavior.
- **screens** - per screen and modal: purpose + GDD/requirement trace, wire mockup with safe-area compliance, screen states for data-driven screens (empty/loading/error with copy), widgets by name, data with endpoint references when a backend change exists, screen-specific operation (initial focus, gestures), analytics event names only.
- **hud** - one block per element: UI-layer classification with rationale, placement + collision behavior, data by GDD mechanic name, visibility rules, customization hooks by settings option name, non-visual feedback channels; subtitles/captions section with concrete values when included.
- **flows** - boot flow (legal placeholders -> title -> first-boot setup), a navigation map covering every screen including gameplay<->pause, modal stack conventions, event->transition tables for guarded transitions, statecharts ONLY for non-trivial internal state.
- **input** - actions, not buttons: one action set per context with a binding table per device, layers for modified contexts, glyph policy (match active device; public fallback when first-party art is NDA), remapping policy (full remap is the baseline), hot-swap behavior, the menu navigation model, haptics hooks.
- **settings** - every option in exactly one bucket (gameplay/display/audio/UI & accessibility/language/controls): type/range/default/effect (by hud/widget/action name)/platforms/accessibility mapping (XAG/GAG item), plus first-boot exposure. Assist/difficulty design traces to the GDD.
- **traceability** - GDD/requirement <-> screen/hud element <-> flow <-> widget <-> input context <-> settings option (+ endpoint column when a backend change exists), plus a gaps section.

**Output**

Summarize: game-ui change name + location, whether design-tokens and the subtitles section were included (and why), artifacts created (one line each), and: "Game-UI detail design complete - no implementation step. The change stays open; re-run `/opsx:game-ui` to add screens or refine widgets. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is the IMPLEMENTABLE GAME-UI SPEC, below architecture and the GDD and above implementation. NO code, ENGINE-AGNOSTIC: wire mockups, layer classifications, binding tables, and option tables are the medium; engine assets and source files are not.
- Diagrams follow `openspec/DIAGRAM-STYLE.md`.
- Do NOT restate the GDD, architecture, or requirements - reference them by name/id. The GDD ux-ui section keeps intent (flow map, key screens, input summary, onboarding); this schema holds the implementable detail. Application UIs (companion apps, web storefronts) belong to the frontend schema, not here.
- State each fact once: system-wide vocabulary in overview, widget facts in widgets; screens and hud reference widgets by name and record only what is specific to them.
- Every screen and HUD element carries its UI-layer classification and respects the overview safe-area and legibility policy - deviations are called out, never silent.
- Input is specified as actions mapped to bindings per device per context - never raw buttons in prose. On-screen glyphs match the active device.
- Settings options define each option ONCE; hud/input reference options by name. Accessibility options carry the XAG/GAG item they serve.
- Platform certification requirements (Sony TRC, Nintendo guidelines, Xbox XR test cases) are NDA-bound project inputs - reference them as placeholders, never restate their content.
- Analytics events appear as NAMES only, cross-referencing the project's tracking plan - never define the tracking taxonomy here.
- The user often narrates the UI one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- Omit design-tokens entirely if styling is not token-based - never create an empty placeholder. Same for the subtitles section when the game has no speech or important audio.
- The change does not close. There is no apply step in the game-ui schema.
- Change name is `{program}-game-ui` (project singleton). Don't invent per-feature names; continue the existing `*-game-ui` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/game-ui/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source architecture/GDD + dependency game-ui artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/WRITING-STYLE.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, ISO 8601 dates.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
