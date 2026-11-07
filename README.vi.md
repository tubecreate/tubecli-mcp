<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="Logo TubeCLI">
</p>

<h1 align="center">TubeCLI MCP Connector</h1>

<p align="center">
  Kết nối Claude, Gemini, Grok, Muse và các app AI khác với máy chủ TubeCLI của bạn qua <b>cloud.tubecreate.com</b>.
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <b>Tiếng Việt</b> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.ja.md">日本語</a> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## TubeCLI là gì?

TubeCLI là hệ thống tự động hoá do bạn tự cài và tự chạy, được làm ra để **tự động tạo video từ A đến Z**:

1. **Kịch bản.** AI tìm hiểu đề tài và viết kịch bản.
2. **Giọng đọc.** Kịch bản được đọc thành tiếng bằng giọng AI.
3. **Hình ảnh và video.** Từng cảnh được minh hoạ bằng ảnh AI và các clip video AI ngắn.
4. **Dựng video.** Thêm phụ đề, bố cục và nhạc, rồi xuất ra video hoàn chỉnh.
5. **Thumbnail và SEO.** Tạo và kiểm tra thumbnail, tiêu đề, mô tả và thẻ tag.
6. **Đăng video.** Video được tải lên YouTube và các nền tảng khác, có thể hẹn giờ nếu bạn muốn.

TubeCLI chạy trên máy tính hoặc VPS của chính bạn. Nó còn điều khiển các hồ sơ trình duyệt thật, chạy agent AI theo lịch và
quản lý bảng công việc. **TubeCLI Cloud** (`cloud.tubecreate.com`) là bảng điều khiển gom tất cả máy chủ của bạn về một chỗ.

**Trình kết nối MCP** giúp app AI làm việc với máy chủ của bạn thông qua TubeCLI Cloud. Bạn có thể nhờ Claude hoặc Gemini
tạo một task video, xem agent đang làm gì, đọc một trang web trong hồ sơ trình duyệt, hoặc chia sẻ video đã làm xong.

## Đường dẫn kết nối

```
https://cloud.tubecreate.com/mcp
```

Đây là máy chủ MCP từ xa (Streamable HTTP), đăng nhập bằng OAuth 2.1. Các app được hỗ trợ sẽ tự đăng ký, nên thường
bạn chỉ cần dán đường dẫn này. Không có API key nào phải sao chép.

## Trước khi bắt đầu

