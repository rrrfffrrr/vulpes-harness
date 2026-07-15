---
schema-version: 1.1.0
document-version: 0
---

# Architecture overview

<!-- Entry point for every role.
     Solution strategy + tech stack + style + constraints,
     then the ISO/IEC 42010 role-concern-view map.
     Reference requirements by id; do not restate.
     Replace every `<...>` placeholder, dropping the backticks unless the value is a literal and example row.
     Delete guidance comments when done. -->

## Solution strategy

<!-- arc42 sec.4.
     Key architectural decisions, one line each.
     Full rationale lives in ADRs. -->
- `<key decision>` (ADR-NNN)

## Technology stack

<!-- Explicit choices with version intent. -->
- **`<tier (frontend/backend/data/infra/ML)>`**: `<choices + version intent>`

## Architecture style

<!-- e.g. modular monolith, microservices, event-driven. -->
`<one paragraph + why (link ADR)>`

## Constraints

<!-- Technical/organizational constraints inherited from requirements. -->
- `<constraint>`

## Role / concern / view map (ISO/IEC 42010)

<!-- The single place roles are linked to views.
     Every role finds its reading list here. -->
| Role | Concerns | Views to read |
|------|----------|---------------|
| `<role>` | `<concerns>` | `<view, view>` |

## Conditional views included

<!-- Which of process-view / data-view / ml-serving-view this design includes, and why. -->
| View | Included? | Reason |
|------|-----------|--------|
| process-view | `<Yes/No>` | `<reason>` |
| data-view | `<Yes/No>` | `<reason>` |
| ml-serving-view | `<Yes/No>` | `<reason>` |
