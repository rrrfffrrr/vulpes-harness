<!-- vulpes-harness 1.2.0 - the "# vulpes-harness" section is harness-managed: update it by re-copying from the harness repo. Every other h1 section (e.g. "# Project") is project-owned; the harness never touches those. -->

# vulpes-harness

## Index

- `specs/` - capability specs, promoted by `openspec archive` from applied spec-driven changes
- `changes/` - in-flight spec-driven changes AND the standing documents below
- `changes/archive/` - completed changes and superseded standing documents
- `schemas/` - vulpes-harness workflow schemas (requirements, gdd, architecture, backend, frontend, persistence, game-ui, verification)
- `DIAGRAM-STYLE.md` - diagram rules for the schemas
- `WRITING-STYLE.md` - prose rules for artifact writing (reader-first, search-friendly)

## Standing documents live in changes/

`specs/` is NOT the whole current truth.
The vulpes-harness schemas keep project-level singleton changes that are living documents - permanently open, no apply step:

- `changes/{program}-requirements/` - KAOS/GORE + BABOK requirements.
  Start: `requirements-document.md`
- `changes/{program}-gdd/` - Game Design Document.
  Start: `overview.md`
- `changes/{program}-architecture/` - technical architecture (4+1 / arc42 / ADR).
  Start: `overview.md`
- `changes/{program}-backend/` - backend interface contracts (OpenAPI / RFC / C4).
  Start: `overview.md`
- `changes/{program}-frontend/` - frontend app-UI detail design (IFML / wireflows / UI Stack).
  Start: `overview.md`
- `changes/{program}-persistence/` - persistence store-level data design (ANSI/SPARC internal level / polyglot persistence / evolutionary migrations).
  Start: `overview.md`
- `changes/{program}-game-ui/` - game UI detail design (UI layers / safe areas / action-based input).
  Start: `overview.md`
- `changes/{program}-verification/` - acceptance & verification design (ISTQB test basis / 29119-3 / Gherkin scenarios).
  Start: `overview.md`

Each of these folders has a `README.md` index (file -> role, reading order).
Read it before reading or editing any artifact in the folder.
Treat these changes as current truth alongside `specs/`.

## Rules

- NEVER run `openspec archive` on a `*-requirements` / `*-gdd` / `*-architecture` change - archive promotes artifacts into `specs/`, which is wrong for these schemas.
  To supersede one, `mv` the folder into `changes/archive/`.
- Update standing documents only via `/opsx:require`, `/opsx:gdd`, `/opsx:architect`, `/opsx:backend`, `/opsx:frontend`, `/opsx:persistence`, `/opsx:game-ui`, `/opsx:verification` - continue the existing singleton change; never create per-feature copies.
- Artifact prose follows `WRITING-STYLE.md` (this folder): semantic line breaks, plain language, front-loaded scannable structure, one term per concept, searchable headings and verbatim literals.
- Every artifact in these changes starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write).
  Increment `document-version` by 1 whenever you revise an artifact; never change `schema-version` by hand (per-version schema changes: `schemas/<schema>/CHANGES.md`).
- If an artifact's `schema-version` is older than the schema's `metadata.version` (no frontmatter = pre-1.1.0), apply the Migration sections in `schemas/<schema>/CHANGES.md` in order before editing further.
  Migrate from a clean git working tree and commit the migration by itself, labeled with the change name and target schema version in the project's own commit convention - git is the backup and the history; no backup copies, no migration log.
- Ordinary spec-driven changes (`/opsx:propose` -> `/opsx:apply` -> `/opsx:archive`) are unaffected by all of the above.
