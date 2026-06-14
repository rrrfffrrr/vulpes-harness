# Goal Model (KAOS)

<!-- Semi-formal: natural language + AND/OR structure. No temporal logic.
     Every goal phrased with a pattern keyword: Achieve / Maintain / Avoid / Cease.
     Leaf goals marked [Requirement] (software) or [Expectation] (environment). -->

## Goal Hierarchy
<!-- One or more top-level business goals; no synthetic super-root. Refine to leaves.
     - G1: Achieve <...>
       - (AND) G1.1: Maintain <...>
       - (AND) G1.2: Achieve <...>
         - (OR) G1.2.a <...> [Requirement] / (OR) G1.2.b <...> [Requirement]
     Mark each leaf [Requirement] or [Expectation]. -->

## Domain Properties
<!-- Facts/laws that hold regardless of the system. -->

## Obstacles
<!-- For each obstacle: the goal it threatens, the obstacle, and the resolution with its
     kind ∈ {prevent, reduce, mitigate, restore, weaken-goal, substitute-agent}.
     [Goal] → [Obstacle] → [Resolution] (kind: <kind>) -->

## Resolved Conflicts
<!-- If business requirements conflicted: the conflict and the rule chosen here. Omit if none. -->
