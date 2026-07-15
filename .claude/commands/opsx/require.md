---
name: "OPSX: Require"
version: "1.1.1"
description: Specify the requirements for a change using KAOS/GORE + BABOK - business requirements, goal/object/responsibility/operation models, synthesized requirements document, traceability. No implementation.
category: Workflow
tags: [workflow, require, babok, kaos, gore, experimental]
---

Capture the requirements for a change - requirements engineering, separate from development. This uses the `requirements` schema (KAOS/GORE under a BABOK structure). It produces:

- business-requirements.md (stakeholder statements, verbatim - the single source of truth)
- goal-model.md (KAOS goal hierarchy AND/OR, domain properties, obstacles, resolved conflicts)
- object-model.md (entities, relationships, attributes, invariants, glossary)
- responsibility-model.md (each leaf goal assigned to a responsible agent)
- operation-model.md (operations with pre/post/trigger, scenarios)
- requirements-document.md (the single synthesis: scope, goals, glossary, responsibilities, behavior)
- traceability.md (BR <-> goal <-> leaf <-> agent <-> operation matrix)

This pipeline stops at requirements - there is **no implementation/apply step**. When you decide to build, run `/opsx:propose` (spec-driven) and feed these requirements artifacts in as the source.

---

**Input**: The argument after `/opsx:require` is a description of what to capture, OR the program name.

**Steps**

1. **If no input provided, ask what they want to capture** (open-ended, no preset options).

2. **Determine the change name - `{program}-requirements`.** The requirements schema has no apply step and is a **project-level singleton** - normally one requirements change per program.
   - If a `*-requirements` change already exists, that is this project's requirements - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name; the user may give a different fixed name. The change name is then `{program}-requirements`.
   - To keep multiple parallel requirements changes (e.g. two products in one repo), the user gives distinct program names -> `{a}-requirements`, `{b}-requirements`.

3. **Create the requirements change**

   ```bash
   openspec new change "{program}-requirements" --schema requirements
   ```

4. **Write the folder README (reading guide).** Copy `openspec/schemas/requirements/templates/README.md` to `openspec/changes/{program}-requirements/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/requirements/templates/README.ko.md` to `openspec/changes/{program}-requirements/README.ko.md`. These static guides are identical for every requirements change - copy verbatim, do NOT hand-edit them per project.

5. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-requirements" --json
   ```

   Parse `artifacts` (status + dependencies). Build in dependency order: `business-requirements -> goal-model -> object-model, responsibility-model -> operation-model -> requirements-document -> traceability`.

6. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-requirements" --json`
   - Read any completed dependency files for context.
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-requirements" --json` and continue with the next `ready` artifact until all are `done`.

7. **Show final status**: `openspec status --change "{program}-requirements"`

**Methodology guidance (apply when filling artifacts)**

- **business-requirements** - preserve stakeholder statements VERBATIM (BR ids), classify [Goal]/[Constraint], keep conflicting statements both and mark the conflict. No analysis.
- **goal-model** - KAOS/GORE: refine goals AND/OR to leaves (G1.2 = AND, G1.2.a = OR), keyword each (Achieve/Maintain/Avoid/Cease), mark leaves [Requirement]/[Expectation]; record domain properties, obstacles+resolutions, and resolve BR conflicts here.
- **object-model** - entities, relationships (cardinality lives here only), attributes, invariants (rules not expressible as cardinality), glossary. Conceptual, not a DB schema.
- **responsibility-model** - assign every leaf goal to exactly one agent (software=requirement, environment=expectation); no orphans.
- **operation-model** - operationalize leaves into operations (pre/post/trigger), plus scenarios (Given/When/Then); don't restate agent ownership (that's traceability).
- **requirements-document** - the ONE synthesis: Scope, Goals, Glossary, Responsibilities, Behavior. Self-contained, current truth, no cross-references.
- **traceability** - bidirectional matrix BR<->goal<->leaf<->agent<->operation; all cross-linking lives here, never in model prose.

**Output**

Summarize: change name + location, artifacts created (one line each), and: "Requirements complete - no implementation step. Run `/opsx:propose` (spec-driven) when ready to build, using these requirements artifacts as the source."

**Guardrails**

- This is REQUIREMENTS. Do NOT produce technical design, tasks, or implementation. Do NOT try to move to apply - the requirements schema has no apply step.
- Change name is `{program}-requirements` (project singleton). Don't invent per-feature names; continue the existing one unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/requirements/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- The user often narrates the requirements one line (one message) at a time. RECEIVE each line, reflect it back accurately, and capture it in the artifacts. Do NOT interrupt that flow with "how far should this go / should we stop / scope?" questions. Only ask about a genuine fork in behavior, not to limit work.
- Do NOT manufacture "out of scope / later" deferrals. Only exclude what the user explicitly excluded.
- Read dependency artifacts before creating the next one.
- **Superseding a requirements change:** the singleton convention means you normally keep refining the same `{program}-requirements`. If the user wants a clean restart that replaces it, move the OLD change into `openspec/changes/archive/<name>/` with a plain folder move (`mv`), NOT `openspec archive` (that promotes artifacts into specs, wrong for requirements). Confirm first; tell them the old requirements change is preserved under `archive/`, not deleted.
- Verify each artifact file exists after writing before proceeding.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/WRITING-STYLE.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, ISO 8601 dates.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit - `chore: migrate <change> to schema <x.y.z>`. Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
