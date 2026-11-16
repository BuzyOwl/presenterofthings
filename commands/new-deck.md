---
description: Start a new PresenterOfThings deck: a short brief, three design directions to pick from, then the full build.
argument-hint: "[topic, who it is for, how long]"
---

Make a new deck in PresenterOfThings about: $ARGUMENTS

Follow the presenterofthings skill exactly:

1. Ask the brief in one message (skip what the request already answers), and wait.
2. Call `get_format` once.
3. If they chose a template: `show_templates`, wait for the pick, `get_template`, then build the whole deck in that style with `template` in the brief, and go to step 6. Otherwise work out what the deck is for (to teach, to sell, to report, to move people). Design **three directions**: three openings of this talk as three different designers would make them: another angle on the story, another composition, another kind of visual, another look. Two cards each. Create them with `create_session` and `directions`. (If the connector has no `directions` or `show_sample` yet, make one 3-card sample instead and show it with `preview_deck`.)
4. Call `show_sample`. If a picker appears in the chat, wait for the choice. Otherwise give the three links, ask which direction and what to change, and wait.
5. `pick_direction` (unless the picker did), fix what was asked, build the rest with `edit_cards` in that direction's style.
6. `preview_deck`, fix what looks wrong, check the brief's must-haves, hand over the link and ask how close it is.
