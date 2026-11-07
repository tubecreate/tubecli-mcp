<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="TubeCLI 로고">
</p>

<h1 align="center">TubeCLI MCP 커넥터</h1>

<p align="center">
  Claude, Gemini, Grok, Muse 등 AI 앱을 <b>cloud.tubecreate.com</b>을 통해 내 TubeCLI 서버에 연결하세요.
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.ja.md">日本語</a> ·
  <b>한국어</b> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## TubeCLI란?

TubeCLI는 **영상 제작을 처음부터 끝까지 자동으로** 해 주는 셀프 호스팅 자동화 시스템입니다.

1. **대본.** AI가 주제를 조사하고 대본을 씁니다.
2. **음성.** AI 음성으로 대본을 읽어 줍니다.
3. **이미지와 영상.** 각 장면을 AI 이미지와 짧은 AI 영상 클립으로 채웁니다.
4. **편집.** 자막, 레이아웃, 음악을 넣고 최종 영상을 렌더링합니다.
5. **썸네일과 SEO.** 썸네일, 제목, 설명, 태그를 만들고 점검합니다.
6. **게시.** 영상을 YouTube와 다른 플랫폼에 업로드합니다. 원하면 예약 게시도 됩니다.

TubeCLI는 내 컴퓨터나 VPS에서 실행됩니다. 실제 브라우저 프로필을 조작하고, AI 에이전트를 일정에 맞춰 실행하며,
작업 보드도 관리합니다. **TubeCLI Cloud**(`cloud.tubecreate.com`)는 내 서버들을 한곳에 모아 주는 대시보드입니다.

**MCP 커넥터**를 쓰면 AI 앱이 TubeCLI Cloud를 통해 내 서버와 대화할 수 있습니다. Claude나 Gemini에게
영상 작업 만들기, 에이전트가 무엇을 하고 있는지 확인하기, 브라우저 프로필에서 페이지 읽기, 완성된 영상 공유하기 등을 부탁할 수 있습니다.

## 커넥터 URL

```
https://cloud.tubecreate.com/mcp
```

OAuth 2.1로 로그인하는 원격 MCP 서버(Streamable HTTP)입니다. 지원되는 앱은 스스로 등록하므로
보통은 URL만 붙여 넣으면 됩니다. 복사해야 할 API 키는 없습니다.

## 시작하기 전에

