# 이 폴더 읽는 법 — planning

**planning** 스키마(KAOS/GORE + BABOK) 산출물입니다.
"무엇을·왜" — 정형 요구를 모읍니다. 구현(apply) 단계는 없습니다.

**여기부터 →** [`requirements-document.md`](requirements-document.md) — 네 모델을 종합한 단일 진실. 빠르게 보려면 이것만.

**읽는 순서**

1. `requirements-document.md` — 종합 (Scope·Goals·Glossary·Responsibilities·Behavior)
2. `business-requirements.md` — 이해관계자 원문 요구(BR) 보존
3. `goal-model.md` — 목표 트리(AND/OR)·도메인 속성·장애/해소
4. `object-model.md` — 개체·관계·불변식(INV)
5. `responsibility-model.md` — leaf 목표별 책임 주체
6. `operation-model.md` — 연산(pre/post/trigger)·시나리오
7. `traceability.md` — BR↔목표↔책임↔연산 추적

---

흐름: **plan → (gdd/design) → propose → apply**
상태 확인: `openspec status --change <이름>`
