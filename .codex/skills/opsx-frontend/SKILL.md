---
name: opsx-frontend
version: "1.2.0"
description: Frontend (application UI) detail design from an architecture change - screens, components, states, flows, tokens, client data. No implementation.
---

Design the application UI in detail - the implementable UI spec for web, mobile, and desktop apps, one level below architecture and separate from development. This uses the `frontend` schema (IFML 1.0 interaction-flow semantics, Harel statecharts as UML 2.5.1 state machines, NN/g wireflows, Atomic Design + Open UI-style component anatomy, the five-state UI Stack, WCAG 2.2). It produces:

**Core artifacts (always):**

- overview.md (platforms/stacks, breakpoint set, interaction-state enum, accessibility target, reader map)
- components.md (shared components: anatomy, variants/sizes, per-state behavior, keyboard/assistive behavior, content rules)
- screens.md (per screen: layout + breakpoint behavior, the five UI Stack states, data, forms with exact error copy, emitted event names)
- flows.md (navigation map, event->transition tables, API call sequences, statecharts for complex interactions)
- traceability.md (requirement <-> screen <-> flow <-> component matrix)

**Conditional artifacts (only when the product has that concern):**

- design-tokens.md - token-based styling (DTCG: color/typography/dimension/motion/themes)
- data.md - client data layer (RFC 9111/5861 freshness vocabulary, invalidation map, optimistic updates, offline)

This pipeline answers WHAT EACH SCREEN SHOWS AND HOW THE UI BEHAVES per state and event; architecture already answered structure/technology. There is **no implementation/apply step** and the change stays open - you can keep adding screens and refining components over time.

---

**Input**: The argument after `/opsx:frontend` is a description OR the program name. An architecture change to build on may be named too (e.g. `--from tycoon-architecture`).

**Steps**

1. **Identify the source architecture change.** Frontend detail design builds on architecture artifacts. If the user named one, use it. Otherwise list `openspec/changes/*-architecture/` and ask which to build on. If there is genuinely no architecture change, proceed from what the user gives, but say so.

2. **Decide which CONDITIONAL artifacts apply - recommend, then confirm.**
   - Auto-recommend: include **design-tokens** if styling is token-based (a design system, theming, or multi-platform styling exists or is planned); include **data** if the UI holds server data across screens (caching/refresh), updates optimistically, or works offline.
   - Present the recommendation (each: include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core artifacts are not negotiable.

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

   Build in dependency order: `overview -> (design-tokens) -> components -> screens -> (data), flows -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-frontend" --json`
   - Read the relevant source architecture files AND any completed dependency frontend files for context.
   - **For conditional artifacts the user excluded in step 2: do NOT create the file.** Leave it absent - an omitted artifact simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-frontend" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-frontend"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the system-wide UI vocabulary, declared ONCE: breakpoint classes with ranges, the interaction-state enum, the WCAG 2.2 conformance level (and how it applies off-web), the localization policy (locales, expansion headroom, fallback fonts, CLDR formats) when multi-locale, reader map, conditional inclusion.
- **design-tokens** - DTCG vocabulary (name/$type/$value): semantic color roles, type scale, spacing, named easing + duration tokens, themes as token-value collections. Components consume tokens by name.
- **components** - shared components only: anatomy (named parts), variants/sizes with concrete dimensions, behavior per applicable interaction state, pointer + keyboard behavior (APG pattern where one exists), microcopy rules (+ text budgets when a localization policy exists), RTL note only where mirroring matters.
- **screens** - per screen: purpose + requirement trace, wire mockup + per-breakpoint behavior (reveal/divide/resize/reposition/swap), ALL five UI Stack states with copy, components by name, data with endpoint references when a backend change exists, error states mapped to the backend error catalog's problem types (retryable types keep a retry affordance), per-field validation + exact error copy, analytics event names only.
- **data** - defaults once (freshness window, revalidate triggers, cache scope, client retry per backend retryability); per resource: source endpoints, displaying screens, invalidation map, optimistic updates + rollback; offline section only when the app works offline. Behavior, never a state library's API.
- **flows** - the navigation map covers every screen; a routes section (pattern/params/guard/deep-link entry) when the platform addresses screens by URL; event->transition tables for guarded/parameterized transitions (backend calls name the endpoint verbatim); API call sequences (client-perspective: screen, data layer, endpoints verbatim, user-observable failure paths) when a flow drives backend calls whose order or failure behavior matters - backend internals stay in the backend design's sequences; statecharts ONLY for non-trivial internal state.
- **traceability** - requirement <-> screen <-> flow <-> component (+ endpoint column when a backend change exists), plus a gaps section.

**Output**

Summarize: frontend change name + location, which conditional artifacts were included (and why), artifacts created (one line each), and: "Frontend detail design complete - no implementation step. The change stays open; re-run `/opsx:frontend` to add screens or refine components. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is the IMPLEMENTABLE UI SPEC for application UIs (web, mobile, desktop), below architecture and above implementation. NO code. Wire mockups, state tables, and token tables are the medium; source files are not.
- Diagrams follow `openspec/DIAGRAM-STYLE.md`.
- Do NOT restate architecture or requirements - reference them by name/id.
- State each fact once: system-wide vocabulary in overview, component facts in components; screens reference components by name and record only screen-specific behavior.
- Every screen covers ALL five UI Stack states (ideal/empty/loading/partial/error) - never only the ideal state.
- Form validation rules and exact error copy are part of the screen contract - never leave them "TBD".
- Analytics events appear as NAMES only, cross-referencing the project's tracking plan - never define the tracking taxonomy here.
- The user often narrates the UI one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- When a backend change exists, error states map the backend error catalog's problem types - never invent error semantics the backend does not define.
- Omit a conditional artifact entirely if its concern is absent - never create an empty placeholder.
- The change does not close. There is no apply step in the frontend schema.
- Change name is `{program}-frontend` (project singleton). Don't invent per-feature names; continue the existing `*-frontend` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/frontend/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source architecture + dependency frontend artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/WRITING-STYLE.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, ISO 8601 dates.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
