---
schema-version: 1.2.0
document-version: 0
---

# API conventions

<!-- The shared rulebook.
     Every rule stated ONCE here with BCP 14 keywords (MUST/SHOULD/MAY);
     endpoints/events/webhooks record only deviations.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Authentication & authorization

<!-- Scheme + the full scope taxonomy.
     Every scope named, with meaning. -->
- Scheme: `<e.g. OAuth2 bearer (JWT) on every request; anonymous endpoints marked explicitly>`

| Scope | Grants |
|-------|--------|
| `<resource.read>` | `<meaning>` |

## Versioning & deprecation

- Version expression: `<e.g. URI /v1, or date-based header>`
- Compatibility promise: `<what changes are non-breaking - e.g. adding optional fields; existing fields MUST keep name and type>`
- Deprecation procedure: `<announcement channel, sunset headers, minimum notice period>`

## Error catalog

<!-- RFC 9457 problem details.
     Retryable tells clients whether to back off and retry. -->
- Error media type: `application/problem+json` (type / title / status / detail / instance)

| Problem type | Status | When | Retryable | Backoff |
|--------------|--------|------|-----------|---------|
| `<urn or URL>` | `<4xx/5xx>` | `<condition>` | `<yes/no>` | `<policy or ->` |

## List endpoints: pagination / filtering / sorting

- Pagination: `<cursor or offset; parameter names; page-size default and max; response envelope>`
- Filtering: `<parameter convention>`
- Sorting: `<parameter convention>`

## Rate limiting (response contract)

<!-- Only the contract clients see.
     Limit values and enforcement are architecture/ops concerns. -->
- On limit: `<429 + Retry-After; any X-RateLimit-* headers and their meaning>`

## Idempotency

- `<which unsafe methods accept an idempotency key; header name; replay semantics (same response replayed, success or failure); key retention window; parameter-mismatch behavior>`

## Concurrency control

- `<which updates require If-Match with ETag; 412 behavior; where ETags are returned>`

## Response caching

<!-- RFC 9111 defaults per resource class. -->
| Resource class | Cache-Control | Validation |
|----------------|---------------|------------|
| `<class>` | `<e.g. private, max-age=60>` | `<ETag / Last-Modified / none>` |

## Long-running operations

<!-- Only if any endpoint uses the pattern; otherwise delete this section. -->
- `<202 + status resource URL; status resource shape; polling guidance; terminal states>`

## Naming

- Paths: `<convention>`. Fields: `<casing>`. `<other naming rules>`
