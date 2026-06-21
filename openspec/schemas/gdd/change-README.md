<!-- 정적 공통 가이드 — opsx 커맨드가 change 생성 시 이 파일을 그 폴더의 README.md로 복사한다.
     프로젝트별로 손대지 말 것(수정 대상 아님). 갱신은 하네스의 이 파일에서만. -->

# 이 폴더 읽는 법 — gdd

이 change는 **gdd** 스키마(게임 디자인 문서) 산출물입니다. 의도된 게임이 "어떻게 플레이/보이/들리/팔리나". 구현(apply) 단계는 없는 살아있는 문서입니다.

**여기부터:** [`overview.md`](overview.md) — 엘리베이터 피치·필러·범위. 전체를 잡은 뒤 관심 섹션으로.

**읽는 순서:**
1. `overview.md` — 한 장 프레이밍(장르·플랫폼·필러·USP·MVP 범위)
2. `gameplay.md` — 코어 루프·상태·승패
3. `mechanics.md` — 시스템 규칙·진행·경제
4. `world-narrative.md` — 배경·캐릭터·콘텐츠 구조 *(해당 시)*
5. `art-direction.md` — 비주얼 방향
6. `audio-direction.md` — 사운드 방향
7. `ux-ui.md` — 화면 흐름·컨트롤·접근성
8. `tech.md` — 엔진·플랫폼·성능·세이브
9. `monetization.md` — 비즈니스 모델·수익화 *(해당 시)*
10. `production.md` — 시장·MoSCoW 피처·마일스톤·리스크(종합)

*(world-narrative·monetization은 게임에 해당할 때만 존재 — 없으면 그 파일이 없습니다.)*

> 전체 워크플로: **plan → gdd → propose → apply**. 산출물·읽는 순서·완료 상태는 `openspec status --change <이름>`.
