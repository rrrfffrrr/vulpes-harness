---
schema-version: 1.2.1
document-version: 0
---

# Goal model

<!-- Semi-formal: natural language + AND/OR structure.
     No temporal logic.
     Every goal phrased with a pattern keyword: Achieve / Maintain / Avoid / Cease.
     Replace every `<...>` placeholder below, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Goal hierarchy

<!-- One or more top-level business goals; no synthetic super-root.
     Refine to leaves.
     Lead each leaf with [Requirement] (software) or [Expectation] (environment) -
     the marker sits before the goal id, never at the end of the line. -->
- **G1: Achieve `<top-level goal>`**
  - (AND) [Requirement] G1.1: Maintain `<subgoal - all needed>`
  - (AND) G1.2: Achieve `<subgoal>`
    - (OR) [Requirement] G1.2.a `<alternative>`
    - (OR) [Requirement] G1.2.b `<alternative>`

## Domain properties

<!-- Facts/laws that hold regardless of the system. -->
- DP1: `<descriptive fact about the environment>`

## Obstacles

<!-- kind in {prevent, reduce, mitigate, restore, weaken-goal, substitute-agent} -->
- **[`<goal id>`] -> [Obstacle: `<name>`]** `<condition that violates the goal>`
  -> **[Resolution]** `<how it is resolved>` **(kind: `<kind>`)**

## Resolved conflicts

<!-- If business requirements conflicted: the conflict and the rule chosen.
     Omit section if none. -->
- **`<conflict in plain words>`:** Adopted rule - `<the rule chosen here>`
