<p align="center">
  <img src="https://cloud.tubecreate.com/logo.svg" width="96" alt="TubeCLI logosu">
</p>

<h1 align="center">TubeCLI MCP Bağlayıcısı</h1>

<p align="center">
  Claude, Gemini, Grok, Muse AI ve diğer AI uygulamalarını <b>cloud.tubecreate.com</b> üzerinden TubeCLI sunucularınıza bağlayın.
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.ja.md">日本語</a> ·
  <a href="README.ko.md">한국어</a> ·
  <a href="README.ru.md">Русский</a> ·
  <b>Türkçe</b> ·
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>

---

## TubeCLI nedir?

TubeCLI, kendi sunucunuzda çalıştırdığınız ve **A'dan Z'ye otomatik video üretimi** için tasarlanmış bir otomasyon sistemidir:

1. **Senaryo.** AI konuyu araştırır ve senaryoyu yazar.
2. **Seslendirme.** Senaryo AI sesleriyle seslendirilir.
3. **Görseller ve video.** Sahneler AI görselleri ve kısa AI video klipleriyle canlandırılır, örneğin Muse AI ile.
4. **Kurgu.** Altyazı, yerleşim ve müzik eklenir, ardından son video oluşturulur.
5. **Küçük resim ve SEO.** Küçük resim, başlık, açıklama ve etiketler hazırlanır ve kontrol edilir.
6. **Yayınlama.** Video YouTube'a ve diğer platformlara yüklenir; isterseniz zamanlanmış olarak.

TubeCLI kendi bilgisayarınızda veya VPS'inizde çalışır. Ayrıca gerçek tarayıcı profillerini yönetir, AI ajanlarını bir zamanlamaya
göre çalıştırır ve bir görev panosu tutar. **TubeCLI Cloud** (`cloud.tubecreate.com`), tüm sunucularınızı bir araya getiren yönetim panelidir.

**MCP bağlayıcısı**, bir AI uygulamasının TubeCLI Cloud üzerinden sunucularınızla konuşmasını sağlar. Claude'a veya Gemini'ye
bir video görevi oluşturmasını, bir ajanın ne yaptığını kontrol etmesini, bir tarayıcı profilinde bir sayfayı okumasını veya
bitmiş bir videoyu paylaşmasını söyleyebilirsiniz.

## Bağlayıcı adresi

```
https://cloud.tubecreate.com/mcp
```

Bu, OAuth 2.1 ile giriş yapılan uzak bir MCP sunucusudur (Streamable HTTP). Desteklenen uygulamalar kendilerini otomatik olarak
kaydeder; bu yüzden genellikle yalnızca adresi yapıştırmanız yeterlidir. Kopyalamanız gereken bir API anahtarı yoktur.

## Başlamadan önce

