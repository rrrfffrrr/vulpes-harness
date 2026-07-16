# TASKS - 상세 설계 계층 보강 로드맵

requirement -> architecture -> backend/frontend 파이프라인의 갭 분석(2026-07-16) 결과와 결정 사항을 정리한다.
확정된 작업, 권고안이 나와 결정을 기다리는 항목, 추후 재논의 항목의 세 묶음이다.
모든 스키마 작업은 착수 전에 근거 표준의 인용 검증을 거친다(미검증 후보는 각 항목에 표시).

## 확정된 작업

### 1. backend: jobs 아티팩트 (배치·스케줄·백그라운드 작업) - 완료 (PR #44)

backend의 인터페이스 표면은 endpoints / events / webhooks 세 종류뿐이라 시간 트리거 작업의 계약이 갈 곳이 없다.
traceability 매트릭스에도 해당 열이 없어, 배치로만 구현되는 requirements operation은 기록 불가능한 GAP으로만 남는다.

- 조건부 아티팩트 `jobs.md` 설계: 스케줄, 중복 실행 정책, 재시작성/멱등성, 실패·백필 규칙
- traceability 매트릭스에 jobs 열 추가
- 근거 어휘 리서치: JSR-352 / Spring Batch (job/step/restartability) - 인용 검증 필요
- 해당 CHANGES.md 기록 + 버전 lockstep

### 2. frontend↔backend 이음새 - 완료 (PR #45)

두 상세 설계가 각자 완결이어도 그 사이가 비어 있다.

- 에러 매핑: backend conventions의 RFC 9457 problem type -> frontend screens의 에러 상태/카피 매핑.
  frontend traceability에 열 추가 또는 screens에 섹션 추가 - 형태는 설계 시 결정
- 클라이언트 데이터 계층: 캐시/staleness, optimistic update, 오프라인, 클라이언트 재시도.
  신규 아티팩트 vs 기존 아티팩트 확장 여부 리서치 필요

## 결정 대기 (권고안 제시됨)

### 3. 영속성(물리 데이터) 설계 - 완료 (persistence 스키마 신설)

ANSI/SPARC 3계층에서 개념(requirements object-model)과 논리(architecture data-view)는 주인이 있으나 물리 수준은 주인이 없다.
backend는 원칙적으로 저장 계층을 배제하므로(externally observable behavior only), DBA 역할이 상세 설계 레벨에서 읽을 문서가 없다.

권고 구조 - 일반 규칙은 "논리 모델은 스토어 무관, 물리 섹션은 스토어별로 해당 엔진 ADR에 키":

- 본문: 스토어 무관 논리 상세(엔티티, 필드, 제약 의도, 보존 정책)
- 스토어별 물리 블록: 그 스토어의 네이티브 단위(테이블/컬렉션/키스페이스/measurement)로 스키마, 인덱스/파티션 키, 그 스토어가 서비스하는 액세스 패턴, 일관성 모델, TTL/보존
- 관계형은 이 규칙의 인스턴스: 표준 SQL 수준의 이식 가능한 core + 엔진 종속 섹션(엔진 미확정·계류 시 OMIT - 회사 MySQL vs 선호 PostgreSQL 같은 다툼을 구조로 흡수)
- NoSQL/시계열은 이식 core가 얇아지고 액세스 패턴·보존 주도 설계가 됨 - 같은 블록 구조로 수용
- 다중 스토어(폴리글랏 퍼시스턴스)는 별도 스키마 없이 스토어 수만큼 블록 - 데이터의 스토어 배치는 architecture data-view의 소유권 결정을 따름

근거: ANSI/SPARC 3-schema, NoSQL Distilled (Sadalage & Fowler, Addison-Wesley 2012 - 검증됨), 스토어별 모델링 관행(작성 시 검증).

### 4. verification (인수·검증) 계층 - 2단 구성 - 완료 (verification 스키마 신설 + requirements 인수 기준)

상세 설계가 이미 test basis이므로(ISTQB 정의: 테스트 케이스의 근거가 되는 문서 일체) 병렬 테스트 스키마는 중복이다.
설계에서 파생 불가능한 것만 새로 소유한다.

- (a) requirements 스키마 개정: operation별 인수 기준 추가 - BABOK v3 기법 10.1 (requirements 스키마 자신의 방법론이 이미 승인)
- (b) 얇은 verification 스키마 신설:
  - `overview` - test basis 참조 선언, 범위
  - `scenarios` - 계층 횡단 E2E를 Gherkin(Given/When/Then)으로, endpoint·화면을 이름으로 참조
  - `test-data-environment` - ISO/IEC/IEEE 29119-3의 Test Data Requirements + Test Environment Requirements
  - `traceability` - 인수 기준·시나리오 커버리지 매트릭스 + GAPS

