# 아티팩트 읽는 법 - gdd

[English](README.md) | [한국어](README.ko.md)

**gdd** 스키마(게임 디자인 문서) 아티팩트 - 만들려는 게임이 어떻게 플레이되고, 보이고, 들리고, 출시되는지.
살아있는 문서이며 구현(apply) 단계 없음.

모든 아티팩트는 frontmatter로 시작: `schema-version`(작성 당시 스키마 semver)과 `document-version`(리비전 카운터 - 최초 작성 0, 개정마다 +1).

**여기서 시작 ->** [`overview.md`](overview.md) - 전체 그림을 잡은 뒤 필요한 섹션으로 이동.

**읽기 순서:**

1. `overview.md` - 프레이밍 (장르 / 플랫폼 / 필러 / USP / MVP 범위)
2. `gameplay.md` - 코어 루프 / 상태 / 승패
3. `mechanics.md` - 시스템 / 진행 / 경제
4. `world-narrative.md` - 세계관 / 캐릭터 / 콘텐츠 구조 *(있을 때만)*
5. `art-direction.md` - 비주얼 디렉션
6. `audio-direction.md` - 오디오 디렉션
7. `ux-ui.md` - 화면 흐름 / 조작 / 접근성
8. `tech.md` - 엔진 / 플랫폼 / 성능 / 저장
9. `monetization.md` - 비즈니스 모델 / 수익화 *(있을 때만)*
10. `production.md` - 시장 / MoSCoW 기능 / 마일스톤 (종합본)

*world-narrative와 monetization은 게임에 해당 요소가 있을 때만 존재.*

---

워크플로: **require -> gdd -> propose -> apply**
상태 확인: `openspec status --change <이름>`
