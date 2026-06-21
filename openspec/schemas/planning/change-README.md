<!-- 정적 공통 가이드 — opsx 커맨드가 change 생성 시 이 파일을 그 폴더의 README.md로 복사한다.
     프로젝트별로 손대지 말 것(수정 대상 아님). 갱신은 하네스의 이 파일에서만. -->

# 이 폴더 읽는 법 — planning

이 change는 **planning** 스키마(KAOS/GORE + BABOK) 산출물입니다. "무엇을·왜" — 정형 요구를 모읍니다. 구현(apply) 단계는 없습니다.

**여기부터:** [`requirements-document.md`](requirements-document.md) — 네 모델을 종합한 단일 진실. 빠르게 보려면 이것 하나면 됩니다.

**읽는 순서 (사람 기준):**
1. `requirements-document.md` — 종합 (Scope·Goals·Glossary·Responsibilities·Behavior)
2. `business-requirements.md` — 이해관계자 원문 요구(BR) 보존
3. `goal-model.md` — 목표 트리(AND/OR)·도메인 속성·장애와 해소
4. `object-model.md` — 개체·관계·불변식(INV)
5. `responsibility-model.md` — leaf 목표별 책임 주체
6. `operation-model.md` — 연산(pre/post/trigger)·시나리오
7. `traceability.md` — BR↔목표↔책임↔연산 추적 매트릭스

> 전체 워크플로: **plan → (gdd/design) → propose → apply**. 산출물·읽는 순서·완료 상태는 `openspec status --change <이름>`.
