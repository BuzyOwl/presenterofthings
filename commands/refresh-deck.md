---
description: Bring an existing PresenterOfThings deck up to what the tool can do today, as a new version beside the original.
argument-hint: "[deck title, or leave empty to choose]"
---

Refresh a PresenterOfThings deck: $ARGUMENTS

1. `list_sessions`. If no deck was named, list the ones marked `refresh` and ask which. Never guess between two decks.
2. `refresh_session` on it. Tell the presenter in three or four lines what would change and why; ask if anything must stay exactly as it is.
3. Read the deck (`get_outline`, `get_card` where needed). Build the improved session: apply the listed changes, fix the listed rules, and keep the presenter's own words, numbers, pictures and notes unless a change needs otherwise.
4. Save it as a new version: `create_session` with `version_of`. The original is not touched.
5. `preview_deck` on the new version; fix what looks wrong.
6. Give both links, with what changed, card by card in one line each. Ask which one they keep.
