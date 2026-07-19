# requirements 아티팩트 읽는 법

[English](README.md) | [한국어](README.ko.md)

**requirements** 스키마(KAOS/GORE + BABOK) 아티팩트.
"무엇을, 왜" - 공식 요구사항.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`requirements-document.md`](requirements-document.md) - 모델들의 단일 종합본.
빠르게 훑을 때는 종합본만으로 충분.

**읽기 순서 (사람용):**

1. `requirements-document.md` - 종합본 (범위 / 목표 / 용어집 / 책임 / 행위)
2. `business-requirements.md` - 이해관계자 진술(BR), 원문 그대로
3. `goal-model.md` - 목표 트리(AND/OR), 도메인 속성, 장애물 + 해소책
4. `object-model.md` - 엔티티, 관계, 불변식(INV)
5. `responsibility-model.md` - 각 말단 목표의 책임 에이전트
6. `operation-model.md` - 오퍼레이션(pre/post/trigger), 시나리오
7. `scenarios/index.md` - 도메인 인덱스; `scenarios/<도메인>.md` - 누가(에이전트) 또는 어떤 스케줄이 어떤 오퍼레이션을 어떤 순서로 작동시키는지, 시퀀스로
8. `traceability.md` - BR <-> 목표 <-> 말단 <-> 에이전트 <-> 오퍼레이션 <-> 시나리오 매트릭스

---

워크플로: **require -> (gdd/architect) -> propose -> apply**
상태 확인: `openspec status --change <이름>`
