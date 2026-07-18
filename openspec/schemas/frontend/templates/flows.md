---
schema-version: 1.2.0
document-version: 0
---

# Flows

<!-- Navigation map covers EVERY screen in screens.md.
     Statecharts only for non-trivial internal state.
     Diagrams per openspec/rules/diagrams.md.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Navigation map

<!-- Wireflow: screens as nodes, user events as labeled edges. -->
```mermaid
flowchart LR
  %% Replace with real screens (nodes) and user events (edge labels).
  ScreenA -->|event| ScreenB
```

## Routes

<!-- Conditional section - only when the platform addresses screens by URL or deep link.
     Mechanism-agnostic: https URLs (iOS Universal Links / Android App Links) and custom
     schemes both fit the pattern column. The /.well-known association files that verify
     the domain (apple-app-site-association, assetlinks.json - RFC 8615) are a
     deployment/hosting concern - reference them, never specify them here.
     Route names mirror the navigation map's nodes. -->
- **Fallback policy** *(stated once)*: `<app-absent chain, e.g. open web page / store redirect / smart banner; deferred deep-link service if the architecture decided one (ADR ref)>`

| Screen | Route pattern | Params | Guard | Deep-link entry |
|--------|---------------|--------|-------|-----------------|
| `<screen>` | `<https://... or scheme:///path/:param>` | `<params>` | `<auth or ->` | `<state restored; where back leads; app-absent fallback for https links>` |

## Event -> transition tables

<!-- Per screen, for transitions the map alone cannot carry (guards, parameters).
     IFML semantics. -->

### `<Screen name>`

| Event (on) | Guard | Action | Target |
|------------|-------|--------|--------|
| `<event (component)>` | `<condition or ->` | `<what happens>` | `<screen/state>` |

## Statecharts

<!-- ONLY for interactions with non-trivial internal state.
     UML state machine notation. -->

### `<Interaction name>`

Traces to: `<requirements operation/goal>`

```mermaid
stateDiagram-v2
  %% Replace with the interaction's real states and events.
  [*] --> StateA
  StateA --> StateB: event [guard]
```
