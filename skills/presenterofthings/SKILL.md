---
name: presenterofthings
description: Build, restyle, review or polish a presentation, lesson, talk, pitch or deck in PresenterOfThings (the PresenterOfThings connector or its tools such as create_session, preview_deck and set_theme). Use whenever the person asks for slides or a deck and the PresenterOfThings tools are available, or names PresenterOfThings, even for a small change to one slide.
---

# PresenterOfThings: making the best deck the room has seen

PresenterOfThings is not a slide file. Every card is a live web page the room can vote on from their phones, tap, and open links from, run from a presenter cockpit. Your job is to use that: build decks a person with taste would be proud to present, then check them with your own eyes before you hand them over.

## The loop (every new deck)

1. **Ask the brief first**, in one message, each question with its default: who is in the room and for how long; formal or informal; colourful or plain; should the room take part on phones (poll, word cloud, quiz, Q&A, feedback form); rich graphics or minimal; research and links, or only their material. Wait for the answers.
2. **Read the format once**: call `get_format`. It is the full specification: fields, visuals, looks, checks, and the design guidance this skill summarises.
3. **Plan before cards**: the story in sections (`section` on the first card of each part), one finding per card, where the room acts (a poll before a reveal, a quiz near the end, Q&A last), and one **signature** the deck owns (an accent word on every section opener, one colour that marks the answer, the presenter's own photos).
4. **Build** with `create_session` (put the answers in `brief`, set `purpose` and `minutes`).
5. **Look at it**: `preview_deck` (12 cards a call, contact sheets). Do the director's pass below and fix with `edit_cards`, `update_card`, `set_theme`. Check changed cards full size with `preview_card`.
6. **Hand over** the "Open it" link from the tool result. Do not also write a PowerPoint, PDF or HTML file: the deck lives in PresenterOfThings and exports to PowerPoint from the website.

Changing an existing deck: `list_sessions`, then edit only the cards asked about. A new look is `set_theme` on the same deck; a whole new design is `create_session` with `version_of`.

## The director's pass

Look at every contact sheet and fix until each answer is yes:

- **One signature** the deck repeats with variation.
- **Squint test**: at half size, each card shows one thing first.
- **Rhythm**: loud, quiet, a picture, a question to the room. Three neighbours that look alike: change one composition.
- **Fill or breathe, never float**: no small object in the middle of a large blank card. Enlarge it, put it beside the headline (`split`), or cut it.
- **The right component**: a comparison → `compare` or a `blocks` row of cards; change over time → `chart`; a process → `diagram` (builds on clicks); a reveal → `flip` or a `poll` first; a price list or scorecard → `blocks` cards, not a table.
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
- **Links open on the projector** inside the deck; put sources on the card (`doc`, `props`) so the presenter shows them without leaving the slides.
- **Notes are the script**: `notes.say` is what the presenter will actually say (about 130 words a minute; the checker compares it with `minutes`).

You cannot show anything to the audience or send anything to phones: the presenter does that in the cockpit.
