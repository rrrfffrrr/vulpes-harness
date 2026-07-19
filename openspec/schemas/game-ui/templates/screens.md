---
schema-version: 1.2.1
document-version: 0
---

# Screens

<!-- Repeat the screen block per screen and modal.
     Screen types in Game UI Database vocabulary where it fits
     (title screen, settings menu, pause, inventory, results...).
     Modals are screen blocks that name their owner screen.
     Widgets by widgets.md name - never respecify.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## `<Screen name>`

`<one-line purpose>` (traces to: `<GDD section / requirement id>`)
<!-- For a modal, add: Owner screen: <screen name>. -->

### Layout

```text
<wire mockup of the nominal state (ascii or mermaid, per openspec/rules/diagrams.md)>
```

- Safe area: `<complies with overview policy - or the deviation, called out>`

### Screen states

<!-- Only for data-driven screens (stores, lobbies, leaderboards, load/save). -->
| State | Shows |
|-------|-------|
| Nominal | `<content>` |
| Empty | `<first-use/no-data view + copy>` |
| Loading | `<indicator + what stays interactive>` |
| Error / connection loss | `<error view + exact copy + recovery action>` |

### Widgets & data

- **Widgets**: `<widgets.md names>`
- **Data**: `<fields displayed; gameplay state by GDD name - reference backend endpoints by METHOD+path when a backend change exists>`

### Operation

<!-- Only what is screen-specific beyond widget definitions. -->
- Initial focus: `<element>`
- `<shortcut/hold actions, touch gestures - if any>`

### Events emitted

<!-- Analytics event NAMES only - cross-references to the project's tracking plan. -->
- `<event.name>`
