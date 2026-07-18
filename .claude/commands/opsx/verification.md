---
name: "OPSX: Verification"
version: "1.2.0"
description: Acceptance & verification design over the requirements and detail designs - cross-layer scenarios, test data/environment requirements. No implementation.
category: Workflow
tags: [workflow, verification, acceptance, qa, detail-design, experimental]
---

Design the acceptance layer - the thin verification design over the requirements and detail-design changes, separate from development. This uses the `verification` schema (ISTQB test-basis vocabulary, ISO/IEC/IEEE 29119-3 dynamic-level documentation types, Specification by Example with Gherkin, BABOK 10.1 acceptance criteria realized from the requirements operation-model). It produces:

**Artifacts (always, in dependency order):**

- overview.md (test basis, scope, explicit out-of-scope, reader map)
- scenarios.md (cross-layer acceptance scenarios in Gherkin, grouped by requirements operation)
- environment.md (test data requirements + test environment requirements)
- traceability.md (criterion <-> scenario <-> surfaces <-> environment matrix, with gaps)

This pipeline answers WHICH JOURNEYS PROVE THE ACCEPTANCE CRITERIA and what they need to run; the detail designs are the test basis, and per-contract test cases are DERIVED from those contracts (29119-4 techniques) - never written here. There is **no implementation/apply step** and the change stays open - you can keep adding scenarios as operations and designs grow.

---

**Input**: The argument after `/opsx:verification` is a description OR the program name. Source changes may be named too (e.g. `--from tycoon-requirements`).

**Steps**

1. **Identify the source changes.** Verification builds on the requirements change (the operation-model's acceptance criteria are what scenarios realize) plus every detail-design change present (`*-backend`, `*-frontend`, `*-persistence`, `*-game-ui`). If the user named changes, use them. Otherwise list `openspec/changes/` and confirm. If there is no requirements change, say so and stop - there is nothing to verify against.

2. **Check the acceptance criteria exist.** If the requirements operation-model predates acceptance criteria (authored against schema < 1.2.0, or the operations simply lack them), pause and run the requirements migration first (`/opsx:require` applies the CHANGES.md Migration sections) - scenarios without criteria to realize have no anchor.

3. **Determine the change name - `{program}-verification`.** The verification schema has no apply step and is a **project-level singleton** - normally one verification design per program.
   - If a `*-verification` change already exists, that is this project's verification design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source requirements program); the user may give a different fixed name. The change name is then `{program}-verification`.
   - To keep multiple parallel verification designs, the user gives distinct program names -> `{a}-verification`, `{b}-verification`.

4. **Create the verification change**

   ```bash
   openspec new change "{program}-verification" --schema verification
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/verification/templates/README.md` to `openspec/changes/{program}-verification/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/verification/templates/README.ko.md` to `openspec/changes/{program}-verification/README.ko.md`. These static guides are identical for every verification change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-verification" --json
   ```

   Build in dependency order: `overview -> scenarios -> environment -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-verification" --json`
   - Read the relevant source artifacts (operation-model, detail-design overviews and traceability) AND any completed dependency verification files for context.
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-verification" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-verification"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - the test basis by change/artifact name (ISTQB sense), operations in scope, explicit out-of-scope (derived test cases, performance/SLO), reader map.
- **scenarios** - grouped by requirements operation; per scenario: the acceptance criteria realized, the surfaces crossed by reference (endpoints METHOD+path, screens, flows, jobs, stores), Gherkin with 3-5 steps and concrete example values. Prefer journeys crossing layers; include the failure journeys acceptance depends on (frontend error mapping). One scenario proves one behavior.
- **environment** - test data requirements (data sets/states per scenario group, synthetic-data policy honoring persistence PII classes, reset/isolation) and test environment requirements (real vs stubbed, device/platform coverage by reference, clock control for jobs/retention). WHAT, never how to provision.
- **traceability** - criterion <-> scenario <-> surfaces <-> environment, plus gaps (unrealized criteria, anchorless scenarios, untested seams).

**Output**

Summarize: verification change name + location, the test basis (changes it builds on), artifacts created (one line each), coverage (criteria realized vs gaps), and: "Verification design complete - no implementation step. The change stays open; re-run `/opsx:verification` to add scenarios as operations and designs grow. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- THIN BY DESIGN: scenario selection and environment/data needs only. NO derived test cases (per-field validation, per-status checks) - those are generated from the detail-design contracts (29119-4 techniques). A per-contract test case in these artifacts should be deleted, not maintained.
- Never restate a contract: endpoints, screens, stores, jobs, and validation rules are referenced by name/METHOD+path only.
- Scenarios here are system-concrete; the requirements operation-model scenarios stay system-agnostic. Do not duplicate them - realize their acceptance criteria against the concrete design surfaces.
- Gherkin, 3-5 steps, concrete example values (Specification by Example). One scenario proves one behavior.
- Every scenario names the acceptance criteria it realizes; every criterion in scope ends up realized or in the traceability gaps.
- Performance/SLO verification is out of scope - targets live in the architecture crosscutting-concepts.
- The user often narrates scenarios one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- The change does not close. There is no apply step in the verification schema.
- Change name is `{program}-verification` (project singleton). Don't invent per-feature names; continue the existing `*-verification` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/verification/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source + dependency verification artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/WRITING-STYLE.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, one-value-per-cell tables, ISO 8601 dates.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
