---
schema-version: 1.2.0
document-version: 0
---

# Design tokens

<!-- CONDITIONAL - only when styling is token-based (centralized stylesheet/theming).
     DTCG vocabulary: name, $type, $value.
     Tokens are named ONCE here; widgets/screens/hud consume them by name.
     Replace every example row; keep only the groups the game uses.
     Delete guidance comments when done. -->

## Color

<!-- Semantic roles, not raw palette dumps. -->
| Token | $type | $value | Role |
|-------|-------|--------|------|
| `<color.primary>` | color | `<value>` | `<role>` |

## Typography

<!-- Few families (production practice); fallback chain per script
     from the overview localization policy. -->
| Token | $type | $value | Fallback chain |
|-------|-------|--------|----------------|
| `<type.body>` | typography | `<family / size / weight / line-height>` | `<per-script fallbacks>` |

## Dimension

| Token | $type | $value |
|-------|-------|--------|
| `<space.md>` | dimension | `<value>` |

## Motion

<!-- Every animated transition in widgets/screens/flows references these by name.
     Motion must remain reducible per the accessibility target. -->
| Token | $type | $value |
|-------|-------|--------|
| `<motion.easing.standard>` | cubicBezier | `<x1,y1,x2,y2>` |
| `<motion.duration.short>` | duration | `<ms>` |

## Themes

<!-- Each theme = a collection of token VALUES over the same names
     (default / high contrast / colorblind variants).
     Widgets never restate per-theme behavior. -->
| Token | `<default>` | `<high-contrast>` |
|-------|-----------|------------------|
| `<color.surface>` | `<value>` | `<value>` |
