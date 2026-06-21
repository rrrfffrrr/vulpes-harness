---
name: "OPSX: Design"
description: Technical architecture design from a planning change - 4+1 views + arc42 + ISO 42010 + ADRs. No implementation.
category: Workflow
tags: [workflow, design, architecture, 4+1, arc42, adr, experimental]
---

Design the technical architecture for a system - solution design, separate from both planning and development. This uses the `design` schema (Kruchten 4+1 views, framed as ISO/IEC 42010 viewpoints, structured with arc42, decisions as Nygard ADRs, traced back to planning with a BABOK RTM). It produces:

**Core views (always):**
- architecture-overview.md (solution strategy, tech stack, style, constraints, + the role->view map)
- logical-view.md (4+1 Logical / arc42 Building Block - functional decomposition)
- deployment-view.md (4+1 Physical / C4 Deployment - topology)
- crosscutting-concepts.md (arc42 sec.8 - security, compliance, logging, ...)
- adr.md (Nygard Architecture Decision Records)
- design-traceability.md (planning <-> design RTM, role coverage)

**Conditional views (only when the system has that concern):**
- process-view.md - non-trivial runtime/concurrency/messaging
- data-view.md - persistent state / a database
- ml-serving-view.md - model inference

This pipeline answers HOW (structure, technology, runtime, deployment); planning already answered WHAT/WHY. There is **no implementation/apply step** and the change stays open - you can keep adding tech-stack and architecture decisions over time.

---

**Input**: The argument after `/opsx:design` is the design change name (kebab-case) OR a description. A planning change to build on may be named too (e.g. `--from kist-safety-platform`).

**Steps**

1. **Identify the source planning change.** Design builds on planning artifacts. If the user named one, use it. Otherwise list `openspec/changes/*/` that contain `requirements-document.md` and ask which to build on. If there is genuinely no planning change, proceed from whatever requirements the user gives, but say so.

2. **Decide which CONDITIONAL views to include - recommend, then confirm.**
   - Read the source planning artifacts (`requirements-document.md`, `operation-model.md`, `object-model.md`).
   - Auto-recommend: include **process-view** if there is non-trivial runtime/concurrency/real-time flow; **data-view** if there is persistent state or a database; **ml-serving-view** if the system performs model inference.
   - Present the recommendation (each view: include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core views are not negotiable.

3. **Determine the change name - `{program}-design`.** The design schema has no apply step and is a **project-level singleton** - normally one technical design per program.
   - If a `*-design` change already exists, that is this project's design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source planning program, e.g. `tycoon` from `tycoon-plan`); the user may give a different fixed name. The change name is then `{program}-design`.
   - To keep multiple parallel designs (e.g. two products in one repo), the user gives distinct program names -> `{a}-design`, `{b}-design`.

4. **Create the design change**
   ```bash
   openspec new change "{program}-design" --schema design
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/design/change-README.md` to `openspec/changes/{program}-design/README.md`, overwriting the stub `openspec new change` created. This static guide is identical for every design change - copy verbatim, do NOT hand-edit it per project.

6. **Get the artifact build order**
   ```bash
   openspec status --change "{program}-design" --json
   ```
   Build in dependency order: `architecture-overview -> logical-view -> (process/data/ml-serving) -> deployment-view -> crosscutting-concepts -> adr -> design-traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-design" --json`
   - Read the relevant source planning files AND any completed dependency design files for context.
   - **For conditional views the user excluded in step 2: do NOT create the file.** Leave it absent - the schema lists it but an omitted view simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-design" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-design"`

**Methodology guidance (apply when filling artifacts)**

- **architecture-overview** - arc42 sec.1,3,4 + the ISO/IEC 42010 stakeholder<->concern<->view map. This map is how each role finds its reading list; it lives ONLY here.
- **logical-view** - 4+1 Logical / C4 Container+Component. Static functional structure; map components to planning responsibility-model agents by id.
- **process-view** - 4+1 Process / arc42 Runtime. Runtime flows tracing to planning operations by name.
- **data-view** - solution-level schema derived from the planning object-model; honor data invariants (minimization, retention) by id.
- **ml-serving-view** - inference pipeline tracing to planning operations; note on-premise/local-weights constraints.
- **deployment-view** - 4+1 Physical / C4 Deployment. Map logical containers onto nodes.
- **crosscutting-concepts** - arc42 sec.8. Map compliance concepts to planning goals/obstacles by id.
- **adr** - Nygard format; append-only, supersede rather than rewrite; cite the planning constraint/obstacle a decision is forced by.
- **design-traceability** - BABOK RTM; confirm every role in the view map has coverage.

**Output**

Summarize: design change name + location, which conditional views were included (and why), artifacts created (one line each), and: "Technical design complete - no implementation step. The change stays open; re-run `/opsx:design <name>` to add more architecture decisions. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**
- This is DESIGN (HOW), not planning (WHAT/WHY) and not implementation. NO code, NO tasks. Diagrams-as-text, interface signatures, schemas, config-level detail are fine; source files are not.
- Do NOT restate planning requirements as prose - reference them by id and link only in design-traceability.
- Reference each fact once; a structural fact belongs to exactly one view. Rationale lives in ADRs, not in view prose.
- The user often narrates decisions one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right view/ADR. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- Omit a conditional view entirely if its concern is absent - never create an empty placeholder.
- The change does not close. There is no apply step in the design schema.
- Change name is `{program}-design` (project singleton). Don't invent per-feature names; continue the existing `*-design` unless the user wants a separate program.
- The folder README.md is a verbatim copy of `openspec/schemas/design/change-README.md` - never hand-write or edit it per project.
- Read source planning + dependency design artifacts before creating the next one. Verify each file exists after writing.
