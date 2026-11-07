<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="TubeCLI logo">
</p>

<h1 align="center">TubeCLI MCP Connector</h1>

<p align="center">
  Connect Claude, Gemini, Grok, Muse AI and other AI apps to your TubeCLI servers through <b>cloud.tubecreate.com</b>.
</p>

<p align="center">
  <b>English</b> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.ja.md">日本語</a> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## What is TubeCLI?

TubeCLI is a self-hosted automation system built for **automatic video creation from A to Z**:

1. **Script.** AI researches the topic and writes the script.
2. **Voice.** The script is read aloud with AI voices.
3. **Images and video.** Scenes are illustrated with AI images and short AI video clips, for example with Muse AI.
4. **Editing.** Subtitles, layout and music are added and the final video is rendered.
5. **Thumbnail and SEO.** A thumbnail, title, description and tags are generated and checked.
6. **Publishing.** The video is uploaded to YouTube and other platforms, on a schedule if you want.

TubeCLI runs on your own computer or VPS. It also drives real browser profiles, runs AI agents on a schedule and
manages a task board. **TubeCLI Cloud** (`cloud.tubecreate.com`) is the dashboard that ties your servers together.

The **MCP connector** lets an AI app talk to your servers through TubeCLI Cloud. You can ask Claude or Gemini to
create a video task, check what an agent is doing, read a page in a browser profile, or share a finished video.

## The connector URL

```
https://cloud.tubecreate.com/mcp
```

This is a remote MCP server (Streamable HTTP) with OAuth 2.1 sign-in. Supported apps register by themselves, so you
normally only paste the URL. There is no API key to copy.

## Before you start

- A **TubeCLI Cloud account** at [cloud.tubecreate.com](https://cloud.tubecreate.com).
- At least one **TubeCLI server** added to that account: your own computer (*Connect my computer*) or a VPS.
  You must be its owner, or it must be shared with you as an **admin**.
- The server runs **TubeCLI 2026.08.09.217 or newer**. The dashboard shows an update button when a server is out of date.

## Connect your AI app

Every app ends at the same TubeCLI sign-in page. There you pick **which servers** the app may use and the
**access level** (*Read only* or *Read & change*), then press **Allow**.

### Claude (claude.ai, Claude Desktop)

1. Open **Settings › Connectors** (on claude.ai: **Customize › Connectors**).
2. Choose **Add custom connector**.
3. Name it `TubeCLI` and paste `https://cloud.tubecreate.com/mcp`.
4. Press **Connect**, sign in to TubeCLI Cloud, pick servers and press **Allow**.

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

Then run `/mcp` inside Claude Code and choose **tubecli** to sign in.

### Gemini

1. Open [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors) and press **+ Custom**.
2. Paste `https://cloud.tubecreate.com/mcp` into **MCP Server URL**.
3. Leave **Client ID** and **Client secret** empty and press **Next**.
4. Sign in to TubeCLI Cloud, pick servers and press **Allow**.

If Gemini still shows an old error, press **Cancel** and open **+ Custom** again.

### Muse AI ([muse.ai](https://muse.ai), Meta)

1. In Muse AI, add a custom connector with the URL `https://cloud.tubecreate.com/mcp`.
2. Press **Connect**, sign in to TubeCLI Cloud, pick servers and press **Allow**.

If Muse AI shows *Missing required parameters*, delete the connector and add it again. Muse AI sometimes reuses an old
session.

### Grok

Add a custom connector (remote MCP server) in Grok with the URL `https://cloud.tubecreate.com/mcp`, then sign in
and press **Allow**.

### Other MCP clients

Any client that supports remote MCP servers with OAuth 2.1 (PKCE and dynamic client registration) can connect.
If your app asks for a Client ID instead, create one in **TubeCLI Cloud › MCP Connector** under
*Apps that ask for a Client ID*: paste the redirect URI the app shows, then copy the Client ID and Client Secret
back into the app. The secret is shown only once.

## What the AI app can do

| Area | Tools |
|---|---|
| Servers and help | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| Any TubeCLI feature (video tasks, agents, Content Studio, schedules…) | `tubecli_api` |
| Task board | `board_list`, `board_task`, `board_create` |
| Browser profiles (your logged-in sessions) | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| Market and server setup | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| Public share links for results | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| Approvals | `approval_result` |

### Example requests

- *"List my TubeCLI servers and show which video tasks are running."*
- *"Create a 6-minute English video about the history of coffee, with a thumbnail, and schedule it on YouTube for tomorrow 9 AM."*
- *"Why did the last video task fail? Retry it."*
- *"Find yesterday's finished videos and give me share links."*
- *"Open my YouTube profile in the browser and read the comments on the newest video."*

## Safety and control

- **You choose the servers.** The app only reaches servers you own or administer and picked when connecting.
  Collaborators cannot connect an app to a shared server.
- **Two access levels.** *Read only* can look but not change anything. *Read & change* can also run ordinary changes.
- **Approval for risky actions.** Deleting or cancelling, stopping a browser, installing extensions and publishing on
  Agent Town return an approval link. Nothing runs until you open it and press **Approve and run**.
- **Off-limits.** Accounts, passwords, API keys and raw files stay off-limits.
- **Public share links are opt-in.** Tick *Allow public share links* for a connection to let the app share images
  and videos. Links last 30 minutes by default. Unticking the box revokes them.
- **Revoke at any time.** **TubeCLI Cloud › MCP Connector** lists every connection with its recent activity.
  *Disconnect* cuts access immediately. Each server also has its own on/off switch.
- **Standard sign-in.** OAuth 2.1 with PKCE is used. Tokens are opaque and stored hashed. Access tokens last 1 hour
  and refresh automatically.

## Troubleshooting

| Problem | What to do |
|---|---|
| The app shows `401` or *session expired* | Remove the connector in the app and add it again. Check that the connection still appears in **MCP Connector**. |
| *Couldn't register* / *redirect URL was rejected* | Make sure you pasted exactly `https://cloud.tubecreate.com/mcp`, then try again. If it persists, open an issue with the app name and the error text. |
| A server does not appear on the sign-in page | It must be online, run TubeCLI 2026.08.09.217+, and you must be its owner or an admin. |
| A tool says the connector is off on a server | In **MCP Connector**, press *On* next to that server. |
| An action returned an approval link | Open the link, check the action and press **Approve and run**, then tell the app it is approved. |

## Links

- TubeCLI Cloud: [cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI: [tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)

Questions or problems? [Open an issue](https://github.com/tubecreate/tubecli-mcp/issues).
