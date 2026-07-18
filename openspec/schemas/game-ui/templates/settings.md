---
schema-version: 1.2.1
document-version: 0
---

# Settings

<!-- Every player-facing option, each in exactly one bucket.
     Buckets: gameplay / display / audio / UI & accessibility / language / controls.
     Effects reference hud elements, widgets, and input actions by name.
     Accessibility column: XAG number / Game Accessibility Guidelines item, when the
     option is an accessibility option.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Gameplay

<!-- Difficulty/assist options are game-specific - trace to the GDD, don't invent here. -->
| Option | Type / range | Default | Effect | Platforms | Accessibility |
|--------|--------------|---------|--------|-----------|---------------|
| `<option>` | `<toggle / enum / slider min-max-step>` | `<value>` | `<what it changes, by name>` | `<all or list>` | `<XAG/GAG item or ->` |

## Display

| Option | Type / range | Default | Effect | Platforms | Accessibility |
|--------|--------------|---------|--------|-----------|---------------|
| `<option>` | <...> | <...> | <...> | <...> | <...> |

## Audio

<!-- Separate volume channels are the accessibility baseline. -->
| Option | Type / range | Default | Effect | Platforms | Accessibility |
|--------|--------------|---------|--------|-----------|---------------|
| `<option>` | <...> | <...> | <...> | <...> | <...> |

## UI & accessibility

<!-- Cover the overview target explicitly: text scaling, subtitle options,
     contrast/colorblind variants, motion reduction. -->
| Option | Type / range | Default | Effect | Platforms | Accessibility |
|--------|--------------|---------|--------|-----------|---------------|
| `<option>` | <...> | <...> | <...> | <...> | <...> |

## Language

| Option | Type / range | Default | Effect | Platforms | Accessibility |
|--------|--------------|---------|--------|-----------|---------------|
| `<option>` | <...> | <...> | <...> | <...> | <...> |

## Controls

<!-- Full input remapping is the accessibility baseline; actions by input.md name. -->
| Option | Type / range | Default | Effect | Platforms | Accessibility |
|--------|--------------|---------|--------|-----------|---------------|
| `<option>` | <...> | <...> | <...> | <...> | <...> |

## First-boot exposure

<!-- Which options the first-boot setup (flows/) surfaces before play begins. -->
- `<option names>`
