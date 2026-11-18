---
name: presenterofthings
description: Build, restyle, review or polish a presentation, lesson, talk, pitch or deck in PresenterOfThings (the PresenterOfThings connector or its tools such as create_session, preview_deck and set_theme). Use whenever the person asks for slides or a deck and the PresenterOfThings tools are available, or names PresenterOfThings, even for a small change to one slide.
---

# PresenterOfThings: making the best deck the room has seen

PresenterOfThings is not a slide file. Every card is a live web page the room can vote on from their phones, tap, and open links from, run from a presenter cockpit. Your job is to use that: build decks a person with taste would be proud to present, then check them with your own eyes before you hand them over.

## The loop (every new deck)

1. **Ask the brief first**, in one message, each question with its default: who is in the room and for how long; formal or informal; colourful or plain; how much text (light, balanced, or reading for rooms that read along); should the room take part on phones (poll, word cloud, quiz, Q&A, feedback form); rich graphics or minimal; research and links, or only their material; anything that must be in it or stay out; how to start: from a ready-made template (the fastest), three design directions made for this talk (the default), one quick sample, or all in one go; or one of their own decks to follow. Wait for the answers.
2. **Read the format once**: call `get_format`. It is the full specification: fields, visuals, looks, checks, and the design guidance this skill summarises.
3. **Plan before cards**: the story in sections (`section` on the first card of each part), one finding per card, where the room acts (a poll before a reveal, a quiz near the end, Q&A last), and one **signature** the deck owns (an accent word on every section opener, one colour that marks the answer, the presenter's own photos).
4. **Build** with `create_session`: everything goes inside `session`, as `{ title, brief, purpose, minutes, cards: [...] }`. `brief` is an object, not prose: `{ audience, tone: formal|informal, style: colourful|plain, interact: [poll, wordcloud, quiz, qa, form], graphics: rich|minimal, links, research }`. Without it the deck is refused. Add `must` (what has to be in or out, their words) and, only if they said to build it all in one go, `sample: "skip"`.
5. **A template, if they want one.** `show_templates`: where the app can draw it they flip through the ready-made decks in the chat and pick; elsewhere give them the links it returns and ask. Then `get_template` for their pick and write the whole deck in that style in one `create_session`: the same look, the same kinds of card and rhythm, every word theirs, with `template: "<id>"` in the brief. A signature template (bauhaus, botanical, brutalist, museum, watercolour) also has a designed `cover`: keep its composition, put in their title and name, and write each picture's `find` for their topic. The brief also asks, optionally, for their LinkedIn profile link: given, it goes on the last slide as a "connect" QR (`brief.linkedin`) and is saved privately to their profile; next time only ask whether to use it. `set_linkedin` changes it or shows/hides it on their public page (private unless they ask). Never invent or look up one yourself. No sample step is needed. To follow one of their own decks, read it and put `style_of: "<its id>"` in the brief. Otherwise:
   **Sample first: three directions.** Work out what the deck is for (to teach, to sell, to report, to move people), then design three openings of this talk as three different designers would: another angle on the story, another composition (one huge line, a full-bleed picture, a visual beside the words, a free canvas), another kind of visual (a picture, an explainer chart the presenter plays, one number, a poll), another look. Recolouring one design is refused. `create_session` with `directions`: three of `{ name, why, theme, cards: [2] }` (the opening, and one card that shows how the rest would look: the two directions not picked are thrown away, so keep them small), no `cards`. If they asked for one quick sample instead, send three `cards` and `sample: "one"` in the brief. **Older connector?** If `create_session` does not list `directions`, or there is no `show_sample` tool, the connector has not been updated yet: make one 3-card sample, show it with `preview_deck`, give the link, ask, and carry on from there. Then `show_sample`: where the app can draw it the presenter sees each direction's real cards in the chat and picks one there (the choice comes back as a message; `pick_direction` may already be done). Elsewhere it returns a link per direction: give them those, ask which and what to change, and wait. Then `pick_direction`, fix what they said, and build the rest in that direction's style with `edit_cards`. More than six cards at once is refused without `sample: "skip"`.
6. **Look at it**: `preview_deck` (12 cards a call, contact sheets). Do the director's pass below and fix with `edit_cards`, `update_card`, `set_theme`. Check changed cards full size with `preview_card`.
7. **Hand over**: check the brief's `must` item by item, give the "Open it" link from the tool result, and ask "How close is this, and what would you change?" Make those changes in place. Do not also write a PowerPoint, PDF or HTML file: the deck lives in PresenterOfThings and exports to PowerPoint from the website.

Refreshing an older deck ("update it", "make it use the new features"): `refresh_session` says what is new since it was made and what to change, card by card, with reasons. Make the improved deck as a new version (`create_session` with `version_of`), look at it, and give both links so they can compare. `list_sessions` marks decks worth refreshing.

Changing an existing deck: `list_sessions`, then edit only the cards asked about. A new look is `set_theme` on the same deck; a whole new design is `create_session` with `version_of`.

**Change, add and delete are different.** "Change / update / fix / redo slide 7" = `update_card` on that card: same id, same place. "Add a slide after 7" = `add_card` with `after_card_id` = slide 7's id: slide 7 stays. Delete a slide only when the presenter asked, in their words, to delete or remove it, never to "replace" it with a new card; the server refuses a deletion without `confirm_delete: ["<card id>"]`. Unclear ("replace slide 7 with…")? Ask: "Shall I rewrite slide 7 “<title>” in place, or keep it and add a new slide after it?" Slide numbers are the `n` in `get_outline` (the top-bar counter; the cover is not counted): say the title back if they might count differently. Afterwards tell them what changed in the tool result's words ("Updated slide 7 “…”", "Inserted new slide 8 after “…”", "Deleted slide 7 “…”: undo is available"); `undo_last_change` brings a deleted slide back.

## The director's pass

Look at every contact sheet and fix until each answer is yes:

- **One signature** the deck repeats with variation.
- **Squint test**: at half size, each card shows one thing first.
- **Rhythm**: loud, quiet, a picture, a question to the room. Three neighbours that look alike: change one composition.
- **Fill or breathe, never float**: no small object in the middle of a large blank card. Enlarge it, put it beside the headline (`split`), or cut it.
- **The right component**: a comparison → `compare` or a `blocks` row of cards; change over time → `chart`; a process → `diagram` (builds on clicks); dated events, a cycle, the parts of a thing, a place, a decision, states or choices → `explainer` (a chart the presenter plays: timeline, clock, exploded view, scene, flowchart, comic, flow machine, game board, catalogue; only when the shape of the content is the point); a reveal → `flip` or a `poll` first; a price list or scorecard → `blocks` cards, not a table.
- **Action headers**: titles state the finding with its number or verb ("HeyGen doubled in eight months"), never the topic.
- **Would a person with taste ship it?** If a card looks like a template, it is one.

## Taste, in short

- Start from the house look `paper` and make it this deck's: an accent colour from the subject (a brand, a material, a place), one title face with character, real pictures of the real thing (`"find": "photo: …"`, large pictures only for full-screen use).
- `accent`: one to three words of a title lettered in the accent face (serif italic, or handwriting with `fonts.accentFont`), on the cover and one or two turning points. Rare is what makes it work.
- Emoji are objects, not ornaments: one per tile or step, where it *is* the thing named, never in a title, one icon family per deck. `3d:` and `animated:` icons for a number or a win, once or twice a deck.
- Colour is a state system: neutral content, one accent for the thing to look at, green and red only for good and bad in data.
- Plain words: no dash asides, no "not just X, but Y", no unlock / elevate / seamless / game-changing.
- At most three text sizes on a card; nothing smaller than the footnote size; never shrink text to fit more in: cut or split.

## What sets PresenterOfThings apart (use it)

- **The room takes part**: polls, word clouds, quizzes with a live leaderboard, Q&A with upvotes, feedback forms, all from phones via the join code. Put one every few cards in a lesson; open with a warm-up poll.
- **Things the presenter touches**: flip cards, myth or fact, diagrams that build step by step, races, galleries, `blocks` cards that turn over.
- **Links open on the projector** inside the deck. Two places, and they are different: **on the slide** (visible and clickable during the talk) is `doc: { label, url }` (one link at the slide's foot, shown as "📘 Official: label ↗") or a `gallery` visual with a `url` per tile, or on a canvas card any text, image or shape with `href: "https://…"` (that box becomes the link); **in the cockpit's Links & files panel** (the presenter opens them on stage or sends them to phones; nothing on the slide) is `props` / `add_links`. `<a>` in text shows as plain text: use `href`.
- **Click to move on, timed slides, the circle transition**: a canvas text, image or shape with `go: "next" | "prev" | "<card id>"` moves there when tapped ("when I tap the dot, open the next slide" = the dot with `go: "next"` and the next card's `transition: "iris"`); a card's `auto: N` (2–600 s) moves on by itself, never on a live poll, quiz, myth/fact, Q&A or form card. These are supported: build them, don't refuse. Asked for links without saying where? Ask: "On the slide itself, or in your links panel for phones?"
- **Notes are the script**: `notes.say` is exactly what the presenter will say out loud (about 130 words a minute; the checker compares it with `minutes`). They read it from the teleprompter, so nothing else goes in it: no labels, stage directions or reminders (those go in `notes.ask`, `notes.try`, `notes.dont`, or nowhere). Short sentences, `- ` for a list, a blank line for a beat.

You cannot send anything to phones or change what the audience sees: the presenter does that in the cockpit. One exception, below.

## Marks on the live slide (`annotate_live`)

While the presenter is presenting and has turned on **Let my AI mark the slides** in the cockpit (off by default, per deck), `annotate_live` circles, boxes, underlines, points at or draws an arrow on the slide the room is looking at, hand-drawn on the projector. **No `session_id` is needed**: left out, it marks the deck on air. Marks show only in the laptop's audience window (after **▶ Present**), not on Cast or the /tv screen.
- **Only when asked**: the presenter says "circle the chart", or you answer a question about what is on screen and the mark shows what your answer is about. Never spontaneously, never to decorate, never on another slide.
- **Pass the slide's `card_id`** (from `get_outline`); a different slide on screen is refused, and the refusal says which one is showing. Leave it out to mark whatever is showing.
- **`marks`: tags only, 1–3 is best, at most 6.** Prefer anchors: `[CIRCLE:@visual:the spike]`, `[UNDERLINE:@title]`, `[POINT:@takeaway:this]`, `[RECT:@3:label]` (canvas element 3), `[ARROW:@1->@4:label]`, `[CLEAR]`. Otherwise numbers 0–1000 of the slide (0,0 top left): `[RECT:x1,y1,x2,y2:label]`, `[CIRCLE:x,y,r:label]`. Labels 1–4 words. `delay` (0–10 s) lands a mark as you finish a sentence.
- **Refused** when nothing is on air, the switch is off, another deck is on air (the refusal names it and its id) or the slide is another one: the refusal says what the presenter must do; tell them in one line and try again once they have. The presenter clears marks with one tap (or Esc / C); a new slide clears them too.

## When something breaks

If something breaks, a tool keeps failing, or the presenter wants a feature, offer to send it with `send_feedback` (kind `bug`, `error`, `feature` or `suggestion`; put the tool name and error in `context`; `via: "plugin"`). Show the presenter the exact text first and send only after they say yes.
