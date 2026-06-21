# SVG 다이어그램 스타일

문서용 다이어그램은 **손수 작성한 SVG를 repo에 커밋**하고 `<img>`로 임베드한다. 자동 레이아웃 도구(mermaid 등)는 엣지 부착/self-loop 제어가 안 되므로, "잘 보여야 하는" 다이어그램은 이 규칙으로 직접 그린다. 빠른 초안/단순 흐름은 mermaid도 가능.

> GitHub은 마크다운 내 인라인 `<svg>`를 막으므로 **반드시 .svg 파일로 커밋**하고 이미지로 임베드한다. 그러면 GitHub/GitLab/VS Code 어디서나 렌더된다.

> **잘림 방지 (중요)**: `viewBox`는 모든 요소를 충분한 여백과 함께 감싸야 한다 - 텍스트의 ascender, 화살표 마커, `stroke-width`까지 고려해 가장자리에 **~12px 이상 패딩**을 둔다. 라벨/도형을 `viewBox` 경계(`0` 또는 `W`/`H`)에 붙이지 말 것. (상단 라벨을 `y`가 0에 가깝게 두면 윗부분이 잘린다.)

## 고정 - 공통 스타일 토큰 (모든 다이어그램 동일)

- **루트**: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 W H" width="W" height="H" font-family="sans-serif" font-size="13">`
- **화살표 마커**:
  ```xml
  <marker id="arr" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto">
    <path d="M0,0 L7,3 L0,6 Z" fill="#557"/>
  </marker>
  ```
- **엣지**: `stroke="#557" stroke-width="1.5" fill="none" stroke-linejoin="round" stroke-linecap="round" marker-end="url(#arr)"`
- **엣지는 직각(`]` 브래킷)** - 곡선 금지. 모서리/끝은 `stroke-linejoin="round"` + `stroke-linecap="round"`로 둥글게.
- **되돌이/자기루프**는 대상 노드의 깔끔한 면(예: 상단 중앙)에 부착. 렌더 때문에 없는 노드/상태를 만들지 말 것(모델 진실 우선).
- **노드 박스**: `rx="6"`, 기본 `fill="#eef2ff" stroke="#557"`, 보조/메뉴류 `fill="#f3f0ff" stroke="#779"`.
- **노드 텍스트**: `fill="#1a2a55"`(보조 `#33305a`), `text-anchor="middle"`.
- **엣지 라벨**: `fill="#555"`, `text-anchor="middle"`, **짧게** (상세는 본문 산문에).
- **텍스트의 비-openspec 유니코드는 ASCII로** (ASCII 선호 규칙; `->` `/` 등).
- **임베드**: `<img alt="..." src="x.svg" width="NN%">`.

## 가변 - 다이어그램별 (공통일 수 없음)

- `viewBox`의 W x H, 전체 방향(가로/세로)
- 노드 위치/크기, 라벨 위치, 분배 방식(예: 허브는 트렁크->버스->분기)
- 표시 크기 `width="NN%"` (기본 50%, 가독성에 맞춰 조절 - 넓은 건 60%+)

## 예시

`management-tycoon: openspec/changes/tycoon-gdd/{core-loop,game-flow,screen-flow}.svg`
