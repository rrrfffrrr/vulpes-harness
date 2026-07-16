---
schema-version: 1.2.0
document-version: 0
---

# Test data & environment requirements

<!-- 29119-3 documentation types, merged.
     WHAT is needed - never how to provision it.
     Replace every `<...>` placeholder and example row.
     Delete guidance comments when done. -->

## Test data requirements

| Scenario group | Data set / state | Notes |
|----------------|------------------|-------|
| `<operation/group>` | `<what must exist, concrete shape>` | `<reset/isolation needs>` |

- **Personal data**: `<synthetic data policy; honoring persistence retention/PII classes when present>`

## Test environment requirements

- **Real vs stubbed**: `<components/stores that must be real; external systems stubbed (payment, webhook receivers, ...)>`
- **Device / platform coverage**: `<from the frontend or game-ui overview, by reference>`
- **Clock/time control**: `<needed for jobs/retention scenarios, or none>`
