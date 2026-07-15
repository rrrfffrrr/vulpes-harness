---
schema-version: 1.1.0
document-version: 0
---

# Logical view

<!-- 4+1 Logical / arc42 sec.5 Building Block View.
     Static functional structure only - no deployment, no runtime sequencing.
     Map components to requirements agents by id.
     Replace every <...> and example row.
     Delete guidance comments when done. -->

## Stakeholders & concerns

- <roles (e.g. frontend, backend)>. Concerns: <concerns this view frames>

## Building block decomposition

<!-- Hierarchical.
     Containers -> components (C4).
     mermaid/ascii diagram. -->
```mermaid
flowchart TB
  subgraph <container>
    <component>[<component>]
  end
  <component> --> <component2>
```

## Components

### <Component>

- Responsibility: <what it does>
- Realizes (requirements agent): <agent id, if any>

## Interfaces

| Interface | Provider | Consumer(s) | Inputs -> Outputs | Purpose |
|-----------|----------|-------------|------------------|---------|
| <name> | <component> | <component> | <in -> out> | <purpose> |
