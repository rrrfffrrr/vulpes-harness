# 아티팩트 읽는 법 - backend

[English](README.md) | [한국어](README.ko.md)

**backend** 스키마(OpenAPI/JSON Schema 계약 + RFC 9110/9457/9111 + BCP 14 + UML 시퀀스 + C4 컴포넌트) 아티팩트 - 아키텍처 한 단계 아래의 정확한 인터페이스 계약.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 인터페이스 표면, 상태 모델, 독자별 읽기 안내.

**읽기 순서:**

1. `overview.md` - 범위 / 인터페이스 표면 / 상태 관리 / 독자 맵
2. `conventions.md` - 공유 규칙집: 인증 스코프, 버저닝, 에러 카탈로그, 페이지네이션, 레이트 리밋, 멱등성, 동시성, 캐싱, 장기 실행 오퍼레이션
3. `components.md` - 미들웨어 파이프라인(순서 있음) + 공유 컴포넌트
4. `endpoints.md` - 엔드포인트별 계약 (conventions와의 차이만 기록)
5. `sequences.md` - 런타임 플로, 클라이언트가 관측하는 실패 경로 포함
6. `events.md` - 채널 / 메시지 / 전달 보장 *(있을 때만)*
7. `webhooks.md` - 아웃바운드 콜백 *(있을 때만)*
8. `jobs.md` - 스케줄/백그라운드 잡 계약 *(있을 때만)*
9. `configuration.md` - 설정 키·피처 플래그 카탈로그 *(있을 때만)*
10. `traceability.md` - 오퍼레이션 <-> 인터페이스 <-> 컴포넌트 <-> 시퀀스 매트릭스

*events, webhooks, jobs, configuration은 시스템에 해당 요소가 있을 때만 존재.*

---

워크플로: **require -> architect -> backend -> propose -> apply**
상태 확인: `openspec status --change <이름>`
