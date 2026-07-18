# Changelog - ml schema

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow the harness release version (`metadata.version` in `schema.yaml`); templates' `schema-version` frontmatter mirrors it.
To migrate documents, apply each version's Migration section in order, from the artifact's `schema-version` (no frontmatter = pre-1.1.0) up to the current version.
A version without a Migration section needs no document rework.

## [1.2.0] - Unreleased

### Added

- Authoring principle: structure follows the new `openspec/rules/structure.md` - boundary declaration, role separation, split on growth, scoped naming, index hubs.
- Initial release: ML (model) detail-design schema (Model Cards for Model Reporting, Datasheets for Datasets, The ML Test Score, ISO/IEC 5338:2023) with 6 artifacts - `overview` -> `models` -> (`data`) -> `evaluation` -> `lifecycle` -> `traceability`; `data` conditional (owned training data only).
- The schema itself is conditional: created only when the architecture includes an `ml-serving-view`. Contracts are inference-location invariant; serving surfaces (backend) and on-device consumers (frontend/game-ui) reference models by name.
- LLM-based models use the same contract structure; prompt templates are project assets referenced by name (no settled prompt-specification standard to ground a dedicated section on yet).
