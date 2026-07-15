---
name: opsx-frontend
version: "1.1.0"
description: Frontend (application UI) detail design from an architecture change - screens, components, states, flows, tokens. No implementation.
---

Design the application UI in detail - the implementable UI spec for web, mobile, and desktop apps, one level below architecture and separate from development. This uses the `frontend` schema (IFML 1.0 interaction-flow semantics, Harel statecharts as UML 2.5.1 state machines, NN/g wireflows, Atomic Design + Open UI-style component anatomy, the five-state UI Stack, WCAG 2.2). It produces:

**Core artifacts (always):**
- overview.md (platforms/stacks, breakpoint set, interaction-state enum, accessibility target, reader map)
- components.md (shared components: anatomy, variants/sizes, per-state behavior, keyboard/assistive behavior, content rules)
- screens.md (per screen: layout + breakpoint behavior, the five UI Stack states, data, forms with exact error copy, emitted event names)
- flows.md (navigation map, event->transition tables, statecharts for complex interactions)
- traceability.md (requirement <-> screen <-> flow <-> component matrix)

**Conditional artifact (only when the product has that concern):**
- design-tokens.md - token-based styling (DTCG: color/typography/dimension/motion/themes)

This pipeline answers WHAT EACH SCREEN SHOWS AND HOW THE UI BEHAVES per state and event; architecture already answered structure/technology. There is **no implementation/apply step** and the change stays open - you can keep adding screens and refining components over time.

---

**Input**: The argument after `/opsx:frontend` is a description OR the program name. An architecture change to build on may be named too (e.g. `--from tycoon-architecture`).

**Steps**

1. **Identify the source architecture change.** Frontend detail design builds on architecture artifacts. If the user named one, use it. Otherwise list `openspec/changes/*-architecture/` and ask which to build on. If there is genuinely no architecture change, proceed from what the user gives, but say so.

2. **Decide whether the CONDITIONAL artifact applies - recommend, then confirm.**
   - Auto-recommend: include **design-tokens** if styling is token-based (a design system, theming, or multi-platform styling exists or is planned).
   - Present the recommendation (include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core artifacts are not negotiable.

3. **Determine the change name - `{program}-frontend`.** The frontend schema has no apply step and is a **project-level singleton** - normally one frontend detail design per program.
   - If a `*-frontend` change already exists, that is this project's frontend design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source architecture program); the user may give a different fixed name. The change name is then `{program}-frontend`.
   - To keep multiple parallel frontend designs, the user gives distinct program names -> `{a}-frontend`, `{b}-frontend`.

4. **Create the frontend change**
   ```bash
   openspec new change "{program}-frontend" --schema frontend
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/frontend/templates/README.md` to `openspec/changes/{program}-frontend/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/frontend/templates/README.ko.md` to `openspec/changes/{program}-frontend/README.ko.md`. These static guides are identical for every frontend change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**
   ```bash
   openspec status --change "{program}-frontend" --json
   ```
   Build in dependency order: `overview -> (design-tokens) -> components -> screens -> flows -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-frontend" --json`
   - Read the relevant source architecture files AND any completed dependency frontend files for context.
   - **If the user excluded design-tokens in step 2: do NOT create the file.** Leave it absent - an omitted artifact simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-frontend" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-frontend"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the system-wide UI vocabulary, declared ONCE: breakpoint classes with ranges, the interaction-state enum, the WCAG 2.2 conformance level (and how it applies off-web), reader map, conditional inclusion.
- **design-tokens** - DTCG vocabulary (name/$type/$value): semantic color roles, type scale, spacing, named easing + duration tokens, themes as token-value collections. Components consume tokens by name.
- **components** - shared components only: anatomy (named parts), variants/sizes with concrete dimensions, behavior per applicable interaction state, pointer + keyboard behavior (APG pattern where one exists), microcopy rules, RTL note only where mirroring matters.
- **screens** - per screen: purpose + requirement trace, wire mockup + per-breakpoint behavior (reveal/divide/resize/reposition/swap), ALL five UI Stack states with copy, components by name, data with endpoint references when a backend change exists, per-field validation + exact error copy, analytics event names only.
- **flows** - the navigation map covers every screen; event->transition tables for guarded/parameterized transitions; statecharts ONLY for non-trivial internal state.
- **traceability** - requirement <-> screen <-> flow <-> component (+ endpoint column when a backend change exists), plus a gaps section.

**Output**

Summarize: frontend change name + location, whether design-tokens was included (and why), artifacts created (one line each), and: "Frontend detail design complete - no implementation step. The change stays open; re-run `/opsx:frontend` to add screens or refine components. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**
- This is the IMPLEMENTABLE UI SPEC for application UIs (web, mobile, desktop), below architecture and above implementation. NO code. Wire mockups, state tables, and token tables are the medium; source files are not.
- Diagrams follow `openspec/DIAGRAM-STYLE.md`.
- Do NOT restate architecture or requirements - reference them by name/id.
- State each fact once: system-wide vocabulary in overview, component facts in components; screens reference components by name and record only screen-specific behavior.
- Every screen covers ALL five UI Stack states (ideal/empty/loading/partial/error) - never only the ideal state.
- Form validation rules and exact error copy are part of the screen contract - never leave them "TBD".
- Analytics events appear as NAMES only, cross-referencing the project's tracking plan - never define the tracking taxonomy here.
- The user often narrates the UI one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- Omit design-tokens entirely if styling is not token-based - never create an empty placeholder.
- The change does not close. There is no apply step in the frontend schema.
- Change name is `{program}-frontend` (project singleton). Don't invent per-feature names; continue the existing `*-frontend` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/frontend/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source architecture + dependency frontend artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style - semantic line breaks (sembr.org):** start each sentence on its own line; break long sentences after clause boundaries (`,` `;` `:`). Line breaks never alter Markdown rendering, but sources stay readable and document-version diffs stay sentence-scoped. Never run a paragraph together on one long line.
