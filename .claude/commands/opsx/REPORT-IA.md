# Report Information Architecture (IA) — design spec for `/opsx:report`

> Define "what is important and why each element is there" BEFORE building the shell, command, or reports.
> Once agreed, the shell / command / reports conform to this document.
>
> **Language convention.** This harness doc is written in **English**. The GENERATED REPORTS are written in **Korean prose**, but **proper nouns stay in their original form** — do NOT force-translate technology names (`PostgreSQL`, `Mermaid`, `NVIDIA GPU`), methodologies (`ISO/IEC 42010`, `4+1`, `arc42`), component/identifier names (`InferenceService`, `EventBus`, `G4.3`), or statute/article citations. Narrative and explanation are Korean; named things keep their language.

---

## 1. Overall principles

- Purpose of a report = **transform the source so a human understands it quickly** — re-present and highlight, not preserve.
- "Important info" **differs by report type.** planning and design have different readers/goals, so different things belong on top.
- Every element must have a reason to exist, and must fit the whole — no overlapping roles, no gaps.

## 2. Top ↔ Bottom relationship (the two regions' division of labor)

| Region | Role | Reader action | Holds |
|--------|------|---------------|-------|
| **Top** (always visible) | ① what document is this (identity) ② the whole picture ③ **a guide INTO the tabs** | skim before expanding, pick a tab | meta + key summary + tab guide |
| **Bottom** (tabs) | depth on one artifact | open only the tab they care about | the artifact's content (transformed) |

**Key relationship:** each key-summary item on top links to "see details in tab ○○" — the top is the **index/navigation** of the bottom, not a place that reprints bottom content. (Summarize on top → click → jump to the tab.)

## 3. No-duplication rule

- Do not put the same table/content in both the top region and a tab. Summary + guide on top; the full content lives in exactly one tab.
- One exception: the top "tab guide" is a set of links into the tabs, not copied content.
- (Violation example: the earlier design report carried the ISO/IEC 42010 table twice — in a "signature" block and in §1.)

---

## 4. planning report — important-info definition

**Reader/purpose:** someone judging *what/why* the system does, *what it does NOT do*, and *which constraints/conflicts are decisive* (planning reviewer, stakeholder, developer before implementation).

**Top key summary (most important — the big picture before expanding anything):**
1. **What/why** — top-level goals G1..G4 (one line each). From `requirements-document` Scope + `goal-model` top level.
2. **Scope boundary** — In scope / Out of scope. (What is *out* matters especially.)
3. **Decisive constraints/conflicts** — the key obstacles + resolved conflicts that shape the system (e.g. no-face-recognition → non-biometric, high-impact AI). Only the decisive ones, not all.
4. **Tab guide** — one line per tab + links.

**Bottom tabs (detail, pick-to-read) — the question each tab answers:**
| Tab | Question it answers | Highlight |
|-----|---------------------|-----------|
| requirements-document | the whole thing synthesized into one doc? | Scope/Goals/Responsibilities/Behavior |
| business-requirements | what stakeholders actually said (verbatim) | BR list + conflicts |
| goal-model | how goals decompose and what threatens them | goal tree (visualized) · obstacles · resolved conflicts |
| object-model | the concepts and invariants involved | entities · relationships · **invariants** |
| responsibility-model | who/what owns each goal | agent ↔ leaf goal |
| operation-model | what operations/scenarios realize the goals | operations (pre/post/trigger) · scenarios |
| traceability | are requirement↔goal↔responsibility↔operation all linked (gap check) | RTM tables + coverage |

## 5. design report — important-info definition

**Reader/purpose:** someone who needs to know *how* it will be built. And **different roles want different things** (frontend / backend / DBA / ML / infra / security / QA).

**Top key summary:**
1. **Key decisions + rationale** — Solution Strategy bullets (each linking to its ADR). The "why it's built this way" summary.
2. **Role→tab guide** — ISO/IEC 42010 role ↔ concerns ↔ **related tabs (links)**. The design report's signature function. "Your role: read these tabs." (Use the word "탭", not "view".)
3. **Conditional views included** — which of process/data/ml-serving this design includes (and why).

**Bottom tabs — question / primary reader:**
| Tab | Answers | Primary reader | Highlight |
|-----|---------|----------------|-----------|
| Overview | strategy/stack/style/constraints at a glance | everyone | decision summary |
| Logical | how function splits into components | frontend·backend | components·interfaces + **diagram** |
| Process | how it flows at runtime | backend·ML·QA | runtime flow **diagrams** |
| Data | how data is stored/retained | DBA·backend | schema tables · retention policy |
| ML Serving | how inference is served | ML·infra | pipeline **diagram** · GPU |
| Deployment | where/how it deploys | infra | topology **diagram** · node mapping |
| Crosscutting | how security/regulation cuts across | security | regulatory mapping table |
| ADR | what was decided and why | everyone | decision cards (rationale·alternatives) |
| Traceability | are planning↔design all linked | everyone·QA | RTM · role coverage · gaps |

## 5.5 Diagram splitting — overview + detail

Big diagrams don't fit one screen and become unreadable. Like C4 zoom levels (Context→Container→Component), split into **one overview (the big connections) + N detail diagrams (each part zoomed in)**.

**When to split (the trigger):**
- The diagram's nodes fall into **3 or more groups** (tiers, trust zones, pipeline stage-groups, etc.). When there are 3+ groups, draw each group's internals SEPARATELY (as detail diagrams) rather than cramming everything into one picture.
- → Fewer than 3 groups: keep it as a single diagram (clearer). Split only when grouping is genuinely 3+; never reflexively.

**How to split — overview + details inside one navigator widget:**
- **One overview diagram**: the groups and the major links between them. Each group is a single collapsed box (name only); internals omitted.
- **N detail diagrams**: each zooms ONE group, showing all its internal nodes/edges. Detail names map **1:1** to the overview's group boxes.
- **Navigation = a side selection list INSIDE the artifact tab** (not a new root-level tab). Layout within the tab: a small vertical list on the side (`Overview / Group A / Group B / …`) + a display area showing the selected diagram. Selecting an item swaps the displayed diagram. So the nesting is 3 levels: **root tab (artifact) → side list (overview/detail) → diagram tabs (Mermaid/ASCII)**.
- Each diagram (overview and every detail) still keeps the **Mermaid tab + ASCII tab** duo (existing rule).
- Default selection = Overview, so the big picture shows first.

**No over-splitting:** an overview is mandatory whenever you split (details with no overview lose the big picture). Don't inflate a 1–2 group diagram into overview+detail.

## 6. Element-coherence self-check (run after generating a report)

- [ ] Does every top key-summary item link down to a tab? (no floating summary)
- [ ] Is any table/content duplicated between top and tabs? (guide links are the only exception)
- [ ] Does each tab have a distinct "question it answers"? Do two tabs answer the same one?
- [ ] Does the top alone convey "what/why + where to go"?
- [ ] Does bulk info (full tables, verbatim lists) live in tabs, not the top?
- [ ] Diagrams with 3+ groups: split into overview + per-group details inside a side-list navigator? Overview present and default? 1–2 group diagrams left un-split?
- [ ] Korean prose, proper nouns in original form (tech/methodology/identifier/statute names not force-translated)?
- [ ] NO meta/navigation/process commentary in the body ("아래 요약은…/전문은 ○○ 탭/이 보고서는…/한 화면에 요약한다" etc.)? Structure shown by layout, not narrated.