인수 기준이란: 솔루션이 이해관계자에게 수용 가능하다고 판정되기 위해 충족해야 하는 조건(BABOK 10.1).
pass/fail로 판정되는 측정 가능한 형태여야 하고, 요구사항("무엇을 해야 하는가")과 달리 "됐다고 어떻게 알 것인가"의 관찰 가능한 판정 조건이다.
무엇을 수용 가능하다고 볼지는 비즈니스 결정이므로 설계 문서에서 도출할 수 없다 - 이것이 요구사항 단계에 두는 이유.
verification의 E2E 시나리오는 이 기준을 구체 시스템에 대해 실행 가능하게 실현한다(기준 = 무엇이 증명인가, 시나리오 = 이 시스템에서 어떻게 실행하는가).

근거(전부 검증됨): ISO/IEC/IEEE 29119-3:2021(문서 타입), 29119-4:2021(기법 - 참조만), ISTQB test basis, BABOK v3 10.1, Specification by Example (Adzic, Manning 2011), Gherkin (cucumber.io).

### 5. ml 상세 스키마 (조건부) - 완료 (ml 스키마 신설 + ml-serving-view 경계 정리)

별도 조건부 스키마로 신설한다 - architecture에 ml-serving-view가 있을 때만 존재.
모델 계약은 추론 위치(서버/온디바이스/엣지) 불변이므로 backend나 frontend에 접으면 반대쪽 추론이 갈 곳을 잃는다.

- `overview` - 모델 인벤토리, 추론 위치(ml-serving-view 참조), reader map, 조건부 아티팩트 표
- `models` - 모델별 계약: intended use + out-of-scope use, I/O 계약(입력 피처·출력·신뢰도 의미론), 품질 목표(architecture 참조), 열화·폴백 동작, caveats.
  LLM이면 프롬프트 계약 조건부 섹션(근거 표준 부재 - 추가 리서치 필요)
- `data` - 조건부(자체 학습 데이터 존재 시): 출처, 수집, 라벨링, 분할, 갱신
- `evaluation` - 메트릭+임계값(릴리스 게이트), 평가 데이터셋/슬라이스, 회귀 정책, 드리프트 모니터링 신호
- `lifecycle` - 버저닝, 업데이트/롤백, 재학습 트리거
- `traceability` - requirements operation <-> 모델 <-> 서빙 표면(backend METHOD+path / frontend·game-ui 화면) <-> 평가 게이트

architecture와의 관계 - **ml-serving-view는 유지한다.**
data-view↔영속성 상세, logical-view↔backend components와 같은 계층 관계다: architecture가 구조·자원(파이프라인 형상, 서빙 모드, 가속기/하드웨어 계획)을, ml 상세가 계약·게이트·절차를 답한다.
단 현재 ml-serving-view instruction의 lifecycle/throughput 언급이 상세와 겹치므로, ml 스키마 작성 시 ml-serving-view는 접근 방식 수준으로 정리하고 구체 절차는 상세로 내린다.

근거(검증됨): Model Cards for Model Reporting (Mitchell et al., FAT* 2019), Datasheets for Datasets (Gebru et al. 2018), ISO/IEC 5338:2023, The ML Test Score (Breck et al., IEEE Big Data 2017).

### 6. 설정 카탈로그 + route/i18n - 완료 (backend configuration 아티팩트 + frontend routes/localization 조건부 섹션)

- 설정: backend 아티팩트로 키/플래그 카탈로그(이름·타입·기본값·적용 범위) 소유. 환경별 실제 값은 ops 소관으로 배제. 근거: 12-factor III (작성 시 검증)
- route: frontend flows의 조건부 섹션(URL이 있는 플랫폼일 때 내비게이션 맵에 라우트 계약)
- i18n: game-ui의 LOCALIZATION POLICY(overview) + TEXT BUDGET(widgets) 패턴을 frontend에 미러링 (IGDA Loc SIG 인용 확보됨)

## 추후 재논의

### a. 게임 상세 설계 분해 (game-ui 형제 스키마)

game-ui는 UI 분야 전용으로 유지하고 이름도 유지한다(frontend와 평행 - 범위를 넓히면 named-methodology 불변식이 희석됨).
GDD 아래 상세 설계는 분야별 형제 스키마로 분해한다는 방향까지 합의, 구체 범위는 추후 논의.

- 최우선 후보 `game-systems`: GDD mechanics의 밸런싱 의도 -> 공식, 튜닝 테이블, 시스템 상태기계, 콘텐츠 데이터 스키마.
  근거 후보: Machinations (Adams & Dormans), UML 상태기계 - 리서치 필요
- 후순위 후보: level/content design (LDD)
- 형제 추가 판단 기준: 해당 GDD 섹션이 구현자용 계약 수준 아티팩트를 필요로 하는가 / 접지할 명명된 방법론이 있는가 / 다른 스키마의 영역이 아닌가
- 선행 과제(gdd 소폭 개정): ux-ui에 입력 컨텍스트 명명 요구, gameplay/ux-ui에 어시스트 개념 명명 요구 - game-ui가 이름으로 참조할 앵커 확보
