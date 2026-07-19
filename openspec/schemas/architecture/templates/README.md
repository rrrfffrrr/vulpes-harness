# How to read the architecture artifacts

[English](README.md) | [한국어](README.ko.md)

**architecture** schema (Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR) artifacts - the "how", the technical structure.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - the role <-> concern <-> view map points each role to the views to read.

**Reading order:**

1. `overview.md` - strategy / stack / style / constraints + view map
2. `logical-view.md` - functional decomposition (components / interfaces)
3. `process-view.md` - runtime / concurrency flows *(if present)*
4. `data-view.md` - data architecture *(if present)*
5. `ml-serving-view.md` - inference pipeline *(if present)*
6. `deployment-view.md` - physical topology
7. `crosscutting-concepts.md` - security / logging / compliance, etc.
8. `adr.md` - architecture decision records (rationale)
9. `traceability.md` - requirements <-> architecture trace, role coverage

*process / data / ml-serving views exist only when that concern is present.*

---

Workflow: **require -> architect -> propose -> apply**
Status: `openspec status --change <name>`
