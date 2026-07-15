---
schema-version: 1.1.0
document-version: 0
---

# Crosscutting concepts

<!-- arc42 sec.8.
     Concerns spanning multiple views.
     State the concept and HOW the design realizes it across views;
     reference affected views/components by name.
     Replace every <...> and example row.
     Delete guidance comments when done. -->

## Security & access control

- <trust zones, authn/authz model, least-privilege>

## Data protection & encryption

<!-- At-rest / in-transit.
     Honor requirements data invariants. -->
- <encryption / data-boundary approach>

## Logging, audit & observability

- <audit log scope/retention, metrics, tracing>

## Error handling & resilience

- <failure model, degradation, retry/fallback policy>

## Regulatory compliance mapping

<!-- For a regulated system.
     Omit if not regulated. -->
| Concept | Requirements goal/obstacle | Governing rule | How design satisfies |
|---------|----------------------------|----------------|----------------------|
| <concept> | <goal/obstacle id> | <rule> | <how> |

## Other concepts

- <any further crosscutting concept (i18n, config, time, etc.)>