- [cloud.tubecreate.com](https://cloud.tubecreate.com) adresinde bir **TubeCLI Cloud hesabı**.
- Bu hesaba eklenmiş en az bir **TubeCLI sunucusu**: kendi bilgisayarınız (*Connect my computer*) veya bir VPS.
  Sunucunun sahibi olmalısınız ya da sunucu sizinle **yönetici** olarak paylaşılmış olmalıdır.
- Sunucuda **TubeCLI 2026.08.09.217 veya daha yeni** bir sürüm çalışıyor olmalıdır. Bir sunucu güncel değilse panelde güncelleme düğmesi görünür.

## AI uygulamanızı bağlayın

Her uygulama sonunda aynı TubeCLI giriş sayfasına çıkar. Orada uygulamanın **hangi sunucuları** kullanabileceğini ve
**erişim düzeyini** (*Yalnızca okuma* veya *Okuma ve değiştirme*) seçer, ardından **İzin ver** düğmesine basarsınız.

### Claude (claude.ai, Claude Desktop)

1. **Settings › Connectors** bölümünü açın (claude.ai'de: **Customize › Connectors**).
2. **Add custom connector** seçeneğini seçin.
3. Adını `TubeCLI` koyun ve `https://cloud.tubecreate.com/mcp` adresini yapıştırın.
4. **Connect** düğmesine basın, TubeCLI Cloud'a giriş yapın, sunucuları seçin ve **İzin ver** düğmesine basın.

### Claude Code

```bash
claude mcp add --transport http tubecli https://cloud.tubecreate.com/mcp
```

Ardından Claude Code içinde `/mcp` komutunu çalıştırın ve giriş yapmak için **tubecli** seçeneğini seçin.

### Gemini

1. [gemini.google.com › Connectors](https://gemini.google.com/customize/connectors) sayfasını açın ve **+ Custom** düğmesine basın.
2. `https://cloud.tubecreate.com/mcp` adresini **MCP Server URL** alanına yapıştırın.
3. **Client ID** ve **Client secret** alanlarını boş bırakın ve **Next** düğmesine basın.
4. TubeCLI Cloud'a giriş yapın, sunucuları seçin ve **İzin ver** düğmesine basın.

Gemini hâlâ eski bir hata gösteriyorsa **Cancel** düğmesine basın ve **+ Custom** seçeneğini yeniden açın.

### Muse AI ([muse.ai](https://muse.ai), Meta)

1. Muse AI'da `https://cloud.tubecreate.com/mcp` adresiyle özel bir bağlayıcı ekleyin.
2. **Connect** düğmesine basın, TubeCLI Cloud'a giriş yapın, sunucuları seçin ve **İzin ver** düğmesine basın.

Muse AI *Missing required parameters* hatası gösterirse bağlayıcıyı silip yeniden ekleyin. Muse AI bazen eski bir oturumu
yeniden kullanır.

### Grok

Grok'ta `https://cloud.tubecreate.com/mcp` adresiyle özel bir bağlayıcı (uzak MCP sunucusu) ekleyin, ardından giriş yapın
ve **İzin ver** düğmesine basın.

### Diğer MCP istemcileri

OAuth 2.1 (PKCE ve dinamik istemci kaydı) ile uzak MCP sunucularını destekleyen her istemci bağlanabilir.
Uygulamanız bunun yerine bir Client ID isterse, **TubeCLI Cloud › MCP Bağlayıcısı** sayfasında
*Client ID isteyen uygulamalar (Gemini)* bölümünden bir tane oluşturun: uygulamanın gösterdiği redirect URI'yi yapıştırın, ardından
Client ID ve Client Secret değerlerini uygulamaya geri kopyalayın. Secret yalnızca bir kez gösterilir.

## AI uygulaması neler yapabilir?

| Alan | Araçlar |
|---|---|
| Sunucular ve yardım | `servers_list`, `tubecli_overview`, `tubecli_doc`, `tubecli_endpoints` |
| Her TubeCLI özelliği (video görevleri, ajanlar, Content Studio, zamanlamalar…) | `tubecli_api` |
| Görev panosu | `board_list`, `board_task`, `board_create` |
| Tarayıcı profilleri (giriş yapılmış oturumlarınız) | `browser_profiles`, `browser_open`, `browser_goto`, `browser_read`, `browser_click`, `browser_type`, `browser_scroll`, `browser_screenshot`, `browser_nav`, `browser_close` |
| Market ve sunucu kurulumu | `market_install`, `server_clone`, `clone_manifest`, `clone_export`, `clone_import`, `clone_status` |
| Sonuçlar için herkese açık paylaşım bağlantıları | `share_find`, `share_file`, `share_files`, `share_list`, `share_revoke` |
| Agent Town | `town_agent_offer` |
| Onaylar | `approval_result` |

### Örnek istekler

- *"TubeCLI sunucularımı listele ve hangi video görevlerinin çalıştığını göster."*
- *"Kahvenin tarihi hakkında, küçük resmi olan 6 dakikalık İngilizce bir video oluştur ve YouTube'da yarın sabah 9'a zamanla."*
- *"Son video görevi neden başarısız oldu? Yeniden dene."*
- *"Dün biten videoları bul ve bana paylaşım bağlantılarını ver."*
- *"Tarayıcıda YouTube profilimi aç ve en yeni videonun yorumlarını oku."*

## Güvenlik ve kontrol

- **Sunucuları siz seçersiniz.** Uygulama yalnızca sahibi ya da yöneticisi olduğunuz ve bağlanırken seçtiğiniz sunuculara erişir.
  Ortak çalışanlar, paylaşılan bir sunucuya uygulama bağlayamaz.
- **İki erişim düzeyi.** *Yalnızca okuma* bakabilir ama hiçbir şeyi değiştiremez. *Okuma ve değiştirme* sıradan değişiklikleri de yapabilir.
- **Riskli işlemler için onay.** Silme veya iptal etme, bir tarayıcıyı durdurma, eklenti yükleme ve Agent Town'da yayınlama
  bir onay bağlantısı döndürür. Siz bağlantıyı açıp **Onayla ve çalıştır** düğmesine basana kadar hiçbir şey çalışmaz.
- **Erişime kapalı.** Hesaplar, şifreler, API anahtarları ve ham dosyalar erişime kapalıdır.
- **Herkese açık paylaşım bağlantıları isteğe bağlıdır.** Uygulamanın görsel ve video paylaşabilmesi için bir bağlantıda
  *Herkese açık paylaşım bağlantılarına izin ver* kutusunu işaretleyin. Bağlantılar varsayılan olarak 30 dakika geçerlidir. Kutunun işaretini kaldırırsanız bağlantılar iptal edilir.
- **İstediğiniz zaman iptal edin.** **TubeCLI Cloud › MCP Bağlayıcısı** sayfası her bağlantıyı son etkinlikleriyle birlikte listeler.
  *Bağlantıyı kes* erişimi hemen sonlandırır. Her sunucunun ayrıca kendi açma/kapama düğmesi vardır.
- **Standart giriş.** PKCE ile OAuth 2.1 kullanılır. Token'lar opaktır ve hash'lenmiş olarak saklanır. Erişim token'ları 1 saat
  geçerlidir ve otomatik olarak yenilenir.

## Sorun giderme

| Sorun | Ne yapmalı |
|---|---|
| Uygulama `401` veya *session expired* gösteriyor | Bağlayıcıyı uygulamadan kaldırıp yeniden ekleyin. Bağlantının **MCP Bağlayıcısı** sayfasında hâlâ göründüğünü kontrol edin. |
| *Couldn't register* / *redirect URL was rejected* | Tam olarak `https://cloud.tubecreate.com/mcp` adresini yapıştırdığınızdan emin olun ve tekrar deneyin. Sorun devam ederse uygulama adını ve hata metnini yazarak bir issue açın. |
| Bir sunucu giriş sayfasında görünmüyor | Sunucu çevrimiçi olmalı, TubeCLI 2026.08.09.217+ çalıştırmalı ve siz sahibi ya da yöneticisi olmalısınız. |
| Bir araç, bağlayıcının bir sunucuda kapalı olduğunu söylüyor | **MCP Bağlayıcısı** sayfasında o sunucunun yanındaki *Aç* düğmesine basın. |
| Bir işlem onay bağlantısı döndürdü | Bağlantıyı açın, işlemi kontrol edin ve **Onayla ve çalıştır** düğmesine basın, ardından uygulamaya onaylandığını söyleyin. |

## Bağlantılar

- TubeCLI Cloud: [cloud.tubecreate.com](https://cloud.tubecreate.com)
- TubeCLI: [tubecli.app](https://tubecli.app) · [github.com/tubecreate/tubecli](https://github.com/tubecreate/tubecli)
- Model Context Protocol: [modelcontextprotocol.io](https://modelcontextprotocol.io)

Sorularınız veya sorunlarınız mı var? [Bir issue açın](https://github.com/tubecreate/tubecli-mcp/issues).
