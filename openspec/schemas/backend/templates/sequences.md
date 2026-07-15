---
schema-version: 1.1.0
document-version: 0
---

# Runtime sequences

<!-- Flows that cross more than one component - happy path AND client-observable failure paths.
     Lifelines use components.md names; messages name endpoints/channels.
     UML Interaction semantics, rendered per openspec/DIAGRAM-STYLE.md.
     Repeat the flow block per flow.
     Replace every <...>.
     Delete guidance comments when done. -->

## <Flow name>

Realizes: <endpoint(s)/channel(s)> - traces to: <requirements operation name>

```mermaid
sequenceDiagram
  participant C as Client
  participant <A> as <component>
  C->><A>: <METHOD path / message>
  <A>-->>C: <status / reply>
```

<!-- Failure path: only where it changes what the client observes (timeout, retry, partial failure, compensation).
     For event-producing writes, show WHEN the event is published relative to the write. -->

**Failure path**: <what fails, what the client observes, recovery/compensation>
