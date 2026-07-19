---
name: opsx-backend
version: "1.2.1"
description: Backend detail design from an architecture change - interface contracts, conventions, components, runtime sequences, events/webhooks/jobs/configuration. No implementation.
---

Design the backend in detail - exact interface contracts, one level below architecture and separate from development. This uses the `backend` schema (OpenAPI 3.2 + JSON Schema 2020-12 contracts under RFC 9110 semantics, RFC 9457 errors, RFC 9111 caching, BCP 14 keywords, UML 2.5.1 sequences, C4 Component inventory). It produces:

**Core artifacts (always):**

- overview.md (interface surfaces + styles, state management, reader map)
- conventions.md (the shared rulebook: auth scopes, versioning/deprecation, error catalog, pagination, rate-limit contract, idempotency, concurrency, caching, long-running operations (LRO))
- components.md (middleware pipeline in order + shared components, C4 Component level)
- endpoints.md (per-endpoint contracts - deviations from conventions only)
- sequences/index.md (domain index) + sequences/\<domain\>.md (backend-internal runtime flows incl. client-observable failure paths)
- traceability.md (operation <-> interface <-> component <-> sequence matrix)

**Conditional artifacts (only when the system has that concern):**

- events.md - message/event-driven APIs (AsyncAPI 3.1 structure, CloudEvents envelope)
- webhooks.md - outbound callbacks (Standard Webhooks conventions)
- jobs.md - time-triggered/background work (Spring Batch + Jakarta Batch vocabulary, Kubernetes CronJob overlap terms)
- configuration.md - config keys & feature flags catalog (12-factor III; names/types/defaults/effects, never per-environment values)

This pipeline answers the EXACT CONTRACTS (what each endpoint/channel accepts, returns, and guarantees); architecture already answered structure/technology. There is **no implementation/apply step** and the change stays open - you can keep adding and refining contracts over time.

---

**Input**: The argument after `/opsx:backend` is a description OR the program name. An architecture change to build on may be named too (e.g. `--from tycoon-architecture`).

**Steps**

1. **Identify the source architecture change.** Backend detail design builds on architecture artifacts. If the user named one, use it. Otherwise list `openspec/changes/*-architecture/` and ask which to build on. If there is genuinely no architecture change, proceed from what the user gives, but say so.

2. **Decide which CONDITIONAL artifacts to include - recommend, then confirm.**
   - Read the source architecture artifacts (`overview.md`, `logical-view.md`, `process-view.md` if present).
   - Auto-recommend: include **events** if the architecture has message/event-driven communication; include **webhooks** if the system delivers outbound callbacks to consumers; include **jobs** if the system runs scheduled/batch/background work outside its request/event surface (the architecture process-view usually shows it); include **configuration** if behavior varies between deploys (env config, feature flags).
   - Present the recommendation (each: include yes/no + one-line reason) and **ask the user to confirm or adjust** before creating the change. Core artifacts are not negotiable.

3. **Determine the change name - `{program}-backend`.** The backend schema has no apply step and is a **project-level singleton** - normally one backend detail design per program.
   - If a `*-backend` change already exists, that is this project's backend design - **continue it** (add/refine artifacts); do not create a second unless the user explicitly wants a separate one.
   - Otherwise, ask the **program name** once: default to the project/repo directory name (or the source architecture program); the user may give a different fixed name. The change name is then `{program}-backend`.
   - To keep multiple parallel backend designs, the user gives distinct program names -> `{a}-backend`, `{b}-backend`.

4. **Create the backend change**

   ```bash
   openspec new change "{program}-backend" --schema backend
   ```

5. **Write the folder README (reading guide).** Copy `openspec/schemas/backend/templates/README.md` to `openspec/changes/{program}-backend/README.md`, overwriting the stub `openspec new change` created, and `openspec/schemas/backend/templates/README.ko.md` to `openspec/changes/{program}-backend/README.ko.md`. These static guides are identical for every backend change - copy verbatim, do NOT hand-edit them per project.

6. **Get the artifact build order**

   ```bash
   openspec status --change "{program}-backend" --json
   ```

   Build in dependency order: `overview -> conventions, components -> endpoints -> sequences, (events, webhooks, jobs, configuration) -> traceability`.

7. **Create artifacts in sequence**

   For each artifact that is `ready`:
   - Get instructions: `openspec instructions <artifact-id> --change "{program}-backend" --json`
   - Read the relevant source architecture files AND any completed dependency backend files for context.
   - **For conditional artifacts the user excluded in step 2: do NOT create the file.** Leave it absent - an omitted artifact simply stays incomplete, which is correct for "no such concern."
   - Create the artifact using the `template` as structure and the `instruction` as guidance.
   - `context`/`rules` are constraints for YOU - do NOT copy them into the file.
   - Re-run `openspec status --change "{program}-backend" --json` and continue with the next `ready` artifact.

