---
schema-version: 1.2.1
document-version: 0
---

# Test data & environment requirements

<!-- 29119-3 documentation types, merged.
     WHAT is needed - never how to provision it.
     Replace every `<...>` placeholder and example row.
     Delete guidance comments when done. -->

## Test data requirements

| Scenario group | Data set | State | Resetting |
|----------------|----------|-------|-----------|
| `<operation/group>` | `<records that must exist, concrete shape>` | `<condition those records are in>` | `<how runs stay isolated: reset steps, or fresh data per run>` |

- **Personal data**: `<synthetic data policy; honoring persistence retention/PII classes when present>`

## Test environment requirements

- **Real components**: `<components/stores that must be real>`
- **Stubbed systems**: `<external systems stubbed (payment, webhook receivers, ...)>`
- **Device / platform coverage**: `<from the frontend or game-ui overview, by reference>`
- **Clock/time control**: `<needed for jobs/retention scenarios, or none>`
