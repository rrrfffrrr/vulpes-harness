# vulpes-harness

[English](README.md) | [한국어](README.ko.md)

vulpes-harness adds repeatable planning commands to AI coding tools like Claude Code and Codex.
Requirements and architecture come out structured and consistent instead of ad-hoc.
You run them as slash commands, and each one writes what you tell it into Markdown documents in your repo.

## Install

Add the harness to your project once - see [INSTALLATION.md](INSTALLATION.md).

## How to use

Work on one kind of document at a time.
Within the same task, add or revise as things come up - don't wait.
Finish one before moving to the next - don't mix different tasks.

<img alt="workflow" src="workflow.svg" width="80%">

- Requirements: `/opsx:require {content}`
- Architecture: `/opsx:architect {content}`
- Prepare: `/opsx:propose {content}`
- Build: `/opsx:apply {content}`

## Schemas

### require

The requirements schema, using KAOS/GORE and BABOK.
Produces business requirements, goal/object/responsibility/operation models, a synthesized requirements document, and a traceability matrix.

### architect

The architecture schema, using Kruchten 4+1, arc42, ISO/IEC 42010, Nygard ADRs, and a BABOK RTM.
Produces an architecture overview, logical/process/data/deployment views, crosscutting concepts, ADRs, and a design-traceability matrix.

### gdd

The game design schema, using the standard GDD sections.
Produces the overview, gameplay, mechanics, world/narrative, art and audio direction, UX/UI, tech, monetization, and production sections.
Game projects only.

## Reference

Layout, naming, and conventions are in [REFERENCE.md](REFERENCE.md).