- [cloud.tubecreate.com](https://cloud.tubecreate.com)의 **TubeCLI Cloud 계정**.
- 그 계정에 추가된 **TubeCLI 서버** 1대 이상: 내 컴퓨터(*Connect my computer*) 또는 VPS.
  내가 그 서버의 소유자이거나, **관리자**로 공유받은 상태여야 합니다.
- 서버에서 **TubeCLI 2026.08.09.217 이상**이 실행 중이어야 합니다. 서버가 오래된 버전이면 대시보드에 업데이트 버튼이 보입니다.

## AI 앱 연결하기

어느 앱이든 마지막에는 같은 TubeCLI 로그인 페이지로 이어집니다. 여기서 앱이 쓸 수 있는 **서버**와
**접근 수준**(*읽기 전용* 또는 *읽기 및 변경*)을 고른 다음 **허용**을 누르세요.

### Claude(claude.ai, Claude Desktop)

1. **Settings › Connectors**를 엽니다(claude.ai에서는 **Customize › Connectors**).
2. **Add custom connector**를 선택합니다.
3. 이름을 `TubeCLI`로 하고 `https://cloud.tubecreate.com/mcp`를 붙여 넣습니다.
4. **Connect**를 누르고 TubeCLI Cloud에 로그인한 뒤, 서버를 고르고 **허용**을 누릅니다.

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

그런 다음 Claude Code 안에서 `/mcp`를 실행하고 **tubecli**를 선택해 로그인합니다.

### Gemini

1. [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors)를 열고 **+ Custom**을 누릅니다.
2. **MCP Server URL**에 `https://cloud.tubecreate.com/mcp`를 붙여 넣습니다.
3. **Client ID**와 **Client secret**은 비워 두고 **Next**를 누릅니다.
4. TubeCLI Cloud에 로그인한 뒤, 서버를 고르고 **허용**을 누릅니다.

Gemini에 예전 오류가 계속 보이면 **Cancel**을 누르고 **+ Custom**을 다시 여세요.

### Muse(Meta)

1. Muse에서 URL `https://cloud.tubecreate.com/mcp`로 사용자 지정 커넥터를 추가합니다.
2. **Connect**를 누르고 TubeCLI Cloud에 로그인한 뒤, 서버를 고르고 **허용**을 누릅니다.

Muse에 *Missing required parameters*(필수 매개변수 누락)가 표시되면 커넥터를 삭제하고 다시 추가하세요. Muse가 가끔
예전 세션을 다시 쓰기 때문입니다.

### Grok

Grok에서 URL `https://cloud.tubecreate.com/mcp`로 사용자 지정 커넥터(원격 MCP 서버)를 추가한 뒤, 로그인하고
**허용**을 누르세요.

### 그 밖의 MCP 클라이언트

OAuth 2.1(PKCE와 동적 클라이언트 등록)을 지원하는 원격 MCP 서버를 쓸 수 있는 클라이언트라면 어떤 것이든 연결할 수 있습니다.
앱이 Client ID를 요구하면 **TubeCLI Cloud › MCP 커넥터**의
*Client ID가 필요한 앱(Gemini)* 항목에서 하나 만드세요. 앱에 표시된 리디렉션 URI를 붙여 넣은 다음, 발급된 Client ID와 Client Secret을
앱에 다시 붙여 넣으면 됩니다. 시크릿은 한 번만 표시됩니다.

## AI 앱으로 할 수 있는 일

| 영역 | 도구 |
|---|---|
| 서버와 도움말 | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| TubeCLI의 모든 기능(영상 작업, 에이전트, Content Studio, 일정 등) | `tubecli_api` |
| 작업 보드 | `board_list`, `board_task`, `board_create` |
| 브라우저 프로필(로그인된 세션) | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| 마켓과 서버 설정 | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| 결과물 공개 공유 링크 | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| 승인 | `approval_result` |

### 요청 예시

- *"내 TubeCLI 서버 목록을 보여 주고, 실행 중인 영상 작업이 무엇인지 알려 줘."*
- *"커피의 역사에 관한 6분짜리 영어 영상을 썸네일과 함께 만들고, YouTube에 내일 오전 9시로 예약해 줘."*
- *"마지막 영상 작업은 왜 실패했어? 다시 시도해 줘."*
- *"어제 완성된 영상을 찾아서 공유 링크를 줘."*
- *"브라우저에서 내 YouTube 프로필을 열고 최신 영상의 댓글을 읽어 줘."*

## 안전과 제어

- **서버는 내가 고릅니다.** 앱은 내가 소유하거나 관리하는 서버 중에서 연결할 때 고른 서버에만 접근합니다.
  공동 작업자는 공유받은 서버에 앱을 연결할 수 없습니다.
- **두 가지 접근 수준.** *읽기 전용*은 보기만 하고 아무것도 바꾸지 않습니다. *읽기 및 변경*은 일반적인 변경도 실행할 수 있습니다.
- **위험한 작업은 승인 필요.** 삭제나 취소, 브라우저 중지, 확장 프로그램 설치, Agent Town 게시를 하면
  승인 링크가 돌아옵니다. 내가 링크를 열고 **승인하고 실행**를 누르기 전까지는 아무것도 실행되지 않습니다.
- **접근 금지 영역.** 계정, 비밀번호, API 키, 원본 파일에는 접근할 수 없습니다.
- **공개 공유 링크는 선택 사항.** 연결마다 *공개 공유 링크 허용*에 체크하면 앱이 이미지와 영상을 공유할 수 있습니다.
  링크는 기본적으로 30분 동안 유효합니다. 체크를 해제하면 링크가 취소됩니다.
- **언제든 취소 가능.** **TubeCLI Cloud › MCP 커넥터**에 모든 연결과 최근 활동이 표시됩니다.
  *연결 해제*를 누르면 즉시 접근이 끊깁니다. 서버마다 켜기/끄기 스위치도 따로 있습니다.
- **표준 로그인.** PKCE가 포함된 OAuth 2.1을 사용합니다. 토큰은 내용을 알 수 없는 형식이며 해시로 저장됩니다. 액세스 토큰은 1시간 동안 유효하고
  자동으로 갱신됩니다.

## 문제 해결

| 문제 | 해결 방법 |
|---|---|
| 앱에 `401` 또는 *session expired*(세션 만료)가 표시됨 | 앱에서 커넥터를 삭제하고 다시 추가하세요. **MCP 커넥터**에 해당 연결이 아직 있는지도 확인하세요. |
| *Couldn't register* / *redirect URL was rejected*가 표시됨 | `https://cloud.tubecreate.com/mcp`를 정확히 붙여 넣었는지 확인하고 다시 시도하세요. 계속되면 앱 이름과 오류 문구를 적어 issue를 등록해 주세요. |
| 로그인 페이지에 서버가 보이지 않음 | 서버가 온라인이고 TubeCLI 2026.08.09.217 이상이 실행 중이어야 하며, 내가 그 서버의 소유자이거나 관리자여야 합니다. |
| 도구가 서버에서 커넥터가 꺼져 있다고 함 | **MCP 커넥터**에서 해당 서버 옆의 *켜기*를 누르세요. |
| 작업 결과로 승인 링크가 돌아옴 | 링크를 열어 작업 내용을 확인하고 **승인하고 실행**를 누른 다음, 승인했다고 앱에 알려 주세요. |

## 링크

- TubeCLI Cloud: [cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI: [tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)

질문이나 문제가 있나요? [issue를 등록해 주세요](https://github.com/tubecreate/tubecli-mcp/issues).
