---
name: "OPSX: Report"
description: Render an OpenSpec change (planning or design) into a single self-contained HTML report — top summary area + per-stage tabs.
category: Workflow
tags: [workflow, report, html, planning, design, experimental]
---

Render the artifacts of an OpenSpec change into ONE self-contained HTML report. Works for any change with markdown artifacts (planning, design, or other schemas). This is a presentation step — it does not modify the change.

**Core principle: the goal is to make the content easy for a human to understand, NOT to preserve the source verbatim.** Source artifacts are written compactly for machines/spec-fidelity (terse identifier lists, arrowed text, dense tables). The report's job is to TRANSFORM that into something a reader grasps quickly: draw real diagrams from text, lay out structure visually, group and label. Do not paste source blocks unchanged and call it a report — re-present them. (Faithfulness to *facts* still holds — invent nothing — but faithfulness to *formatting* is explicitly NOT a goal.)

The report has a fixed two-region layout:
- **Top region** (always visible, outside the tabs): cover/meta + key summary.
- **Bottom region**: one **tab per stage** (per artifact), inline-JS tab switching.

---

**Input**: The argument after `/opsx:report` is the change name (e.g. `kist-safety-platform-v3`). Optionally an output path.

**Steps**

1. **Resolve the change.** If no name given, list `openspec/changes/*/` (excluding `archive/`) and ask which to render. Read its artifacts in dependency order — get the order from `openspec status --change "<name>" --json` (the `artifacts` array). Skip artifacts whose file does not exist (e.g. omitted conditional views) — do NOT invent a tab for a missing artifact.

2. **Read every artifact markdown fully.** The report content is the artifacts, verbatim in meaning. Do NOT add facts not in the source.

3. **Pick the output path.** Default `reports/<change-name>.html`. `mkdir -p reports` if needed.

4. **Generate the HTML by filling the fixed shell** at `.claude/commands/opsx/report-shell.html`. The shell holds the canonical CSS (light/dark theme + toggle), the tab JS (with hashchange), and the diagram-navigator JS/CSS — DO NOT rewrite or restyle them; every report shares one look. Fill only the `{{PLACEHOLDER}}` slots: `{{TITLE}}`, `{{COVER_AND_SUMMARY}}` (top region per IA §4/§5), `{{TABBAR_BUTTONS}}`, `{{STAGE_PANELS}}` (use the diagram-widget markup shown in the shell comments — `.dgm` for single, `.dgm-nav` for split), `{{FOOTER}}`, and `{{MERMAID_BUNDLE}}` (inline `<script>` with mermaid.min.js if any diagrams, else empty). For planning, set `--maxw:900px` in the one `:root` line; design keeps 960px. Follow the LAYOUT and RULES below for what goes in each slot.

5. **Verify** the file exists (`ls -la`), report line count + size, and confirm zero external references.

**LAYOUT (fixed)**

```
┌─ Top region (always visible) ───────────────────────────┐
│  Cover/meta: project name · doc type (planning|design)   │
│              · methodology · source change · generated    │
│  Key summary: the whole picture + a guide into the tabs   │
│              (contents differ by report type — see IA)    │
├─ Tab bar ────────────────────────────────────────────────┤
│ [stage 1] [stage 2] [stage 3] ...   (one tab per artifact)│
├─ Tab panels (only active shown) ─────────────────────────┤
│  full rendered content of the selected artifact           │
└──────────────────────────────────────────────────────────┘
```

- Tab order = artifact dependency order. Tab label = human stage name (e.g. "비즈니스 요구사항", "Goal Model", "Logical View").
- First tab active by default. Clicking a tab shows its panel, hides others.

**INFORMATION ARCHITECTURE (the binding spec for what goes where).** Follow `REPORT-IA.md` (next to this command). The essence:
- **Top = navigation, not duplication.** The top region carries (1) identity/meta, (2) a key summary that is the WHOLE picture at a glance, (3) a guide INTO the tabs. Every key-summary item must link down to the tab where it is detailed. The top is the index of the bottom — it summarizes and points, it does not reprint tab content.
- **Bottom = depth on demand.** Each tab answers ONE clear question (see the per-artifact question table in REPORT-IA.md). No two tabs answer the same question; nothing is left without a home.
- **"Important info" differs by report type** — put the right 3 things on top:
  - **planning top**: ① top-level goals G1..G4 (what/why) ② scope boundary, especially what is OUT ③ the DECISIVE obstacles/conflicts (not all of them) — plus the tab guide.
  - **design top**: ① key decisions + rationale (each linking to its ADR) ② role→tab guide (ISO 42010 mapping; word it "탭", link the tabs) ③ which conditional views are included and why.
