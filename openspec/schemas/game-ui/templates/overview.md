---
schema-version: 1.2.0
document-version: 0
---

# Game UI overview

<!-- Entry point.
     System-wide UI vocabulary lives HERE, once:
     UI layers, safe area & scale, legibility floors, widget states,
     localization budgets, accessibility target.
     Reference architecture/GDD/requirements by id; do not restate.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Platforms, input devices & UI stack

<!-- From the architecture technology stack, by reference. -->
| Platform | Input devices | UI stack (architecture ref) |
|----------|---------------|------------------------------|
| `<PC / console / mobile / handheld>` | `<gamepad / keyboard+mouse / touch>` | `<engine + UI system>` |

## UI-layer vocabulary

<!-- Fagerholt & Lorentzon design space; Andrews' four terms.
     Every screen/hud element carries one of these classes. -->
| Layer | Meaning in this game | Example |
|-------|----------------------|---------|
| diegetic | `<in-world, seen by the character>` | `<example element>` |
| non-diegetic | `<overlay, seen only by the player>` | `<example element>` |
| spatial | `<in-world position, not part of the fiction>` | `<example element>` |
| meta | `<on the "camera lens" - effects, vignettes>` | `<example element>` |

## Safe area & scale policy

- Safe area: `<per platform - e.g. title-safe 90% on TV-connected, device cutouts on mobile>`
- UI scale option: `<range, e.g. 80-150%>`
- Aspect-ratio decision: `<ultrawide/letterbox behavior - a recorded project decision>`

## Text legibility floors

<!-- Minimum sizes per platform/viewing distance. -->
| Platform | Minimum text size | Basis |
|----------|-------------------|-------|
| `<console/TV>` | `<size @ resolution>` | `<XAG 101 / project decision>` |

## Widget-state enum

<!-- Declared once; widgets state behavior per applicable state. -->
`<idle / focused / pressed / disabled / selected / ...>`

## Localization policy

- Languages: `<target list>`
- Text expansion headroom: `<30-40% unless justified otherwise>`
- Font fallback: `<per-script expectations>`
- Pseudo-localization pass: `<when it runs>`

## Accessibility target

- Guidelines committed to: `<Game Accessibility Guidelines tier; XAG guidelines by number>`
- Legal note *(only when the game has player-to-player communication or in-game purchasing)*: `<CVAA/EAA scope note>`

## Platform certification

<!-- NDA-bound project inputs - reference, never restate content. -->
- `<which cert documents apply - e.g. Sony TRC / Nintendo guidelines / Xbox XR>`

## Reader map

| Reader | Start with | Then |
|--------|-----------|------|
| UI designer | widgets.md | screens.md, hud.md |
| UI engineer | screens.md | input.md, flows.md |
| QA | settings.md | traceability.md |

## Conditional artifacts included

| Artifact / section | Included? | Reason |
|--------------------|-----------|--------|
| design-tokens | `<Yes/No>` | `<reason>` |
| hud subtitles/captions section | `<Yes/No>` | `<reason>` |
