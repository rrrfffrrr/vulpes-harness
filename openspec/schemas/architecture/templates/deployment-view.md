---
schema-version: 1.1.0
document-version: 0
---

# Deployment view

<!-- 4+1 Physical / arc42 sec.7 + C4 Deployment.
     Topology + mapping of logical-view containers onto nodes.
     Reference containers by name; do not redefine responsibilities.
     Replace every <...> and example row.
     Delete guidance comments when done. -->

## Stakeholders & concerns

- <roles (e.g. DevOps, infra, hardware)>. Concerns: <concerns this view frames>

## Topology

<!-- Nodes/hosts/racks, networks, trust zones. -->
```
<deployment diagram>
```

## Container -> node mapping

| Container | Node | Notes |
|-----------|------|-------|
| <container> | <node> | <notes> |

## Scaling & availability

- <scaling approach, redundancy, availability targets>

## Infrastructure constraints

<!-- Inherited from requirements (e.g. on-premise rack, no cloud, network isolation). -->
- <constraint>
