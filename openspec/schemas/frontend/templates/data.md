---
schema-version: 1.2.1
document-version: 0
---

# Client data layer

<!-- CONDITIONAL - only when the app manages client-side server-state
     (caching, optimistic updates, offline) beyond fetching per render.
     Freshness vocabulary: RFC 9111 / RFC 5861 (stale-while-revalidate, stale-if-error).
     Behavior only - never a state library's API.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal; repeat the resource block per resource.
     Delete guidance comments when done. -->

## Defaults

<!-- Stated once for all resources. -->
| Rule | Value |
|------|-------|
| Freshness window | `<duration a response serves as fresh>` |
| Revalidate triggers | `<focus / interval / navigation / reconnect>` |
| Cache scope | `<memory / persisted>` |
| Client retry | `<which problem types retry (per backend error catalog retryability) + backoff>` |

## Resources

### `<resource name>`

- **Source**: `<METHOD path (backend endpoints) / local>`
- **Displayed on**: `<screens.md names>`
- **Freshness**: `<deviations from defaults - window, stale-while-revalidate behavior>`
- **Invalidated by**: `<mutations (METHOD path) or events that invalidate this resource>`
- **Optimistic updates**: `<mutations rendered optimistically; on failure: rollback + what the user sees>`

## Offline

<!-- Conditional section - only when the app works offline. -->
- **Reads**: `<serve cached/stale (stale-if-error) / blocked + copy>`
- **Writes**: `<queued and replayed / rejected + copy>`
- **Reconciliation**: `<on reconnect: replay order and the conflict behavior the user observes>`
