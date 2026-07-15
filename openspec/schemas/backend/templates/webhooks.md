---
schema-version: 1.1.1
document-version: 0
---

# Webhooks

<!-- CONDITIONAL - only when the system sends outbound callbacks.
     Standard Webhooks conventions.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Event types

| Type | Fired when | Payload | Source (events channel / sequences flow) |
|------|-----------|---------|------------------------------------------|
| `<name>` | `<trigger>` | `<schema summary or table>` | `<ref>` |

## Delivery

- Signing: `<scheme + verification headers the consumer checks>`
- Timeout: `<value>` - Failure: `<what counts as failed>`
- Retry: `<backoff schedule; when delivery is exhausted; what happens then>`

## Receiver requirements

<!-- BCP 14 keywords. -->
- `<e.g. MUST return 2xx within timeout; MUST verify signature; MUST handle redelivery idempotently>`
