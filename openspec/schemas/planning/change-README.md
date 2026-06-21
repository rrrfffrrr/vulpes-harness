# How to read this folder - planning

This change holds **planning** schema (KAOS/GORE + BABOK) artifacts. The "what and why" - formal requirements. No implementation (apply) step.

**Start here ->** [`requirements-document.md`](requirements-document.md) - the single synthesis of the four models. For a quick read, this one is enough.

**Reading order (for humans):**

1. `requirements-document.md` - synthesis (Scope / Goals / Glossary / Responsibilities / Behavior)
2. `business-requirements.md` - stakeholder statements (BR), verbatim
3. `goal-model.md` - goal tree (AND/OR), domain properties, obstacles + resolutions
4. `object-model.md` - entities, relationships, invariants (INV)
5. `responsibility-model.md` - the agent responsible for each leaf goal
6. `operation-model.md` - operations (pre/post/trigger), scenarios
7. `traceability.md` - BR <-> goal <-> leaf <-> agent <-> operation matrix

---

Workflow: **plan -> (gdd/design) -> propose -> apply**
Status: `openspec status --change <name>`
