---
schema-version: 1.2.0
document-version: 0
---

# Acceptance scenarios - domain index

<!-- This file lives at scenarios/index.md.
     Index ONLY - every scenario lives in a per-domain file (scenarios/<domain>.md).
     Domains mirror the requirements scenarios domains.
     Replace every `<...>` placeholder; repeat the row per domain.
     Delete guidance comments when done. -->

| Domain | File | Scope |
|--------|------|-------|
| `<domain>` | `<domain>.md` | `<one-line scope>` |

## Per-domain file skeleton

<!-- Copy the block below (without the outer fence) into each scenarios/<domain>.md,
     repeat the scenario block per scenario, then delete this section from the index. -->

````markdown
---
schema-version: 1.2.0
document-version: 0
---

# Acceptance scenarios - `<domain>`

<!-- Cross-layer journeys, grouped by requirements operation.
     Each realizes named acceptance criteria; surfaces by reference, contracts never restated.
     Gherkin, 3-5 steps, concrete example values. -->

## Operation: `<name>`

### Scenario: `<name>`

- **Realizes**: `<operation>` - `<acceptance criterion>`
- **Surfaces**: `<METHOD path / screen / flow / job / store names>`

```gherkin
Given <context with concrete example values>
When <the action>
Then <the observable outcome>
```
````
