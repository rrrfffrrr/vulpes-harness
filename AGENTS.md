# Vulpes harness

vulpes-harness is a versioned bundle of planning assets for AI coding tools (Claude Code, Codex), layered on OpenSpec: five workflow schemas plus the slash commands that drive them.
This repository IS the harness - editing here changes what installed projects copy; it is not a project that merely uses the harness.
There is no build or test suite; verification is `openspec schema validate` plus the invariants below.

## Index

- `openspec/schemas/<name>/` : one schema - `schema.yaml` (artifacts + authoring principles), `templates/` (artifact skeletons + `README(.ko).md` reading guides), `CHANGES.md` (Keep a Changelog)
- `.claude/commands/opsx/` : Claude slash commands (require / gdd / architect / backend / frontend)
- `.codex/skills/opsx-*/` : Codex mirrors of the commands - bodies must stay identical below the frontmatter
- `openspec/AGENTS.md`, `openspec/CLAUDE.md` : the agent guide INSTALLED into target projects (different audience from this file)
- `openspec/DIAGRAM-STYLE.md` : diagram rules the schemas follow
- `openspec/WRITING-STYLE.md` : prose rules for generated artifacts (reader-first, search-friendly)
- `INSTALLATION.md` : copy-based install procedure
- `README.md` / `README.ko.md` : user docs (change together)
- `assets/workflow.svg`, `assets/workflow-game.svg` : pipeline diagrams (app / game)

## Harness invariants

Breaking one of these breaks installed projects - check before committing.

- **Command/skill parity**: a Claude command body and its Codex skill body are identical below the frontmatter. Edit one -> apply the same edit to the other -> run the parity check below.
- **Version lockstep**: the harness release semver moves together in `schema.yaml` `metadata.version`, command/skill frontmatter `version`, and every template's `schema-version` frontmatter. Record what changed in that schema's `CHANGES.md` - installed projects have no git history of this repo, so CHANGES.md is their only migration guide.
- **Artifact naming**: plain names (`overview.md`, `traceability.md`) - the change folder namespaces artifacts; no schema-name prefixes.
- **Reading guides** (`templates/README(.ko).md`) are copied verbatim, name-preserving, into change folders - keep wording location-neutral so it reads correctly in both places.
- **English/Korean sync**: root `README.md` <-> `README.ko.md` and per-schema `templates/README.md` <-> `README.ko.md` change together.
- **Named-methodology grounding**: every schema stands on named, cited standards (see each `schema.yaml` description). Structural changes research the standard first - no improvised structure.
- **The frontend schema contains zero game references** - positive scoping only (web, mobile, desktop). Game UI is a separate future schema.
- **Renames/moves** update `INSTALLATION.md` (copy list) and the affected `CHANGES.md` in the same change.
- `openspec/AGENTS.md` installed-copy contract: only its `# vulpes-harness` h1 section is harness-managed; other h1 sections are project-owned and survive updates.

## Checks

- `openspec schema validate <name>` for every edited schema (`requirements` | `gdd` | `architecture` | `backend` | `frontend`). Requires OpenSpec CLI >= 1.4.x (`npm i -g @fission-ai/openspec`).
- Command/skill parity - must print OK for all five:

  ```bash
  for t in require gdd architect backend frontend; do
    diff -q <(awk 'f{print} /^---$/{c++; if(c==2) f=1}' .claude/commands/opsx/$t.md) \
            <(awk 'f{print} /^---$/{c++; if(c==2) f=1}' .codex/skills/opsx-$t/SKILL.md) \
      >/dev/null && echo "OK $t" || echo "MISMATCH $t"
  done
  ```

## Git flow

| Branch | Purpose | Env |
|--------|---------|-----|
| `main` | Production (release-ready only). No direct commits/pushes. Tag `vX.Y.Z` on deploy. | production |
| `develop` | Integration branch. Merge target for features. | development |
| `release/<ver>` | Review/CBT. Branch from `main`, merge in `develop` (release ← develop) → deploy to `main` (tag) + back-merge to `develop`. | review/CBT |
| `feature/<name>` | Branch from `develop` → merge back to `develop` (delete after merge). | — |
| `fix/<name>` | Bugs found during review. Branch from `release` → merge to `release` + `develop`. | — |
| `hotfix/<name>` | Production bugs. Branch from `main` → merge to `main` + `develop` (+ active `release`). | — |

- Commit messages follow Conventional Commits 1.0.0 (conventionalcommits.org): `feat:` / `fix:` / `refactor:` / `docs:` / `chore:`.
- Per-schema `CHANGES.md` follows Keep a Changelog with one deliberate deviation: the unreleased section is pre-named `## [x.y.z] - Unreleased` (not `## [Unreleased]`), because the version-lockstep invariant pre-assigns the release version across schema metadata and template frontmatter.

## Workflow: the work loop

A reported symptom is an **example**, not the problem itself. Never jump symptom → patch. In order:

1. **Reset the goal** — restate what the user actually wants as a general outcome, not the one example.
2. **Declare boundaries** — before touching code, write down every in-scope case plus what must not break (the regression boundary).
3. **Survey real behavior** — observe how each case behaves *now in the real runtime*. Synthetic events and a green build are not evidence.
4. **Design** — a fix that doesn't tangle the structure further; state the regression impact. Put the decision in a traceable object (OpenSpec BR/INV/ADR), not just your head.
5. **Implement.**
6. **Verify** — every case + regressions, exercised like a real user. Bypassing checks fail. "Done" is broad — all cases, no regressions, tests, docs — and **the user confirms it**.

## Workflow: git checkpoints

During a task, use git as a **reversible checkpoint**.

- Commit at each small working state (WIP allowed) — if it breaks, roll back to the last good commit.
- Before a risky change (large refactor, deletion), leave a checkpoint commit or stash.
- Passing step 6 of the work loop = a commit-worthy checkpoint.
- Squash temporary WIP commits before the PR. Never leave a broken state on `develop` or `main`.

## Workflow: task boundaries (on start and end)

- **On start**: clean up any uncommitted changes (commit/stash) to start from a clean state, and record the task and goal in memory.
- **On end**: update memory with decisions, state, and open questions, and commit per task unit (at least one commit per task). The finished task should be in both memory and a commit.

## Workflow: what to cut and what to keep

Stop at the first rung that holds — does it need to exist (YAGNI) → does stdlib/native do it → does an existing dependency do it → can it be one line → only then the minimum code.

- An interface with one implementation, config for a value that never changes, scaffolding "for later" = **cut it**.
- Deletion > addition. The short diff wins. Before adding a dependency, see if a few lines do it.
- Mark deliberate simplifications with a `// ponytail:` comment naming the ceiling and upgrade path.
- **But never cut**: input validation at trust boundaries, error handling that prevents data loss, security, accessibility, anything explicitly requested.
