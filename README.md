# vulpes-harness

[English](README.md) | [한국어](README.ko.md)

vulpes-harness adds repeatable planning commands to AI coding tools like Claude Code and Codex.

Requirements and architecture come out structured and consistent instead of ad-hoc.

You run them as slash commands, and each one writes what you tell it into Markdown documents in your repo.

## Install

Add the harness to your project once - see [INSTALLATION.md](INSTALLATION.md).

## How to use

- Work on one kind of document at a time.
- Within the same task, add or revise as things come up - don't wait.
- Finish one before moving to the next - don't mix different tasks.

<img alt="workflow" src="assets/workflow.svg" width="80%">

For game projects:

<img alt="game workflow" src="assets/workflow-game.svg" width="90%">

- Requirements: `/opsx:require {content}`
- GDD: `/opsx:gdd {content}`
- Architecture: `/opsx:architect {content}`
- Backend detail: `/opsx:backend {content}`
- Frontend detail: `/opsx:frontend {content}`
- Persistence detail: `/opsx:persistence {content}`
- Game UI detail: `/opsx:game-ui {content}`
- Prepare: `/opsx:propose {content}`
- Build: `/opsx:apply {content}`

## Schemas

### require

The requirements schema, using KAOS/GORE and BABOK.

Produces business requirements, goal/object/responsibility/operation models, a synthesized requirements document, and a traceability matrix.

### architect

The architecture schema, using Kruchten 4+1, arc42, ISO/IEC 42010, Nygard ADRs, and a BABOK RTM.

Produces an architecture overview, logical/process/data/deployment views, crosscutting concepts, ADRs, and a traceability matrix.

### backend

The backend detail-design schema, using OpenAPI/JSON Schema, RFC 9110/9457/9111, BCP 14, UML sequences, and C4 components.

Produces an overview, API conventions, components, endpoint contracts, runtime sequences, optional events/webhooks/jobs, and a traceability matrix.

### frontend

The frontend detail-design schema for web, mobile, and desktop apps, using IFML, UML state machines, wireflows, Atomic Design, the UI Stack, and WCAG 2.2.

Produces an overview, optional design tokens, a component inventory, screens, an optional client data layer, flows, and a traceability matrix.

### persistence

The persistence detail-design schema, using the ANSI/SPARC internal level, polyglot persistence, access-pattern-driven store design, and evolutionary database design.

Produces an overview with the store inventory, a field-level logical model, per-store designs, a migration policy, and a traceability matrix.

### gdd

The game design schema, using the standard GDD sections.

Produces the overview, gameplay, mechanics, world/narrative, art and audio direction, UX/UI, tech, monetization, and production sections.

Game projects only.

### game-ui

The game UI detail-design schema, using the diegetic/non-diegetic/spatial/meta UI-layer taxonomy, Game UI Database screen vocabulary, SMPTE safe areas, Game Accessibility Guidelines/XAG, action-based input, and UML state machines.

Produces an overview, optional design tokens, widgets, screens, HUD, flows, input, settings, and a traceability matrix.

Game projects only.
