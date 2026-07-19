# How to read the verification artifacts

[English](README.md) | [한국어](README.ko.md)

**verification** schema (ISTQB test basis + ISO/IEC/IEEE 29119-3 documentation types + Specification by Example/Gherkin + BABOK 10.1 acceptance criteria) artifacts - the thin acceptance layer over the requirements and detail designs.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - the test basis, scope, and what is deliberately NOT here.

**Reading order:**

1. `overview.md` - test basis / scope / out of scope / reader map
2. `scenarios/index.md` - domain index; `scenarios/<domain>.md` - cross-layer acceptance scenarios (Gherkin), grouped by requirements operation
3. `environment.md` - test data requirements + test environment requirements
4. `traceability.md` - criterion <-> scenario <-> surfaces <-> environment matrix, with gaps

*per-contract test cases are NOT here - they are derived from the detail-design contracts at build time.*

---

Workflow: **require -> architect -> detail designs -> verification -> propose -> apply**
Status: `openspec status --change <name>`
