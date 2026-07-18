# verification 아티팩트 읽는 법

[English](README.md) | [한국어](README.ko.md)

**verification** 스키마(ISTQB test basis + ISO/IEC/IEEE 29119-3 문서 타입 + Specification by Example/Gherkin + BABOK 10.1 인수 기준) 아티팩트 - 요구사항과 상세 설계 위의 얇은 인수 계층.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - test basis, 범위, 그리고 여기에 의도적으로 없는 것.

**읽기 순서:**

1. `overview.md` - test basis / 범위 / 범위 밖 / 독자 맵
2. `scenarios/index.md` - 도메인 인덱스; `scenarios/<도메인>.md` - 계층 횡단 인수 시나리오(Gherkin), 요구사항 오퍼레이션별 그룹
3. `environment.md` - 테스트 데이터 요구사항 + 테스트 환경 요구사항
4. `traceability.md` - 기준 <-> 시나리오 <-> 표면 <-> 환경 매트릭스와 갭

*계약별 테스트 케이스는 여기 없음 - 상세 설계 계약에서 빌드 시점에 도출.*

---

워크플로: **require -> architect -> 상세 설계 -> verification -> propose -> apply**
상태 확인: `openspec status --change <이름>`
