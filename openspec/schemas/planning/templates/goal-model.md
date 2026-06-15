# Goal Model

<!-- Semi-formal: natural language + AND/OR structure. No temporal logic.
     Every goal phrased with a pattern keyword: Achieve / Maintain / Avoid / Cease.
     Replace every <...> below. Delete guidance comments when done. -->

## Goal Hierarchy

<!-- One or more top-level business goals; no synthetic super-root. Refine to leaves.
     Mark each leaf [Requirement] (software) or [Expectation] (environment). -->
- **G1: Achieve <top-level goal>**
  - (AND) G1.1: Maintain <subgoal — all needed> [Requirement]
  - (AND) G1.2: Achieve <subgoal>
    - (OR) G1.2.a <alternative> [Requirement]
    - (OR) G1.2.b <alternative> [Requirement]

## Domain Properties

<!-- Facts/laws that hold regardless of the system. -->
- DP1: <descriptive fact about the environment>

## Obstacles

<!-- kind ∈ {prevent, reduce, mitigate, restore, weaken-goal, substitute-agent} -->
- **[<goal id>] → [Obstacle: <name>]** <condition that violates the goal>
  → **[Resolution]** <how it is resolved> **(kind: <kind>)**

## Resolved Conflicts

<!-- If business requirements conflicted: the conflict and the rule chosen. Omit section if none. -->
- **<conflict in plain words>:** 채택 규칙 — <the rule chosen here>
