---
name: "OPSX: Architect"
version: "1.2.0"
description: Technical architecture from a requirements change - 4+1 views + arc42 + ISO 42010 + ADRs. No implementation.
category: Workflow
tags: [workflow, architect, architecture, 4+1, arc42, adr, experimental]
---

Architect a system - technical architecture, separate from both requirements and development. This uses the `architecture` schema (Kruchten 4+1 views, framed as ISO/IEC 42010 viewpoints, structured with arc42, decisions as Nygard ADRs, traced back to requirements with a BABOK RTM). It produces:

**Core views (always):**

- overview.md (solution strategy, tech stack, style, constraints, + the role->view map)
- logical-view.md (4+1 Logical / arc42 Building Block - functional decomposition)
- deployment-view.md (4+1 Physical / C4 Deployment - topology)
- crosscutting-concepts.md (arc42 sec.8 - security, compliance, logging, ...)
- adr.md (Nygard Architecture Decision Records)
- traceability.md (requirements <-> architecture RTM, role coverage)

**Conditional views (only when the system has that concern):**

- process-view.md - non-trivial runtime/concurrency/messaging
- data-view.md - persistent state / a database
- ml-serving-view.md - model inference

This pipeline answers HOW (structure, technology, runtime, deployment); requirements already answered WHAT/WHY. There is **no implementation/apply step** and the change stays open - you can keep adding tech-stack and architecture decisions over time.

---

**Input**: The argument after `/opsx:architect` is the architecture change name (kebab-case) OR a description. A requirements change to build on may be named too (e.g. `--from kist-safety-platform`).

**Steps**

1. **Identify the source requirements change.** Architecture builds on requirements artifacts. If the user named one, use it. Otherwise list `openspec/changes/*/` that contain `requirements-document.md` and ask which to build on. If there is genuinely no requirements change, proceed from whatever requirements the user gives, but say so.

2. **Decide which CONDITIONAL views to include - recommend, then confirm.**
   - Read the source requirements artifacts (`requirements-document.md`, `operation-model.md`, `object-model.md`).
   - Auto-recommend: include **process-view** if there is non-trivial runtime/concurrency/real-time flow; **data-view** if there is persistent state or a database; **ml-serving-view** if the system performs model inference.
   - Present the recommendation (each view: include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core views are not negotiable.

3. **Determine the change name - `{program}-architecture`.** The architecture schema has no apply step and is a **project-level singleton** - normally one technical architecture per program.
   - If a `*-architecture` change already exists, that is this project's architecture - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source requirements program, e.g. `tycoon` from `tycoon-requirements`); the user may give a different fixed name. The change name is then `{program}-architecture`.
   - To keep multiple parallel architectures (e.g. two products in one repo), the user gives distinct program names -> `{a}-architecture`, `{b}-architecture`.

4. **Create the architecture change**

   ```bash
   openspec new change "{program}-architecture" --schema architecture
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/architecture/templates/README.md` to `openspec/changes/{program}-architecture/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/architecture/templates/README.ko.md` to `openspec/changes/{program}-architecture/README.ko.md`. These static guides are identical for every architecture change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-architecture" --json
   ```

   Build in dependency order: `overview -> logical-view -> (process/data/ml-serving) -> deployment-view -> crosscutting-concepts -> adr -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-architecture" --json`
   - Read the relevant source requirements files AND any completed dependency architecture files for context.
   - **For conditional views the user excluded in step 2: do NOT create the file.** Leave it absent - the schema lists it but an omitted view simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-architecture" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-architecture"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - arc42 sec.1,3,4 + the ISO/IEC 42010 stakeholder<->concern<->view map. This map is how each role finds its reading list; it lives ONLY here.
- **logical-view** - 4+1 Logical / C4 Container+Component. Static functional structure; map components to requirements responsibility-model agents by id.
- **process-view** - 4+1 Process / arc42 Runtime. Runtime flows tracing to requirements operations by name.
- **data-view** - solution-level schema derived from the requirements object-model; honor data invariants (minimization, retention) by id.
- **ml-serving-view** - inference pipeline tracing to requirements operations; note on-premise/local-weights constraints.
- **deployment-view** - 4+1 Physical / C4 Deployment. Map logical containers onto nodes.
- **crosscutting-concepts** - arc42 sec.8. Map compliance concepts to requirements goals/obstacles by id.
- **adr** - Nygard format; append-only, supersede rather than rewrite; cite the requirements constraint/obstacle a decision is forced by.
- **traceability** - BABOK RTM; confirm every role in the view map has coverage.

**Output**

Summarize: architecture change name + location, which conditional views were included (and why), artifacts created (one line each), and: "Technical architecture complete - no implementation step. The change stays open; re-run `/opsx:architect <name>` to add more architecture decisions. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is ARCHITECTURE (HOW), not requirements (WHAT/WHY) and not implementation. NO code, NO tasks. Diagrams, interface signatures, schemas, config-level detail are fine; source files are not.
- Diagrams follow `openspec/rules/diagrams.md`.
- Do NOT restate the requirements as prose - reference them by id and link only in traceability.
- Reference each fact once; a structural fact belongs to exactly one view. Rationale lives in ADRs, not in view prose.
- The user often narrates decisions one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right view/ADR. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- Omit a conditional view entirely if its concern is absent - never create an empty placeholder.
- The change does not close. There is no apply step in the architecture schema.
- Change name is `{program}-architecture` (project singleton). Don't invent per-feature names; continue the existing `*-architecture` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/architecture/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source requirements + dependency architecture artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/rules/writing.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, ISO 8601 dates.
- **Structure:** follow `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
