---
schema-version: 1.2.0
document-version: 0
---

# Backend overview

<!-- Entry point.
     Interface surfaces, state management, reader map, conditional artifacts.
     Reference architecture components/ADRs by name/id; do not restate them.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Scope

<!-- Which services/containers (architecture logical-view names) this design gives contracts for. -->
- `<service/container (logical-view name)>`

## Interface surfaces

<!-- One row per surface.
     Style rationale is one line + the ADR that fixed it. -->
| Surface | Style | Consumers | Rationale (ADR) |
|---------|-------|-----------|-----------------|
| `<name>` | `<REST / GraphQL / gRPC / events>` | `<who calls it>` | `<one line>` (ADR-NNN) |

## State management

<!-- Per surface: stateless (RFC 7519 token-carried) or stateful (RFC 6265 server session), and why (ADR ref). -->
| Surface | Model | Mechanism | Rationale (ADR) |
|---------|-------|-----------|-----------------|
| `<name>` | `<stateless/stateful>` | `<JWT bearer / session cookie / ...>` | `<one line>` (ADR-NNN) |

## Reader map

| Reader | Start with | Then |
|--------|-----------|------|
| API consumer | conventions.md | endpoints.md |
| Backend engineer | components.md | sequences.md |
| QA | endpoints.md | traceability.md |

## Conditional artifacts included

| Artifact | Included? | Reason |
|----------|-----------|--------|
| events | `<Yes/No>` | `<reason>` |
| webhooks | `<Yes/No>` | `<reason>` |
