# game-ui 아티팩트 읽는 법

[English](README.md) | [한국어](README.ko.md)

**game-ui** 스키마(UI 레이어 분류 + safe area/판독성 하한 + 액션 기반 입력 + Game Accessibility Guidelines/XAG + UML 상태 머신 + wireflow) 아티팩트 - PC/콘솔/모바일/휴대기 게임 UI의 구현 가능한 스펙, 아키텍처와 GDD 한 단계 아래.
구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 시스템 전역 UI 어휘(UI 레이어, safe area와 스케일, 판독성 하한, 위젯 상태, 로컬라이제이션 예산, 접근성 목표)와 독자 맵.

**읽기 순서:**

1. `overview.md` - 플랫폼·입력 장치 / UI 레이어 / safe area·스케일 / 판독성 / 위젯 상태 enum / 로컬라이제이션 / 접근성 목표 / 독자 맵
2. `design-tokens.md` - 색 / 폴백 포함 타이포 / 치수 / 모션 / 테마 토큰 *(있을 때만)*
3. `widgets.md` - 공유 위젯: 해부도, 변형, 상태, 장치별 입력 동작, 텍스트 예산
4. `screens.md` - 화면·모달별: 레이아웃 + safe area, 화면 상태, 데이터, 장치별 조작
5. `hud.md` - HUD 요소별: UI 레이어, 배치, 표시 규칙, 커스터마이즈 훅, 피드백 채널 *(+ 자막 섹션, 있을 때만)*
6. `flows/index.md` - 도메인 인덱스; `flows/<도메인>.md` - 부트 플로, 내비게이션 맵, 모달·일시정지 관례, statechart
7. `input.md` - 콘텍스트별 액션 셋, 장치별 바인딩, 글리프, 리맵, 핫스왑
8. `settings.md` - 옵션 인벤토리: 옵션별 타입/범위/기본값/효과/접근성 매핑
9. `traceability.md` - GDD·요구사항 <-> 화면·HUD <-> 플로 <-> 위젯 <-> 입력 <-> 설정 매트릭스

*design-tokens는 토큰 기반 스타일링일 때만, 자막 섹션은 음성·중요 오디오가 있을 때만 존재.*

---

워크플로: **require -> gdd -> architect -> game-ui -> propose -> apply**
상태 확인: `openspec status --change <이름>`
