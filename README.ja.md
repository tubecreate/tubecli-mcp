<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="TubeCLI ロゴ">
</p>

<h1 align="center">TubeCLI MCP コネクタ</h1>

<p align="center">
  Claude、Gemini、Grok、Muse AI などの AI アプリを、<b>cloud.tubecreate.com</b> 経由であなたの TubeCLI サーバーにつなげます。
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.es.md">Español</a> ·
  <b>日本語</b> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## TubeCLI とは？

TubeCLI は、**動画づくりを最初から最後まで自動化する**ためのセルフホスト型の自動化システムです。

1. **台本。** AI がテーマを調べて台本を書きます。
2. **音声。** 台本を AI の声で読み上げます。
3. **画像と動画。** 各シーンを AI 画像と短い AI 動画クリップで描きます（例：Muse AI）。
4. **編集。** 字幕、レイアウト、音楽を加えて、完成した動画を書き出します。
5. **サムネイルと SEO。** サムネイル、タイトル、説明文、タグを作成してチェックします。
6. **公開。** 動画を YouTube などのプラットフォームにアップロードします。予約投稿もできます。

TubeCLI はあなた自身のパソコンや VPS で動きます。実際のブラウザープロフィールの操作、AI エージェントの定期実行、
タスクボードの管理もできます。**TubeCLI Cloud**（`cloud.tubecreate.com`）は、あなたのサーバーをまとめて管理するダッシュボードです。

**MCP コネクタ**を使うと、AI アプリが TubeCLI Cloud を通してあなたのサーバーとやり取りできます。Claude や Gemini に、
動画タスクの作成、エージェントが今何をしているかの確認、ブラウザープロフィールでのページの読み取り、完成した動画の共有などを頼めます。

## コネクタの URL

```
https://cloud.tubecreate.com/mcp
```

これは OAuth 2.1 でサインインするリモート MCP サーバー（Streamable HTTP）です。対応アプリは自分で登録を済ませるので、
ふつうは URL を貼り付けるだけで大丈夫です。コピーする API キーはありません。

## はじめる前に

