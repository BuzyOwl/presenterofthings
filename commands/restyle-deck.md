---
description: Try a PresenterOfThings deck in other looks without changing it, then apply the one the presenter picks.
argument-hint: "[deck title, and the feeling wanted]"
---

Restyle this PresenterOfThings deck: $ARGUMENTS

1. `list_sessions`, find it. `get_brand`: with a brand kit set, keep its colours and fonts and say so.
2. `show_sample` on the deck: a picker in the chat shows its first cards in three looks; elsewhere give the three links. Wait for the choice.
3. Apply it with `set_theme` (the picker may already have). For a whole new design rather than a new look, offer a v2: `create_session` with `version_of`.
4. `preview_deck`; fix any card the new look breaks (text on pictures, charts that lost contrast).
