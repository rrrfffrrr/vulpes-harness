# How to read these artifacts - backend

[English](README.md) | [한국어](README.ko.md)

**backend** schema (OpenAPI/JSON Schema contracts + RFC 9110/9457/9111 + BCP 14 + UML sequences + C4 components) artifacts - the exact interface contracts, one level below architecture.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - interface surfaces, state model, and the reader map pointing each reader to their documents.

**Reading order:**

1. `overview.md` - scope / interface surfaces / state management / reader map
2. `conventions.md` - the shared rulebook: auth scopes, versioning, error catalog, pagination, rate limits, idempotency, concurrency, caching, long-running operations
3. `components.md` - middleware pipeline (ordered) + shared components
4. `endpoints.md` - per-endpoint contracts (deviations from conventions only)
5. `sequences.md` - backend-internal runtime flows, including client-observable failure paths; splits into `sequences/<domain>.md` when it outgrows one sitting (the file stays as the index)
6. `events.md` - channels / messages / delivery guarantees *(if present)*
7. `webhooks.md` - outbound callbacks *(if present)*
8. `jobs.md` - scheduled/background job contracts *(if present)*
9. `configuration.md` - config keys & feature flags catalog *(if present)*
10. `traceability.md` - operation <-> interface <-> component <-> sequence matrix

*events, webhooks, jobs, and configuration exist only when the system has that concern.*

---

Workflow: **require -> architect -> backend -> propose -> apply**
Status: `openspec status --change <name>`
