# How to read this folder - design

This change holds **design** schema (Kruchten 4+1 + arc42 + ISO/IEC 42010 + Nygard ADR) artifacts - the "how", the technical structure. No implementation (apply) step.

**Start here ->** [`architecture-overview.md`](architecture-overview.md) - the role <-> concern <-> view map points each role to the views to read.

**Reading order:**

1. `architecture-overview.md` - strategy / stack / style / constraints + view map
2. `logical-view.md` - functional decomposition (components / interfaces)
3. `process-view.md` - runtime / concurrency flows *(if present)*
4. `data-view.md` - data architecture *(if present)*
5. `ml-serving-view.md` - inference pipeline *(if present)*
6. `deployment-view.md` - physical topology
7. `crosscutting-concepts.md` - security / logging / compliance, etc.
8. `adr.md` - architecture decision records (rationale)
9. `design-traceability.md` - planning <-> design trace, role coverage

*process / data / ml-serving views exist only when that concern is present.*

---

Workflow: **plan -> design -> propose -> apply**
Status: `openspec status --change <name>`
