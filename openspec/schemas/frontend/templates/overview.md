---
schema-version: 1.1.0
document-version: 0
---

# Frontend Overview

<!-- Entry point. System-wide UI vocabulary lives HERE, once: breakpoints, interaction states,
     accessibility target. Reference architecture/requirements by id; do not restate.
     Replace every <...> and example row. Delete guidance comments when done. -->

## Platforms & UI Stacks

<!-- From the architecture technology stack, by reference. -->
| Platform | UI stack (architecture ref) |
|----------|------------------------------|
| <web / mobile / desktop> | <stack + version intent> |

## Breakpoint Set

<!-- The named window-size classes this product uses. Screens describe behavior per class. -->
| Class | Range | Typical |
|-------|-------|---------|
| <compact> | <range> | <phone> |

## Interaction-State Enum

<!-- Declared once; components state behavior per applicable state. -->
`<enabled / disabled / hovered / focused / pressed / selected / ...>`

## Accessibility Target

- Conformance: <WCAG 2.2 level>
- Non-web platforms: <how the criteria apply>

## Reader Map

| Reader | Start with | Then |
|--------|-----------|------|
| Designer | components.md | screens.md |
| UI engineer | screens.md | flows.md |
| QA | flows.md | traceability.md |

## Conditional Artifacts Included

| Artifact | Included? | Reason |
|----------|-----------|--------|
| design-tokens | <Yes/No> | <reason> |