8. **Show final status**: `openspec status --change "{program}-backend"`

**Methodology guidance (apply when filling artifacts)**

- **overview** - surfaces + styles with ADR references (do not re-argue decisions), state model per surface (stateless JWT / stateful session), reader map, conditional inclusion table.
- **conventions** - every shared rule ONCE, in BCP 14 keywords: scope taxonomy, versioning + compatibility promise + deprecation, RFC 9457 error catalog with retryability, pagination/filtering, 429 + Retry-After contract, idempotency replay semantics, ETag/If-Match, RFC 9111 cache classes, LRO pattern, naming.
- **components** - the middleware pipeline as an ORDERED table (order is a contract) with per-stage rejection behavior; shared components at C4 Component altitude, deepening architecture logical-view names.
- **endpoints** - per endpoint: purpose + requirements operation, scopes, parameter/body tables with constraints, per-status responses using the error catalog, guarantees ONLY as deviations. Field constraints are the contract. One example pair max.
- **sequences** - sequences/index.md is the domain INDEX only (domains mirror the requirements scenarios domains where they exist, system seams otherwise); per-domain sequences/\<domain\>.md holds backend-internal multi-component flows only, happy + client-observable failure paths; lifelines = components.md names plus stores/brokers, the client at most one boundary lifeline (client-side behavior belongs to the frontend flows); show when events publish relative to writes. COVERAGE: walk endpoints/events/jobs item by item - every state-changing trigger is in a flow or explicitly single-component, and every outbound effect (publish, webhook, notification) appears in its trigger's flow.
- **events** - AsyncAPI channel structure, envelope stated once, delivery guarantees + consistency relation to the write path per channel.
- **webhooks** - Standard Webhooks: event types, signing, retry schedule, receiver MUSTs.
- **jobs** - defaults stated once (timezone, late start, overlap, retry); per job: trigger, run identity (identifying parameters), restart/rerun semantics, input scope, effects incl. write-vs-publish relation, failure, backfill.
- **configuration** - per key: name/type/default/reading component/effect (altered surface by name); flags add lifecycle (temporary vs permanent); secrets by name + consumer only. Never per-environment values.
- **traceability** - operation <-> interface <-> component <-> sequence, plus a gaps section.

**Output**

Summarize: backend change name + location, which conditional artifacts were included (and why), artifacts created (one line each), and: "Backend detail design complete - no implementation step. The change stays open; re-run `/opsx:backend` to add or refine contracts. Run `/opsx:propose` (spec-driven) when ready to build."

**Guardrails**

- This is INTERFACE-LEVEL detail design, below architecture (structure/technology) and above implementation. NO code, NO tasks. Payload schemas, header tables, and sequence diagrams are fine; source files are not.
- Diagrams follow `openspec/rules/diagrams.md`.
- Do NOT restate architecture - reference components, views, and ADRs by name/id.
- State each fact once: shared rules live in conventions; endpoints/events/webhooks/jobs record only deviations.
- Document externally observable behavior only: interface guarantees, not DB transaction boundaries. Observability conventions, SLOs, and capacity live in architecture crosscutting-concepts - do not duplicate them.
- Contract language uses BCP 14 keywords (MUST/SHOULD/MAY).
- The user often narrates contracts one line (one message) at a time. RECEIVE each line, reflect it back, capture it in the right artifact. Do NOT interrupt with scope/stop questions. Only ask about a genuine fork.
- Omit a conditional artifact entirely if its concern is absent - never create an empty placeholder.
- The change does not close. There is no apply step in the backend schema.
- Change name is `{program}-backend` (project singleton). Don't invent per-feature names; continue the existing `*-backend` unless the user wants a separate program.
- The folder README.md and README.ko.md are verbatim copies of `openspec/schemas/backend/templates/README.md` / `templates/README.ko.md` - never hand-write or edit them per project.
- Read source architecture + dependency backend artifacts before creating the next one. Verify each file exists after writing.
- **Artifact versioning:** every artifact keeps the frontmatter its template provides - `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter). First write leaves `document-version: 0`; every subsequent revision of that artifact increments it by 1 in the same edit. Never change `schema-version` by hand - it moves only when the artifact is reworked against a newer schema (see the schema's `CHANGES.md`).
- **Prose style:** follow `openspec/rules/writing.md` - semantic line breaks (one sentence per line), plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals, one-value-per-cell tables, ISO 8601 dates.
- **Structure:** follow `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- **Migration:** when continuing an existing change, if any artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), first apply that schema's `CHANGES.md` Migration sections in order, oldest to newest, then continue. Migration REQUIRES a clean git working tree (commit or stash first) and lands as its own commit, labeled with the change name and target schema version in the project's own commit convention (default when it has none: `chore: migrate <change> to schema <x.y.z>`). Git is both the backup and the migration history: never create backup copies or a separate migration log. If the project is not a git repository, stop and ask the user how to back up first.
