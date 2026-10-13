# Appabl plugins for Claude

A Claude plugin marketplace with one plugin, `appabl`. It steers Claude to build, publish and share web apps on [Appabl](https://appabl.ai) through your Appabl connector, instead of making a Claude artifact.

## Before you install

The plugin bundles no connector: each organization's MCP URL is its own (`https://<org>.<host>/mcp`). Add your Appabl connector first, from the **Connect your AI** page in your Appabl dashboard.

## Install

### Claude.ai, the desktop app and Cowork

1. Open **Customize → Plugins**.
2. Select **Add → Add marketplace** and enter `b1tcrx/appabl`.
3. Find **appabl** in the list and select **Add**.

The plugin is saved to your account, so it also reaches Claude Code the next time you sign in there.

### Claude Code

In a session:

```
/plugin marketplace add b1tcrx/appabl
/plugin install appabl@appabl
```

Or from your shell:

```bash
claude plugin marketplace add b1tcrx/appabl
claude plugin install appabl@appabl
```

## What it does

The plugin has one skill, `build` (`/appabl:build`). It loads when you ask for something you can open in a browser, or mention an app you already have on Appabl. Then:

- **Claude works through your Appabl connector.** It recognizes the connector by its tools (`create_app`, `get_upload_url`, `get_app_check_url`), not its name. If you have several, Claude asks which one to use and keeps to it for the rest of the conversation. If you have none, Claude tells you to add one and doesn't build the app elsewhere.
- **Claude makes no artifacts.** The deliverable is the app's URL. Source code appears as plain code blocks.

These are instructions Claude follows, not enforcement.

## Layout

```
.claude-plugin/marketplace.json        the marketplace catalog
plugins/appabl/
  .claude-plugin/plugin.json           the plugin manifest
  skills/build/SKILL.md                the skill
```

## Releasing a change

Installed copies update only when the version changes. Bump `version` in `plugins/appabl/.claude-plugin/plugin.json` with every change, then check the result:

```bash
claude plugin validate --strict .
```
