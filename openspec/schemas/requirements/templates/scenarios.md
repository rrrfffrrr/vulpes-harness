---
schema-version: 1.2.0
document-version: 0
---

# Operational scenarios - domain index

<!-- This file lives at scenarios/index.md.
     Index ONLY - every scenario lives in a per-domain file (scenarios/<domain>.md).
     Domains mirror the goal model's top-level goals.
     Replace every `<...>` placeholder; repeat the row per domain.
     Delete guidance comments when done. -->

| Domain | File | Top-level goal |
|--------|------|----------------|
| `<domain>` | `<domain>.md` | `<G1>` |

## Per-domain file skeleton

<!-- Copy the block below (without the outer fence) into each scenarios/<domain>.md,
     repeat the scenario block per scenario, then delete this section from the index. -->

````markdown
---
schema-version: 1.2.0
document-version: 0
---

# Operational scenarios - `<domain>`

## `<Scenario name>`

Trigger: `<agent (responsibility-model name) or schedule/time condition>` - outcome: `<satisfied goal, by name>`

```mermaid
sequenceDiagram
  %% Lifelines are AGENTS (responsibility-model names); messages are OPERATIONS (operation-model names).
  participant U as HumanAgent
  participant S as SoftwareAgent
  U->>S: Operation
  S-->>U: outcome
```

**Obstacle variant**: `<obstacle id - what changes in the interaction>` (only when a resolved obstacle changes it)
````
