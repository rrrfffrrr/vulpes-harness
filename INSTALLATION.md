# 설치 (Installation)

이 하네스는 `openspec init`이 깐 base(spec-driven) 위에 **plan/gdd/design 계층**을 얹는다. 프로젝트에 넣어야 하는 건 두 트리뿐이다:

- `openspec/schemas/{planning,gdd,design}/` — 스키마 + 템플릿 + `change-README.md`
- `.claude/commands/opsx/{plan,gdd,design}.md` — opsx 슬래시 커맨드

base(`propose/apply/archive/explore` 커맨드·스킬, spec-driven 스키마)는 하네스에 없다 — `openspec init`이 설치 버전에 맞춰 만든다.

## 0. 사전 준비

- Node.js (LTS)
- OpenSpec CLI ≥ 1.4.x

  ```bash
  npm i -g @fission-ai/openspec     # 전역 설치
  # 또는 설치 없이: npx @fission-ai/openspec@latest <command>
  ```

## 1. base 설치 (프로젝트 repo에서)

```bash
openspec init . --tools claude
```

→ `openspec/`(spec-driven 스키마) + `.claude/commands/opsx/{propose,apply,archive,explore}.md` + `.claude/skills/openspec-*` 생성.

## 2. 하네스 계층 얹기 (택 1)

먼저 하네스를 받아 둔다(이미 로컬에 있으면 그 경로 사용):

```bash
git clone <harness-repo-url> ../vulpes-harness
```

### A. 복사 — 가장 단순·Windows 친화 (권장)

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

### B. symlink — 업데이트가 자동 반영 (Windows는 개발자 모드/관리자 필요)

```bash
ln -s "$(realpath ../vulpes-harness/openspec/schemas/planning)" openspec/schemas/planning
ln -s "$(realpath ../vulpes-harness/openspec/schemas/gdd)"      openspec/schemas/gdd
ln -s "$(realpath ../vulpes-harness/openspec/schemas/design)"   openspec/schemas/design
ln -s "$(realpath ../vulpes-harness/.claude/commands/opsx/plan.md)"   .claude/commands/opsx/plan.md
ln -s "$(realpath ../vulpes-harness/.claude/commands/opsx/gdd.md)"    .claude/commands/opsx/gdd.md
ln -s "$(realpath ../vulpes-harness/.claude/commands/opsx/design.md)" .claude/commands/opsx/design.md
```

### C. git submodule / subtree

하네스 전체가 한 경로에만 들어가 `openspec/schemas`·`.claude/commands` 위치와 안 맞는다 — 서브모듈로 받은 뒤 위 경로들로 symlink를 거는 조합이 필요하다. 단순함이 목적이면 A를 쓴다.

## 3. 검증

```bash
openspec schemas                 # planning, gdd, design 이 보여야 함
openspec schema validate gdd     # ✓ Schema 'gdd' is valid
ls .claude/commands/opsx         # plan.md gdd.md design.md (+ base 4종)
```

## 4. 사용

```
/opsx:plan   → /opsx:gdd 또는 /opsx:design   → /opsx:propose   → /opsx:apply
```

- change명은 `{프로그램명}-{스키마}`로 고정된다(예: `myapp-plan`). 커맨드가 프로그램명을 1회 묻는다(기본 = repo 폴더명).
- 각 change 폴더의 `README.md`는 스키마의 `change-README.md`에서 자동 복사된 읽기 가이드다 — 손대지 않는다.

## 5. 업데이트

- **복사(A)**: 하네스를 `git pull` 후 2-A를 다시 실행해 덮어쓴다.
- **symlink(B)**: 하네스를 `git pull`하면 끝.
- 이미 생성된 change 폴더의 `README.md`를 최신 가이드로 맞추려면 스키마의 `change-README.md`를 그 폴더로 다시 복사한다.
