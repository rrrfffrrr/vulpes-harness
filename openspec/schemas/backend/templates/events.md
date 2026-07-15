---
schema-version: 1.1.0
document-version: 0
---

# Event & message APIs

<!-- CONDITIONAL - only when the system has message/event-driven APIs.
     AsyncAPI structure; envelope stated once; deviations from conventions.md only.
     Replace every <...> and example row; repeat the channel block per channel.
     Delete guidance comments when done. -->

## Envelope

<!-- Stated once for all messages.
     CloudEvents attributes or equivalent. -->
| Attribute | Value/format |
|-----------|--------------|
| <id / source / type / time / ...> | <format> |

## Channels

### <channel name>

- **Protocol**: <AsyncAPI binding, e.g. kafka / mqtt / websockets> - **Direction**: <send/receive>
- **Delivery**: <at-least-once / at-most-once>; ordering: <scope or none>; redelivery: <behavior>
- **Consistency**: <what a consumer may assume about store state on receipt; see sequences: <flow>>

**Messages**

| Message | Payload field | Type | Constraints |
|---------|---------------|------|-------------|
| <type> | <field> | <type> | <constraints> |
