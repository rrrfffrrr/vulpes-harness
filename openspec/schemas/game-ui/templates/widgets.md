---
schema-version: 1.2.1
document-version: 0
---

# Widget inventory

<!-- Shared/reused widgets only - one-off screen arrangements live in screens.md.
     Repeat the widget block per widget.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## `<Widget name>`

`<one-line purpose>`

- **Anatomy**: `<named parts, e.g. frame / label / value / glyph slot>`
- **Variants / sizes**:

  | Variant | Size | Dimensions |
  |---------|------|------------|
  | `<variant>` | `<size>` | `<concrete values>` |

- **States** *(from the overview enum; only states that apply)*:

  | State | Appearance / behavior |
  |-------|------------------------|
  | `<state>` | `<what changes>` |

- **Input behavior**:

  | Device | Operation |
  |--------|-----------|
  | Pointer | `<hover/click behavior>` |
  | Gamepad | `<focus visual + cardinal navigation behavior>` |
  | Touch | `<tap/gesture behavior + target size>` |

- **Text budget**: `<per text part: length limit incl. localization headroom; wrap/truncate behavior when exceeded>`
- **Glyph slots**: `<where device-matching input glyphs appear - or none>`
- **Assistive**: `<narration/labeling; behavior under text scaling>`
- **Tokens**: `<tokens consumed by name - or concrete values when design-tokens is absent>`