- Một **tài khoản TubeCLI Cloud** tại [cloud.tubecreate.com](https://cloud.tubecreate.com).
- Ít nhất một **máy chủ TubeCLI** đã thêm vào tài khoản đó: máy tính của bạn (*Connect my computer*) hoặc một VPS.
  Bạn phải là chủ máy chủ, hoặc được chia sẻ máy chủ với vai trò **quản trị viên** (admin).
- Máy chủ chạy **TubeCLI 2026.08.09.217 trở lên**. Khi máy chủ đang dùng bản cũ, bảng điều khiển sẽ hiện nút cập nhật.

## Kết nối app AI của bạn

App nào rồi cũng dẫn tới cùng một trang đăng nhập TubeCLI. Tại đó bạn chọn **những máy chủ** mà app được dùng và
**mức quyền** (*Chỉ đọc* hoặc *Đọc và thay đổi*), rồi bấm **Cho phép**.

### Claude (claude.ai, Claude Desktop)

1. Mở **Settings › Connectors** (trên claude.ai: **Customize › Connectors**).
2. Chọn **Add custom connector**.
3. Đặt tên là `TubeCLI` và dán `https://cloud.tubecreate.com/mcp`.
4. Bấm **Connect**, đăng nhập TubeCLI Cloud, chọn máy chủ rồi bấm **Cho phép**.

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

Sau đó chạy `/mcp` trong Claude Code và chọn **tubecli** để đăng nhập.

### Gemini

1. Mở [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors) và bấm **+ Custom**.
2. Dán `https://cloud.tubecreate.com/mcp` vào ô **MCP Server URL**.
3. Để trống **Client ID** và **Client secret**, rồi bấm **Next**.
4. Đăng nhập TubeCLI Cloud, chọn máy chủ rồi bấm **Cho phép**.

Nếu Gemini vẫn hiện lỗi cũ, hãy bấm **Cancel** rồi mở lại **+ Custom**.

### Muse (Meta)

1. Trong Muse, thêm một connector tuỳ chỉnh với đường dẫn `https://cloud.tubecreate.com/mcp`.
2. Bấm **Connect**, đăng nhập TubeCLI Cloud, chọn máy chủ rồi bấm **Cho phép**.

Nếu Muse báo *Missing required parameters* (thiếu tham số bắt buộc), hãy xoá connector rồi thêm lại. Đôi khi Muse dùng
lại một phiên cũ.

### Grok

Thêm một connector tuỳ chỉnh (máy chủ MCP từ xa) trong Grok với đường dẫn `https://cloud.tubecreate.com/mcp`, rồi đăng nhập
và bấm **Cho phép**.

### Các app MCP khác

App nào hỗ trợ máy chủ MCP từ xa với OAuth 2.1 (PKCE và tự đăng ký client) đều kết nối được.
Nếu app của bạn lại đòi Client ID, hãy tạo một Client ID trong **TubeCLI Cloud › Trình kết nối MCP**, ở mục
*App cần Client ID (Gemini)*: dán redirect URI mà app hiện ra, rồi chép Client ID và Client Secret
ngược lại vào app. Secret chỉ hiện đúng một lần.

## App AI làm được gì

| Mảng | Công cụ |
|---|---|
| Máy chủ và trợ giúp | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| Mọi tính năng của TubeCLI (task video, agent, Content Studio, lịch chạy…) | `tubecli_api` |
| Bảng công việc | `board_list`, `board_task`, `board_create` |
| Hồ sơ trình duyệt (các phiên bạn đã đăng nhập sẵn) | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| Chợ và thiết lập máy chủ | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| Link chia sẻ công khai cho kết quả | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| Duyệt thao tác | `approval_result` |

### Ví dụ yêu cầu

- *"Liệt kê các máy chủ TubeCLI của tôi và cho biết task video nào đang chạy."*
- *"Tạo một video tiếng Anh dài 6 phút về lịch sử cà phê, kèm thumbnail, và hẹn đăng lên YouTube lúc 9 giờ sáng mai."*
- *"Vì sao task video vừa rồi bị lỗi? Chạy lại giúp tôi."*
- *"Tìm các video làm xong hôm qua và gửi tôi link chia sẻ."*
- *"Mở hồ sơ YouTube của tôi trong trình duyệt và đọc bình luận của video mới nhất."*

## An toàn và quyền kiểm soát

- **Bạn chọn máy chủ.** App chỉ vào được những máy chủ bạn sở hữu hoặc quản trị và đã chọn lúc kết nối.
  Cộng tác viên không thể kết nối app vào máy chủ được chia sẻ cho họ.
- **Hai mức quyền.** *Chỉ đọc* được xem nhưng không được thay đổi gì. *Đọc và thay đổi* được làm thêm các thay đổi thông thường.
- **Thao tác rủi ro phải được duyệt.** Xoá hoặc huỷ, dừng trình duyệt, cài extension và đăng lên Agent Town sẽ trả về
  một link duyệt. Không có gì chạy cho tới khi bạn mở link đó và bấm **Duyệt và chạy**.
- **Vùng cấm.** Tài khoản, mật khẩu, API key và file thô luôn nằm ngoài tầm tay của app.
- **Link chia sẻ công khai chỉ có khi bạn bật.** Đánh dấu *Cho phép tạo link chia sẻ công khai* cho một kết nối để app
  được chia sẻ ảnh và video. Mặc định mỗi link dùng được 30 phút. Bỏ đánh dấu thì các link sẽ bị thu hồi.
- **Thu hồi bất cứ lúc nào.** **TubeCLI Cloud › Trình kết nối MCP** liệt kê mọi kết nối kèm hoạt động gần đây.
  *Ngắt kết nối* cắt quyền truy cập ngay lập tức. Mỗi máy chủ cũng có công tắc bật/tắt riêng.
- **Đăng nhập theo chuẩn.** Dùng OAuth 2.1 với PKCE. Token là chuỗi không đọc được nội dung (opaque) và chỉ được lưu dưới
  dạng băm. Access token có hạn 1 giờ và tự làm mới.

## Xử lý sự cố

| Vấn đề | Cách xử lý |
|---|---|
| App hiện `401` hoặc *session expired* | Gỡ connector trong app rồi thêm lại. Kiểm tra xem kết nối vẫn còn trong **Trình kết nối MCP** không. |
| *Couldn't register* / *redirect URL was rejected* | Kiểm tra bạn đã dán đúng chính xác `https://cloud.tubecreate.com/mcp`, rồi thử lại. Nếu vẫn lỗi, hãy mở issue kèm tên app và nội dung lỗi. |
| Một máy chủ không hiện trên trang đăng nhập | Máy chủ phải đang online, chạy TubeCLI 2026.08.09.217+, và bạn phải là chủ hoặc quản trị viên của máy chủ đó. |
| Một công cụ báo connector đang tắt trên một máy chủ | Trong **Trình kết nối MCP**, bấm *Bật* cạnh máy chủ đó. |
| Một thao tác trả về link duyệt | Mở link, xem lại thao tác và bấm **Duyệt và chạy**, rồi báo cho app biết là bạn đã duyệt. |

## Liên kết

- TubeCLI Cloud: [cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI: [tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)

Có câu hỏi hoặc gặp sự cố? [Mở issue](https://github.com/tubecreate/tubecli-mcp/issues).
