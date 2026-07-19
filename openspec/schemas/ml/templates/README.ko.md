# ml 아티팩트 읽는 법

[English](README.md) | [한국어](README.ko.md)

**ml** 스키마(Model Cards + Datasheets for Datasets + ML Test Score + ISO/IEC 5338) 아티팩트 - 아키텍처 ml-serving-view 한 단계 아래의 모델별 계약, 추론 위치와 무관하게 동일.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 모델 인벤토리와 독자 맵.

**읽기 순서:**

1. `overview.md` - 모델 인벤토리 / 독자 맵 / 조건부 아티팩트
2. `models.md` - 모델별 계약: intended use, 신뢰도 의미론 포함 I/O, 열화/폴백, caveats
3. `data.md` - 자체 학습 데이터 datasheet *(있을 때만)*
4. `evaluation.md` - 릴리스 게이트, 슬라이스, 회귀 정책, 모니터링 신호
5. `lifecycle.md` - 버저닝, 업데이트/롤백 절차, 재학습 트리거, 폐기
6. `traceability.md` - 오퍼레이션 <-> 모델 <-> 표면 <-> 게이트 매트릭스

*data는 자체 학습/파인튜닝 데이터를 소유할 때만 존재. 서빙 API 표면은 backend 변경에, 온디바이스 소비는 frontend/game-ui에 있으며 모두 모델을 이름으로 참조.*

---

워크플로: **require -> architect -> ml (아키텍처에 ml-serving-view가 있을 때) -> propose -> apply**
상태 확인: `openspec status --change <이름>`
