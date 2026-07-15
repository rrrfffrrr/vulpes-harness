---
schema-version: 1.1.0
document-version: 0
---

# Operation model

<!-- Leaf goals operationalized into operations.
     Semi-formal: conditions in natural language, not temporal logic.
     Agent ownership lives in the responsibility model.
     Replace every <...>.
     Delete guidance comments when done. -->

## Operations

### Operation: <name>

- Pre-condition: <what must hold before>
- Post-condition: <what holds after>
- Trigger: <what initiates it>

## Scenarios

<!-- At least one per operation, plus one per resolved obstacle that adds runtime behavior.
     For weaken-goal / out-of-software substitute-agent resolutions, note "no scenario applies". -->
### Scenario: <name>

- Given <context>
- When <action/operation>
- Then <outcome; reference the satisfied goal by name>
