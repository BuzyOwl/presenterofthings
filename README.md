# PresenterOfThings for Claude

[PresenterOfThings](https://maker-of-things.pages.dev/presenter.html) is a projector-first presentation tool: every slide is a live web page the room can vote on, tap and open links from, run from a presenter cockpit. Two parts:

- **The connector** (`https://aivg-relay.dev357753.workers.dev/mcp`): add the connector once, and Claude builds and edits your decks directly. The first time, it asks you to sign in with your free PresenterOfThings account (passkey or Google). This is the one way to connect: the plugin has no connector of its own, so you sign in only once.
- **This plugin** (`skills/presenterofthings` and the commands): the deck-design playbook Claude follows (ask the brief first, build, look at every slide, fix, hand over). Optional, for better decks.

## Commands

- `/presenterofthings:new-deck [topic, audience, length]`: brief, three design directions to pick from, then the full build.
- `/presenterofthings:refresh-deck [deck]`: bring an older deck up to what the tool can do today, as a new version beside the original.
- `/presenterofthings:review-deck [deck]`: a creative director's review, then fix what you approve.
- `/presenterofthings:restyle-deck [deck]`: see a deck in other looks, apply the one you pick.

## Install

### Claude Code

1. Add the connector (in your terminal):

```
claude mcp add --transport http presenterofthings https://aivg-relay.dev357753.workers.dev/mcp
```

2. In Claude Code, type `/mcp`, pick **presenterofthings** and sign in in the browser window that opens.
3. Optional, the playbook:

```
/plugin install presenterofthings --marketplace BuzyOwl/presenterofthings
```

This repository carries its own `.claude-plugin/marketplace.json`, so it is a one-plugin marketplace. Done: ask *"Make a talk on AI for nurses with a quiz. Show me a sample first."*

To try it from a local copy instead: `claude --plugin-dir ./presenterofthings`.

### Claude (claude.ai, Desktop, Cowork)

1. Add the connector, one click: open [this link](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=PresenterOfThings&connectorUrl=https%3A%2F%2Faivg-relay.dev357753.workers.dev%2Fmcp). Claude shows its **Add custom connector** box with the name and address filled in: click **Add**, then **Connect**, and sign in. By hand: Customize → Connectors → **Add custom connector**.
2. Skill: Customize → Plugins → **Add** → **Add marketplace** → `BuzyOwl/presenterofthings` → add the plugin (its skill loads at once; it uses the connector from step 1). Or upload the zip ([presenterofthings-skill.zip](https://maker-of-things.pages.dev/kit/presenterofthings-skill.zip)) under Customize → Skills → **+** → **Create skill** → **Upload a skill**.

Other apps (ChatGPT, Codex, Cursor, VS Code) can use the same connector URL; steps are on [Your sessions → Connect your AI](https://maker-of-things.pages.dev/sessions.html).

## Privacy

Signing in lets the connected app read, create, change and delete the decks in your account; it never sees your passkeys or backup. Disconnect an app any time on [your account page](https://maker-of-things.pages.dev/account.html#apps) → Connected apps. Details: [privacy](https://maker-of-things.pages.dev/privacy.html).

## Files

```
.claude-plugin/plugin.json        the plugin
.claude-plugin/marketplace.json   makes this folder a one-plugin marketplace
skills/presenterofthings/SKILL.md the design playbook
```
