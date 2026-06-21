# Crosscutting Concepts

<!-- arc42 §8. Concerns spanning multiple views. State the concept and HOW the design
     realizes it across views; reference affected views/components by name.
     Replace every <...> and example row. Delete guidance comments when done. -->

## Security & Access Control

- <trust zones, authn/authz model, least-privilege>

## Data Protection & Encryption

<!-- At-rest / in-transit. Honor planning data invariants. -->
- <encryption / data-boundary approach>

## Logging, Audit & Observability

- <audit log scope/retention, metrics, tracing>

## Error Handling & Resilience

- <failure model, degradation, retry/fallback policy>

## Regulatory Compliance Mapping

<!-- For a regulated system. Omit if not regulated. -->
| Concept | Planning goal/obstacle | Governing rule | How design satisfies |
|---------|------------------------|----------------|----------------------|
| <concept> | <goal/obstacle id> | <rule> | <how> |

## Other Concepts

- <any further crosscutting concept (i18n, config, time, etc.)>