- **No duplication.** Do not place the same table/content both in the top region and in a tab. The only exception is the top "tab guide", which is links into the tabs, not copied content. (The earlier design report putting the ISO-42010 table in both a "signature" block and §1 was the violation to avoid.)
- **Self-check before done** (from REPORT-IA.md §6): every top item links to a tab? no top/tab content duplicated? each tab's question distinct? top alone conveys "what/why + where to go"? bulk data (full tables, verbatim lists) lives in tabs, not the top?

**RULES (non-negotiable — these are why the report is reliable)**

1. **Self-contained.** Single `.html`. ALL CSS inline in `<style>`; ALL JS inline in `<script>` — including the Mermaid library, which is INLINE-BUNDLED (rule 3), never CDN-linked. NO external CDN/font/`@import`/`<script src=...>`/`http(s)://` references of any kind. Must open and fully render (Mermaid included) offline. (Verify with grep that no `src=`/`href=` points to a URL and no `https://` remains, before finishing.)
2. **Tabs = inline JS.** A small `<script>` toggles `.active` on panels/tab-buttons. Support deep links: on load, if `location.hash` matches a tab id, open that tab. Give each tab panel an `id` so `report.html#stage-goal-model` works.
3. **Diagrams are DRAWN by the report, not copied from source.** The source fenced blocks are CONTENT (a list of nodes/edges/steps), NOT finished diagrams — often just arrowed text. The report must turn that content into ACTUAL diagrams. Each diagram is a small **two-tab widget**: a **Mermaid** tab and an **ASCII** tab. Both render the SAME content; they need not look identical.
   - **ASCII tab** = an ASCII-ART diagram YOU draw from the source content — show real structure: hierarchy as a `├── └──` tree, branch/merge flows with lines that visibly split and rejoin, etc. Put it in `<pre><code>` (`white-space: pre`, monospace, `overflow-x:auto`), `<` `>` `&` escaped. **Do NOT paste the source text block verbatim** — that is the exact mistake to avoid. If the source is "A→B→C / D→B", the ASCII tab is a drawn graph where you can SEE D and A converging into B, not the two lines retyped.
   - **Mermaid tab** = the same content as a proper Mermaid diagram, using the kind that FITS: `sequenceDiagram` for runtime/message flows (actors + ordered messages over time), `flowchart` (LR/TD) for topology / building-block / pipeline / branch-merge. It is a different representation than the ASCII tab and that is fine. Put it in `<div class="mermaid">`. Use only nodes/edges/steps the source content states — invent nothing.
   - Drawing fidelity: both tabs must contain every node/edge/step the source lists, and contradict neither the source nor each other. A widget that just reprints the raw source text in the ASCII tab is a FAILURE.
   - **Mermaid library is INLINE-BUNDLED, not CDN.** Obtain the dist once at generation time (`npm pack mermaid` → extract `dist/mermaid.min.js`) and embed its full contents in an inline `<script>` (use shell `cat part1 mermaid.min.js part2 > out.html` — never Read the 3MB file into context). NO `<script src="https://...">`. Must render Mermaid offline.
   - **Fallback is automatic.** Default the widget to the Mermaid tab; render each `.mermaid` in try/catch. If Mermaid fails to load/parse/render, auto-switch that widget to its ASCII tab and mark the Mermaid tab unavailable. The ASCII tab lives in the DOM (hidden by tab-inactive class, not removed) so it is readable even with no JS / broken bundle.
