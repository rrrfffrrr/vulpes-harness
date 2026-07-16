---
schema-version: 1.2.0
document-version: 0
---

# Model lifecycle

<!-- Procedures only - the ml-serving-view keeps the approach.
     ISO/IEC 5338 vocabulary at design altitude.
     Replace every `<...>` placeholder.
     Delete guidance comments when done. -->

## Versioning

- `<the scheme tying model + training data + config versions; what identifies "the model" for rollback>`

## Update

- `<how a new version reaches production (staged/shadow/canary as procedure); the evaluation gates that must pass first>`

## Rollback

- `<procedure + time bound; what state (features, caches) rolls back with the model>`

## Retraining triggers

- `<schedule (backend jobs.md name) / drift signal (evaluation.md) / data refresh (data.md)>`

## Deprecation

- `<how a model is retired and consumers migrate>`
