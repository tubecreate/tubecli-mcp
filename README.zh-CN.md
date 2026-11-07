<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="TubeCLI 标志">
</p>

<h1 align="center">TubeCLI MCP 连接器</h1>

<p align="center">
  通过 <b>cloud.tubecreate.com</b>，把 Claude、Gemini、Grok、Muse 等 AI 应用连接到你的 TubeCLI 服务器。
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.ja.md">日本語</a> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <b>简体中文</b> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## TubeCLI 是什么？

TubeCLI 是一套自托管的自动化系统，专为**从头到尾自动制作视频**而打造：

1. **脚本。** AI 调研选题并撰写脚本。
2. **配音。** 用 AI 语音把脚本朗读出来。
3. **图片和视频。** 用 AI 图片和 AI 短视频片段为每个场景配画面。
4. **剪辑。** 加上字幕、版式和音乐，渲染出成片。
5. **缩略图和 SEO。** 自动生成并检查缩略图、标题、简介和标签。
6. **发布。** 把视频上传到 YouTube 等平台，也可以按计划定时发布。

TubeCLI 运行在你自己的电脑或 VPS 上。它还能操作真实的浏览器配置文件、按计划运行 AI 智能体，并管理任务看板。
**TubeCLI Cloud**（`cloud.tubecreate.com`）是把你所有服务器集中在一起的控制面板。

**MCP 连接器**让 AI 应用可以通过 TubeCLI Cloud 与你的服务器对话。你可以让 Claude 或 Gemini
创建视频任务、查看某个智能体正在做什么、在浏览器配置文件里读取网页，或者分享做好的视频。

## 连接器地址

```
https://cloud.tubecreate.com/mcp
```

这是一个远程 MCP 服务器（Streamable HTTP），使用 OAuth 2.1 登录。支持的应用会自动完成注册，所以
通常只需粘贴这个地址即可，不需要复制任何 API 密钥。

## 开始之前

