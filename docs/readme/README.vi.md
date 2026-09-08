<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Một ứng dụng desktop để tạo hàng loạt ảnh &amp; video trên mọi nền tảng AI lớn — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI và ChatGPT GPT Image 2.</b></p>

<p align="center">
  <a href="../../README.md">English</a> ·
  <b>Tiếng Việt</b> ·
  <a href="README.zh.md">简体中文</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.pt.md">Português</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.hi.md">हिन्दी</a> ·
  <a href="README.bn.md">বাংলা</a> ·
  <a href="README.th.md">ไทย</a> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.ur.md">اردو</a> ·
  <a href="README.ar.md">العربية</a> ·
  <a href="README.de.md">Deutsch</a> ·
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

![G-Labs Studio](../screenshots/01-image.png)

---

## Cài đặt

Tải bản mới nhất từ **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**:

| Nền tảng | Tệp |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-v<version>-win.exe` — chạy trình cài đặt (admin/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-v<version>-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-v<version>-mac-intel.dmg` |

**Lần mở đầu tiên trên macOS** — ứng dụng chưa được Apple ký nên macOS sẽ cách ly nó. Mở lần đầu bằng **chuột phải → Open**, hoặc gỡ cờ cách ly từ Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**Bạn cần một tài khoản G-Labs.** Mở ứng dụng, đăng nhập bằng Google và chọn gói. Các gói (**FREE / PLUS / MAX**) mở khóa những công cụ và mô hình khác nhau; bạn có thể mua ngay trong ứng dụng (QR ngân hàng, PayPal hoặc USDT). Một tài khoản chỉ chạy trên **một máy tại một thời điểm** — đăng nhập ở nơi khác sẽ đăng xuất máy trước đó. Huy hiệu ở góc dưới bên trái thanh bên hiển thị hạng hiện tại của bạn.

Ứng dụng **tự cập nhật**: nó kiểm tra GitHub Releases khi khởi động và có thể tải rồi cài đặt phiên bản mới ngay trong ứng dụng.

---

## Lần chạy đầu tiên

1. **Mở ứng dụng và đăng nhập bằng Google.** Huy hiệu hạng (góc dưới bên trái) xác nhận gói của bạn.
2. **Kết nối các tài khoản cho những công cụ bạn sẽ dùng** (Settings → tab tài khoản tương ứng):
   - Tài khoản **Google** → Flow Image / Flow Video
   - Tài khoản **ChatGPT** → GPT Image 2
   - Tài khoản **Meta** → Meta Media
   - **Grok** → chạy qua tab `grok.com` đã đăng nhập của bạn thông qua tiện ích trình duyệt đồng hành (Auth Helper) — không cần kho tài khoản
   Mỗi tab tài khoản hiển thị **"Active: N accounts"** trên thanh tiêu đề để bạn biết có bao nhiêu tài khoản dùng được.
3. **Chọn một trang từ thanh bên trái** và bắt đầu tạo. Mọi trang tạo đều theo cùng một nhịp: gõ hoặc nhập prompt ở bên trái, chúng rơi vào một **bảng** ở bên phải, rồi nhấn **Run**.

Mỗi tiêu đề trang mang một **thanh trạng thái** trực tiếp — *Running · Queued · Done · Failed · Accounts* — để bạn thấy toàn cảnh lô công việc trong nháy mắt. Nhấp **Queued** để mở trình quản lý hàng đợi, nhấp **Accounts** để nhảy tới cài đặt tài khoản.

---

## Tính năng

- **Mọi trình tạo lớn, trong một ứng dụng** — Google Flow (ảnh + video), Grok Imagine, Meta AI (vibes.ai) và OpenAI GPT Image 2, mỗi cái trên trang riêng với các mô hình và tỷ lệ mà nhà cung cấp đó hỗ trợ.
- **Được thiết kế để làm hàng loạt** — dán một danh sách prompt (mỗi dòng một prompt) hoặc nhập tệp `.txt`/Excel; mỗi prompt thành một dòng. Ảnh tham chiếu tự khớp theo tên tệp. Chạy cả danh sách với số luồng đồng thời bạn chọn.
- **Thêm trước, chạy khi sẵn sàng** — các dòng vào hàng đợi; **Run / Pause / Stop** tách riêng. Không có gì khởi chạy cho tới khi bạn ra lệnh, và trình quản lý hàng đợi cho phép bạn sắp xếp lại và kiểm tra.
- **Kho nhân vật** — lưu một nhân vật một lần (ảnh tham chiếu + giọng riêng + ghi chú) và thả vào bất kỳ prompt nào bằng `@name`; video giữ nguyên diện mạo và giọng của nhân vật đó.
- **Workflow (đồ thị node)** — nối các node thành một pipeline: prompt → ảnh → video → trích khung hình cuối → video kế tiếp, cùng một node **Merge Video** ghép hai clip với cắt xén và chuyển cảnh (crossfade, wipe, slide, dissolve…). Các node lô lặp toàn bộ chuỗi theo từng prompt hoặc từng ảnh.
- **Webhook API** — một máy chủ REST cục bộ để script và tác nhân AI có thể gửi các tác vụ image/video/Grok/Meta/OpenAI và truy vấn kết quả.
- **Image Upscaler** và một **Video Editor** (cắt, ghép, trình chiếu) để hoàn thiện.
- **Bền bỉ** — kết quả được kiểm tra và tự lưu; phiên làm việc được khôi phục; các dòng thất bại thử lại.
- **Giao diện Sáng / Tối**, UI theo hạng, và **15 ngôn ngữ**.

