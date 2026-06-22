# Reference

## Layout

```
openspec/schemas/<schema>/   schema.yaml + templates/ + change-README.md
.claude/commands/opsx/        require.md / gdd.md / architect.md   (Claude)
.codex/skills/opsx-<name>/    SKILL.md                             (Codex)
```

- Templates: requirements 7, gdd 10, architecture 9.
- `schema.yaml` defines the artifacts, build order, and ID rules.
- The Claude command and Codex skill for a workflow share one body - edit both.
- Add a schema: a new folder under `openspec/schemas/` plus a matching opsx command and Codex skill.
- Other asset types like hooks and prompts live under `.claude/`/`.codex/`.

## Change naming

Each schema is a project singleton named `{program}-{schema}` (e.g. `tycoon-requirements`).
A workflow continues an existing `*-{schema}` change, or asks once for the program name (default: repo folder).
Use distinct names for parallel programs.

## change-README.md

Each schema's `change-README.md` is its reading guide.
The workflow copies it verbatim into the change folder as `README.md`.
Edit the harness copy, not the per-project one.

## Requirements artifact order

```
business-requirements -> goal-model -> object-model, responsibility-model
  -> operation-model -> requirements-document -> traceability
```

## Goal IDs

- `G<n>.<m>` - AND-refinement (all sub-goals required)
- `G<n>.<m>.<a>` - OR-refinement (alternatives)
