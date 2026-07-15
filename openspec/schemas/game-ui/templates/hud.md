---
schema-version: 1.2.0
document-version: 0
---

# HUD & world-space UI

<!-- Every persistent or transient in-game element, itemized individually
     (vitals, minimap, objective tracker, reticle, markers, damage numbers,
     notifications, boss bars...).
     Repeat the element block per element.
     Widgets reused inside elements by widgets.md name.
     Replace every `<...>` placeholder and example row, dropping the backticks unless the value is a literal.
     Delete guidance comments when done. -->

## `<Element name>`

`<one-line purpose>`

- **UI layer**: `<diegetic / non-diegetic / spatial / meta>` - `<one-line rationale>`
- **Placement**: `<screen region or world anchor; safe-area compliance; collision behavior with other elements>`
- **Data**: `<gameplay state displayed, by GDD mechanic/state name>`
- **Visibility**: `<always-on / contextual / on change / hold-to-view; fade rules; behavior in photo mode if one exists>`
- **Customization**: `<settings.md option names that affect it - scale / opacity / position / toggle / contrast variant>`
- **Feedback channels**: `<the non-visual channels carrying the same information - audio cue / haptics; no essential information on one channel alone>`

## Subtitles & captions

<!-- CONDITIONAL section - when the game has speech or important audio.
     Concrete values, not intents. -->
- Line limits: `<max characters per line / max lines>`
- Size: `<floor + scaling range>`
- Background: `<opacity range>`
- Speaker identification: `<how>`
- Placement: `<where + repositioning rules>`
- Controlled by: `<settings.md option names>`
