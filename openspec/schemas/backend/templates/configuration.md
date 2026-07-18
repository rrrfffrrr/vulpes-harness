---
schema-version: 1.2.1
document-version: 0
---

# Configuration catalog

<!-- CONDITIONAL - only when behavior varies between deploys (12-factor III).
     Names, types, defaults, effects - NEVER per-environment values, never secret values.
     Replace every `<...>` placeholder and example row.
     Delete guidance comments when done. -->

## Keys

| Key | Type | Default | Read by | Effect |
|-----|------|---------|---------|--------|
| `<KEY_NAME>` | `<string / int / duration / ...>` | `<default>` | `<component>` | `<what changes; endpoint/job/channel altered, by name>` |

## Feature flags

| Flag | Default | Read by | Effect | Lifecycle |
|------|---------|---------|--------|-----------|
| `<flag>` | `<on/off>` | `<component>` | `<what it gates>` | `<temporary (removal intent) / permanent toggle>` |

## Secrets

<!-- Names and consuming components only - never values, never storage/rotation mechanics. -->
| Secret | Consumed by |
|--------|-------------|
| `<SECRET_NAME>` | `<component>` |
