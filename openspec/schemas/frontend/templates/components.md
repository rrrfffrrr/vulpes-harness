---
schema-version: 1.2.1
document-version: 0
---

# Component inventory

<!-- Shared/reused components only - one-off screen arrangements live in screens.md.
     Repeat the component block per component.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## `<Component name>`

`<one-line purpose>` - Level: `<atom / molecule / organism>`

- **Anatomy**: `<named parts, e.g. container / label / leading icon>`
- **Variants / sizes**:

  | Variant | Size | Dimensions |
  |---------|------|------------|
  | `<variant>` | `<size>` | `<concrete values>` |

- **States** *(from the overview enum; only states that apply)*:

  | State | Appearance / behavior |
  |-------|------------------------|
  | `<state>` | `<what changes>` |

- **Behavior**: `<pointer + keyboard interaction; APG pattern followed if one exists; label/announcement for assistive tech>`
- **Content**: `<microcopy rules for its text parts - casing, length, verb form>`
- **Text budget** *(only when the overview declares a localization policy)*: `<length limit per text part incl. expansion headroom; truncation/wrap behavior>`
- **Tokens**: `<tokens consumed by name - or concrete values when design-tokens is absent>`

<!-- Add an RTL/mirroring note only for components whose layout or iconography must mirror. -->
