# Installation

This harness layers the **plan/gdd/design layer** on top of the base (spec-driven) that `openspec init` installs. Only two trees go into a project:

- `openspec/schemas/{planning,gdd,design}/` - schemas + templates + `change-README.md`
- `.claude/commands/opsx/{plan,gdd,design}.md` - opsx slash commands

The base (`propose/apply/archive/explore` commands/skills, spec-driven schema) is not in the harness - `openspec init` creates it, matched to the installed version.

## 0. Prerequisites

- Node.js (LTS)
- OpenSpec CLI >= 1.4.x

  ```bash
  npm i -g @fission-ai/openspec     # global install
  # or without installing: npx @fission-ai/openspec@latest <command>
  ```

## 1. Install the base (in the project repo)

```bash
openspec init . --tools claude
```

-> creates `openspec/` (spec-driven schema) + `.claude/commands/opsx/{propose,apply,archive,explore}.md` + `.claude/skills/openspec-*`.

## 2. Layer the harness (pick one)

First get the harness (use its path if you already have it locally):

```bash
git clone <harness-repo-url> ../vulpes-harness
```

### A. Copy - simplest / Windows-friendly (recommended)

bash:
```bash
HARNESS=../vulpes-harness
cp -r "$HARNESS"/openspec/schemas/planning openspec/schemas/
cp -r "$HARNESS"/openspec/schemas/gdd      openspec/schemas/
cp -r "$HARNESS"/openspec/schemas/design   openspec/schemas/
cp "$HARNESS"/.claude/commands/opsx/plan.md   .claude/commands/opsx/
cp "$HARNESS"/.claude/commands/opsx/gdd.md    .claude/commands/opsx/
cp "$HARNESS"/.claude/commands/opsx/design.md .claude/commands/opsx/
```

PowerShell:
```powershell
$H = "..\vulpes-harness"
Copy-Item "$H\openspec\schemas\planning","$H\openspec\schemas\gdd","$H\openspec\schemas\design" openspec\schemas\ -Recurse -Force
Copy-Item "$H\.claude\commands\opsx\plan.md","$H\.claude\commands\opsx\gdd.md","$H\.claude\commands\opsx\design.md" .claude\commands\opsx\ -Force
```

### B. symlink - updates flow automatically (Windows needs Developer Mode / admin)

```bash
ln -s "$(realpath ../vulpes-harness/openspec/schemas/planning)" openspec/schemas/planning
ln -s "$(realpath ../vulpes-harness/openspec/schemas/gdd)"      openspec/schemas/gdd
ln -s "$(realpath ../vulpes-harness/openspec/schemas/design)"   openspec/schemas/design
ln -s "$(realpath ../vulpes-harness/.claude/commands/opsx/plan.md)"   .claude/commands/opsx/plan.md
ln -s "$(realpath ../vulpes-harness/.claude/commands/opsx/gdd.md)"    .claude/commands/opsx/gdd.md
ln -s "$(realpath ../vulpes-harness/.claude/commands/opsx/design.md)" .claude/commands/opsx/design.md
```

### C. git submodule / subtree

The whole harness lands at one path, which does not match the `openspec/schemas` / `.claude/commands` locations - you would need a submodule plus symlinks from those paths into it. For simplicity, use A.

## 3. Verify

```bash
openspec schemas                 # planning, gdd, design should appear
openspec schema validate gdd     # OK: Schema 'gdd' is valid
ls .claude/commands/opsx         # plan.md gdd.md design.md (+ the 4 base ones)
```

## 4. Use

```
/opsx:plan   -> /opsx:gdd or /opsx:design   -> /opsx:propose   -> /opsx:apply
```

- Change names are fixed as `{program}-{schema}` (e.g. `myapp-plan`). The command asks once for the program name (default = repo folder name).
- Each change folder's `README.md` is a reading guide auto-copied from the schema's `change-README.md` - do not edit it.

## 5. Updating

- **Copy (A)**: `git pull` the harness, then re-run 2-A to overwrite.
- **symlink (B)**: `git pull` the harness and you are done.
- To refresh an existing change folder's `README.md` to the latest guide, copy the schema's `change-README.md` into that folder again.
