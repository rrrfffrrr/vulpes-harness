# vulpes-harness

OpenSpec 기획·개발 워크플로를 위한 재사용 가능한 하네스. 프로젝트 repo에서 분리해 한곳에서 버전 관리한다.

기본 `openspec init`이 깔아주는 개발(spec-driven) 워크플로에 더해 다음을 포함한다:
- **기획(planning) 워크플로** — `opsx:plan` 커맨드 + `planning` 스키마 (KAOS/GORE + BABOK)
- **기술 설계(design) 워크플로** — `opsx:design` 커맨드 + `design` 스키마 (Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR + BABOK RTM)

planning·design 워크플로 모두 apply(구현) 단계가 없다 — 코드가 아니라 산출물 문서를 만든다.

## 구성

```
openspec/schemas/planning/      planning 스키마 — 기획 전용 (apply 단계 없음)
  schema.yaml                   스키마 정의 본체 (7개 산출물 instruction, goal ID 표기 규칙 등 SSOT)
  templates/                    7개 산출물 템플릿 (business-requirements / goal-model /
                                object-model / responsibility-model / operation-model /
                                requirements-document / traceability)
openspec/schemas/design/        design 스키마 — 기술 설계 전용 (apply 단계 없음)
  schema.yaml                   9개 산출물 instruction (코어 view + 조건부 view)
  templates/                    architecture-overview / logical-view / process-view /
                                data-view / ml-serving-view / deployment-view /
                                crosscutting-concepts / adr / design-traceability
.claude/commands/opsx/          opsx 슬래시 커맨드
  plan.md                       기획 (planning 스키마)
  design.md                     기술 설계 (design 스키마, planning을 source로)
  propose.md  apply.md  archive.md  explore.md   개발 (spec-driven)
.claude/skills/openspec-*/      opsx 스킬 (propose / apply / archive / explore)
```

## 산출물 의존성 순서

```
business-requirements
  → goal-model
    → object-model, responsibility-model
      → operation-model
        → requirements-document
          → traceability
```

새 요구사항은 다음 `BR<n>`으로 raw(`business-requirements.md`)에 원문 보존 후, 영향받는 7개 산출물 전체에 추적 가능하게 반영한다.

## goal ID 표기 규칙

- `G<n>.<m>` (점-숫자) = AND-refinement (모두 필요한 하위 목표)
- `G<n>.<m>.<a>` (끝 알파벳) = OR-refinement (대안)

정의의 SSOT는 `openspec/schemas/planning/schema.yaml`의 goal-model instruction.

## 기본 `openspec init`과의 차이

`openspec init . --tools claude` (v1.3.1)가 만드는 것은 **개발 워크플로뿐**이다:

```
.claude/commands/opsx/   propose · apply · archive · explore
.claude/skills/           openspec-{propose,apply,archive,explore}
openspec/changes/archive/ (빈 폴더)
openspec/specs/           (빈 폴더)
```

이 하네스가 기본 init에 **추가**하는 것:

- `opsx/plan.md`, `opsx/design.md` — 기획·설계 커맨드
- `openspec/schemas/planning/` — planning 스키마 + 7개 산출물 템플릿
- `openspec/schemas/design/` — design 스키마 + 9개 산출물 템플릿

즉 `openspec init`만으로는 기획·설계 워크플로가 복원되지 않는다. 이 하네스가 그 차이를 담는다.

## 전제조건

- 커맨드/스킬 동작(Claude가 지시문을 읽고 산출물을 쓰는 것)에는 별도 설치가 필요 없다 — `.claude/` 안의 마크다운일 뿐이다.
- `openspec` CLI 명령(`openspec init`, `openspec status --change <id>`로 산출물 7/7 검증, `openspec validate`)을 쓰려면 CLI가 필요하다 (≥ 1.3.1).

  ```
  npm i -g @fission-ai/openspec     # 전역 설치
  # 또는 설치 없이
  npx @fission-ai/openspec@latest <command>
  ```

## 프로젝트에서 쓰기

이 하네스를 프로젝트 repo에 연결하는 방식(submodule / symlink / 복사)은 프로젝트마다 정한다.
