---
schema-version: 1.1.0
document-version: 0
---

# Backend Components

<!-- C4 Component altitude. Deepens architecture logical-view components by name - do not rename them.
     Replace every <...> and example row. Delete guidance comments when done. -->

## Middleware Pipeline

<!-- Ordered - the order is a contract. Failure behavior names a problem type from conventions.md. -->
| # | Stage | Responsibility | On rejection |
|---|-------|----------------|--------------|
| 1 | <e.g. auth> | <one line> | <status + problem type> |

## Shared Components

<!-- Validators, serializers, clients, repositories. Interface = name + inputs/outputs + purpose, NOT code. -->
| Component (logical-view name) | Responsibility | Exposes | Used by |
|-------------------------------|----------------|---------|---------|
| <name> | <one line> | <interface summary> | <components/endpoints> |

<!-- Mark components that exist only at this detail level: (detail-level). -->

## Ownership Boundaries

<!-- Which component owns which domain concept. Bounded-context vocabulary where it helps. -->
| Domain concept | Owning component | Notes |
|----------------|------------------|-------|
| <concept> | <component> | <invariants it guards> |
