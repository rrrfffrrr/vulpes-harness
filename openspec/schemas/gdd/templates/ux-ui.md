---
schema-version: 1.1.0
document-version: 0
---

# UX / UI

<!-- Player-facing interface and FLOW.
     Layout and flow here; visual styling is art-direction; rules are mechanics.
     Mockups as ascii/mermaid, not final art.
     Replace every `<...>` placeholder, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Screen / menu flow

<!-- The map: title -> menus -> game -> results -> back. -->
```text
<screen> -> <screen> -> <screen>
```

## Key screens

<!-- One block per important screen: layout + the actions on it. -->
### `<screen name>`

- **Serves**: `<which gameplay state / mechanic>`
- **Layout**:

```text
<ascii / mermaid wire mockup>
```

- **Actions**: `<buttons / inputs and what they do>`

## Controls / input

<!-- Every input and what it does, per input method. -->
| Input | Action |
|-------|--------|
| `<touch/button>` | <...> |

## Onboarding / tutorial

<!-- How a new player learns the core loop. -->
`<paragraph>`

## Accessibility

<!-- Text size, colorblind, remap, audio-independent feedback, input assists. -->
- <...>