- 一个 **TubeCLI Cloud 账号**，在 [cloud.tubecreate.com](https://cloud.tubecreate.com) 注册。
- 该账号下至少添加了一台 **TubeCLI 服务器**：你自己的电脑（*Connect my computer*）或一台 VPS。
  你必须是它的所有者，或者它以**管理员**身份共享给了你。
- 服务器运行的是 **TubeCLI 2026.08.09.217 或更新版本**。服务器版本过旧时，控制面板会显示更新按钮。

## 连接你的 AI 应用

所有应用最后都会进入同一个 TubeCLI 登录页面。你在那里选择应用可以使用**哪些服务器**，以及
**访问权限**（*只读* 或 *读取和更改*），然后点击 **允许**。

### Claude（claude.ai、Claude Desktop）

1. 打开 **Settings › Connectors**（在 claude.ai 上是 **Customize › Connectors**）。
2. 选择 **Add custom connector**。
3. 名称填 `TubeCLI`，地址粘贴 `https://cloud.tubecreate.com/mcp`。
4. 点击 **Connect**，登录 TubeCLI Cloud，选择服务器后点击 **允许**。

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

然后在 Claude Code 里运行 `/mcp`，选择 **tubecli** 进行登录。

### Gemini

1. 打开 [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors)，点击 **+ Custom**。
2. 把 `https://cloud.tubecreate.com/mcp` 粘贴到 **MCP Server URL**。
3. **Client ID** 和 **Client secret** 留空，点击 **Next**。
4. 登录 TubeCLI Cloud，选择服务器后点击 **允许**。

如果 Gemini 仍然显示之前的错误，点击 **Cancel**，再重新打开 **+ Custom**。

### Muse（Meta）

1. 在 Muse 中添加一个自定义连接器，地址填 `https://cloud.tubecreate.com/mcp`。
2. 点击 **Connect**，登录 TubeCLI Cloud，选择服务器后点击 **允许**。

如果 Muse 显示 *Missing required parameters*（缺少必需参数），请删除这个连接器后重新添加。Muse 有时会
沿用旧的会话。

### Grok

在 Grok 中添加一个自定义连接器（远程 MCP 服务器），地址填 `https://cloud.tubecreate.com/mcp`，然后登录
并点击 **允许**。

### 其他 MCP 客户端

任何支持带 OAuth 2.1（PKCE 和动态客户端注册）的远程 MCP 服务器的客户端都可以连接。
如果你的应用要求填写 Client ID，请在 **TubeCLI Cloud › MCP 连接器** 的
*需要 Client ID 的应用（Gemini）* 部分创建一个：粘贴应用显示的重定向 URI，然后把 Client ID 和 Client Secret
复制回应用里。密钥只显示一次。

## AI 应用能做什么

| 领域 | 工具 |
|---|---|
| 服务器与帮助 | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| 任何 TubeCLI 功能（视频任务、智能体、Content Studio、定时计划…） | `tubecli_api` |
| 任务看板 | `board_list`, `board_task`, `board_create` |
| 浏览器配置文件（你已登录的会话） | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| 市场与服务器配置 | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| 成果的公开分享链接 | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| 审批 | `approval_result` |

### 示例请求

- *“列出我的 TubeCLI 服务器，并显示哪些视频任务正在运行。”*
- *“做一个 6 分钟的英文视频，讲咖啡的历史，配上缩略图，并安排在明天上午 9 点发布到 YouTube。”*
- *“上一个视频任务为什么失败了？重试一下。”*
- *“找出昨天做好的视频，给我分享链接。”*
- *“在浏览器里打开我的 YouTube 配置文件，读一下最新视频下面的评论。”*

## 安全与控制

- **服务器由你来选。** 应用只能访问你拥有或管理、并且在连接时选中的服务器。
  协作者无法把应用连接到共享给他们的服务器。
- **两种访问权限。** *只读* 只能查看，不能做任何更改。*读取和更改* 还可以执行一般的更改操作。
- **高风险操作需要审批。** 删除或取消、停止浏览器、安装扩展以及在 Agent Town 上发布，都会返回一个审批链接。
  在你打开链接并点击 **批准并运行**之前，什么都不会执行。
- **禁止访问的内容。** 账号、密码、API 密钥和原始文件一律不开放。
- **公开分享链接需要你主动开启。** 为某个连接勾选 *允许公开分享链接*，应用才能分享图片
  和视频。链接默认有效 30 分钟。取消勾选会撤销这些链接。
- **随时可以撤销。** **TubeCLI Cloud › MCP 连接器** 列出了每个连接及其最近的活动。
  *断开连接* 会立即切断访问。每台服务器也有各自的开关。
- **标准登录方式。** 使用带 PKCE 的 OAuth 2.1。令牌是不透明的，并以哈希形式存储。访问令牌有效期 1 小时，
  会自动刷新。

## 故障排除

| 问题 | 解决方法 |
|---|---|
| 应用显示 `401` 或 *session expired*（会话已过期） | 在应用中删除连接器后重新添加。确认这个连接仍然出现在 **MCP 连接器** 中。 |
| *Couldn't register* / *redirect URL was rejected* | 确认你粘贴的地址正好是 `https://cloud.tubecreate.com/mcp`，然后再试一次。如果问题依旧，请提交 issue，写明应用名称和错误信息。 |
| 登录页面上看不到某台服务器 | 这台服务器必须在线、运行 TubeCLI 2026.08.09.217 或更新版本，并且你必须是它的所有者或管理员。 |
| 某个工具提示该服务器上的连接器已关闭 | 在 **MCP 连接器** 中，点击该服务器旁边的 *开*。 |
| 某个操作返回了审批链接 | 打开链接，确认操作内容后点击 **批准并运行**，然后告诉应用已经批准。 |

## 链接

- TubeCLI Cloud：[cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI：[tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol：[modelcontextprotocol.io](https://modelcontextprotocol.io)

有问题或遇到困难？[提交 issue](https://github.com/tubecreate/tubecli-mcp/issues)。
