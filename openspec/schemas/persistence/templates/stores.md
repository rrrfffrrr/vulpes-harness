---
schema-version: 1.2.1
document-version: 0
---

# Store designs

<!-- One block per store from overview.md.
     Access patterns justify structure - a structure serving no pattern is a gap.
     Engine undecided -> keep the block portable-only and mark OPEN.
     Replace every `<...>` placeholder and example row; repeat the store block per store.
     Delete guidance comments when done. -->

## `<Store name>` (`<engine / OPEN>`)

### Units

| Entity (model.md) | Native unit | Key | Partition | Indexes |
|-------------------|-------------|-----|-----------|---------|
| `<entity>` | `<table / collection / keyspace / measurement>` | `<PK>` | `<partition/shard key, or ->` | `<indexes>` |

### Access patterns

| Pattern | Served by | Cardinality | Frequency |
|---------|-----------|-------------|-----------|
| `<query/lookup>` | `<unit + index>` | `<result size>` | `<how often it runs>` |

### Consistency & durability

- `<isolation level / replication ack / read-write concerns the design depends on>`

### Retention mechanism

- `<model retention class -> TTL / partition drop / cleanup job (backend jobs.md name)>`

### Engine-specific

<!-- Features beyond the portable level, each keyed to the engine ADR.
     OMIT this section while the engine is OPEN; instead list what the pending decision blocks. -->
- `<feature used>` (ADR-NNN)
