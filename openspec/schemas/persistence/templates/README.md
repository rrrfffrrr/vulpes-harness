# How to read the persistence artifacts

[English](README.md) | [한국어](README.ko.md)

**persistence** schema (ANSI/SPARC internal level + polyglot persistence + access-pattern-driven store design + evolutionary database design) artifacts - the store-level data design, one level below the architecture data-view.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - the store inventory (engine + deciding ADR or OPEN) and the reader map.

**Reading order:**

1. `overview.md` - store inventory / data domains / reader map
2. `model.md` - store-agnostic logical detail: full field lists, integrity, retention/PII classes
3. `stores.md` - per-store design: native units, keys/indexes, access patterns, retention mechanisms, engine-specific features
4. `migrations.md` - migration policy, expand-contract for breaking changes, seed data, backfills
5. `traceability.md` - object <-> entity <-> store <-> access-pattern matrix

*a store whose engine is undecided is marked OPEN and stays engine-portable until the architecture ADR lands.*

---

Workflow: **require -> architect -> persistence -> propose -> apply**
Status: `openspec status --change <name>`