---

## Các trang

### 🖼 Flow Image — tạo ảnh Google Flow

![Flow Image](../screenshots/01-image.png)

Tạo ảnh hàng loạt với **Nano Banana Pro / 2 / Lite**. Chọn mô hình, tỷ lệ khung hình và độ phân giải (**1K / 2K / 4K** — 2K/4K dùng bộ nâng cấp của mô hình), đặt số dòng chạy cùng lúc và độ trễ giữa chúng. Dán prompt (hoặc nhập tệp), đính kèm ảnh tham chiếu cho từng dòng (kéo một thư mục và chúng tự khớp theo tên tệp), và dùng `@name` để kéo nhân vật vào. **Run** gửi cả danh sách vào hàng đợi.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Ba tab: **Text / Frames → Video** (một prompt văn bản, hoặc khung đầu/cuối), **Image / Video ingredients → Video** (ảnh tham chiếu hoặc video tham chiếu) và **Scene stitch → Video**. Mô hình: **Veo 3.1 Fast / Lite / Quality** và **Omni Flash**. Chọn tỷ lệ khung hình, nâng cấp (720p / 1080p / 4K) và seed. Di chuột lên **?** trên thanh tab để có lời giải thích dễ hiểu về frames so với ingredients.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Text-to-image, image-to-image, text-to-video và image-to-video qua Grok Imagine (tab `grok.com` đã đăng nhập của bạn thông qua tiện ích Auth Helper). Ảnh có **8 tỷ lệ khung hình** (gồm 4:3, 21:9, 5:2); video tạo ở **480p / 720p / 1080p**. Image-to-video có hai chế độ: **First frame** (ảnh mở đầu clip) và **Reference** (tối đa 14 ảnh dẫn hướng).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Tạo ảnh và video qua Meta AI. Các chế độ: text-to-image, image-to-image (thành phần Character / Scene / Style), text-to-video và image-to-video (khung đầu / cuối).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

Tạo với OpenAI **GPT Image 2** bằng tài khoản ChatGPT của bạn, với tối đa 5 ảnh tham chiếu. Chọn tỷ lệ (10 tùy chọn gồm 21:9, 4:5 và **custom** — nơi bạn viết tỷ lệ ngay trong prompt), chất lượng, chế độ prompt, mức độ suy luận và tìm kiếm web.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Nâng cấp một thư mục ảnh ngay tại máy — chọn đích và để nó xử lý hàng đợi, với tiến độ và trạng thái theo từng dòng (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

Xây dựng một kho nhân vật tái sử dụng: một ảnh tham chiếu, một giọng tùy chỉnh không bắt buộc, và ghi chú về diện mạo/tính cách. Gắn thẻ chúng bằng `@name` trong bất kỳ prompt Flow nào và bản tạo sẽ giữ nguyên danh tính đó.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Một canvas node trực quan. Nhấp chuột phải vào socket của một node và menu chỉ đề xuất những node phù hợp — chọn một cái và nó tự nối dây. Nối chuỗi prompt → generate → video → **Extract Frame** → video kế tiếp, và dùng **Merge Video** để ghép hai clip (cắt xén mỗi đầu, chọn chuyển cảnh). Lưu/nạp cả đồ thị dưới dạng tệp `.json`; **Run Flow** thực thi nó từ đầu đến cuối.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Biến ứng dụng thành máy chủ tự động hóa cục bộ. Khởi chạy nó, sao chép API key, và POST các tác vụ tới `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` hoặc `/api/openai/generate`, rồi truy vấn `/api/status/<id>`. Trang liệt kê mọi mô hình và các tỷ lệ khung hình được hỗ trợ. Lược đồ đầy đủ: [`docs/WEBHOOK_INTEGRATION.vi.md`](../WEBHOOK_INTEGRATION.vi.md).

---

## Nơi lưu dữ liệu

| Gì | macOS | Windows |
|---|---|---|
| Đầu ra (ảnh / video) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Cài đặt, phiên, tài khoản | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Cài đặt, danh sách prompt, phiên làm việc, kho nhân vật và danh sách tài khoản của bạn được lưu và khôi phục vào lần tiếp theo bạn mở ứng dụng.

---

## Khắc phục sự cố

**Mọi thứ bị khóa / màn hình mua hàng cứ mở ra** — gói của bạn đã hết hạn, hoặc tài khoản đã đăng nhập trên một máy khác. Kiểm tra huy hiệu hạng (góc dưới bên trái) và gia hạn.

**Một bản tạo Grok không làm gì cả** — Grok chạy qua tab `grok.com` của bạn. Cài đặt/bật tiện ích trình duyệt **Auth Helper** (Settings → Grok) và đảm bảo bạn đã đăng nhập grok.com.

**"Active: 0 accounts" trên một trang** — thêm hoặc bật lại một tài khoản trong tab tài khoản của trang đó (Settings), hoặc token của nó đã hết hạn — nhấn **Refresh all**.

**macOS báo ứng dụng bị hỏng / không mở được** — nó chưa được Apple ký. Chuột phải → **Open** ở lần đầu, hoặc chạy `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Một bản cập nhật không cài được** — tải bản mới nhất thủ công từ [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
