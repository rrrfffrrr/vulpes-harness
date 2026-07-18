# 아티팩트 읽는 법 - persistence

[English](README.md) | [한국어](README.ko.md)

**persistence** 스키마(ANSI/SPARC internal 수준 + 폴리글랏 퍼시스턴스 + 액세스 패턴 주도 스토어 설계 + 진화적 데이터베이스 설계) 아티팩트 - 아키텍처 data-view 한 단계 아래의 스토어 수준 데이터 설계.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 스토어 인벤토리(엔진 + 결정 ADR 또는 OPEN)와 독자 맵.

**읽기 순서:**

1. `overview.md` - 스토어 인벤토리 / 데이터 도메인 / 독자 맵
2. `model.md` - 스토어 무관 논리 상세: 전체 필드 목록, 무결성, 보존/PII 분류
3. `stores.md` - 스토어별 설계: 네이티브 단위, 키/인덱스, 액세스 패턴, 보존 메커니즘, 엔진 종속 기능
4. `migrations.md` - 마이그레이션 정책, 파괴적 변경의 expand-contract, 시드 데이터, 백필
5. `traceability.md` - 객체 <-> 엔티티 <-> 스토어 <-> 액세스 패턴 매트릭스

*엔진 미확정 스토어는 OPEN으로 표기하고 아키텍처 ADR이 확정될 때까지 엔진 무관 수준을 유지.*

---

워크플로: **require -> architect -> persistence -> propose -> apply**
상태 확인: `openspec status --change <이름>`
