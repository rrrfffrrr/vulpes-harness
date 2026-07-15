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

<!-- Constraint/decision BRs that yield no leaf goal are traced here as rationale. -->
| BR | Goal(s) | Kind | Rationale |
|----|---------|------|-----------|
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

## Coverage notes

- `<any BR not covered, any leaf without agent/operation, deferred items>`
