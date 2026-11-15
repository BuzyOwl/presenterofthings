# PresenterOfThings for Claude

[PresenterOfThings](https://maker-of-things.pages.dev/presenter.html) is a projector-first presentation tool: every slide is a live web page the room can vote on, tap and open links from, run from a presenter cockpit. This plugin gives Claude:

- **the connector** (`https://aivg-relay.dev357753.workers.dev/mcp`): Claude builds and edits your decks directly. The first time, it asks you to sign in with your free PresenterOfThings account (passkey or Google). There is no private link to copy.
- **the skill** (`skills/presenterofthings`): the deck-design playbook Claude follows (ask the brief first, build, look at every slide, fix, hand over).

## Install

### Claude Code

```
/plugin marketplace add BuzyOwl/presenterofthings
/plugin install presenterofthings@presenterofthings
```

This repository carries its own `.claude-plugin/marketplace.json`, so it is a one-plugin marketplace. Then type `/mcp`, pick **presenterofthings** and sign in in the browser window that opens. Done: ask *"Make a talk on AI for nurses with a quiz. Show me a sample first."*

To try it from a local copy instead: `claude --plugin-dir ./presenterofthings`.

### Claude (claude.ai, Desktop, Cowork)

1. Customize → Connectors → **Add custom connector** → name it **PresenterOfThings** → URL `https://aivg-relay.dev357753.workers.dev/mcp` → **Add**, then **Connect** and sign in.
2. Add the skill: zip the `skills/presenterofthings` folder (or download [presenterofthings-skill.zip](https://maker-of-things.pages.dev/kit/presenterofthings-skill.zip)) and upload it under Customize → Skills.

Other apps (ChatGPT, Codex, Cursor, VS Code) can use the same connector URL; steps are on [Your sessions → Connect your AI](https://maker-of-things.pages.dev/sessions.html).

## Privacy

Signing in lets the connected app read, create, change and delete the decks in your account; it never sees your passkeys or backup. Disconnect an app any time on [your account page](https://maker-of-things.pages.dev/account.html#apps) → Connected apps. Details: [privacy](https://maker-of-things.pages.dev/privacy.html).

## Files

```
.claude-plugin/plugin.json        the plugin
.claude-plugin/marketplace.json   makes this folder a one-plugin marketplace
.mcp.json                         the connector (HTTP, OAuth sign-in)
skills/presenterofthings/SKILL.md the design playbook
```
