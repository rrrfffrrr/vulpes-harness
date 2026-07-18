---
name: opsx-ml
version: "1.2.0"
description: ML detail design from an architecture change with an ml-serving-view - per-model contracts, evaluation gates, lifecycle procedures. No implementation.
---

Design the models in detail - the per-model contracts one level below the architecture ml-serving-view and separate from development. This uses the `ml` schema (Model Cards for Model Reporting, Datasheets for Datasets, The ML Test Score, ISO/IEC 5338 lifecycle vocabulary). It produces:

**Core artifacts (always):**

- overview.md (model inventory: task, inference location, consuming surfaces; reader map)
- models.md (per-model contracts: intended use, I/O with confidence semantics, degradation/fallback, caveats)
- evaluation.md (pass/fail release gates on named datasets and slices, regression policy, monitoring signals)
- lifecycle.md (versioning, update/rollback procedures, retraining triggers, deprecation)
- traceability.md (operation <-> model <-> surfaces <-> gates matrix)

**Conditional artifact (only when the project owns training/fine-tuning data):**

- data.md - owned datasets as Datasheets (composition, collection, labeling, splits, refresh, PII)

This pipeline answers the MODEL CONTRACTS (what each model accepts, returns, and guarantees, and how quality is gated); the ml-serving-view already answered pipeline shape, serving mode, and hardware. Contracts are inference-location invariant - the serving API surface stays in the backend change and on-device consumption in frontend/game-ui, all referencing models by name. There is **no implementation/apply step** and the change stays open - you can keep adding models and refining gates over time.

---

**Input**: The argument after `/opsx:ml` is a description OR the program name. An architecture change to build on may be named too (e.g. `--from tycoon-architecture`).

**Steps**

1. **Identify the source architecture change.** ML detail design builds on the ml-serving-view. If the user named a change, use it. Otherwise list `openspec/changes/*-architecture/` and ask which to build on. If the architecture has NO ml-serving-view (no model inference), say so and stop - there is nothing to design.

2. **Decide whether the CONDITIONAL artifact applies - recommend, then confirm.**
   - Auto-recommend: include **data** if the project trains or fine-tunes on its own data; exclude it when every model is third-party or a pretrained API.
   - Present the recommendation (include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core artifacts are not negotiable.

3. **Determine the change name - `{program}-ml`.** The ml schema has no apply step and is a **project-level singleton** - normally one ML detail design per program.
   - If a `*-ml` change already exists, that is this project's ML design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source architecture program); the user may give a different fixed name. The change name is then `{program}-ml`.
   - To keep multiple parallel ML designs, the user gives distinct program names -> `{a}-ml`, `{b}-ml`.

4. **Create the ml change**

   ```bash
   openspec new change "{program}-ml" --schema ml
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/ml/templates/README.md` to `openspec/changes/{program}-ml/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/ml/templates/README.ko.md` to `openspec/changes/{program}-ml/README.ko.md`. These static guides are identical for every ml change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-ml" --json
   ```

   Build in dependency order: `overview -> models, (data) -> evaluation -> lifecycle -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-ml" --json`
   - Read the relevant source architecture files (ml-serving-view, ADRs) AND any completed dependency ml files for context.
   - **If the user excluded data in step 2: do NOT create the file.** Leave it absent - an omitted artifact simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-ml" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-ml"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the model inventory (task one-liner, inference location per ml-serving-view, consuming surfaces by name), reader map, conditional inclusion.
- **models** - Model Cards at design altitude: intended + out-of-scope use, I/O tables with confidence semantics, quality targets by reference, degradation/fallback per unavailable/timeout/low-confidence, caveats with factors. LLM prompt templates referenced by name only.
- **data** - Datasheets: motivation, composition, collection/labeling with known biases, splits and leakage rules, refresh, PII per requirements/persistence ids.
- **evaluation** - pass/fail release gates on named datasets and slices; regression policy naming what must not regress; monitoring signals referencing architecture observability conventions.
- **lifecycle** - procedures only (the view keeps the approach): versioning tying model+data+config, update procedure gated by evaluation, rollback with time bound and co-rolled state, retraining triggers (jobs by name, drift, refresh), deprecation.
- **traceability** - operation <-> model <-> surfaces <-> gates (+ dataset column when data exists), plus gaps (ungated models, unconsumed models, model-less inference steps).

**Output**

Summarize: ml change name + location, whether data was included (and why), artifacts created (one line each), and: "ML detail design complete - no implementation step. The change stays open; re-run `/opsx:ml` to add models or refine gates. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is MODEL-LEVEL detail design, below the ml-serving-view (pipeline/serving/hardware) and above implementation. NO code, NO notebooks, NO training configs. Contract and metric tables are the medium; source files are not.
- Diagrams follow `openspec/DIAGRAM-STYLE.md`.
- Do NOT restate the ml-serving-view or requirements - reference views, components, targets, and ADRs by name/id.
- Contracts are inference-location invariant - never fork a model's contract per server/on-device/edge.
- Every model contract includes degradation/fallback (unavailable, timeout, low confidence) - a contract without them is incomplete.
- Every model has at least one pass/fail release gate; a model without a gate is a traceability gap.
- The serving API surface belongs to the backend change; on-device consumption to frontend/game-ui - reference models by name, do not document surfaces here.
- LLM-based models follow the same contract structure; prompt templates are project assets referenced by name, never restated or structured here.
- The user often narrates contracts one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- Omit data entirely when all models are third-party/pretrained - never create an empty placeholder.
- The change does not close. There is no apply step in the ml schema.
- Change name is `{program}-ml` (project singleton). Don't invent per-feature names; continue the existing `*-ml` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/ml/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source architecture + dependency ml artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/WRITING-STYLE.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, ISO 8601 dates.
- **Structure:** follow `openspec/CONVENTIONS.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
