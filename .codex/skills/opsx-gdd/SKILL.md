---
name: opsx-gdd
version: "1.2.1"
description: Author a Game Design Document - the cross-discipline blueprint of the intended game (overview, gameplay, mechanics, art, audio, UX, tech, monetization, production). No implementation.
---

Author a Game Design Document - the cross-discipline blueprint of the intended game, separate from formal requirements and from development. This uses the `gdd` schema (standard GDD sections, from a high-concept overview down to a production scope). It produces:

**Core sections (always):**

- overview.md (elevator pitch, genre, platform, audience, design pillars, USPs, scope/MVP)
- gameplay.md (core loop, moment-to-moment, game flow & states, win/lose, difficulty)
- mechanics.md (systems & rules, progression, economy sources/sinks, balancing intent)
- art-direction.md (visual style, palette/mood, character/environment art, animation, VFX, UI art)
- audio-direction.md (music, SFX, voice/ambience, audio feedback & feel)
- ux-ui.md (screen/menu flow, key screens & layout, controls, onboarding, accessibility)
- tech.md (engine, platforms/min-spec, performance, save/network, dependencies, build/release)
- production.md (market & positioning, KPIs, MoSCoW feature list, milestones, risks & cut list)

**Conditional sections (only when the game has that concern):**

- world-narrative.md - the game has a setting, story, or characters
- monetization.md - the game is commercial (F2P/IAP/ads/premium pricing)

This is a GDD (the intended game - what it is, how it plays/looks/sounds, how it ships). It is NOT formal requirements capture (that is `/opsx:require`) and NOT technical architecture (that is `/opsx:architect`). There is **no implementation/apply step**, and the change stays open - a GDD is a living document you keep updating.

---

**Input**: The argument after `/opsx:gdd` is a description of the game OR the program name. An existing requirements change to build on may be named too (e.g. `--from tycoon-requirements`).

**Steps**

1. **If no input provided, ask what game they want to document** (open-ended, no preset options).

2. **Identify any source requirements change.** If a requirements change exists for this game (an `openspec/changes/*/requirements-document.md`), use it as source so the GDD references goals/requirements by id instead of re-deriving them. If the user named one, use it. If there is none, proceed from what the user gives and say so.

3. **Decide which CONDITIONAL sections to include - recommend, then confirm.**
   - Auto-recommend: include **world-narrative** if the game has a setting/story/characters; include **monetization** if the game is commercial (F2P/IAP/ads/premium price).
   - Present the recommendation (each: include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core sections are not negotiable.

4. **Determine the change name - `{program}-gdd`.** The gdd schema has no apply step and is a **project-level singleton** - normally one GDD per program.
   - If a `*-gdd` change already exists, that is this project's GDD - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name; the user may give a different fixed name. The change name is then `{program}-gdd`.
   - To keep multiple parallel GDDs (e.g. two products in one repo), the user gives distinct program names -> `{a}-gdd`, `{b}-gdd`.

5. **Create the GDD change**

   ```bash
   openspec new change "{program}-gdd" --schema gdd
   ```

6. **Write the folder README (reading guide).** Copy `openspec/schemas/gdd/templates/README.md` to `openspec/changes/{program}-gdd/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/gdd/templates/README.ko.md` to `openspec/changes/{program}-gdd/README.ko.md`. These static guides are identical for every gdd change - copy verbatim, do NOT hand-edit them per project.

7. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-gdd" --json
   ```

   Build in dependency order: `overview -> gameplay -> mechanics -> (world-narrative) -> art-direction -> audio-direction -> ux-ui -> tech -> (monetization) -> production`.

8. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-gdd" --json`
   - Read any source requirements files AND any completed dependency GDD files for context.
   - **For conditional sections the user excluded in step 3: do NOT create the file.** Leave it absent - an omitted section simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-gdd" --json` and continue with the next `ready` artifact.

9. **Show final status**: `openspec status --change "{program}-gdd"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the one-page framing every role reads first: elevator pitch, genre, platform, audience, 3-5 design pillars, USPs, core fantasy, MVP/scope boundary. Keep it skimmable.
- **gameplay** - how it PLAYS: core loop (as a diagram), moment-to-moment feel, game flow/states, progression feel, win/lose/difficulty. Not internal systems.
- **mechanics** - systems and RULES in detail, progression, the economy (resources, sources, sinks), and balancing intent with concrete numbers/ranges.
- **world-narrative** - setting/theme, narrative, characters (role/function, not art), content/level structure. Fiction in service of gameplay.
- **art-direction** - visual style with reference LINKS, palette/mood, character/environment art, animation, VFX, UI art style, consistency rules.
- **audio-direction** - music, key SFX tied to the events that trigger them, voice/ambience, audio's role in feedback/feel.
- **ux-ui** - screen/menu flow map, key screens with ascii/mermaid wire mockups, control scheme, onboarding, accessibility. Layout/flow, not styling.
- **tech** - engine + key tech with version intent, platforms/min-spec, performance targets, save/network, dependencies, build/release, hard constraints. GDD altitude, not deep architecture.
- **monetization** - business model, IAP/ads/pass, real-money vs soft currency (reference mechanics economy), retention/LiveOps, fairness/compliance, KPIs.
- **production** - market & positioning, KPIs, MoSCoW feature list (by reference to other sections), milestones, risks & cut list. The single synthesis artifact.

**Output**

Summarize: GDD change name + location, which conditional sections were included (and why), artifacts created (one line each), and: "GDD complete - no implementation step. The change stays open; re-run `/opsx:gdd` to keep it current. Run `/opsx:architect` for technical architecture or `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is a GDD - the intended game (WHAT it is and HOW it plays/looks/sounds/sells). NOT formal requirements (`/opsx:require`), NOT architecture (`/opsx:architect`), NOT code/tasks.
- Change name is `{program}-gdd` (project singleton). Don't invent per-feature names; continue the existing one unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/gdd/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Show, don't only tell: diagrams/flows/mockups follow `openspec/rules/diagrams.md`. LINK mood boards and reference images - never embed binaries or paste long asset dumps.
- State each fact once; each concern in exactly one section. `production` is the only synthesis artifact and may restate features by reference.
- If a requirements change exists, reference its goals/requirements/invariants by id rather than re-deriving the formal model - add the player-facing design on top.
- The user often narrates the GDD one line (one message) at a time. RECEIVE each line, reflect it back accurately, and capture it in the right section. Do NOT interrupt that flow with scope/stop questions. Only ask about a genuine fork.
- Do NOT manufacture "out of scope / later" deferrals. Only exclude what the user explicitly excluded.
- Omit a conditional section entirely if its concern is absent - never create an empty placeholder.
- The change does not close. There is no apply step in the gdd schema.
- Read source requirements + dependency GDD artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/rules/writing.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, one-value-per-cell tables, ISO 8601 dates.
- **Structure:** follow `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
