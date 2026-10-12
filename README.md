# Solstice Platform plugin

Public listing for the hosted Solstice MCP. This repository has no server code. Cursor and Claude Code call `https://api.solsticehealth.co/mcp`. Codex calls the AgentCore gateway URL in `plugins/solstice-platform/codex.mcp.json`, which forwards to that same service.

Each person signs in with Auth0 after install. The plugin does not share credentials, and it does not grant Solstice access. The signed-in user still needs a Solstice account.

Marketplace name: `solstice-tools`. Plugin name: `solstice-platform`.

## Cursor

A team admin imports this repository once:

1. Open [Dashboard → Plugins & MCPs](https://cursor.com/dashboard?tab=plugins).
2. Under **Team Marketplaces**, choose **Add Marketplace → Import from Repo**.
3. Paste `https://github.com/Solstice-Health/solstice-mcp-plugin`.
4. Confirm **solstice-platform** is listed, set who can install it, then save. Turn on **Auto Refresh** so later pushes update the listing. That needs the Cursor GitHub App on this repo.

Each teammate then installs it:

1. Open **Customize** in Cursor.
2. Install **Solstice Platform**.
3. Open **Settings → MCP**, select `solstice-platform`, and finish the Auth0 login.

To update or remove it, use **Customize**. Admins refresh the marketplace from the dashboard, or rely on **Auto Refresh**.

## Claude Code

Add the marketplace, then install the plugin. In a Claude Code session:

```text
/plugin marketplace add Solstice-Health/solstice-mcp-plugin
/plugin install solstice-platform@solstice-tools
/reload-plugins
```

From a shell, the same steps are:

```bash
claude plugin marketplace add Solstice-Health/solstice-mcp-plugin
claude plugin install solstice-platform@solstice-tools
```

Start a new session, or run `/reload-plugins` in the open one. If reload warns that it would invalidate the prompt cache, run `/reload-plugins --force`. See [Install and manage plugins](https://code.claude.com/docs/en/plugins/install).

Then authenticate `solstice-platform` from `/mcp`, or run `claude mcp login solstice-platform` when that command is available. Claude Code uses callback `http://localhost:8787/callback`.

Update or uninstall:

```text
/plugin marketplace update solstice-tools
/plugin update solstice-platform@solstice-tools
/plugin uninstall solstice-platform@solstice-tools
```

Run `/reload-plugins` after an update or uninstall.

## Codex

Codex 0.142.0 or newer is required. Auth0 only accepts a fixed loopback callback, so set this at the top level of `~/.codex/config.toml` before logging in:

```toml
mcp_oauth_callback_port = 8788
```

That setting is required for both a marketplace install and a local install. Codex derives `http://127.0.0.1:8788/callback/TL-8G9qfe5UK` for the production gateway.

Add the marketplace and install the plugin:

```bash
codex plugin marketplace add Solstice-Health/solstice-mcp-plugin
codex plugin add solstice-platform@solstice-tools
codex mcp login solstice-platform
```

Restart Codex after installing or updating. Read tools run under normal policy. Codex prompts before write tools because the plugin uses `writes` approval mode.

From a local clone, the marketplace source can be the repo path instead of the GitHub name:

```bash
codex plugin marketplace add "$(pwd)"
codex plugin add solstice-platform@solstice-tools
codex mcp login solstice-platform
```

Update or remove:

```bash
codex plugin marketplace upgrade solstice-tools
codex plugin remove solstice-platform@solstice-tools
```

Restart Codex after either command.
