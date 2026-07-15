# SVG diagram style

Documentation diagrams are **hand-authored SVG committed to the repo** and embedded via `<img>`.
Auto-layout engines (mermaid, D2, Graphviz, etc.) **cannot control edge attachment or layout and offer limited theming** - we evaluated them all and they hit the same wall.
So "must-look-good" diagrams are drawn by these rules, not delegated to an engine.
Quick drafts / simple flows may use mermaid.

> GitHub blocks inline `<svg>` in Markdown, so **commit the diagram as a .svg file** and embed it as an image.
> Then it renders on GitHub/GitLab/VS Code alike.
>
> **viewBox fits the content tightly (important)**: set `viewBox` (`minX minY W H`; the origin need not be 0) to the actual content bounds (accounting for text ascenders/descenders, arrow markers, and `stroke` width), leaving only the **minimum safe margin of 4px** to avoid clipping.
> No generous margins: at a fixed display width (`width=NN%`), large margins render the content smaller and **hurt legibility**.
> Content bounds differ per diagram, so viewBox/size/layout **cannot be common** (per-diagram).

## Fixed - shared style tokens (identical across all diagrams)

- **Root**: `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 W H" width="W" height="H" font-family="sans-serif" font-size="13">`
- **Arrow marker**:

  ```xml
  <marker id="arr" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto">
    <path d="M0,0 L7,3 L0,6 Z" fill="#557"/>
  </marker>
  ```

- **Edges**: `stroke="#557" stroke-width="1.5" fill="none" stroke-linejoin="round" stroke-linecap="round" marker-end="url(#arr)"`
- **Edges are orthogonal (`]` brackets)** - no curves.
  Round the corners/ends with `stroke-linejoin="round"` + `stroke-linecap="round"`.
- **Return/self-loop** attaches to a clean node face (e.g. top center).
  **Keep bracket protrusion minimal - hug the node row** (a large fixed offset wastes vertical space).
  Never invent a node/state just to make it render (model truth first).
- **Node box**: `rx="6"`, primary `fill="#eef2ff" stroke="#557"`, secondary/menu `fill="#f3f0ff" stroke="#779"`.
- **Node text**: `fill="#1a2a55"` (secondary `#33305a`), `text-anchor="middle"`.
- **Edge labels**: `fill="#555"`, `text-anchor="middle"`, **short** (detail goes in prose).
- **ASCII over Unicode symbols** in text (`->` `/` etc.).
- **Embed**: `<img alt="..." src="x.svg" width="NN%">`.

## Variable - per-diagram (cannot be common)

- `viewBox` W x H, overall orientation (horizontal/vertical)
- node positions/sizes, label positions, distribution shape (e.g. a hub: trunk -> bus -> branches)
- display size `width="NN%"` (default 50%, tune for legibility - wide ones 60%+)

## Layout principles (tune per diagram, by eye)

Size/placement is adjusted by eye every time - don't freeze coordinates; tune with these heuristics (graph-drawing aesthetics + flowchart conventions).

- **Consistent direction**: one direction per diagram (left->right or top->bottom), kept throughout.
- **Minimize edge crossings** (most important): if crossings appear, reorder/reposition nodes or split the diagram.
  Don't route edges across nodes.
- **Minimize bends**: few bends even with orthogonal routing.
- **Alignment + even spacing**: uniform node size/spacing (grid-like).
  No raggedness.
- **No overlap**: nodes, labels, and label-vs-edge.
- **Concise labels**: short / verb-first; branches as yes/no.
- **Color for structure**: 2-4 colors (within the style tokens).
- **Inner balance vs outer tightness**: keep *inner* spacing breathable, but the *outer* viewBox margin tight at 4px.
  (Inner balance != outer margin.)

## Examples

`management-tycoon: openspec/changes/tycoon-gdd/{core-loop,game-flow,screen-flow}.svg`
