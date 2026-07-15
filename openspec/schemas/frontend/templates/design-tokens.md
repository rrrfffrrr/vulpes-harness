---
schema-version: 1.1.1
document-version: 0
---

# Design tokens

<!-- CONDITIONAL - only when styling is token-based.
     DTCG vocabulary: name, $type, $value.
     Tokens are named ONCE here; components/screens consume them by name.
     Replace every example row; keep only the groups the product uses.
     Delete guidance comments when done. -->

## Color

<!-- Semantic roles, not raw palette dumps. -->
| Token | $type | $value | Role |
|-------|-------|--------|------|
| `<color.primary>` | color | `<value>` | `<role>` |

## Typography

| Token | $type | $value |
|-------|-------|--------|
| `<type.body>` | typography | `<family / size / weight / line-height>` |

## Dimension

| Token | $type | $value |
|-------|-------|--------|
| `<space.md>` | dimension | `<value>` |

## Motion

<!-- Every animated transition in components/screens references these by name. -->
| Token | $type | $value |
|-------|-------|--------|
| `<motion.easing.standard>` | cubicBezier | `<x1,y1,x2,y2>` |
| `<motion.duration.short>` | duration | `<ms>` |

## Themes

<!-- Each theme = a collection of token VALUES over the same names.
     Components never restate per-theme behavior. -->
| Token | `<light>` | `<dark>` |
|-------|---------|--------|
| `<color.surface>` | `<value>` | `<value>` |
