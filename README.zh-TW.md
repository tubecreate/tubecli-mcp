<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="TubeCLI 標誌">
</p>

<h1 align="center">TubeCLI MCP 連接器</h1>

<p align="center">
  透過 <b>cloud.tubecreate.com</b>，把 Claude、Gemini、Grok、Muse AI 等 AI 應用程式連線到你的 TubeCLI 伺服器。
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.ja.md">日本語</a> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <b>繁體中文</b>
</p>

---

## TubeCLI 是什麼？

TubeCLI 是一套自架的自動化系統，專為**從頭到尾自動製作影片**而打造：

1. **腳本。** AI 研究主題並撰寫腳本。
2. **配音。** 用 AI 語音把腳本唸出來。
3. **圖片與影片。** 用 AI 圖片和 AI 短影片片段為每個場景配上畫面（例如使用 Muse AI）。
4. **剪輯。** 加上字幕、版面和音樂，算繪出完成的影片。
5. **縮圖與 SEO。** 自動產生並檢查縮圖、標題、說明和標籤。
6. **發布。** 把影片上傳到 YouTube 等平台，也可以排程定時發布。

TubeCLI 在你自己的電腦或 VPS 上執行。它還能操作真實的瀏覽器設定檔、依排程執行 AI 代理程式，並管理任務看板。
**TubeCLI Cloud**（`cloud.tubecreate.com`）是把你所有伺服器整合在一起的控制台。

**MCP 連接器**讓 AI 應用程式可以透過 TubeCLI Cloud 和你的伺服器溝通。你可以請 Claude 或 Gemini
建立影片任務、查看某個代理程式正在做什麼、在瀏覽器設定檔裡讀取網頁，或分享做好的影片。

## 連接器網址

```
https://cloud.tubecreate.com/mcp
```

這是一個遠端 MCP 伺服器（Streamable HTTP），使用 OAuth 2.1 登入。支援的應用程式會自動完成註冊，所以
通常只要貼上這個網址就好，不需要複製任何 API 金鑰。

## 開始之前

