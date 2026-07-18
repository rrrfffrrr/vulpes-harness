---
schema-version: 1.2.0
document-version: 0
---

# Traceability matrix

<!-- BABOK requirements traceability - separate from the model prose.
     All linking lives here.
     Relationship kinds: derive, satisfy, depends, rationale.
     Replace the example rows.
     Delete guidance comments when done. -->

## Business requirement -> goals

<!-- Constraint/decision BRs that yield no leaf goal are traced here as rationale.
     One value per cell - a BR deriving several goals repeats the row per goal (rules/writing.md tables rule). -->
| BR | Goal | Kind | Rationale |
|----|------|------|-----------|
| `<BR1>` | `<goal id>` | derive | `<why>` |

## Goal -> leaf (Requirement / Expectation)

| Goal | Leaf | Type (Req/Exp) | Kind |
|------|------|----------------|------|
| `<G1>` | `<leaf id>` | Req | derive |

## Leaf -> agent (responsibility)

| Leaf | Agent | Kind |
|------|-------|------|
| `<leaf id>` | `<Agent>` | satisfy |

## Leaf -> operation

| Leaf | Operation | Kind |
|------|-----------|------|
| `<leaf id>` | `<Operation>` | satisfy |

## Operation -> scenario

<!-- One row per operation-scenario link; repeat rows. -->
| Operation | Scenario | Domain file |
|-----------|----------|-------------|
| `<Operation>` | `<scenario name>` | `scenarios/<domain>.md` |

## Coverage notes

- `<any BR not covered, any leaf without agent/operation, operations no scenario exercises, deferred items>`