- [cloud.tubecreate.com](https://cloud.tubecreate.com) の **TubeCLI Cloud アカウント**。
- そのアカウントに追加された **TubeCLI サーバー**が 1 台以上：あなた自身のパソコン（*Connect my computer*）または VPS。
  あなたがそのサーバーのオーナーであるか、**管理者**として共有されている必要があります。
- サーバーで **TubeCLI 2026.08.09.217 以降**が動いていること。サーバーが古い場合は、ダッシュボードに更新ボタンが表示されます。

## AI アプリをつなぐ

どのアプリでも、最後は同じ TubeCLI のサインインページにたどり着きます。そこで、アプリが使える**サーバー**と
**アクセスレベル**（「読み取りのみ」または「読み取りと変更」）を選び、**許可**を押します。

### Claude（claude.ai、Claude Desktop）

1. **Settings › Connectors** を開きます（claude.ai では **Customize › Connectors**）。
2. **Add custom connector** を選びます。
3. 名前を `TubeCLI` にして、`https://cloud.tubecreate.com/mcp` を貼り付けます。
4. **Connect** を押して TubeCLI Cloud にサインインし、サーバーを選んで**許可**を押します。

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

続いて Claude Code の中で `/mcp` を実行し、**tubecli** を選んでサインインします。

### Gemini

1. [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors) を開き、**+ Custom** を押します。
2. **MCP Server URL** に `https://cloud.tubecreate.com/mcp` を貼り付けます。
3. **Client ID** と **Client secret** は空のまま、**Next** を押します。
4. TubeCLI Cloud にサインインし、サーバーを選んで**許可**を押します。

Gemini に古いエラーが表示されたままの場合は、**Cancel** を押してから、もう一度 **+ Custom** を開いてください。

### Muse AI ([muse.ai](https://muse.ai), Meta)

1. Muse AI で、URL `https://cloud.tubecreate.com/mcp` のカスタムコネクタを追加します。
2. **Connect** を押して TubeCLI Cloud にサインインし、サーバーを選んで**許可**を押します。

Muse AI に *Missing required parameters*（必須パラメーターが不足しています）と表示された場合は、コネクタを削除して追加し直してください。
Muse AI は古いセッションを使い回すことがあります。

### Grok

Grok で URL `https://cloud.tubecreate.com/mcp` のカスタムコネクタ（リモート MCP サーバー）を追加し、サインインして
**許可**を押します。

### そのほかの MCP クライアント

OAuth 2.1（PKCE と動的クライアント登録）に対応したリモート MCP サーバーを使えるクライアントなら、どれでも接続できます。
アプリが Client ID を求めてくる場合は、**TubeCLI Cloud › MCP コネクタ** の
「Client ID が必要なアプリ（Gemini）」で作成します。アプリに表示されたリダイレクト URI を貼り付け、発行された Client ID と Client Secret を
アプリに貼り戻してください。シークレットは一度しか表示されません。

## AI アプリでできること

| 分野 | ツール |
|---|---|
| サーバーとヘルプ | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| TubeCLI のあらゆる機能（動画タスク、エージェント、Content Studio、スケジュールなど） | `tubecli_api` |
| タスクボード | `board_list`, `board_task`, `board_create` |
| ブラウザープロフィール（ログイン済みのセッション） | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| マーケットとサーバーのセットアップ | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| 成果物の公開共有リンク | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| 承認 | `approval_result` |

### お願いの例

- *「私の TubeCLI サーバーを一覧にして、実行中の動画タスクを見せて。」*
- *「コーヒーの歴史についての 6 分間の英語動画を、サムネイル付きで作って、YouTube で明日の午前 9 時に予約公開して。」*
- *「最後の動画タスクはなぜ失敗したの？もう一度やり直して。」*
- *「昨日完成した動画を探して、共有リンクをちょうだい。」*
- *「ブラウザーで私の YouTube プロフィールを開いて、最新の動画のコメントを読んで。」*

## 安全とコントロール

- **サーバーはあなたが選びます。** アプリが使えるのは、あなたがオーナーまたは管理者で、接続時に選んだサーバーだけです。
  共同作業者は、共有されたサーバーにアプリをつなぐことはできません。
- **2 つのアクセスレベル。** 「読み取りのみ」は見るだけで、何も変更できません。「読み取りと変更」は、ふだんの変更も実行できます。
- **危険な操作には承認が必要。** 削除やキャンセル、ブラウザーの停止、拡張機能のインストール、Agent Town での公開を行うと、
  承認リンクが返されます。あなたがリンクを開いて **承認して実行** を押すまで、何も実行されません。
- **立ち入り禁止の領域。** アカウント、パスワード、API キー、生のファイルには触れられません。
- **公開共有リンクはオプトイン。** 接続ごとに「公開共有リンクを許可」にチェックを入れると、アプリが画像や動画を共有できるようになります。
  リンクの有効期限は標準で 30 分です。チェックを外すと、リンクは取り消されます。
- **いつでも取り消せます。** **TubeCLI Cloud › MCP コネクタ** に、すべての接続と最近のアクティビティが一覧表示されます。
  「接続を解除」を押すと、すぐにアクセスが止まります。サーバーごとにもオン／オフのスイッチがあります。
- **標準的なサインイン。** PKCE 付きの OAuth 2.1 を使っています。トークンは中身の読めない形式で、ハッシュ化して保存されます。アクセストークンの有効期限は 1 時間で、
  自動的に更新されます。

## 困ったときは

| 問題 | 対処法 |
|---|---|
| アプリに `401` または *session expired*（セッションの期限切れ）と表示される | アプリでコネクタを削除して、追加し直してください。**MCP コネクタ** にその接続がまだ表示されているかも確認してください。 |
| *Couldn't register* / *redirect URL was rejected* と表示される | `https://cloud.tubecreate.com/mcp` を正確に貼り付けたか確認して、もう一度試してください。それでも続く場合は、アプリ名とエラーの文面を添えて issue を作成してください。 |
| サインインページにサーバーが表示されない | サーバーがオンラインで、TubeCLI 2026.08.09.217 以降が動いていて、あなたがそのオーナーか管理者である必要があります。 |
| ツールが「このサーバーではコネクタがオフです」と言う | **MCP コネクタ** で、そのサーバーの横にある「オン」を押してください。 |
| 操作の結果として承認リンクが返ってきた | リンクを開いて操作内容を確認し、**承認して実行** を押してから、承認したことをアプリに伝えてください。 |

## リンク

- TubeCLI Cloud: [cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI: [tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)

質問や問題がありますか？ [issue を作成してください](https://github.com/tubecreate/tubecli-mcp/issues)。
