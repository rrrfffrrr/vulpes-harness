# vulpes-harness

OpenSpec 기획/설계 워크플로를 위한 재사용 하네스. 프로젝트 repo에서 분리해 한곳에서 버전 관리한다.

기본 `openspec init`이 깔아주는 개발(spec-driven) 워크플로 **위에 얹는 계층**으로, 다음을 추가한다:
- **기획(planning)** - `opsx:plan` + `planning` 스키마 (KAOS/GORE + BABOK)
- **게임 디자인(gdd)** - `opsx:gdd` + `gdd` 스키마 (표준 GDD 섹션)
- **기술 설계(design)** - `opsx:design` + `design` 스키마 (Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR + BABOK RTM)

세 워크플로 모두 apply(구현) 단계가 없다 - 코드가 아니라 산출물 문서를 만드는 살아있는 문서다.

> **전제: `openspec init` 먼저.** 이 하네스는 base(spec-driven 스키마 + `propose/apply/archive/explore` 커맨드/스킬)를 **포함하지 않는다** - 그건 `openspec init`이 설치 버전에 맞춰 생성한다. 하네스는 init이 만들지 않는 plan/gdd/design 계층만 담는다(중복/버전 드리프트 방지). 따라서 단독으로는 쓰지 않고 init 후 얹는다.

## 워크플로 흐름

```
openspec init                          # base(spec-driven) 설치
  -> plan -> [ gdd | design ] -> propose -> apply
   (요구 취합)  (게임/기술 설계)        (스펙화)   (구현)
```

- **plan** = 모든 프로젝트 공통 1단계(정형 요구 취합).
- **gdd / design** = 프로젝트 성격별 중간 산출물. gdd=게임, design=기술 구조(게임 포함 공통). 한 프로젝트가 둘 다 가질 수 있다.
- **propose / apply** = init이 주는 spec-driven 개발 단계.

## 구성

```
openspec/schemas/planning/      planning 스키마 (apply 없음)
  schema.yaml                   7개 산출물 instruction (goal ID 표기 규칙 등 SSOT)
  templates/                    business-requirements / goal-model / object-model /
                                responsibility-model / operation-model /
                                requirements-document / traceability
  change-README.md              change 폴더에 복사되는 읽기 가이드(정적 공통)
openspec/schemas/gdd/           gdd 스키마 (apply 없음)
  schema.yaml                   10개 산출물 (코어 8 + 조건부 2)
  templates/                    overview / gameplay / mechanics / world-narrative /
                                art-direction / audio-direction / ux-ui / tech /
                                monetization / production
  change-README.md              읽기 가이드(정적 공통)
openspec/schemas/design/        design 스키마 (apply 없음)
  schema.yaml                   9개 산출물 (코어 view + 조건부 view)
  templates/                    architecture-overview / logical-view / process-view /
                                data-view / ml-serving-view / deployment-view /
                                crosscutting-concepts / adr / design-traceability
  change-README.md              읽기 가이드(정적 공통)
.claude/commands/opsx/          plan.md / gdd.md / design.md  (opsx 슬래시 커맨드)
```

## change 네이밍 규칙

apply 없는 스키마(plan/gdd/design)는 **프로젝트 싱글톤** - change명을 `{프로그램명}-{스키마}`로 고정한다 (예: `tycoon-plan`, `tycoon-gdd`).

- 커맨드는 같은 `*-{스키마}` change가 있으면 그걸 이어가고, 없으면 **프로그램명을 1회 질문**한다(기본 제안 = repo 폴더명, 다른 고정명 가능).
- 한 repo에 여러 개가 필요하면 프로그램명을 달리해 병렬로 둔다(`{a}-plan`, `{b}-plan`).

## change 폴더 README (읽는 순서)

각 스키마 폴더의 `change-README.md`는 그 스키마의 "여기부터 읽기 + 읽는 순서" 가이드다. opsx 커맨드가 change 생성 시 이 파일을 그 change 폴더의 `README.md`로 **그대로 복사**한다(openspec이 만든 스텁을 덮어씀). 정적 공통 자산이므로 프로젝트별로 손대지 않는다 - 갱신은 하네스의 `change-README.md`에서만.

## 산출물 의존성 순서 (planning)

```
business-requirements
  -> goal-model
    -> object-model, responsibility-model
      -> operation-model
        -> requirements-document
          -> traceability
```

새 요구는 다음 `BR<n>`으로 raw(`business-requirements.md`)에 원문 보존 후 영향받는 산출물 전체에 추적 가능하게 반영한다.

## goal ID 표기 규칙

- `G<n>.<m>` (점-숫자) = AND-refinement (모두 필요한 하위 목표)
- `G<n>.<m>.<a>` (끝 알파벳) = OR-refinement (대안)

정의의 SSOT는 `openspec/schemas/planning/schema.yaml`의 goal-model instruction.

## 전제조건

- 커맨드 동작(Claude가 지시문을 읽고 산출물을 쓰는 것)에는 별도 설치가 필요 없다 - `.claude/` 안의 마크다운일 뿐이다.
- `openspec` CLI(`openspec init`, `openspec new change --schema <s>`, `openspec status --change <id>`, `openspec schema validate <s>`)를 쓰려면 CLI가 필요하다 (>= 1.4.x 권장).

  ```
  npm i -g @fission-ai/openspec     # 전역 설치
  # 또는 설치 없이
  npx @fission-ai/openspec@latest <command>
  ```

## 프로젝트에서 쓰기

설치/연결 절차는 [INSTALLATION.md](INSTALLATION.md) 참고. 요약: `openspec init`(base) -> 하네스의 `openspec/schemas/`/`.claude/commands/opsx/` 얹기(복사/심링크) -> `/opsx:plan` -> `/opsx:gdd` 또는 `/opsx:design` -> `/opsx:propose`.
