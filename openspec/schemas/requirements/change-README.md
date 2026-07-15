# How to read this folder - requirements

[English](README.md) | [한국어](README.ko.md)

This change holds **requirements** schema (KAOS/GORE + BABOK) artifacts. The "what and why" - formal requirements. No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

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

Workflow: **require -> (gdd/architect) -> propose -> apply**
Status: `openspec status --change <name>`
