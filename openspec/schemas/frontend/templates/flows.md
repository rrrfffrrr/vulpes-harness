---
schema-version: 1.1.0
document-version: 0
---

# Flows

<!-- Navigation map covers EVERY screen in screens.md.
     Statecharts only for non-trivial internal state.
     Diagrams per openspec/DIAGRAM-STYLE.md.
     Replace every <...> and example row.
     Delete guidance comments when done. -->

## Navigation map

<!-- Wireflow: screens as nodes, user events as labeled edges. -->
```mermaid
flowchart LR
  <ScreenA> -->|<event>| <ScreenB>
```

## Event -> transition tables

<!-- Per screen, for transitions the map alone cannot carry (guards, parameters).
     IFML semantics. -->

### <Screen name>

| Event (on) | Guard | Action | Target |
|------------|-------|--------|--------|
| <event (component)> | <condition or -> | <what happens> | <screen/state> |

## Statecharts

<!-- ONLY for interactions with non-trivial internal state.
     UML state machine notation. -->

### <Interaction name>

Traces to: <requirements operation/goal>

```mermaid
stateDiagram-v2
  [*] --> <State>
  <State> --> <State2>: <event [guard]>
```
