---
schema-version: 1.2.0
document-version: 0
---

# Screens

<!-- Repeat the screen block per screen.
     Components by components.md name - never respecify.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## `<Screen name>`

`<one-line purpose>` (traces to: `<requirement/goal id>`)

### Layout

```text
<wire mockup of the ideal state (ascii or mermaid, per openspec/DIAGRAM-STYLE.md)>
```

**Breakpoint behavior**

| Breakpoint | Behavior |
|------------|----------|
| `<class>` | `<revealed / divided / resized / repositioned / swapped elements>` |

### UI Stack states

| State | Shows |
|-------|-------|
| Ideal | `<content>` |
| Empty | `<first-use/no-data view + copy>` |
| Loading | `<indicator/skeleton>` |
| Partial | `<some data + how more loads>` |
| Error | `<error view + exact copy + recovery action>` |

### Components & data

- **Components**: `<components.md names>`
- **Data**: `<fields displayed; source - reference backend endpoints by METHOD+path when a backend change exists>`

### Forms

<!-- Only if the screen has input.
     Validation is part of the contract. -->
| Field | Rules | Error copy (exact) |
|-------|-------|---------------------|
| `<field>` | `<constraints>` | "`<copy>`" |

- Focus order: `<order, where non-obvious>`

### Events emitted

<!-- Analytics event NAMES only - cross-references to the project's tracking plan. -->
- `<event.name>`
