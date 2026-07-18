---
name: opsx-persistence
version: "1.2.0"
description: Persistence detail design from an architecture change - store-level data design, access patterns, migrations. No implementation.
---

Design the data stores in detail - the store-level data design one level below the architecture data-view and separate from development. This uses the `persistence` schema (ANSI/SPARC internal level, polyglot persistence per Sadalage & Fowler, access-pattern-driven store design, evolutionary database design per Ambler & Sadalage). It produces:

**Artifacts (always, in dependency order):**

- overview.md (store inventory with engine + deciding ADR or OPEN, data domains, reader map)
- model.md (store-agnostic logical detail: ER diagram, full field lists, integrity, retention/PII classes)
- stores.md (per-store design: native units, keys/indexes, access patterns, consistency/durability, retention mechanisms, engine-specific features)
- migrations.md (migration policy, expand-contract for breaking changes, seed data, backfills)
- traceability.md (object <-> entity <-> store <-> access-pattern matrix)

This pipeline answers HOW DATA IS STORED AND EVOLVED (units, keys, indexes, migrations); the architecture data-view already answered the logical model and ownership, and the backend schema owns the interfaces over it. There is **no implementation/apply step** and the change stays open - you can keep adding stores and refining designs over time.

---

**Input**: The argument after `/opsx:persistence` is a description OR the program name. An architecture change to build on may be named too (e.g. `--from tycoon-architecture`).

**Steps**

1. **Identify the source architecture change.** Persistence detail design builds on the architecture data-view. If the user named a change, use it. Otherwise list `openspec/changes/*-architecture/` and ask which to build on. If the architecture has NO data-view (no persistent state), say so and stop - there is nothing to design.

2. **Identify the stores and their engine status.** From the data-view and ADRs, list the stores this design covers. For each store, find the ADR that fixed its engine; when the engine is undecided or contested (e.g. a company standard vs a team preference), record it as OPEN with the candidates - the decision lands as an architecture ADR later, not here.

3. **Determine the change name - `{program}-persistence`.** The persistence schema has no apply step and is a **project-level singleton** - normally one persistence design per program.
   - If a `*-persistence` change already exists, that is this project's persistence design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source architecture program); the user may give a different fixed name. The change name is then `{program}-persistence`.
   - To keep multiple parallel persistence designs, the user gives distinct program names -> `{a}-persistence`, `{b}-persistence`.

4. **Create the persistence change**

   ```bash
   openspec new change "{program}-persistence" --schema persistence
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/persistence/templates/README.md` to `openspec/changes/{program}-persistence/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/persistence/templates/README.ko.md` to `openspec/changes/{program}-persistence/README.ko.md`. These static guides are identical for every persistence change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-persistence" --json
   ```

   Build in dependency order: `overview -> model -> stores -> migrations -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-persistence" --json`
   - Read the relevant source architecture files (data-view, ADRs) AND any completed dependency persistence files for context.
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-persistence" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-persistence"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the store inventory with engine + deciding ADR (or OPEN + candidates), data domains by requirements object ids, reader map.
- **model** - store-agnostic and full field level: ONE ER diagram (mermaid erDiagram, crow's foot) owning relationships and cardinality, then per entity logical types, constraints, nullability, integrity/cascade notes the diagram cannot carry, retention/PII class citing the requirements invariant. No store-native types.
- **stores** - per store: entity -> native unit mapping with keys/partitions/indexes, the access patterns each structure serves (patterns justify structure - query-first for non-relational stores), consistency/durability settings as design decisions, retention mechanisms (cleanup via backend jobs by name), engine-specific features keyed to the engine ADR. OPEN engine -> portable-only block + what the pending decision blocks.
- **migrations** - versioning/ordering, the compatibility window, expand-contract (expand -> dual-write -> backfill -> cut over -> contract) for breaking changes, seed data, backfills via backend jobs by name.
- **traceability** - object/invariant <-> entity <-> store/unit <-> access pattern, plus a gaps section (entities with no store, structures serving no pattern, unenforced retention invariants, OPEN engines).

**Output**

Summarize: persistence change name + location, the store inventory (engine decided/OPEN each), artifacts created (one line each), and: "Persistence detail design complete - no implementation step. The change stays open; re-run `/opsx:persistence` to add stores or refine designs. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is STORE-LEVEL detail design, below the architecture data-view and above implementation. NO code, NO migration scripts. Field tables, index/partition tables, access-pattern tables, and migration plans are the medium; DDL and source files are not.
- Diagrams follow `openspec/rules/diagrams.md`.
- Do NOT restate the data-view or requirements - reference entities, components, invariants, and ADRs by name/id.
- The logical detail (model) stays store-agnostic; every store-specific fact lives in that store's block in stores.md, keyed to the engine ADR.
- Never silently assume an engine. Undecided or contested engine -> the store is OPEN with candidates, its block stays engine-portable, and the engine-specific section is omitted.
- Access patterns justify structure: a unit or index serving no listed access pattern is a gap, not a feature.
- Interface behavior (endpoints, client-facing consistency guarantees) belongs to the backend schema - do not duplicate it here.
- The user often narrates the design one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- The change does not close. There is no apply step in the persistence schema.
- Change name is `{program}-persistence` (project singleton). Don't invent per-feature names; continue the existing `*-persistence` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/persistence/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source architecture + dependency persistence artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/rules/writing.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, one-value-per-cell tables, ISO 8601 dates.
- **Structure:** follow `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
