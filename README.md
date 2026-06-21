# vulpes-harness

A reusable harness for the OpenSpec planning/design workflow. Kept separate from project repos and versioned in one place.

A **layer on top of** the development (spec-driven) workflow that `openspec init` installs by default. It adds:
- **planning** - `opsx:plan` + the `planning` schema (KAOS/GORE + BABOK)
- **game design (gdd)** - `opsx:gdd` + the `gdd` schema (standard GDD sections)
- **technical design (design)** - `opsx:design` + the `design` schema (Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR + BABOK RTM)

All three have no apply (implementation) step - they produce living documents, not code.

Documentation diagrams follow [DIAGRAM-STYLE.md](DIAGRAM-STYLE.md) - hand-authored SVG committed to the repo + shared style tokens (size/layout are per-diagram).

> **Prerequisite: run `openspec init` first.** This harness does **not** include the base (spec-driven schema + `propose/apply/archive/explore` commands/skills) - `openspec init` generates those, matched to the installed version. The harness only holds the plan/gdd/design layer that init does not create (avoiding duplication/version drift). So it is not used standalone; it is layered on after init.

## Workflow

```
openspec init                          # installs base (spec-driven)
  -> plan -> [ gdd | design ] -> propose -> apply
   (gather reqs) (game/tech design)     (specify)  (build)
```

- **plan** = the common first stage for any project (formal requirements).
- **gdd / design** = the per-project middle artifacts. gdd = games, design = technical structure (common, games included). One project may have both.
- **propose / apply** = the spec-driven development stages that init provides.

## Layout

```
openspec/schemas/planning/      planning schema (no apply)
  schema.yaml                   7 artifact instructions (goal ID convention, etc. - SSOT)
  templates/                    business-requirements / goal-model / object-model /
                                responsibility-model / operation-model /
                                requirements-document / traceability
  change-README.md              reading guide copied into the change folder (static, shared)
openspec/schemas/gdd/           gdd schema (no apply)
  schema.yaml                   10 artifacts (8 core + 2 conditional)
  templates/                    overview / gameplay / mechanics / world-narrative /
                                art-direction / audio-direction / ux-ui / tech /
                                monetization / production
  change-README.md              reading guide (static, shared)
openspec/schemas/design/        design schema (no apply)
  schema.yaml                   9 artifacts (core views + conditional views)
  templates/                    architecture-overview / logical-view / process-view /
                                data-view / ml-serving-view / deployment-view /
                                crosscutting-concepts / adr / design-traceability
  change-README.md              reading guide (static, shared)
.claude/commands/opsx/          plan.md / gdd.md / design.md  (opsx slash commands)
```

## Change naming

The no-apply schemas (plan/gdd/design) are **project singletons** - fix the change name as `{program}-{schema}` (e.g. `tycoon-plan`, `tycoon-gdd`).

- If a `*-{schema}` change exists, the command continues it; otherwise it **asks once for the program name** (default suggestion = the repo folder name; a different fixed name is allowed).
- For several in one repo, use distinct program names in parallel (`{a}-plan`, `{b}-plan`).

## Change-folder README (reading order)

Each schema folder's `change-README.md` is that schema's "start here + reading order" guide. The opsx command **copies it verbatim** into the new change folder as `README.md` (overwriting the stub `openspec` created). It is a static shared asset, so do not edit it per project - update only the harness `change-README.md`.

## Artifact dependency order (planning)

```
business-requirements
  -> goal-model
    -> object-model, responsibility-model
      -> operation-model
        -> requirements-document
          -> traceability
```

A new requirement is preserved verbatim as the next `BR<n>` in `business-requirements.md`, then propagated traceably to every affected artifact.

## Goal ID convention

- `G<n>.<m>` (dotted number) = AND-refinement (all subgoals required)
- `G<n>.<m>.<a>` (trailing letter) = OR-refinement (alternative)

The SSOT for the definition is the goal-model instruction in `openspec/schemas/planning/schema.yaml`.

## Prerequisites

- Command behavior (Claude reading the instructions and writing artifacts) needs no install - it is just Markdown under `.claude/`.
- The `openspec` CLI (`openspec init`, `openspec new change --schema <s>`, `openspec status --change <id>`, `openspec schema validate <s>`) requires the CLI (>= 1.4.x recommended).

  ```
  npm i -g @fission-ai/openspec     # global install
  # or without installing
  npx @fission-ai/openspec@latest <command>
  ```

## Using it in a project

See [INSTALLATION.md](INSTALLATION.md). In short: `openspec init` (base) -> layer the harness `openspec/schemas/` and `.claude/commands/opsx/` (copy or symlink) -> `/opsx:plan` -> `/opsx:gdd` or `/opsx:design` -> `/opsx:propose`.
