# 아티팩트 읽는 법 - frontend

[English](README.md) | [한국어](README.ko.md)

**frontend** 스키마(IFML + UML 상태 머신 + wireflow + Atomic Design/Open UI 해부도 + UI Stack + WCAG 2.2) 아티팩트 - 웹/모바일/데스크톱 앱 UI의 구현 가능한 스펙, 아키텍처 한 단계 아래. 구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 시스템 전역 UI 어휘(브레이크포인트, 인터랙션 상태, 접근성 목표)와 독자 맵.

**읽기 순서:**

1. `overview.md` - 플랫폼 / 브레이크포인트 / 인터랙션 상태 enum / 접근성 목표 / 독자 맵
2. `design-tokens.md` - 색 / 타이포 / 치수 / 모션 / 테마 토큰 *(있을 때만)*
3. `components.md` - 공유 컴포넌트: 해부도, 변형, 상태, 동작, 콘텐츠 규칙
4. `screens.md` - 화면별: 레이아웃 + 브레이크포인트 동작, UI Stack 5상태, 데이터, 폼(정확한 에러 문구 포함)
5. `flows.md` - 내비게이션 맵, 이벤트→전이 표, 복잡한 인터랙션의 statechart
6. `traceability.md` - 요구사항 <-> 화면 <-> 플로 <-> 컴포넌트 매트릭스

*design-tokens는 토큰 기반 스타일링일 때만 존재.*

---

워크플로: **require -> architect -> frontend -> propose -> apply**
상태 확인: `openspec status --change <이름>`