4. **Markdown tables → real `<table>`.** Never paste pipe-table text. Convert `**bold**`, backtick-code, `>` quotes to proper HTML.
5. **No fabrication.** Only what the source artifacts contain. Summaries/reordering are fine; new facts, stacks, numbers, or sections are not. No invented author/date metadata (the source has none).
6. **No cross-reference clutter in prose.** Mirror the source: ids like `G4.3` stay where the source has them; do not add `(BR..)`/file-path references that the source doesn't have.
6b. **No meta / navigation / process commentary.** Never narrate the report's own structure or purpose in the body. Banned: "아래 요약은 큰 그림과 길잡이이고, 전문은 각 탭에", "요약 (전문은 ○○ 탭)", "이 보고서는 …", "모든 역할의 진입점", "…을 한눈에/한 화면에 요약한다", "상단 길잡이를 따른다", and any "이 섹션에서는 …을 다룬다" sentence. Structure is conveyed by the LAYOUT (tabs, headings, the tab-guide links) — not by sentences describing it. Show the content; do not announce it. A heading or a link is fine; a sentence explaining where things live is not. (User-standing feedback — see memory `no-meta-commentary`.)
6c. **No decorative wrappers.** Do not wrap a table, list, or section in a callout/card box (e.g. the `role-hint` dashed box) just to "emphasize" it — a heading + the table/list is enough, and the shell's structural styling already separates sections. The `role-hint` style exists only for genuinely auxiliary one-liners, not to frame primary content (the role→tab guide table, scope lists, etc. are primary — no box). Don't add a `<div class="lbl">다이어그램</div>` or similar label above a diagram side-list; the side-list items speak for themselves.
7. **Readable, professional, restrained.** Korean-friendly SYSTEM font stack (no web fonts). Body width ~900px for planning, ~960px for design (diagrams/tables are wider). Section rules, monospace identifiers, small badges for markers (`[Requirement]`, ADR `Status`). No heavy color or animation — it is a report.
   - **Language: write the report in Korean prose, but keep proper nouns in their original form.** Do NOT force-translate technology names (`PostgreSQL`, `Mermaid`, `NVIDIA GPU`), methodologies (`ISO/IEC 42010`, `4+1`, `arc42`, `KAOS`), component/identifier names (`InferenceService`, `EventBus`, `G4.3`, `BR1`), or statute/article citations — render them as-is. Narrative, labels, and explanation are Korean; named things keep their language. (This command/spec itself stays in English; only the generated report is Korean.)
8. **Anchor integrity + clickable cross-links.** Every tab-bar entry and any in-page link must point to a real tab-panel id; no dead links. Any table/list that names a tab (e.g. a "which tab to read" guide) must make those names **clickable `<a href="#stage-...">` links**, not plain text. AND the tab JS must open the target tab on `hashchange` (not only on initial load) — wrap the hash-to-tab logic in a function and call it both at load and from a `window.addEventListener('hashchange', …)`, or clicking an in-page tab link on an already-loaded page does nothing.
9. **Footer.** Source path (`openspec/changes/<name>`) and the stage note: planning → "기획 단계 — 구현/코드 없음"; design → "기술 설계 단계 — 구현/코드 없음".

**Top-region rendering notes (what to pull — full spec in REPORT-IA.md §4–5)**
- **planning**: top-level goals G1..G4 + scope in/out + the decisive obstacles/conflicts, each linking to its tab.
- **design**: the role→tab guide is a table with columns "역할 / 관심사 / 관련 탭"; the "관련 탭" cell holds `<a href="#stage-...">` links (rule 8). Use the word **탭**, not "view" (the source's 4+1 "view" term confuses here). Render this guide ONCE — do not also label a separate block "signature" or repeat the table.

**Output**

Report: output path, line count + size, tabs created (one per stage, in order), diagram widgets created (count, each with Mermaid+ASCII), confirmation of "self-contained: 0 external refs (Mermaid inline-bundled)", and any artifact skipped because its file was absent (e.g. an omitted conditional view).

**Guardrails**
- Presentation only — never edit the change's artifacts. (Mermaid is generated INTO the report from the source ASCII; the source `.md` is not modified.)
- If an artifact is large, the tab panel holds all of it — do not truncate content to fit. Tabs exist so length is not a problem.
- Verify before declaring done: external-ref = 0 (no `https://`, no `<script src>`), ASCII tabs byte-intact, Mermaid bundle present inline.
- **Diagram review (use a separate subagent for any change with diagrams).** After generating, have an independent subagent check each diagram widget: (a) ASCII tab matches the source block byte-for-byte; (b) the generated Mermaid is valid syntax AND represents the same nodes/edges/direction as the ASCII (no invented or dropped elements); (c) the fallback works — Mermaid-tab failure leaves the ASCII tab reachable and complete. Fix any Mermaid that contradicts its ASCII; the ASCII is the source of truth.
- If the output file already exists, ask whether to overwrite or write a new path.
