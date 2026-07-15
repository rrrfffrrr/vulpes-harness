# Installing vulpes-harness

Procedure to add the harness to a project, on top of OpenSpec.

Run every command from the project root.

Wherever a tool name appears (`claude`, `codex`), use the one(s) the project actually uses.

## Prerequisites

- Node.js (LTS).
- OpenSpec CLI >= 1.4.x: `npm i -g @fission-ai/openspec`.

## 1. Install the OpenSpec base

```bash
openspec init . --tools claude,codex   # or just claude / codex
```

Creates `openspec/` and the base commands for each tool listed.

## 2. Copy the harness in

Get the harness from <https://github.com/rrrfffrrr/vulpes-harness> and copy these into your project at the same paths:

- `openspec/schemas/requirements/`, `openspec/schemas/gdd/`, `openspec/schemas/architecture/`, `openspec/schemas/backend/`, `openspec/schemas/frontend/`
- `openspec/DIAGRAM-STYLE.md` and `openspec/WRITING-STYLE.md`  (diagram and prose rules for the schemas)
- `openspec/AGENTS.md` and `openspec/CLAUDE.md`  (agent guide to the openspec folder; CLAUDE.md just imports AGENTS.md)
- `.claude/commands/opsx/require.md`, `gdd.md`, `architect.md`, `backend.md`, `frontend.md`  (Claude)
- `.codex/skills/opsx-require/`, `opsx-gdd/`, `opsx-architect/`, `opsx-backend/`, `opsx-frontend/`  (Codex)

Copy only the lines for the tool(s) you installed in step 1.
Commit the copied files.

Exception - `openspec/AGENTS.md` and `openspec/CLAUDE.md` are not a blind `cp` when the target file already exists:

- `AGENTS.md`: add or replace only the `# vulpes-harness` h1 section.
  Every other h1 section is project-owned - keep them as-is.
- `CLAUDE.md`: make sure the `@AGENTS.md` import line is present; keep the rest of the file.

## 3. Verify

```bash
openspec schemas                 # lists requirements, gdd, architecture, backend, frontend
openspec schema validate gdd     # Schema 'gdd' is valid
```

If a schema is missing, redo the copy in step 2.

## Updating an installed harness

Updates REPLACE each unit whole instead of copying over it - an overlay copy leaves files that the new version deleted or renamed lying around.

1. Replace each unit:
   - `openspec/schemas/<name>/` - delete the folder, then copy the new one in.
   - `.claude/commands/opsx/*.md`, `.codex/skills/opsx-*/`, `openspec/DIAGRAM-STYLE.md`, `openspec/WRITING-STYLE.md`, `openspec/CLAUDE.md` - overwrite with the new files.
   - `openspec/AGENTS.md` - replace only the `# vulpes-harness` section (the exception above).
2. Read each schema's `CHANGES.md` for what changed between your version and the new one.
3. Existing documents migrate on next use: the next run of each `/opsx:*` command applies the pending Migration sections in order.
   To migrate immediately, ask your agent to apply them now.

`openspec schema validate` checks the schema definition only, so it passes even before documents migrate.
Pending document migration shows up in `openspec status --change <name>` instead - renamed artifacts report as missing until migrated.

## Next

Run the workflows: `/opsx:require` -> `/opsx:gdd` or `/opsx:architect` -> `/opsx:backend` / `/opsx:frontend` -> `/opsx:propose`.
