---
schema-version: 1.2.1
document-version: 0
---

# Input

<!-- Actions, not buttons. One action set per input context;
     layered modifications (aim-down-sights, vehicle...) as layers.
     Sensitivity/assist options by settings.md option name - defined once there.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## Device matrix

<!-- From overview, by reference. -->
| Platform | Devices |
|----------|---------|
| `<platform>` | `<gamepad / keyboard+mouse / touch>` |

## Action sets

<!-- Repeat per input context (gameplay contexts by GDD name, menus, photo mode...). -->

### `<Context name>`

| Action | Gamepad | Keyboard+mouse | Touch |
|--------|---------|----------------|-------|
| `<action>` | `<binding>` | `<binding>` | `<control>` |

- Layers: `<layered modifications of this set, with what they override - or none>`

## Glyph policy

- Prompts match the active device: `<how the switch happens>`
- Glyph art source: `<per platform; the public fallback when first-party art is NDA-bound>`

## Remapping

- Remappable: `<what - full remap is the accessibility baseline>`
- Reserved: `<bindings that cannot be remapped + why>`
- Presets/profiles: `<if any>`

## Hot-swap

- Device connected / disconnected mid-session: `<pause on disconnect, glyph refresh, reconnection prompt>`

## Menu navigation model

- Cardinal navigation: `<wrap rules, initial focus convention>`
- Back/cancel semantics: `<shared with flows/ modal conventions>`

## Haptics

<!-- Only when the platform has them. -->
- `<per-context haptic feedback + settings.md option names>`
