---
schema-version: 1.1.0
document-version: 0
---

# ML Serving View

<!-- CONDITIONAL - omit if no model inference. Trace inference steps to requirements operations
     by name. Note on-premise/edge constraints (local weights, no external model APIs).
     Replace every <...> and example row. Delete guidance comments when done. -->

## Stakeholders & Concerns

- <roles (e.g. ML engineer, infra)>. Concerns: <concerns this view frames>

## Inference Pipeline

<!-- End to end: input -> pre-process -> model(s) -> post-process -> output. -->
```
<pipeline diagram>
```

## Models

| Model | Role | Serving mode | Notes |
|-------|------|--------------|-------|
| <model> | <role> | <batch/stream/real-time> | <notes> |

## Hardware / Accelerator Plan

- <GPU/accelerator resources, placement, capacity>

## Model Lifecycle

- <versioning, update, rollback, evaluation gate>

## Performance Targets

- <throughput/latency targets per model or pipeline>
