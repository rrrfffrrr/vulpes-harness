<!-- 정적 공통 가이드 — opsx 커맨드가 change 생성 시 이 파일을 그 폴더의 README.md로 복사한다.
     프로젝트별로 손대지 말 것(수정 대상 아님). 갱신은 하네스의 이 파일에서만. -->

# 이 폴더 읽는 법 — design

이 change는 **design** 스키마(Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR) 산출물입니다. "어떻게" — 기술 구조. 구현(apply) 단계는 없습니다.

**여기부터:** [`architecture-overview.md`](architecture-overview.md) — 솔루션 전략·기술 스택·**역할↔관심사↔뷰 맵**(직군별 읽을 뷰 안내).

**읽는 순서:**
1. `architecture-overview.md` — 전략·스택·스타일·제약 + 뷰 맵
2. `logical-view.md` — 기능 분해(컴포넌트·인터페이스)
3. `process-view.md` — 런타임·동시성 흐름 *(해당 시)*
4. `data-view.md` — 데이터 아키텍처 *(해당 시)*
5. `ml-serving-view.md` — 추론 파이프라인 *(해당 시)*
6. `deployment-view.md` — 물리 토폴로지
7. `crosscutting-concepts.md` — 보안·로깅·컴플라이언스 등 횡단 개념
8. `adr.md` — 아키텍처 결정 기록(근거)
9. `design-traceability.md` — planning↔design 추적·역할 커버리지

*(process/data/ml-serving 뷰는 해당 관심사가 있을 때만 존재.)*

> 전체 워크플로: **plan → design → propose → apply**. 산출물·읽는 순서·완료 상태는 `openspec status --change <이름>`.
