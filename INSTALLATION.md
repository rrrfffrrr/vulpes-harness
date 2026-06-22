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

Get the harness from https://github.com/rrrfffrrr/vulpes-harness and copy these into your project at the same paths:

- `openspec/schemas/requirements/`, `openspec/schemas/gdd/`, `openspec/schemas/architecture/`
- `openspec/DIAGRAM-STYLE.md`  (diagram rules for gdd and architecture)
- `.claude/commands/opsx/require.md`, `gdd.md`, `architect.md`  (Claude)
- `.codex/skills/opsx-require/`, `opsx-gdd/`, `opsx-architect/`  (Codex)

Copy only the lines for the tool(s) you installed in step 1.

Commit the copied files, and copy them again to update.

## 3. Verify

```bash
openspec schemas                 # lists requirements, gdd, architecture
openspec schema validate gdd     # Schema 'gdd' is valid
```

If a schema is missing, redo the copy in step 2.

## Next

Run the workflows: `/opsx:require` -> `/opsx:gdd` or `/opsx:architect` -> `/opsx:propose`.
