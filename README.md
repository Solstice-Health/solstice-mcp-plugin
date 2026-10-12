# Solstice Platform plugin

Public listing for the hosted Solstice MCP. This repository has no server code. Cursor and Claude Code call `https://api.solsticehealth.co/mcp`. Codex calls the AgentCore gateway, which forwards to that same service. Each user signs in with Auth0.

## Cursor

A team admin imports this repository:

1. Open [Dashboard → Plugins & MCPs](https://cursor.com/dashboard?tab=plugins).
2. Under **Team Marketplaces**, choose **Add Marketplace → Import from Repo**.
3. Paste `https://github.com/Solstice-Health/solstice-mcp-plugin`.
4. Confirm **solstice-platform** is listed, set who can install it, then save. Turn on **Auto Refresh** if you want pushes to update the listing.

Each teammate then installs it:

1. Open **Customize** in Cursor.
2. Install **Solstice Platform**.
3. Open **Settings → MCP**, select `solstice-platform`, and finish the Auth0 login.

Installing the plugin does not grant Solstice access. The signed-in user still needs a Solstice account.
