---
schema-version: 1.2.0
document-version: 0
---

# Operation model

<!-- Leaf goals operationalized into operations.
     Semi-formal: conditions in natural language, not temporal logic.
     Agent ownership lives in the responsibility model.
     Replace every `<...>` placeholder, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Operations

### Operation: `<name>`

- Pre-condition: `<what must hold before>`
- Post-condition: `<what holds after>`
- Trigger: `<what initiates it>`
- Acceptance criteria:
  - `<measurable pass/fail condition stakeholders accept the operation by (BABOK 10.1)>`

## Scenarios

<!-- At least one per operation, plus one per resolved obstacle that adds runtime behavior.
     For weaken-goal / out-of-software substitute-agent resolutions, note "no scenario applies". -->
### Scenario: `<name>`

- Given `<context>`
- When `<action/operation>`
- Then `<outcome; reference the satisfied goal by name>`
