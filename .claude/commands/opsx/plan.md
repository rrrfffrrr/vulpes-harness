---
name: "OPSX: Plan"
description: Plan a change using KAOS/GORE + BABOK - business requirements, goal/object/responsibility/operation models, synthesized requirements document, traceability. No implementation.
category: Workflow
tags: [workflow, planning, babok, kaos, gore, experimental]
---

Plan a change - pure planning, separate from development. This uses the `planning` schema (KAOS/GORE under a BABOK structure). It produces:
- business-requirements.md (stakeholder statements, verbatim - the single source of truth)
- goal-model.md (KAOS goal hierarchy AND/OR, domain properties, obstacles, resolved conflicts)
- object-model.md (entities, relationships, attributes, invariants, glossary)
- responsibility-model.md (each leaf goal assigned to a responsible agent)
- operation-model.md (operations with pre/post/trigger, scenarios)
- requirements-document.md (the single synthesis: scope, goals, glossary, responsibilities, behavior)
- traceability.md (BR <-> goal <-> leaf <-> agent <-> operation matrix)

This pipeline stops at planning - there is **no implementation/apply step**. When you decide to build, run `/opsx:propose` (spec-driven) and feed these planning artifacts in as the source.

---

**Input**: The argument after `/opsx:plan` is a description of what to plan, OR the program name.

**Steps**

1. **If no input provided, ask what they want to plan** (open-ended, no preset options).

2. **Determine the change name - `{program}-plan`.** The planning schema has no apply step and is a **project-level singleton** - normally one plan per program.
   - If a `*-plan` change already exists, that is this project's plan - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name; the user may give a different fixed name. The change name is then `{program}-plan`.
   - To keep multiple parallel plans (e.g. two products in one repo), the user gives distinct program names -> `{a}-plan`, `{b}-plan`.

3. **Create the planning change**
   ```bash
   openspec new change "{program}-plan" --schema planning
   ```

4. **Write the folder README (reading guide).** Copy `openspec/schemas/planning/change-README.md` to `openspec/changes/{program}-plan/README.md`, overwriting the stub `openspec new change` created. This static guide is identical for every planning change - copy verbatim, do NOT hand-edit it per project.

5. **Get the artifact build order**
   ```bash
   openspec status --change "{program}-plan" --json
   ```
   Parse `artifacts` (status + dependencies). Build in dependency order: `business-requirements -> goal-model -> object-model, responsibility-model -> operation-model -> requirements-document -> traceability`.

6. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-plan" --json`
   - Read any completed dependency files for context.
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-plan" --json` and continue with the next `ready` artifact until all are `done`.

7. **Show final status**: `openspec status --change "{program}-plan"`

**Methodology guidance (apply when filling artifacts)**

- **business-requirements** - preserve stakeholder statements VERBATIM (BR ids), classify [Goal]/[Constraint], keep conflicting statements both and mark the conflict. No analysis.
- **goal-model** - KAOS/GORE: refine goals AND/OR to leaves (G1.2 = AND, G1.2.a = OR), keyword each (Achieve/Maintain/Avoid/Cease), mark leaves [Requirement]/[Expectation]; record domain properties, obstacles+resolutions, and resolve BR conflicts here.
- **object-model** - entities, relationships (cardinality lives here only), attributes, invariants (rules not expressible as cardinality), glossary. Conceptual, not a DB schema.
- **responsibility-model** - assign every leaf goal to exactly one agent (software=requirement, environment=expectation); no orphans.
- **operation-model** - operationalize leaves into operations (pre/post/trigger), plus scenarios (Given/When/Then); don't restate agent ownership (that's traceability).
- **requirements-document** - the ONE synthesis: Scope, Goals, Glossary, Responsibilities, Behavior. Self-contained, current truth, no cross-references.
- **traceability** - bidirectional matrix BR<->goal<->leaf<->agent<->operation; all cross-linking lives here, never in model prose.

**Output**

Summarize: change name + location, artifacts created (one line each), and: "Planning complete - no implementation step. Run `/opsx:propose` (spec-driven) when ready to build, using these planning artifacts as the source."

**Guardrails**
- This is PLANNING. Do NOT produce technical design, tasks, or implementation. Do NOT try to move to apply - the planning schema has no apply step.
- Change name is `{program}-plan` (project singleton). Don't invent per-feature names; continue the existing one unless the user wants a separate program.
- The folder README.md is a verbatim copy of `openspec/schemas/planning/change-README.md` - never hand-write or edit it per project.
- The user often narrates the plan one line (one message) at a time. RECEIVE each line, reflect it back accurately, and capture it in the artifacts. Do NOT interrupt that flow with "how far should this go / should we stop / scope?" questions. Only ask about a genuine fork in behavior, not to limit work.
- Do NOT manufacture "out of scope / 후속" deferrals. Only exclude what the user explicitly excluded.
- Read dependency artifacts before creating the next one.
- **Superseding a plan:** the singleton convention means you normally keep refining the same `{program}-plan`. If the user wants a clean restart that replaces it, move the OLD change into `openspec/changes/archive/<name>/` with a plain folder move (`mv`), NOT `openspec archive` (that promotes artifacts into specs, wrong for planning). Confirm first; tell them the old plan is preserved under `archive/`, not deleted.
- Verify each artifact file exists after writing before proceeding.
