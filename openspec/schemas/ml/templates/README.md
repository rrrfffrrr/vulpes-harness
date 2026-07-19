# How to read the ml artifacts

[English](README.md) | [한국어](README.ko.md)

**ml** schema (Model Cards + Datasheets for Datasets + ML Test Score + ISO/IEC 5338) artifacts - the per-model contracts one level below the architecture ml-serving-view, invariant to where inference runs.
No implementation (apply) step.

Every artifact starts with frontmatter: `schema-version` (semver of the schema it was authored against) and `document-version` (revision counter - 0 at first write, +1 per revision).

**Start here ->** [`overview.md`](overview.md) - the model inventory and the reader map.

**Reading order:**

1. `overview.md` - model inventory / reader map / conditional artifacts
2. `models.md` - per-model contracts: intended use, I/O with confidence semantics, degradation/fallback, caveats
3. `data.md` - owned training data as datasheets *(if present)*
4. `evaluation.md` - release gates, slices, regression policy, monitoring signals
5. `lifecycle.md` - versioning, update/rollback procedures, retraining triggers, deprecation
6. `traceability.md` - operation <-> model <-> surfaces <-> gates matrix

*data exists only when the project owns training/fine-tuning data. The serving API surface lives in the backend change; on-device consumption in frontend/game-ui - all reference models by name.*

---

Workflow: **require -> architect -> ml (when the architecture has an ml-serving-view) -> propose -> apply**
Status: `openspec status --change <name>`
