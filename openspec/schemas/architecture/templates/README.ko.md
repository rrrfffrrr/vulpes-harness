# 아티팩트 읽는 법 - architecture

[English](README.md) | [한국어](README.ko.md)

**architecture** 스키마(Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR) 아티팩트 - "어떻게", 기술 구조.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 역할 <-> 관심사 <-> 뷰 맵이 각 역할이 읽을 뷰를 안내.

**읽기 순서:**

1. `overview.md` - 전략 / 스택 / 스타일 / 제약 + 뷰 맵
2. `logical-view.md` - 기능 분해 (컴포넌트 / 인터페이스)
3. `process-view.md` - 런타임 / 동시성 흐름 *(있을 때만)*
4. `data-view.md` - 데이터 아키텍처 *(있을 때만)*
5. `ml-serving-view.md` - 추론 파이프라인 *(있을 때만)*
6. `deployment-view.md` - 물리 토폴로지
7. `crosscutting-concepts.md` - 보안 / 로깅 / 컴플라이언스 등
8. `adr.md` - 아키텍처 결정 기록 (근거)
9. `traceability.md` - 요구사항 <-> 아키텍처 추적, 역할 커버리지

*process / data / ml-serving 뷰는 해당 관심사가 있을 때만 존재.*

---

워크플로: **require -> architect -> propose -> apply**
상태 확인: `openspec status --change <이름>`
