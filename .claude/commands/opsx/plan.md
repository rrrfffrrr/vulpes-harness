---
name: "OPSX: Plan"
description: Plan a change using BABOK + KAOS/GORE — vision, goal model, domain model, scenarios. No implementation.
category: Workflow
tags: [workflow, planning, babok, kaos, gore, experimental]
---

Plan a change — pure planning, separate from development. This uses the `planning` schema (BABOK + KAOS/GORE) and produces:
- vision.md (BABOK: need, stakeholders, value, context, solution scope, objectives)
- goal-model.md (KAOS: goal hierarchy, obstacles, agents/responsibilities)
- domain-model.md (entities, types, attributes, relationships, constraints)
- scenarios.md (user scenarios/flows tied to goals)

This pipeline stops at planning — there is **no implementation/apply step**. When you decide to build, run `/opsx:propose` (spec-driven) and feed these planning artifacts in as the source.

---

**Input**: The argument after `/opsx:plan` is the change name (kebab-case), OR a description of what to plan.

**Steps**

1. **If no input provided, ask what they want to plan** (open-ended, no preset options). Derive a kebab-case name from their description.

2. **Create the planning change**
   ```bash
   openspec new change "<name>" --schema planning
   ```

3. **Get the artifact build order**
   ```bash
   openspec status --change "<name>" --json
   ```
   Parse `artifacts` (with status + dependencies). Build them in dependency order: `vision → goal-model → domain-model → scenarios`.

4. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "<name>" --json`
   - Read any completed dependency files for context.
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU — do NOT copy them into the file.
   - Re-run `openspec status --change "<name>" --json` and continue with the next `ready` artifact until all are `done`.

5. **Show final status**: `openspec status --change "<name>"`

**Methodology guidance (apply when filling artifacts)**

- **vision** — BABOK BACCM: Need, Stakeholder, Value, Context, Change, Solution; plus Strategy Analysis: solution scope and measurable business objectives.
- **goal-model** — KAOS/GORE: refine high-level goals into subgoals (AND/OR), identify Obstacles per goal with resolutions, assign Agents (responsibility model) to leaf goals.
- **domain-model** — entities, types (and kinds), attributes, relationships, and constraints/invariants. Conceptual model, not a DB schema or code.
- **scenarios** — user scenarios/flows that satisfy goals over the domain; each links back to a goal and the operations/agents involved; Given/When/Then narration where helpful.

**Output**

Summarize: change name + location, artifacts created (one line each), and: "Planning complete — no implementation step. Run `/opsx:propose` (spec-driven) when ready to build, using these planning artifacts as the source."

**Guardrails**
- This is PLANNING. Do NOT produce technical design, tasks, or implementation. Do NOT try to move to apply — the planning schema has no apply step.
- The user often narrates the plan one line (one message) at a time. RECEIVE each line, reflect it back accurately, and capture it in the artifacts. Do NOT interrupt that flow with "how far should this go / should we stop / scope?" questions. Only ask about a genuine fork in behavior, not to limit work.
- Do NOT manufacture "out of scope / 후속" deferrals. Only exclude what the user explicitly excluded.
- Read dependency artifacts before creating the next one.
- If a change with that name already exists, ask whether to continue it or create a new one.
- Verify each artifact file exists after writing before proceeding.