- 一個 **TubeCLI Cloud 帳號**，可在 [cloud.tubecreate.com](https://cloud.tubecreate.com) 註冊。
- 該帳號下至少新增了一台 **TubeCLI 伺服器**：你自己的電腦（*Connect my computer*）或一台 VPS。
  你必須是它的擁有者，或者它是以**管理員**身分分享給你的。
- 伺服器執行的是 **TubeCLI 2026.08.09.217 或更新版本**。伺服器版本過舊時，控制台會顯示更新按鈕。

## 連線你的 AI 應用程式

所有應用程式最後都會進入同一個 TubeCLI 登入頁面。你在那裡選擇應用程式可以使用**哪些伺服器**，以及
**存取權限**（*唯讀* 或 *讀取與變更*），然後按下 **允許**。

### Claude（claude.ai、Claude Desktop）

1. 開啟 **Settings › Connectors**（在 claude.ai 上是 **Customize › Connectors**）。
2. 選擇 **Add custom connector**。
3. 名稱填 `TubeCLI`，網址貼上 `https://cloud.tubecreate.com/mcp`。
4. 按下 **Connect**，登入 TubeCLI Cloud，選擇伺服器後按下 **允許**。

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

接著在 Claude Code 裡執行 `/mcp`，選擇 **tubecli** 登入。

### Gemini

1. 開啟 [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors)，按下 **+ Custom**。
2. 把 `https://cloud.tubecreate.com/mcp` 貼到 **MCP Server URL**。
3. **Client ID** 和 **Client secret** 留空，按下 **Next**。
4. 登入 TubeCLI Cloud，選擇伺服器後按下 **允許**。

如果 Gemini 仍然顯示先前的錯誤，按下 **Cancel**，再重新開啟 **+ Custom**。

### Muse AI ([muse.ai](https://muse.ai), Meta)

1. 在 Muse AI 中新增一個自訂連接器，網址填 `https://cloud.tubecreate.com/mcp`。
2. 按下 **Connect**，登入 TubeCLI Cloud，選擇伺服器後按下 **允許**。

如果 Muse AI 顯示 *Missing required parameters*（缺少必要參數），請刪除這個連接器再重新新增。Muse AI 有時會
沿用舊的工作階段。

### Grok

在 Grok 中新增一個自訂連接器（遠端 MCP 伺服器），網址填 `https://cloud.tubecreate.com/mcp`，然後登入
並按下 **允許**。

### 其他 MCP 用戶端

任何支援搭配 OAuth 2.1（PKCE 與動態用戶端註冊）的遠端 MCP 伺服器的用戶端都可以連線。
如果你的應用程式要求填寫 Client ID，請在 **TubeCLI Cloud › MCP 連接器** 的
*需要 Client ID 的應用程式（Gemini）* 區塊建立一組：貼上應用程式顯示的重新導向 URI，再把 Client ID 和 Client Secret
複製回應用程式裡。密鑰只會顯示一次。

## AI 應用程式能做什麼

| 範圍 | 工具 |
|---|---|
| 伺服器與說明 | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| 任何 TubeCLI 功能（影片任務、代理程式、Content Studio、排程…） | `tubecli_api` |
| 任務看板 | `board_list`, `board_task`, `board_create` |
| 瀏覽器設定檔（你已登入的工作階段） | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| 市集與伺服器設定 | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| 成果的公開分享連結 | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| 核准 | `approval_result` |

### 請求範例

- *「列出我的 TubeCLI 伺服器，並顯示哪些影片任務正在執行。」*
- *「做一支 6 分鐘的英文影片，介紹咖啡的歷史，附上縮圖，並排程在明天上午 9 點發布到 YouTube。」*
- *「上一個影片任務為什麼失敗？幫我重試。」*
- *「找出昨天完成的影片，給我分享連結。」*
- *「在瀏覽器裡開啟我的 YouTube 設定檔，讀一下最新影片底下的留言。」*

## 安全與控管

- **伺服器由你決定。** 應用程式只能存取你擁有或管理、而且在連線時選取的伺服器。
  協作者無法把應用程式連線到分享給他們的伺服器。
- **兩種存取權限。** *唯讀* 只能查看，不能做任何變更。*讀取與變更* 還可以執行一般的變更操作。
- **高風險操作需要核准。** 刪除或取消、停止瀏覽器、安裝擴充功能，以及在 Agent Town 上發布，都會傳回一個核准連結。
  在你開啟連結並按下 **核准並執行**之前，什麼都不會執行。
- **禁止存取的內容。** 帳號、密碼、API 金鑰和原始檔案一律不開放。
- **公開分享連結需要你主動開啟。** 為某個連線勾選 *允許公開分享連結*，應用程式才能分享圖片
  和影片。連結預設有效 30 分鐘。取消勾選就會撤銷這些連結。
- **隨時可以撤銷。** **TubeCLI Cloud › MCP 連接器** 列出每個連線及其最近的活動。
  *中斷連線* 會立即切斷存取。每台伺服器也有各自的開關。
- **標準登入方式。** 使用搭配 PKCE 的 OAuth 2.1。權杖是不透明的，並以雜湊形式儲存。存取權杖有效期 1 小時，
  會自動更新。

## 疑難排解

| 問題 | 處理方式 |
|---|---|
| 應用程式顯示 `401` 或 *session expired*（工作階段已過期） | 在應用程式中移除連接器後重新新增。確認這個連線仍然出現在 **MCP 連接器** 中。 |
| *Couldn't register* / *redirect URL was rejected* | 確認你貼上的網址正好是 `https://cloud.tubecreate.com/mcp`，然後再試一次。如果問題持續，請建立 issue，寫明應用程式名稱和錯誤訊息。 |
| 登入頁面上看不到某台伺服器 | 這台伺服器必須在線上、執行 TubeCLI 2026.08.09.217 或更新版本，而且你必須是它的擁有者或管理員。 |
| 某個工具提示該伺服器上的連接器已關閉 | 在 **MCP 連接器** 中，按下該伺服器旁邊的 *開*。 |
| 某個操作傳回了核准連結 | 開啟連結，確認操作內容後按下 **核准並執行**，然後告訴應用程式已經核准。 |

## 連結

- TubeCLI Cloud：[cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI：[tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol：[modelcontextprotocol.io](https://modelcontextprotocol.io)

有問題或遇到困難嗎？[建立 issue](https://github.com/tubecreate/tubecli-mcp/issues)。
