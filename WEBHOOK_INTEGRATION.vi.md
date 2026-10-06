# G-Labs Automation - Hướng dẫn tích hợp Webhook API

> Đối tượng đọc: lập trình viên, người tích hợp kỹ thuật, và AI agent.
> Mục tiêu: cung cấp đầy đủ mọi thứ cần để tích hợp đúng Webhook REST API nội bộ -
> danh sách endpoint, xác thực, schema request/response, model, tham số, xử lý lỗi,
> và quy trình bất đồng bộ (gửi yêu cầu → hỏi trạng thái → tải kết quả).

Tài liệu này mô tả API do tab **Webhook** của ứng dụng desktop G-Labs Automation
(v5.0.8+) cung cấp. Nó cho phép các công cụ bên ngoài (n8n, Make.com, script tự
viết, AI agent) điều khiển việc tạo ảnh (Flow, Google Pics) / video (Veo, Omni Flash, Google Vids) / Grok /
Meta AI / OpenAI - và nâng cấp ảnh cục bộ - qua REST API đơn giản.

---

## 1. Tổng quan & khái niệm chính

- **Yêu cầu gói MAX.** Máy chủ Webhook chỉ bật được với license **MAX**.
- **Địa chỉ bind (mặc định loopback).** API chạy ở `http://<host>:<port>`. Mặc định
  `host` là `127.0.0.1` (chỉ máy này). Bạn đổi được trong tab Webhook: đặt `0.0.0.0`
  (mọi interface) hoặc một **IP LAN** cụ thể để máy khác trong mạng truy cập được.
  **Đừng dùng `127.0.0.0`** - đó là địa chỉ *network* của loopback, không client nào
  connect tới được. Muốn truy cập qua internet thì vẫn phải tự dựng tunnel/reverse
  proxy. Cho truy cập LAN, nhớ mở cổng trên tường lửa hệ điều hành.
- **Port mặc định:** `8765` (đổi được trong tab Webhook).
- **Bạn phải bật máy chủ.** Mở app → tab **Webhook** → **Start**. Tab này cũng hiển
  thị **API key**, cho đổi host / port / tạo lại key, và có tùy chọn **Tự động bật**
  máy chủ khi mở app.
- **Bất đồng bộ theo thiết kế.** Việc tạo nội dung tốn thời gian, nên API theo mô
  hình **gửi → hỏi trạng thái → tải về**:
  1. `POST` yêu cầu tạo → nhận `task_id` ngay lập tức (HTTP `202`).
  2. `GET /api/status/{task_id}` lặp lại cho đến khi `status` là `completed` hoặc `failed`.
  3. Khi `completed`, tải file từ các URL trong `results`.
- **Đồng thời.** Máy chủ nhận nhiều request cùng lúc. Tối đa **10 task được bóc
  tách song song**; còn *chạy tạo* được bao nhiêu cái một lúc thì tùy endpoint:
  Ảnh/Video/Meta/OpenAI co giãn theo số tài khoản (khoảng 5 mỗi tài khoản), Grok
  trần **10**, Google Vids và Google Pics nhận số việc mỗi tài khoản do máy chủ cấp trên từng tài
  khoản Google,
  riêng Upscale chạy **lần lượt từng cái** (chỉ có một GPU - xem §5.6).
- **Tạo nội dung dùng tài khoản đã đăng nhập trong app.** Ảnh/Video dùng tài khoản
  Google (Flow/Veo) cấu hình trong app; Grok dùng phiên Super Grok đã kết nối;
  **Meta AI** dùng tài khoản Meta (vibes.ai) đã đăng nhập; **OpenAI (GPT Image 2)**
  dùng tài khoản ChatGPT/OpenAI đã đăng nhập; **Google Vids** (`omni_vids`) và **Google Pics**
  (`nano_pics`) dùng tài khoản Google ở Cài đặt → Tài khoản Google. Nếu không có tài khoản hợp lệ, task sẽ
  thất bại (xem bảng lỗi). App phải đang chạy với các tài khoản đó đã đăng nhập & đang bật.

---

## 2. Xác thực

Tất cả endpoint **trừ** `GET /api/health` và `GET /api/files/{filename}` đều yêu cầu
API key, gửi qua HTTP header:

```
X-API-Key: <api-key-của-bạn>
```

- Key do app sinh ra (token URL-safe 32 byte) và hiển thị trong tab **Webhook**.
  Bạn có thể tạo lại key ở đó.
- Thiếu/sai key → `401 {"error": "Invalid or missing API key"}`.

CORS đã bật (`Access-Control-Allow-Origin: *`) và có xử lý preflight `OPTIONS`, nên
client trên trình duyệt cũng dùng được.

---

## 3. Danh sách Endpoint

| Method | Path | Auth | Mục đích |
|--------|------|:----:|----------|
| `GET`  | `/api/health` | ❌ | Tình trạng máy chủ / uptime / số task trong hàng đợi |
| `POST` | `/api/image/generate` | ✅ | Đưa task tạo **ảnh** vào hàng đợi |
| `POST` | `/api/video/generate` | ✅ | Đưa task tạo **video** vào hàng đợi |
| `POST` | `/api/grok/generate`  | ✅ | Đưa task **Grok** (ảnh/video) vào hàng đợi |
| `POST` | `/api/meta/generate`  | ✅ | Đưa task **Meta AI** (ảnh/video) vào hàng đợi |
| `POST` | `/api/openai/generate` | ✅ | Đưa task **OpenAI GPT Image 2** vào hàng đợi |
| `POST` | `/api/upscale/generate` | ✅ | Nâng cấp ảnh bằng engine **Real-ESRGAN chạy local** |
| `GET`  | `/api/status/{task_id}` | ✅ | Hỏi trạng thái task; trả kết quả hoặc lỗi |
| `GET`  | `/api/result/{task_id}` | ✅ | Lấy kết quả (chỉ khi đã `completed`) |
| `GET`  | `/api/files/{filename}` | ❌ | Tải file kết quả đã tạo |
| `GET`  | `/api/tasks` | ✅ | Liệt kê 50 task gần nhất |
| `POST` | `/api/stop` | ✅ | **Dừng** mọi task đang chờ / đang chạy - hoặc một task: `/api/stop/{task_id}` hay body `{"task_id": "..."}`. Chỉ cần API key (không kiểm tra gói MAX), nên client luôn huỷ được. |

Dấu `/` ở cuối được chấp nhận (vd `/api/health/`).

**Dừng việc đang làm.** Client đổi ý (tạo lại, prompt sai, người dùng bấm huỷ) nên gọi
`POST /api/stop` thay vì để hàng đợi chạy tiếp: mọi task được nhắm tới lỗi ngay với
`error_code 499` / `STOPPED_BY_CLIENT`, việc đang xếp hàng không bao giờ bắt đầu, provider đang
chạy được yêu cầu dừng, và kết quả về sau của một request đã gửi tới provider bị bỏ (request đó
vẫn bị tính phí - một cuộc gọi HTTP không huỷ ngang được).

---

## 4. Quy trình bất đồng bộ (từng bước)

### Bước 1 - Gửi yêu cầu

`POST` tới một trong các endpoint generate (image / video / grok / meta / openai)
kèm JSON body (xem schema ở §5). Phản hồi là **HTTP 202**:

```json
{
  "task_id": "abc12345",
  "status": "pending",
  "message": "Image task queued for processing",
  "poll_url": "/api/status/abc12345"
}
```

> `task_id` là chuỗi hex 8 ký tự. Giữ lại để hỏi trạng thái và lấy kết quả.

### Bước 2 - Hỏi trạng thái

`GET /api/status/{task_id}` (kèm header `X-API-Key`). Các giá trị `status` có thể là:
`pending` → `running` → `completed` | `failed`.

**Đang chạy:**
```json
{ "task_id": "abc12345", "type": "image", "status": "running", "prompt": "a cat ...", "created_at": 1707782400.0 }
```

**Hoàn thành:**
```json
{
  "task_id": "abc12345",
  "type": "image",
  "status": "completed",
  "prompt": "a cat ...",
  "created_at": 1707782400.0,
  "results": ["http://127.0.0.1:8765/api/files/image_001.png"],
  "completed_at": 1707782460.0
}
```

**Thất bại:**
```json
{
  "task_id": "abc12345",
  "type": "image",
  "status": "failed",
  "prompt": "a cat ...",
  "created_at": 1707782400.0,
  "error_code": 429,
  "error": "Đã hết giới hạn tạo ảnh trong ngày (user@gmail.com)",
  "error_detail": "429: Đã hết giới hạn tạo ảnh trong ngày (user@gmail.com)"
}
```

> Khoảng thời gian hỏi đề xuất: mỗi 3-5 giây. Ảnh thường xong trong vài giây tới vài
> phút; video có thể mất vài phút (dịch vụ phía trên có thể xếp hàng). Máy chủ có cơ
> chế watchdog để báo thất bại cho task bị treo quá lâu không có kết quả.

### Bước 3 - Tải kết quả

`results` là mảng URL dạng `http://<host>:<port>/api/files/<tên-đã-url-encode>`.
`<host>` khớp với địa chỉ đã bind của máy chủ, nên client vào bằng IP LAN sẽ nhận link
tải trên đúng IP đó (khi bind `0.0.0.0`, máy chủ tự quảng bá IP LAN chính). `GET` từng
URL (không cần API key) để tải dữ liệu thô. `Content-Type` được đặt theo phần mở rộng
file (`image/png`, `image/jpeg`, `video/mp4`, …). File lưu nội bộ trên máy đang chạy app.

**Trả về bao nhiêu file (và ở độ phân giải nào):**

- **Ảnh, không `upscale`** → 1 file (ảnh gốc).
- **Google Pics** (`nano_pics`) → tối đa `keep` file (mặc định 1; `keep: 0` = mọi ảnh của lượt,
  3-9).
- **Ảnh có `upscale`** → một file **cho mỗi độ phân giải upscale yêu cầu**, theo thứ
  tự tăng dần - vd `["2K"]` → `[2K]`, `["2K","4K"]` → `[2K, 4K]`. Ảnh gốc
  (không upscale) **không** được kèm khi đã yêu cầu `upscale`.
- **Video** → một file **cho mỗi độ phân giải tạo được** - vd `["720p","1080p"]` →
  tối đa 2 file.
- **Grok** → luôn đúng 1 file.
- **Meta AI** → `count` file (1-4): `count` ảnh (một lô) hoặc `count` clip video.
- **OpenAI (GPT Image 2)** → luôn đúng 1 file.
- **Google Vids** (`omni_vids`) → đúng 1 file ở độ phân giải đã yêu cầu; task `upscale` của
  `omni_vids` → 1 file (clip 1080p).
- **Upscale** → luôn đúng 1 file (một ảnh vào, một ảnh ra).

(Nên `len(results)` và thứ tự khớp với các độ phân giải bạn yêu cầu.)

---

## 5. Schema body của request

Mọi body đều là JSON. `prompt` là **bắt buộc** cho mọi endpoint tạo nội dung; prompt
rỗng/thiếu sẽ làm task thất bại với lỗi `Missing required field: prompt`. Ngoại lệ duy
nhất là `/api/upscale/generate` (§5.6) - nhận ảnh, không có prompt.

**Trần kích thước body: 50 MB** cho mọi endpoint. Base64 làm dữ liệu nhị phân phình
~4/3, nên một request chứa được khoảng 37 MB dữ liệu ảnh thô. Vượt trần thì chính lệnh
`POST` trả `413` - task không được tạo. Cách hay vấp nhất là nhét nhiều ảnh tham chiếu
lớn vào cùng một request.

### 5.1 Ảnh - `POST /api/image/generate`

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | - | Mô tả ảnh. |
| `model` | string | ❌ | `nano_banana_2` | Một trong `nano_banana_pro`, `nano_banana_2`, `nano_banana_2_lite`, `nano_pics`. Không hợp lệ → `nano_banana_2`. **`nano_pics`** = Google Pics, có trường riêng (`mode`, `keep`, `remove_logo`) và kiểm tra chặt - xem ghi chú Google Pics bên dưới. |
| `aspect_ratio` | string | ❌ | `1:1` | Một trong `1:1`, `3:4`, `4:3`, `9:16`, `16:9`. Không hợp lệ → `1:1`. |
| `reference_images` | array | ❌ | `[]` | Tối đa **10** ảnh base64 (xem §6). Mỗi ảnh có thể kèm `name` để gắn theo `@tên` trong prompt (§6.1). |
| `upscale` | array | ❌ | `[]` | Bất kỳ `"2K"`, `"4K"`. **4K cần tài khoản ULTRA** và model hỗ trợ upscale. Giá trị sai bị bỏ. |

```json
{
  "prompt": "a modern minimalist house, golden hour",
  "model": "nano_banana_pro",
  "aspect_ratio": "16:9",
  "reference_images": ["data:image/png;base64,iVBORw0KGgo..."],
  "upscale": ["4K"]
}
```

> Nếu yêu cầu `upscale` mà không tạo được độ phân giải đó (vd 4K hết quota), task sẽ
> báo **failed** kèm lý do - **không** âm thầm trả về ảnh gốc độ phân giải thấp hơn.

> **Google Pics (`model: "nano_pics"`)** - trình tạo ảnh của Google (docs.google.com/images), chạy
> bằng **tài khoản Google** ở Cài đặt → Tài khoản Google (cùng tài khoản với Google Vids; gói
> PLUS/MAX). Cùng endpoint, có trường và quy tắc riêng:
> - `mode` (không phân biệt hoa thường, không bắt buộc): `text_to_image` hoặc `image_to_image`
>   (bí danh `t2i` / `i2i`). Bỏ trống → `image_to_image` nếu có gửi `reference_images`, ngược lại
>   `text_to_image`. Giá trị khác → `400 INVALID_MODE`; `image_to_image` mà không có ảnh →
>   `400 MISSING_REFERENCE`; `text_to_image` bỏ qua mọi ảnh gửi kèm.
> - `reference_images`: **1-14** ảnh (base64 hoặc `path`, §6), theo vị trí - Google Pics **không
>   có** gắn `@tag`, `name` / `category` bị bỏ qua. Vượt giới hạn máy chủ (14) →
>   `400 TOO_MANY_REFERENCES` (không bao giờ lặng lẽ cắt bớt).
> - `aspect_ratio`: một giá trị trong danh sách máy chủ - hiện là `16:9, 9:16, 1:1, 4:3, 3:4, 3:2,
>   2:3, 5:4, 4:5, 21:9` (bảng model ở tab Webhook hiện danh sách đang dùng). Mặc định `1:1`. Giá
>   trị khác → `400 INVALID_ASPECT_RATIO` (không tự đổi về mặc định như các model Flow).
> - `keep`: số ảnh của lượt cần trả về. Google trả **3-9 ảnh mỗi lượt**; `keep` là số nguyên, một
>   trong `1`, `2`, `3`, `4` hoặc `0` (= mọi ảnh của lượt). Bỏ trống hoặc `null` → `1`. Giá trị
>   khác (kể cả `true`, `2.7` hay chuỗi `"2"`) → `400 INVALID_KEEP`.
> - `remove_logo`: `true` xoá logo ✦ Gemini khỏi mọi ảnh (khôi phục điểm ảnh sạch, không làm mờ);
>   `false` giữ nguyên ảnh như Google tạo. **Không gửi** (hoặc `null`) → theo nút **"Hiển thị logo
>   Gemini"** của trang Google Pics (mặc định nút tắt = xoá). Không phải boolean → `400 INVALID_FIELD`.
> - Không hỗ trợ `upscale` (bị bỏ qua).
> - **Hạn mức:** một task = **một lượt = 1 đơn vị** hạn mức Pics của tài khoản, bất kể ra bao nhiêu
>   ảnh. Hạn mức đọc thật từ Google (còn / tổng), tách riêng với số giây của Vids.
> - **Tài khoản:** chỉ dùng tài khoản đang **BẬT** và đang tích ô **Ảnh** ở Cài đặt → Tài khoản
>   Google, còn ít nhất 1 lượt Pics (tài khoản chưa từng đọc hạn mức vẫn được thử - việc sẽ đọc
>   trước khi tạo). Mỗi tài khoản nhận tối đa số việc đồng thời máy chủ cấp. Xoay vòng round-robin,
>   lỗi auth / hạn mức / giới hạn tốc độ / máy chủ, hoặc tài khoản không dùng được Google Pics thì
>   chuyển sang tài khoản kế; cookie chết được làm mới từ profile trước. Cookie không làm mới được
>   thì tài khoản bị **TẮT** (cả cho Vids). Tài khoản cookie vẫn sống nhưng không có Google Pics (bị
>   từ chối ngay cả khi vừa làm mới cookie) chỉ bị **bỏ qua** - không bao giờ bị tắt. Hết lượt Pics
>   cũng **không** tắt tài khoản: khi bật *Tự động tắt tài khoản bị hết giới hạn* chỉ ô **Ảnh** bị
>   bỏ tích; qua mốc reset hạn mức Pics thì tài khoản được thử lại và ô được tích lại - Google Vids
>   vẫn dùng tiếp suốt thời gian đó. Khi mọi tài khoản dùng được đều bận, task trở về `pending` và
>   **chờ** slot trống (tối đa 15 phút), kể cả sau khi đã chuyển tài khoản.
> - **Kết quả:** `results` = các ảnh được giữ (PNG), tối đa `keep` file (ít hơn nếu có ảnh tải
>   lỗi). Task hoàn thành có thêm `meta`: `mode` (`t2i` / `i2i`), `aspect_ratio`, `images` (số file
>   trả về), `logo_removed` (số ảnh thực sự đã được xoá logo Gemini - `0` khi `remove_logo: false`),
>   `account` (email tài khoản Google) và `partial: true` khi lượt bị dừng
>   / lỗi sau khi đã lưu được một số ảnh.
> - Prompt bị từ chối → `400 CONTENT_POLICY` (không tốn hạn mức, không thử lại trên tài khoản khác).

Ví dụ Google Pics - ảnh sang ảnh, 16:9, giữ 2 ảnh:

```json
{
  "prompt": "the same girl reading in a cozy cafe",
  "model": "nano_pics",
  "aspect_ratio": "16:9",
  "keep": 2,
  "reference_images": ["data:image/png;base64,..."]
}
```

### 5.2 Video - `POST /api/video/generate`

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | - | Mô tả chuyển động / khung cảnh. Chỉ không bắt buộc với request `upscale` của `omni_vids`. |
| `model` | string | ✅ | - | Một trong `veo_31_fast`, `veo_31_lite`, `veo_31_quality`, `veo_31_lite_relaxed`, `omni_flash`, `omni_vids`. Thiếu → `400 MISSING_MODEL`; tên Veo lạ → `veo_31_fast`. **`omni_vids`** = Google Vids (xem ghi chú Google Vids bên dưới). `veo_31_lite_relaxed` cần tài khoản **ULTRA**. **`omni_flash`**: xem ghi chú `mode`. |
| `aspect_ratio` | string | ❌ | `16:9` | `16:9` hoặc `9:16`. |
| `mode` | string | ❌ | `text_to_video` | `text_to_video` (0 ảnh) · `start_image` (1 ảnh) · `start_end_image` (2 ảnh: khung đầu + khung cuối) · `components` (Veo tối đa 3 ảnh, Omni Flash tối đa 7; hỗ trợ `voice` và `reference_video`). **Mọi mode dùng được cho cả Veo lẫn Omni Flash** (`start_end_image` của Omni Flash cần server config có mapping `i2v_end` - thiếu sẽ bị từ chối kèm lý do rõ). |
| `reference_images` | array | ❌ | `[]` | Tối đa **3** ảnh base64 (Veo); **Omni Flash `components` tối đa 7** (có `reference_video` thì tối đa **5**). **Bắt buộc khi `mode != text_to_video`** - riêng `components` có thể thay bằng `reference_video`. Mỗi ảnh có thể kèm `name` để gắn theo `@tên` trong prompt - Veo (§6.1). |
| `reference_video` | string/object | ❌ | - | **Chỉ Omni Flash + mode `components`** - luồng **edit video**: clip (≤ **10s**) được dựng lại theo prompt, có thể kèm tối đa 5 ảnh thành phần. Nhận chuỗi base64/data-URI (`data:video/mp4;base64,...`) hoặc `{"path": "...", "name": "..."}` (file có sẵn trên máy chạy app). Luôn xuất **720p** (không dùng cùng `"360p"`). Clip dài quá 10s bị từ chối - cắt trước khi gửi. |
| `resolution` | array | ❌ | `["720p"]` | Bất kỳ `"360p"`, `"720p"`, `"1080p"`, `"4K"`. **`360p` chỉ có ở Omni Flash** (server config quyết định) - bản gốc tạo ở 360p, rẻ credit hơn; **nguồn 360p chỉ upscale được lên 720p** nên tổ hợp hợp lệ là `["360p"]` hoặc `["360p", "720p"]` (kèm `1080p`/`4K` sẽ bị từ chối). `1080p`/`4K` tạo bằng upscale từ nguồn 720p; **chỉ `4K` cần tài khoản ULTRA**. Giá trị sai → `720p`. Mỗi độ phân giải tạo ra một file. |
| `voice` | string | ❌ | `""` | Tên giọng (chữ thường). Chỉ dùng ở mode `components`. |
| `video_length` | int | ❌ | (mặc định model) | Độ dài clip (giây). Veo: `4`/`6`/`8`; Omni Flash: `4`/`6`/`8`/`10`. Giá trị không hỗ trợ → dùng mặc định (8s). **Veo `4`/`6` cần tài khoản ULTRA** (Omni Flash không cần). Luồng edit (`reference_video`) bỏ qua trường này - độ dài theo clip gốc. |

```json
{
  "prompt": "water flowing over rocks, cinematic",
  "model": "veo_31_fast",
  "aspect_ratio": "16:9",
  "mode": "start_image",
  "reference_images": ["data:image/png;base64,iVBORw0KGgo..."],
  "resolution": ["720p", "1080p"],
  "video_length": 8
}
```

> **Thứ tự ảnh tham chiếu:** với `start_end_image`, `reference_images[0]` là khung
> đầu, `reference_images[1]` là khung cuối. Với `start_image`, chỉ dùng
> `reference_images[0]`.
>
> **`mode` không được kiểm tra chặt** (Veo / Omni Flash): mode không hợp lệ sẽ hoạt động như
> `text_to_video` (bỏ qua ảnh tham chiếu). Chỉ `components` đọc trường `voice`
> (Veo tối đa 3 ảnh tham chiếu, Omni Flash tối đa 7). **Riêng `omni_vids`** kiểm tra chặt
> `mode`, `resolution`, `video_length`, `aspect_ratio` và trả `400` kèm tên lỗi (xem ghi chú Google Vids).
>
> **Dùng được cả Veo lẫn Omni Flash.** Omni Flash (`model: "omni_flash"`) hỗ trợ
> đủ `text_to_video`, `start_image`, `start_end_image`, `components` - và riêng nó
> có thêm: mốc `video_length` **10s**, độ phân giải **360p**, và luồng **edit video**
> (`reference_video` trong mode `components`). Nó không cần tài khoản ULTRA.
>
> `resolution` có thể liệt kê nhiều giá trị; mỗi giá trị được tạo nếu hạng tài khoản
> cho phép.

Ví dụ Omni Flash - khung đầu + khung cuối, bản nháp 360p:

```json
{
  "prompt": "animate",
  "model": "omni_flash",
  "mode": "start_end_image",
  "reference_images": ["data:image/png;base64,...", "data:image/png;base64,..."],
  "resolution": ["360p"]
}
```

Ví dụ Omni Flash - edit video (dựng lại clip ≤10s theo prompt):

```json
{
  "prompt": "make it snow heavily",
  "model": "omni_flash",
  "mode": "components",
  "reference_video": "data:video/mp4;base64,...",
  "reference_images": ["data:image/png;base64,..."]
}
```

> **Google Vids (`model: "omni_vids"`)** chạy bằng tài khoản Google thêm ở Cài đặt → Tài khoản Google
> (gói PLUS/MAX). Cùng dạng request với Veo, với các quy tắc:
> - `mode` (không phân biệt hoa thường): `text_to_video` (không ảnh, mặc định), `start_image`
>   (1 ảnh = khung hình đầu; ảnh thừa bị bỏ qua), `components` (1-3 ảnh làm nguyên liệu) hoặc
>   `upscale` (xem dưới). Nhận cả tên tắt `t2v` / `i2v` / `r2v`. Giá trị khác - kể cả
>   `start_end_image` → `400 INVALID_MODE`.
> - `resolution`: **một** giá trị trong danh sách máy chủ (hiện `720p` / `1080p`), chuỗi hoặc list một
>   phần tử - tạo thẳng, không qua bước upscale. Bỏ trống → giá trị đầu tiên của danh sách máy chủ.
>   Hai giá trị, `360p`, `4K` hay giá trị lạ → `400 INVALID_RESOLUTION`.
> - `video_length`: số nguyên **3-10** giây (mặc định 5); 1 giây video trừ 1 giây hạn mức tài khoản.
>   Ngoài khoảng → `400 INVALID_VIDEO_LENGTH`.
> - `orientation` (`landscape` / `portrait`) hoặc `aspect_ratio` (`16:9` / `9:16`); gửi cả hai thì
>   `orientation` được ưu tiên. Mặc định `16:9`. Giá trị khác → `400 INVALID_ASPECT_RATIO`.
> - `reference_video` → `400 INVALID_FIELD`. `voice` và `category` bị bỏ qua.
> - Ở mode `components`, đặt `"name"` cho từng ảnh và viết `@tên` trong prompt để đặt ảnh đúng vị trí
>   (`"@luna gặp @grandpa"`); ảnh không được @ vẫn được gửi kèm ở đầu. **Nhân vật trong thư viện**
>   (Cài đặt → Nhân vật) gọi được cùng cách - `@Anna` thêm ảnh của nhân vật làm nguyên liệu
>   (Google Vids chỉ đồng nhất hình ảnh - không đồng nhất giọng nói). Quy tắc: tính năng Nhân vật
>   phải đang bật; tag phải là **đúng tên đầy đủ** của nhân vật (không phân biệt hoa thường); nhân
>   vật chỉ được thêm khi request còn dưới 3 ảnh; ảnh **bạn gửi** có cùng `name` được ưu tiên hơn
>   nhân vật. Tổng tối đa 3 nguyên liệu; không có nguyên liệu nào → `400 MISSING_REFERENCE`.
> - **Tài khoản:** chỉ dùng tài khoản đang **BẬT** ở Cài đặt → Tài khoản Google (và đang tích ô Video) và còn ít
>   nhất `video_length` giây; mỗi tài khoản nhận tối đa số việc đồng thời máy chủ cấp, và số giây
>   được giữ chỗ trong lúc việc chạy. Xoay vòng round-robin, lỗi auth / hạn mức / giới hạn tốc độ /
>   máy chủ thì chuyển sang tài khoản kế; cookie chết được làm mới từ profile trước. Tài khoản không
>   làm mới được cookie bị **TẮT** trong app; tài khoản hết giây chỉ bị bỏ tích ô **Video** (khi bật
>   *Tự động tắt tài khoản bị hết giới hạn*) - Google Pics vẫn dùng tiếp (giống trang Vids). Khi mọi tài
>   khoản dùng được đều bận, task giữ trạng thái `pending` và **chờ** slot trống (tối đa 15 phút)
>   thay vì lỗi.
> - **Kết quả:** task hoàn thành có thêm `meta` trong `GET /api/status/{task_id}` và
>   `GET /api/result/{task_id}`:
>   `mode` (`t2v` / `i2v` / `r2v` / `upscale`), `resolution` (`720p` / `1080p`), `orientation`
>   (`landscape` / `portrait`), `duration` (giây), `account` (email tài khoản Google Vids đã tạo
>   clip), `clip_temp_id` (id mà request upscale cần), `upscale_available` (`true` khi clip
>   còn nâng phân giải được - chưa phải 1080p) và `logo_removed` (`true` khi logo ✦ Gemini đã
>   được xoá khỏi file trả về).
> - `remove_logo` (tuỳ chọn, cả request tạo lẫn `upscale`): `true` xoá logo ✦ Gemini khỏi video
>   (720p / 1080p; bản 1080p là bản nâng cấp nên đôi khi còn vết rất mờ trên nền nhiều vân);
>   `false` giữ nguyên video như Google tạo. **Không gửi** (hoặc `null`) → theo nút **"Hiển thị
>   logo Gemini"** của trang Google Vids (mặc định nút tắt = xoá). Không phải boolean →
>   `400 INVALID_FIELD`. Video không có logo, hoặc xoá lỗi, được trả nguyên bản (`logo_removed: false`).
> - **Upscale:** `{"model": "omni_vids", "mode": "upscale", "clip_temp_id": "<meta.clip_temp_id>"}`
>   (không cần `prompt`) tạo bản 1080p của clip do **một task webhook `omni_vids` đã hoàn thành
>   trong cùng phiên chạy app** tạo ra - clip tạo ở trang Vids không dùng được. Chỉ chạy trên đúng
>   tài khoản đã tạo clip, giữ nguyên độ dài và hướng, không bao giờ chuyển sang tài khoản khác
>   (tài khoản đó đang bận thì task chờ). Kết quả là một task mới với file riêng. Id lạ →
>   `400 UNKNOWN_CLIP`, đã 1080p → `400 ALREADY_UPSCALED`, tài khoản đó đang tắt hoặc đã lỗi →
>   `409 CLIP_ACCOUNT_UNAVAILABLE`, clip đã hết hạn phía Google → `400 CLIP_GONE`.

Ví dụ Google Vids - thành phần với @tên:

```json
{
  "prompt": "@luna đi bộ trên đường thì gặp @grandpa",
  "model": "omni_vids",
  "mode": "components",
  "aspect_ratio": "16:9",
  "resolution": ["1080p"],
  "video_length": 6,
  "reference_images": [
    {"data": "data:image/png;base64,...", "name": "luna"},
    {"data": "data:image/png;base64,...", "name": "grandpa"}
  ]
}
```

Ví dụ Google Vids - nâng phân giải clip của một task đã xong:

```json
{
  "model": "omni_vids",
  "mode": "upscale",
  "clip_temp_id": "ABCD...WXYZ"
}
```

### 5.3 Grok - `POST /api/grok/generate`

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | - | Prompt. |
| `mode` | string | ❌ | `t2v` | `t2i` (văn bản→ảnh) · `i2i` (ảnh→ảnh) · `t2v` (văn bản→video) · `i2v` (ảnh→video). Mode sai → task thất bại. |
| `aspect_ratio` | string | ❌ | `9:16` | Ảnh (`t2i`/`i2i`): `9:16, 16:9, 1:1, 2:3, 3:2, 4:3, 21:9, 5:2`. Video (`t2v`/`i2v`): `9:16, 16:9, 1:1, 2:3, 3:2`. Không hợp lệ → `9:16`. |
| `reference_images` | array | ❌ | `[]` | Tối đa **5** ảnh base64. **Bắt buộc cho `i2i` và `i2v`** (≥1, không có thì task thất bại). Bị bỏ qua với `t2i` / `t2v`. |
| `video_length` | int | ❌ | `6` | `6`, `10` hoặc `15` (giây). **Chỉ mode video** (`t2v`/`i2v`). Giá trị khác → `6`. |
| `resolution` | string | ❌ | `480p` | `480p`, `720p` hoặc `1080p`. **Chỉ mode video.** Mode ảnh (`t2i`/`i2i`) luôn xuất **1K**. |
| `first_frame` | bool | ❌ | `false` | **Chỉ `i2v`.** `true` = ảnh làm khung hình đầu (1 ảnh, tỷ lệ theo ảnh); `false` = ảnh thành phần tham chiếu (nhiều ảnh). |

```json
{
  "prompt": "make it rain over the city",
  "mode": "i2v",
  "aspect_ratio": "16:9",
  "video_length": 6,
  "resolution": "720p",
  "first_frame": false,
  "reference_images": ["data:image/png;base64,iVBORw0KGgo..."]
}
```

> Grok luôn tạo **một** ảnh/video mỗi request và trả về kết quả đầu tiên. Không có
> tham số `image_generation_count`.

### 5.4 Meta AI - `POST /api/meta/generate`

Tạo nội dung trên **Meta AI (vibes.ai)** bằng tài khoản Meta đã đăng nhập. Khác với
các endpoint kia, ảnh tham chiếu được truyền qua **trường có tên** (không phải mảng
`reference_images`) - xem §6.2.

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | - | Prompt. |
| `mode` | string | ❌ | `t2i` | `t2i` (văn bản→ảnh) · `t2v` (văn bản→video) · `i2i` (ảnh→ảnh, thành phần) · `i2v` (ảnh→video). Mode sai → task thất bại. |
| `aspect_ratio` | string | ❌ | `9:16` | Một trong `9:16`, `16:9`, `1:1`. Không hợp lệ → `9:16`. |
| `resolution` | string | ❌ | `720p` | `480p` hoặc `720p`. **Chỉ mode video** (`t2v`/`i2v`). Ảnh tự suy theo site: `1:1` → 1280p, còn lại → 720p. |
| `count` | int | ❌ | `1` | Số đầu ra mỗi prompt, **1-4** (kẹp về khoảng này). Ảnh: `count` ảnh trong một lô; video: `count` clip. |
| `character_image` | base64 | i2i¹ | - | Thành phần nhân vật/chủ thể (§6.2). Cũng chấp nhận `subject_image`. |
| `scene_image` | base64 | i2i¹ | - | Thành phần bối cảnh. |
| `style_image` | base64 | i2i¹ | - | Thành phần phong cách. |
| `start_image` | base64 | i2v | - | **Bắt buộc cho `i2v`** - khung đầu. |
| `end_image` | base64 | ❌ | - | Khung cuối tùy chọn cho `i2v` (nội suy đầu→cuối). |

¹ **i2i** cần **ít nhất một** trong `character_image` / `scene_image` / `style_image`.
**i2v** cần `start_image`. Mode văn bản (`t2i` / `t2v`) bỏ qua mọi ảnh gửi kèm.

```json
{
  "prompt": "a cat astronaut floating in space",
  "mode": "t2i",
  "aspect_ratio": "1:1",
  "count": 1
}
```
```json
{
  "prompt": "same character in a forest at dawn",
  "mode": "i2i",
  "aspect_ratio": "16:9",
  "character_image": "data:image/png;base64,iVBORw0KGgo...",
  "scene_image": "data:image/jpeg;base64,/9j/4AAQ..."
}
```
```json
{
  "prompt": "slow pan across the scene",
  "mode": "i2v",
  "aspect_ratio": "16:9",
  "resolution": "720p",
  "start_image": "data:image/png;base64,iVBORw0KGgo...",
  "end_image": "data:image/png;base64,iVBORw0KGgo..."
}
```

> Meta AI **không có `@tag`** gắn theo tên (cái đó chỉ có ở Flow/Veo); thành phần
> được gắn bằng các trường có tên ở trên.

### 5.5 OpenAI (GPT Image 2) - `POST /api/openai/generate`

Tạo ảnh trên **OpenAI GPT Image 2** bằng tài khoản ChatGPT/OpenAI đã đăng nhập. Luôn
ra **đúng một ảnh** mỗi request (như Grok/Meta trả kết quả đầu). Ảnh tham chiếu đi
theo **VỊ TRÍ** (không có `@tag`).

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | - | Mô tả ảnh. |
| `aspect_ratio` | string | ❌ | `1:1` | Một trong `1:1`, `3:2`, `4:3`, `16:9`, `21:9`, `2:3`, `3:4`, `4:5`, `9:16`, `custom`. Không hợp lệ → `1:1`. |
| `quality` | string | ❌ | `high` | Một trong `low`, `medium`, `high`. Không hợp lệ → `high`. |
| `prompt_mode` | string | ❌ | `auto` | `auto` (model tinh chỉnh prompt) hoặc `direct` (dùng nguyên văn). Không hợp lệ → `auto`. |
| `reasoning` | string | ❌ | `none` | Mức suy luận: `none`, `low`, `medium`, `high`, `xhigh`, `max`. Không hợp lệ → `none`. |
| `web_search` | bool | ❌ | `false` | Cho phép tra cứu web trước khi tạo. |
| `reference_images` | array | ❌ | `[]` | Tối đa **5** ảnh base64 (xem §6). Truyền theo **vị trí** - GPT Image 2 **không** hỗ trợ `@tag`. |

```json
{
  "prompt": "a modern minimalist house, golden hour",
  "aspect_ratio": "16:9",
  "quality": "high",
  "prompt_mode": "auto",
  "reasoning": "none",
  "web_search": false,
  "reference_images": ["data:image/png;base64,iVBORw0KGgo..."]
}
```

> **Không cần trường `model`** - endpoint chỉ có một model (GPT Image 2). Gửi `model`
> cũng bị bỏ qua.
> **Độ phân giải native bị cap ~1.57 MP** ở backend OpenAI (giữ đúng tỉ lệ, không ra
> đủ 2K/4K theo số pixel tuyệt đối). Endpoint này **không** có `upscale`. Xem §9.

### 5.6 Nâng cấp ảnh - `POST /api/upscale/generate`

Phóng to một ảnh bằng **engine Real-ESRGAN chạy local** - đúng engine của tab
**Image Upscaler**. Không cần tài khoản, không tốn credit, không đụng quota: chạy
trên GPU của chính máy bạn.

Khác mọi endpoint còn lại, endpoint này **không có `prompt`** - ảnh chính là toàn bộ
nội dung request.

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|-------|------|:--------:|---------|-------|
| `image_path` | string | ⚠️ | - | Đường dẫn tuyệt đối tới ảnh nguồn **trên máy đang chạy G-Labs**. Dùng cái này *hoặc* `image`. |
| `image` | string | ⚠️ | - | Ảnh nguồn dạng base64 (xem §6). Dùng khi client nằm ở máy khác. |
| `filename` | string | ❌ | - | Chỉ dùng kèm `image`: làm gốc tên cho ảnh ra - xem quy tắc đặt tên bên dưới. Không có thì ảnh ra tên `wh_ups_<ngẫu nhiên>_upscaled_x4.png`. |
| `model` | string | ❌ | model đang chọn ở tab Upscaler | Phải là model đã cài, ví dụ `upscayl-standard-4x`, `remacri-4x`, `digital-art-4x`. Model lạ → `400 UNKNOWN_MODEL` kèm danh sách model *đang có*. |
| `scale` | int | ❌ | `4` | Tỉ lệ cuối, `2`-`8`. Model chạy gốc 4x; giá trị khác được resize từ kết quả 4x. Ngoài khoảng → `4`. |
| `format` | string | ❌ | `auto` | `auto` (theo ảnh gốc), `png`, `jpg`, `webp`. |
| `suffix` | string | ❌ | `_upscaled` | Nối vào tên ảnh ra, trước phần `_x<scale>`. Chuỗi rỗng → quay về `_upscaled`. |
| `tile` | int | ❌ | `0` | Kích thước ô xử lý của engine; `0` = tự động. Hạ xuống nếu GPU hết VRAM. |
| `tta` | bool | ❌ | `false` | Chế độ TTA - đẹp hơn chút, chậm hơn **rất** nhiều. |

Bắt buộc có đúng một trong hai `image_path` / `image`; gửi cả hai thì `image_path` thắng.

```json
{ "image_path": "E:/anh/meo.png", "scale": 4, "model": "upscayl-standard-4x" }
```

```json
{
  "image": "data:image/png;base64,iVBORw0KGgo...",
  "filename": "meo.png",
  "scale": 2,
  "format": "png"
}
```

**Mỗi request một ảnh.** Muốn chạy lô thì gửi nhiều request - mỗi cái có `task_id`
riêng.

> ⚠️ **Các request chạy lần lượt, không song song.** Engine là một tiến trình GPU;
> chạy nhiều cái cùng lúc là tranh nhau VRAM. Request thừa nằm trong hàng đợi FIFO,
> báo `pending` rồi chuyển `running` khi tới lượt. Đây là endpoint duy nhất **không**
> song song hoá - các endpoint khác chia tải theo *tài khoản*, còn cái này bị buộc
> vào một GPU.

> 💡 **Cùng máy thì nên dùng `image_path`** (n8n, script chạy local). Base64 làm
> payload phình ~4/3 mà trần body là 50 MB, nên một ảnh PNG 4K lớn có thể vượt trần.
> `image_path` không giới hạn kích thước và bỏ qua luôn bước mã hoá.

#### File nằm ở đâu và được đặt tên thế nào

**Thư mục**, xét theo thứ tự:

1. **Thư mục lưu** đã đặt ở tab **Image Upscaler** trong app, nếu không để trống.
2. Không thì `<thư mục output của G-Labs>/upscale_output` - nằm cạnh `image_output`,
   `veo_output`…

Không bao giờ lưu cạnh ảnh nguồn (đó là cách *tab* Upscaler làm): nguồn qua webhook
thường là file tạm, để vậy thì ảnh kết quả rơi vào thư mục temp của hệ điều hành rồi
bị dọn mất. Tuỳ chọn **Chế độ lưu / thư mục con theo lượt** ở tab Upscaler cũng
**không** được áp dụng - kết quả qua webhook luôn đi thẳng vào thư mục trên.

**Tên file:**

```
<base><suffix>_x<scale>.<ext>
```

| Thành phần | Lấy từ đâu |
|------|---------------------|
| `<base>` | Dùng `image_path`: tên file nguồn, bỏ phần mở rộng. Dùng `image`: tên bạn gửi ở `filename`, cộng thêm một chuỗi ngẫu nhiên ngắn (payload được ghi ra file tạm trước). Không gửi cả hai → `wh_ups_<ngẫu nhiên>`. |
| `<suffix>` | Trường `suffix` - mặc định `_upscaled`. Gửi **chuỗi rỗng thì vẫn quay về `_upscaled`**, giống hệt khi bỏ trống ô ở tab Upscaler; không có cách nào ra tên không hậu tố. |
| `<scale>` | Trường `scale` - mặc định `4`. |
| `<ext>` | Trường `format`. `auto` (mặc định) lấy theo phần mở rộng ảnh nguồn, thứ gì không phải png/jpg/webp thì về `png`; `jpeg` quy về `jpg`. |

Ví dụ:

```
image_path=E:/anh/meo.png, scale=4                 → meo_upscaled_x4.png
image_path=E:/anh/meo.heic, scale=2, format=webp   → meo_upscaled_x2.webp
image + filename="meo.png", scale=4                → meo_a1b2c3d4_upscaled_x4.png
```

**Trùng tên không bao giờ ghi đè.** Nếu tên đích đã tồn tại, phần mở rộng sẽ được chèn
thêm `_2`, `_3`, … phía trước - nên nâng cùng một ảnh hai lần bạn nhận được
`meo_upscaled_x4.png` và `meo_upscaled_x4_2.png`, chứ không phải một file bị lặng lẽ
thay thế.

API chỉ trả URL `/api/files/...`, **không** lộ đường dẫn cục bộ. Tên file trong URL
chính là tên dựng theo quy tắc trên nên bạn nhận ra được - nhưng hãy tải qua URL thay
vì đoán đường dẫn trên đĩa.

**Mã lỗi riêng của endpoint này:**

| `error_code` | `error` | Nghĩa |
|---|---|---|
| 503 | `ENGINE_MISSING` | Chưa cài binary Real-ESRGAN trong `bin/`. |
| 503 | `NO_VULKAN_DEVICE` | Không tìm thấy GPU hỗ trợ Vulkan. |
| 507 | `GPU_OUT_OF_MEMORY` | GPU hết VRAM. Hạ `tile` (vd `256`) hoặc dùng ảnh nguồn nhỏ hơn. Khác `NO_VULKAN_DEVICE`: GPU vẫn tốt, chỉ là ảnh không vừa bộ nhớ. |
| 400 | `UNKNOWN_MODEL` | `model` chưa được cài; thông báo có kèm danh sách model đang có. |
| 400 | `UNREADABLE_IMAGE` | Ảnh nguồn hỏng hoặc định dạng không đọc được. |
| 500 | `RESIZE_FAILED` | Engine chạy xong nhưng resize về đúng `scale` thất bại. |
| 500 | `OUTPUT_DIR_UNWRITABLE` | Không tạo được thư mục đích (ổ đĩa bị rút?). |

### 5.7 Bảng tham chiếu Model

| Giá trị API (`model` / `mode`) | Tên hiển thị | Đầu ra / Tỉ lệ |
|------|--------------|--------|
| `nano_banana_pro` | Nano Banana Pro | `1:1, 3:4, 4:3, 9:16, 16:9` |
| `nano_banana_2` | Nano Banana 2 | `1:1, 3:4, 4:3, 9:16, 16:9` |
| `nano_banana_2_lite` | Nano Banana 2 Lite | `1:1, 3:4, 4:3, 9:16, 16:9` |
| `nano_pics` | Google Pics (ảnh; `text_to_image` / `image_to_image` (1-14 ảnh, theo vị trí); 3-9 ảnh mỗi lượt, `keep` 1-4 hoặc tất cả; mặc định xoá logo Gemini; chạy bằng tài khoản Google ở Cài đặt → Tài khoản Google, gói PLUS/MAX) | `16:9, 9:16, 1:1, 4:3, 3:4, 3:2, 2:3, 5:4, 4:5, 21:9` |
| `veo_31_fast` | Veo 3.1 Fast | `16:9, 9:16` |
| `veo_31_lite` | Veo 3.1 Lite | `16:9, 9:16` |
| `veo_31_quality` | Veo 3.1 Quality | `16:9, 9:16` |
| `veo_31_lite_relaxed` | Veo 3.1 Lite Lower Priority [0 Credit] (chỉ ULTRA) | `16:9, 9:16` |
| `omni_flash` | Omni Flash (video; 4/6/8/10s; tối đa 7 ảnh ref; 360p hoặc 720p; edit video ≤10s qua `reference_video`; không cần ULTRA) | `16:9, 9:16` |
| `omni_vids` | Google Vids Omni (video; 3-10 s; 720p hoặc 1080p tạo thẳng; `text_to_video` / `start_image` (1 ảnh) / `components` (1-3 ảnh, `@tên`); chạy bằng tài khoản Google ở Cài đặt → Tài khoản Google, gói PLUS/MAX) | `16:9, 9:16` |
| *upscale* `model` | Tuỳ những gì đang có trong `bin/realesrgan/models/` - bảng model ở tab Webhook liệt kê đúng bộ trên máy bạn. Bản gốc: `upscayl-standard-4x`, `upscayl-lite-4x`, `digital-art-4x`, `high-fidelity-4x`, `remacri-4x`, `ultramix-balanced-4x`, `ultrasharp-4x` | scale `2`-`8` (giữ nguyên khung ảnh) |
| Grok `mode=t2i` | Text → Image (1K) | `9:16, 16:9, 1:1, 2:3, 3:2, 4:3, 21:9, 5:2` |
| Grok `mode=i2i` | Image → Image (1K) | `9:16, 16:9, 1:1, 2:3, 3:2, 4:3, 21:9, 5:2` |
| Grok `mode=t2v` | Text → Video (480p/720p/1080p) | `9:16, 16:9, 1:1, 2:3, 3:2` |
| Grok `mode=i2v` | Image → Video (480p/720p/1080p) | `9:16, 16:9, 1:1, 2:3, 3:2` |
| Meta `mode=t2i` | Meta AI Văn bản → Ảnh | `9:16, 16:9, 1:1` |
| Meta `mode=t2v` | Meta AI Văn bản → Video (480p/720p) | `9:16, 16:9, 1:1` |
| Meta `mode=i2i` | Meta AI Ảnh → Ảnh (thành phần) | `9:16, 16:9, 1:1` |
| Meta `mode=i2v` | Meta AI Ảnh → Video (đầu/cuối) | `9:16, 16:9, 1:1` |
| OpenAI `GPT_IMAGE` | GPT Image 2 (~1.57 MP, không upscale) | `1:1, 3:2, 4:3, 16:9, 21:9, 2:3, 3:4, 4:5, 9:16, custom` |

---

## 6. Định dạng ảnh tham chiếu

Mọi endpoint có nhận ảnh đều chấp nhận **hai kiểu** - base64 nhúng thẳng, hoặc đường
dẫn tới file đã có sẵn trên máy đang chạy G-Labs. Quy ước này giống nhau ở
`/api/image`, `/api/video`, `/api/grok`, `/api/meta` và `/api/upscale`.

> ⚠️ **`path` chỉ dùng được khi client và app nằm CÙNG một thiết bị.** App mở đường dẫn
> đó trên hệ thống file của chính nó - nó không tải file từ phía bạn về. Client ở máy
> khác (hoặc trong container) bắt buộc phải gửi base64; đường dẫn không tồn tại bên đó
> sẽ làm hỏng cả task với lỗi `reference path not found: <đường dẫn>`.

Mỗi phần tử trong `reference_images` là một trong ba dạng:

1. **Chuỗi base64** - data URI hoặc base64 thô:
   - `"data:image/png;base64,iVBORw0KGgo..."`
   - `"data:image/jpeg;base64,/9j/4AAQ..."`
   - base64 thô `"iVBORw0KGgo..."` (được coi là PNG)
2. **Object có `data`**: `{"data": "data:image/...;base64,...", "category": "subject", "name": "red_car.png"}`
3. **Object có `path`**: `{"path": "E:/anh/xe_do.png", "category": "subject"}`
   - File được đọc tại chỗ - không copy, không xoá. Ảnh gốc của bạn an toàn: chỉ
     những ảnh G-Labs tự giải mã từ base64 mới bị dọn sau khi task xong.
   - Không cần `name` ở dạng này - cơ chế `@tag` (§6.1) dùng luôn tên file thật.

`category` và `name` áp dụng như nhau cho cả hai:
- `category` không bắt buộc: `subject` | `scene` | `style`. Được chấp nhận nhưng
  **bị bỏ qua với model ảnh Flow** (chúng dùng một ô tham chiếu chung).
- `name` (hoặc `filename`) không bắt buộc, dành cho dạng **base64**: tên file gốc của
  ảnh, dùng để gắn vào prompt bằng `@<từ_khoá>` (xem §6.1).

**Chuỗi trần luôn được hiểu là base64**, không bao giờ là đường dẫn - base64 dùng cả
`/` lẫn `+` nên không có cách nào phân biệt chắc chắn. Muốn truyền đường dẫn thì phải
dùng dạng object.

Trộn cả hai dạng trong cùng một request cũng được.

Ràng buộc:
- Kiểu giải mã hỗ trợ: PNG, JPG/JPEG, WEBP (nhận diện qua header data-URI; mặc định
  PNG khi không có header). Dạng `path` thì trỏ tới định dạng nào engine đọc được cũng được.
- Base64 giải mã ra dưới ~100 byte sẽ bị bỏ (coi là không hợp lệ). Ngược lại, `path`
  không tồn tại sẽ **làm hỏng task** - gõ nhầm đường dẫn mà vẫn lặng lẽ render thiếu
  một ảnh tham chiếu thì tệ hơn nhiều.
- Số lượng tối đa theo endpoint: **ảnh = 10** (**Google Pics = 14**), **grok = 5**, **openai = 5**,
  **video = 3** (**Omni Flash = 7** - chỉ `components` dùng quá 2; **Google Vids = 3**).
  Phần dư vượt mức tối đa bị bỏ qua - riêng Google Pics thì từ chối
  (`400 TOO_MANY_REFERENCES`).
- **Vì sao nên dùng `path`:** base64 làm payload phình ~4/3 và mỗi request bị chặn ở
  50 MB (§5). Đường dẫn cục bộ không giới hạn kích thước và bỏ qua luôn khâu mã hoá/
  giải mã ở cả hai đầu.

### 6.1 Gắn ảnh theo tên bằng `@tag`

Khi một ảnh tham chiếu có `name` (hoặc `filename`), bạn có thể trỏ tới nó **ngay trong
prompt** bằng `@<từ_khoá>` - **đúng cùng cơ chế** ở trang Image / Veo trong app (tín hiệu
webhook đi qua chính các hàm xử lý đó nên payload gửi Flow API khớp y như tạo trực tiếp).

- **Khớp**: `<từ_khoá>` là **chuỗi con** không phân biệt hoa thường của tên file (đã bỏ
  đuôi). Vd `name: "red_car.png"` → `@red_car`, `@car`, `@red` đều trúng; ảnh đầu tiên theo
  thứ tự trong `reference_images` thắng.
- **Tác dụng**: gắn đúng ảnh đó vào đúng vị trí danh từ trong câu (Flow structured prompt
  "Mode-2"), thay vì truyền tất cả ảnh như tham chiếu chung vô danh.
- **Phạm vi**: dùng cho **image (Flow)**, **video (Veo)** và **Google Vids `components`** (`omni_vids`, ở đó tên nhân vật trong thư viện cũng là tag hợp lệ); **Grok**, **OpenAI (GPT Image 2)** và **Google Pics** **không hỗ trợ** `@tag` (ref đi theo vị trí).
- Tên file được làm sạch (bỏ thành phần thư mục và ký tự không hợp lệ) trước khi dùng.
- **Tag không khớp** được giữ nguyên là văn bản - không gây lỗi.
- **Không gửi `name`**: ảnh vẫn dùng như tham chiếu theo vị trí như trước (tương thích ngược).

**Image (Flow):**
```json
{
  "prompt": "a @red_car parked next to a @house at night",
  "reference_images": [
    {"data": "data:image/png;base64,...", "name": "red_car.png"},
    {"data": "data:image/jpeg;base64,...", "name": "house.jpg"}
  ]
}
```

**Video (Veo) - mode `components`** (ghép nhiều "nguyên liệu" theo tên; cũng áp dụng cho
`start_image` / `start_end_image`):
```json
{
  "prompt": "the @character walks through the @forest at dawn",
  "model": "veo_31_fast",
  "mode": "components",
  "aspect_ratio": "16:9",
  "reference_images": [
    {"data": "data:image/png;base64,...", "name": "character.png"},
    {"data": "data:image/jpeg;base64,...", "name": "forest.jpg"}
  ]
}
```

### 6.2 Trường ảnh tham chiếu có tên của Meta AI

**Meta AI (`/api/meta/generate`) KHÔNG dùng mảng `reference_images`.** Nó có các
trường riêng có tên, mỗi trường nhận **hoặc** chuỗi base64 theo đúng định dạng ở §6
(data URI hoặc base64 thô; PNG/JPG/WEBP; dưới ~100 byte bị bỏ) **hoặc**
`{"path": "..."}` - cùng hai dạng như `reference_images`, và cũng kèm điều kiện phải
cùng thiết bị:

| Trường | Mode | Vai trò |
|--------|------|---------|
| `character_image` (hoặc `subject_image`) | `i2i` | Thành phần nhân vật / chủ thể |
| `scene_image` | `i2i` | Thành phần bối cảnh |
| `style_image` | `i2i` | Thành phần phong cách |
| `start_image` | `i2v` | Khung đầu (**bắt buộc** cho i2v) |
| `end_image` | `i2v` | Khung cuối (tùy chọn; bật nội suy đầu→cuối) |

- **i2i** dùng tổ hợp bất kỳ của `character_image` / `scene_image` / `style_image`
  (ít nhất một).
- **i2v** dùng `start_image` (và tùy chọn `end_image`).
- `t2i` / `t2v` **không** nhận ảnh - ảnh gửi kèm sẽ bị bỏ qua.
- Meta AI **không có `@tag`**; tên trường quyết định vai trò.

---

## 7. Tham chiếu Response & trạng thái

### POST generate → `202`
```json
{ "task_id": "abc12345", "status": "pending", "message": "...", "poll_url": "/api/status/abc12345" }
```

### GET `/api/status/{task_id}` → `200`
- `pending` / `running`: `{ task_id, type, status, prompt, created_at }`
- `type`: `image`, `video`, `grok`, `vibes` (task Meta AI), `openai` hoặc `upscale`.
- `completed`: thêm `results` (mảng URL file) và `completed_at` (unix giây); task Google Vids
  còn có thêm `meta` (§5.2), task Google Pics cũng vậy (§5.1).
- `failed`: thêm `error_code` (int), `error` (string), `error_detail` (string).
- task_id không tồn tại → `404 {"error": "Task <id> not found"}`. Máy chủ giữ 200 task **đã
  xong** gần nhất; task cũ hơn bị xoá và cũng trả `404`.

### GET `/api/result/{task_id}` → `200`
- Nếu chưa xong: `{ task_id, status, message: "Task not yet completed" }` - task `failed` cũng
  nhận đúng dạng này, **không** có trường lỗi: đọc lỗi ở `GET /api/status/{task_id}`.
- Nếu đã xong: `{ task_id, status: "completed", results: [...], completed_at }` (thêm `meta`
  với Google Vids / Google Pics).
### GET `/api/health` → `200`
```json
{ "status": "ok", "server": "G-Labs Webhook", "uptime": 123, "tasks_pending": 0, "tasks_running": 1 }
```

### GET `/api/tasks` → `200`
```json
{ "tasks": [ { "task_id": "...", "type": "image", "status": "completed", "prompt": "50 ký tự đầu...", "created_at": 1707782400.0 } ] }
```
(Mới nhất trước, tối đa 50.)

### POST `/api/stop` (hoặc `/api/stop/{task_id}`) → `200`
```json
{ "stopped": ["a1b2c3d4", "e5f6a7b8"], "skipped": [], "count": 2 }
```
`stopped` = các task đang chờ / đang chạy nay đã `failed` (`499 STOPPED_BY_CLIENT`);
`skipped` = task được gọi đích danh nhưng đã xong từ trước. `task_id` không tồn tại → `404`.
Lệnh này chỉ cần API key. Body không phải JSON object → `400 {"error": "Body must be a JSON
object"}`; body quá 64 KB → `413` - cả hai đều không dừng gì cả.

### Các response lỗi
| HTTP | Body | Khi nào |
|------|------|---------|
| `400` | `{"error": "Empty body"}` | POST không có body |
| `400` | `{"error": "Invalid Content-Length"}` | Header `Content-Length` sai định dạng |
| `401` | `{"error": "Invalid or missing API key"}` | Thiếu/sai `X-API-Key` |
| `403` | `{"error": "Webhook requires MAX plan"}` | Kết nối được máy chủ nhưng license không phải MAX |
| `404` | `{"error": "Not found"}` | Route không tồn tại |
| `404` | `{"error": "Task <id> not found"}` | task không tồn tại ở status/result/stop |
| `404` | `{"error": "File not found: <name>"}` | File không tồn tại/đã hết hạn |
| `413` | `{"error": "Payload too large (max 52428800 bytes)"}` | Body vượt trần **50 MB** - xem §5 |
| `500` | `{"error": "Failed to read file"}` | File kết quả có trong registry nhưng không đọc được |

Đây là các lỗi ở **tầng truyền tải**, do chính lệnh `POST`/`GET` trả về. Request đã đi
qua được các lỗi này sẽ nhận `202`, và mọi trục trặc sau đó hiện ra dưới dạng task
`failed` kèm `error_code` / `error` (§8) chứ không phải lỗi HTTP.

---

## 8. Mã lỗi (`error_code` / `error` / `error_detail`)

Khi task thất bại, response trạng thái mang ba trường:

- **`error_code`** - số nguyên. Với lỗi từ API phía trên, nó phản ánh mã kiểu HTTP
  (`400`, `403`, `429`, `500`, …). **`429` nghĩa là hết quota / giới hạn tần suất**
  (vd hết giới hạn tạo trong ngày). Bằng `0` khi không có mã số phù hợp (vd lỗi
  validate, "không có tài khoản").
- **`error`** - thông điệp dễ đọc. Với các status đã biết từ phía trên, đây là status
  tiếng Anh ổn định (vd `PERMISSION_DENIED`, `RESOURCE_EXHAUSTED`). Với các thông điệp
  thân thiện (quota, upscale thất bại, timeout), phần chữ **theo ngôn ngữ giao diện
  của app** (vd tiếng Việt nếu app đang để tiếng Việt).
- **`error_detail`** - chuỗi lỗi gốc đầy đủ (vd `"429: Đã hết giới hạn tạo ảnh trong ngày (user@gmail.com)"`).

Các trường hợp phổ biến:

| `error_code` | Ý nghĩa | `error` điển hình |
|:---:|---------|-------------------|
| `429` | Hết quota trong ngày / bị giới hạn tần suất | thông điệp quota (kèm email tài khoản) |
| `403` | Bị từ chối quyền / lỗi phiên | `PERMISSION_DENIED` |
| `400` | Request không hợp lệ / vi phạm chính sách prompt | `INVALID_ARGUMENT`, thông điệp vi phạm |
| `500` | Lỗi máy chủ phía trên | `INTERNAL` / `HTTP_500` |
| `0` | Lỗi validate / môi trường | `No active accounts available`, `Missing required field: prompt`, `Invalid mode '...'`, thông điệp upscale thất bại, `Timeout: no result generated`, `Task timed out (no completion signal received)` (watchdog task treo) |

> Mẹo xử lý bằng code: rẽ nhánh theo `error_code` (không phụ thuộc ngôn ngữ). Dùng
> `error` / `error_detail` cho log hiển thị cho người. `error_code == 429` là tín hiệu
> để giãn nhịp / xoay tài khoản / thử lại sau.
>
> Mã có tên luôn kèm lời giải thích phía sau: `error` là toàn bộ phần sau `"<mã>: "`, vd
> `"INVALID_MODE - omni_vids supports text_to_video, …"`. Hãy so **phần đầu** của `error`
> (`error.startswith("INVALID_MODE")`), đừng so cả chuỗi.

Lưu ý riêng của app này:
- **Video** yêu cầu độ phân giải không tạo được (vd `4K` mà không có tài khoản ULTRA)
  → `failed`.
- **Ảnh** yêu cầu `upscale` (`2K`/`4K`) không tạo được → `failed` kèm lý do upscale
  (không trả về ảnh gốc nhỏ hơn).
- **Upscale** có mã riêng (`503 ENGINE_MISSING`, `503 NO_VULKAN_DEVICE`,
  `507 GPU_OUT_OF_MEMORY`, `400 UNKNOWN_MODEL`, …) - xem bảng ở §5.6. Không bao giờ trả
  `429`: không có quota nào để hết.
- **Meta AI**: cookie tài khoản hết hạn → `failed` `401` (`Meta cookie expired`);
  hết quota → `429` (`Meta quota exhausted`); không có tài khoản Meta đang bật cho
  loại yêu cầu → `error_code 0` (`No enabled Meta account for image/video`); không
  tạo ra gì → `Meta produced no output`.
- **Task bất kỳ** bị dừng qua `POST /api/stop` → `failed` với `499` / `STOPPED_BY_CLIENT`.
- **Google Vids** (`omni_vids`): request bị từ chối → `400` `INVALID_MODE` / `INVALID_RESOLUTION` /
  `INVALID_VIDEO_LENGTH` / `INVALID_ASPECT_RATIO` / `INVALID_FIELD` / `MISSING_REFERENCE` /
  `UNKNOWN_CLIP` / `ALREADY_UPSCALED`; gói thấp → `403 PLAN_REQUIRED`; thiếu config máy chủ →
  `503 VIDS_CONFIG` / `503 RUNTIME_CONFIG`; không tài khoản nào đủ giây → `503 NO_VIDS_ACCOUNT`;
  mọi tài khoản bận suốt 15 phút → `503 NO_FREE_SLOT`; sau một lỗi mà không còn tài khoản nào nhận được task → `502 ALL_ACCOUNTS_FAILED` (còn lại là lỗi của chính tài khoản cuối, bên dưới);
  việc tự lỗi → `401 VIDS_COOKIE_EXPIRED`, `429 VIDS_QUOTA_EXHAUSTED`, `429 RATE_LIMITED`,
  `400 CONTENT_POLICY`, `400 BAD_REQUEST`, `400 CLIP_GONE` (upscale), `409 CLIP_ACCOUNT_UNAVAILABLE`
  (upscale), `502 UPSTREAM`, `502 NO_OUTPUT`; máy chủ webhook bị tắt khi task đang chờ hoặc đang chạy
  → `503 SERVER_STOPPED`.
- **Google Pics** (`nano_pics`): request bị từ chối → `400` `INVALID_MODE` / `MISSING_REFERENCE` /
  `TOO_MANY_REFERENCES` / `INVALID_ASPECT_RATIO` / `INVALID_KEEP` / `INVALID_FIELD`; gói thấp →
  `403 PLAN_REQUIRED`; thiếu config máy chủ → `503 PICS_CONFIG` / `503 RUNTIME_CONFIG`; không tài
  khoản nào dùng được còn lượt → `503 NO_PICS_ACCOUNT`; mọi tài khoản bận suốt 15 phút →
  `503 NO_FREE_SLOT`; sau một lỗi mà không còn tài khoản nào nhận được task →
  `502 ALL_ACCOUNTS_FAILED` (còn lại là lỗi của chính tài khoản cuối, bên dưới); việc tự lỗi →
  `401 PICS_COOKIE_EXPIRED`, `403 PICS_NO_ACCESS` (tài khoản không dùng được Google Pics; vẫn
  được giữ bật), `504 PICS_TIMEOUT` (đã gửi yêu cầu mà không nhận được trả lời - có thể đã trừ lượt
  nên KHÔNG tự thử lại, không chuyển tài khoản khác), `429 PICS_QUOTA_EXHAUSTED`, `429 RATE_LIMITED`, `400 CONTENT_POLICY`,
  `400 BAD_REQUEST`, `502 UPSTREAM`, `502 NO_OUTPUT`; máy chủ webhook bị tắt → `503 SERVER_STOPPED`.

---

## 9. Ràng buộc, hạng tài khoản & lưu ý

- **Yêu cầu gói MAX** để bật máy chủ Webhook.
- **Địa chỉ bind.** Mặc định `127.0.0.1` (chỉ cùng máy). Đặt host thành `0.0.0.0`
  hoặc IP LAN trong tab Webhook để máy khác trong mạng vào được (nhớ mở cổng trên
  tường lửa); URL file kết quả khi đó dùng đúng host này. `127.0.0.0` không phải địa
  chỉ bind/connect hợp lệ. Muốn qua internet thì tự dựng tunnel.
- **Tài khoản & hạng:**
  - Ảnh/Video cần tài khoản Google đã đăng nhập và **đang bật** trong app.
  - Upscale ảnh `4K`, video **`4K`**, và `veo_31_lite_relaxed` cần tài khoản
    **ULTRA** (video `1080p` không cần ULTRA). Không có tài khoản hợp lệ thì task `failed`.
  - Tài khoản đã **TẮT** trong app sẽ không được dùng.
- **Grok** cần phiên Super Grok đang kết nối trong app.
- **Mỗi request Grok trả 1 kết quả** (ảnh/video đầu tiên được tạo).
- **Meta AI** cần tài khoản Meta (vibes.ai) đã đăng nhập và **đang bật** trong app
  (tab Meta AI) - `image_enabled` cho `t2i`/`i2i`, `video_enabled` cho `t2v`/`i2v`.
  Dùng tài khoản hợp lệ đầu tiên (không xoay vòng); tài khoản đầu hết hạn sẽ làm task
  thất bại.
- **OpenAI (GPT Image 2)** cần tài khoản ChatGPT/OpenAI đã đăng nhập và **đang bật**
  trong app (GPT Image 2 → tài khoản ChatGPT). Tài khoản dùng **xoay vòng** (round-robin)
  và **fail-over** sang tài khoản kế khi lỗi ở mức tài khoản (hết hạn/quota/5xx). Token
  được làm mới tự động trước mỗi lượt. Trần luồng = **5 luồng mỗi tài khoản** (số tài
  khoản đang bật × 5), giống Flow/Meta. Ảnh ra bị cap ~1.57 MP (không 2K/4K, không upscale).
- **Google Vids** (`omni_vids`) cần gói **PLUS/MAX** và ít nhất một tài khoản Google ở
  Cài đặt → Tài khoản Google đang BẬT (tích ô Video) và còn giây. Số giây là hạn mức riêng của tài khoản (1 giây video =
  1 giây). Upscale chỉ chạy trên đúng tài khoản đã tạo clip.
- **Google Pics** (`nano_pics`) cần gói **PLUS/MAX** và ít nhất một tài khoản Google ở Cài đặt →
  Tài khoản Google đang BẬT (tích ô Ảnh) và còn lượt Pics. Một task = một lượt = 1 đơn vị hạn
  mức Pics của tài khoản, bất kể lượt đó ra bao nhiêu ảnh.
- **Upscale** không cần tài khoản, không cần hạng nào - engine Real-ESRGAN chạy trên
  GPU máy bạn nên không tốn credit, không đụng quota. Chỉ cần có sẵn engine + model
  trong `bin/realesrgan/` (thiếu thì `503 ENGINE_MISSING`) và một GPU hỗ trợ Vulkan.
  Các request được xử lý **lần lượt từng cái**; gửi dồn thì xếp hàng chứ không chạy
  song song (nhiều tiến trình engine sẽ tranh nhau VRAM). Lưu ý endpoint này vẫn nằm
  sau máy chủ Webhook, mà cái đó chỉ mở cho gói MAX.
- **Task lưu trong bộ nhớ.** Trạng thái task và ánh xạ `task_id` → kết quả nằm trong
  app đang chạy; sẽ mất nếu app khởi động lại. Hãy gửi, hỏi trạng thái và tải về
  trong cùng một phiên chạy app.
- **File lưu nội bộ** và có thể bị dọn theo thời gian; hãy tải ngay sau khi `completed`.
- **Tính tái lập:** cùng một `prompt` không đảm bảo cho ra kết quả giống hệt.

---

## 10. Ví dụ đầu-cuối

### 10.1 cURL

```bash
# --- Ảnh (cơ bản) ---
curl -X POST http://127.0.0.1:8765/api/image/generate \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt": "a cat wearing sunglasses", "model": "nano_banana_2"}'
# → {"task_id":"abc12345","status":"pending","poll_url":"/api/status/abc12345"}

# --- Hỏi trạng thái tới khi xong ---
curl http://127.0.0.1:8765/api/status/abc12345 -H "X-API-Key: YOUR_API_KEY"

# --- Ảnh + tham chiếu + upscale 4K (cần ULTRA) ---
curl -X POST http://127.0.0.1:8765/api/image/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"modern house","model":"nano_banana_pro","reference_images":["data:image/png;base64,..."],"upscale":["4K"]}'

# --- Video (ảnh đầu) ---
curl -X POST http://127.0.0.1:8765/api/video/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"flowing water","mode":"start_image","reference_images":["data:image/png;base64,..."],"resolution":["1080p"]}'

# --- Video (mode components + voice) ---
curl -X POST http://127.0.0.1:8765/api/video/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"she says hello","mode":"components","reference_images":["data:image/png;base64,..."],"voice":"aoede"}'

# --- Grok: văn bản → ảnh ---
curl -X POST http://127.0.0.1:8765/api/grok/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a girl swimming in a pool","mode":"t2i","aspect_ratio":"16:9"}'

# --- Grok: ảnh → video ---
curl -X POST http://127.0.0.1:8765/api/grok/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"make it rain","mode":"i2v","aspect_ratio":"16:9","resolution":"720p","reference_images":["data:image/png;base64,..."]}'

# --- Meta AI: văn bản → ảnh ---
curl -X POST http://127.0.0.1:8765/api/meta/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a cat astronaut","mode":"t2i","aspect_ratio":"1:1","count":1}'

# --- Meta AI: văn bản → video ---
curl -X POST http://127.0.0.1:8765/api/meta/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"waves on a beach at dawn","mode":"t2v","aspect_ratio":"9:16","resolution":"720p"}'

# --- Meta AI: ảnh → ảnh (thành phần) ---
curl -X POST http://127.0.0.1:8765/api/meta/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"same character in a forest","mode":"i2i","aspect_ratio":"16:9","character_image":"data:image/png;base64,...","scene_image":"data:image/png;base64,..."}'

# --- Meta AI: ảnh → video (đầu + cuối tùy chọn) ---
curl -X POST http://127.0.0.1:8765/api/meta/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"pan across the scene","mode":"i2v","aspect_ratio":"16:9","resolution":"720p","start_image":"data:image/png;base64,...","end_image":"data:image/png;base64,..."}'

# --- OpenAI GPT Image 2: văn bản → ảnh ---
curl -X POST http://127.0.0.1:8765/api/openai/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a modern minimalist house, golden hour","aspect_ratio":"16:9","quality":"high"}'

# --- OpenAI GPT Image 2: kèm ảnh tham chiếu (theo vị trí, không @tag) ---
curl -X POST http://127.0.0.1:8765/api/openai/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"same subject on a beach","aspect_ratio":"1:1","reference_images":["data:image/png;base64,..."]}'

# --- Ảnh kèm tham chiếu đọc thẳng từ đĩa (cùng máy, khỏi base64) ---
curl -X POST http://127.0.0.1:8765/api/image/generate   -H "Content-Type: application/json" -H "X-API-Key: $KEY"   -d '{"prompt":"chiếc @xe trên đường đèo","reference_images":[{"path":"E:/anh/xe.png"}]}'

# --- Upscale: ảnh nguồn có sẵn trên máy này (không giới hạn cỡ, khỏi mã hoá) ---
curl -X POST http://127.0.0.1:8765/api/upscale/generate   -H "Content-Type: application/json" -H "X-API-Key: $KEY"   -d '{"image_path":"E:/anh/meo.png","scale":4,"model":"upscayl-standard-4x"}'

# --- Upscale: gửi ảnh dạng base64 (client ở máy khác) ---
curl -X POST http://127.0.0.1:8765/api/upscale/generate   -H "Content-Type: application/json" -H "X-API-Key: $KEY"   -d '{"image":"data:image/png;base64,...","filename":"meo.png","scale":2,"format":"png"}'

# --- Google Pics: văn bản → ảnh (16:9, giữ 2 ảnh, xoá logo Gemini) ---
curl -X POST http://127.0.0.1:8765/api/image/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a red fox in the snow","model":"nano_pics","aspect_ratio":"16:9","keep":2}'

# --- Google Pics: ảnh → ảnh (ảnh tham chiếu đọc từ đĩa) ---
curl -X POST http://127.0.0.1:8765/api/image/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"the same girl in a cafe","model":"nano_pics","mode":"image_to_image","reference_images":[{"path":"E:/photos/girl.png"}]}'

# --- Google Vids: văn bản → video (1080p dọc, 5 giây) ---
curl -X POST http://127.0.0.1:8765/api/video/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a cat walking on a wall at sunset","model":"omni_vids","mode":"text_to_video","aspect_ratio":"9:16","resolution":["1080p"],"video_length":5}'

# --- Google Vids: nâng phân giải clip của một task đã xong (clip_temp_id lấy từ meta) ---
curl -X POST http://127.0.0.1:8765/api/video/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"model":"omni_vids","mode":"upscale","clip_temp_id":"ABCD...WXYZ"}'

# --- Dừng một task / dừng tất cả ---
curl -X POST http://127.0.0.1:8765/api/stop/abc12345 -H "X-API-Key: YOUR_API_KEY"
curl -X POST http://127.0.0.1:8765/api/stop -H "X-API-Key: YOUR_API_KEY"

# --- Tải file kết quả ---
curl -o out.png "http://127.0.0.1:8765/api/files/image_001.png"

# --- Liệt kê task gần đây ---
curl http://127.0.0.1:8765/api/tasks -H "X-API-Key: YOUR_API_KEY"
```

### 10.2 Python (gửi → hỏi → tải)

```python
import base64, time, requests

BASE = "http://127.0.0.1:8765"
KEY  = "YOUR_API_KEY"
H    = {"X-API-Key": KEY, "Content-Type": "application/json"}

def b64(path):
    ext = "png" if path.lower().endswith(".png") else "jpeg"
    with open(path, "rb") as f:
        return f"data:image/{ext};base64," + base64.b64encode(f.read()).decode()

def generate(endpoint, body, poll=4, timeout=900):
    r = requests.post(f"{BASE}/api/{endpoint}/generate", json=body, headers=H, timeout=30)
    r.raise_for_status()
    task_id = r.json()["task_id"]

    deadline = time.time() + timeout
    while time.time() < deadline:
        s = requests.get(f"{BASE}/api/status/{task_id}", headers=H, timeout=30).json()
        status = s.get("status")
        if status == "completed":
            return s["results"]                      # danh sách URL file
        if status == "failed":
            raise RuntimeError(f"[{s.get('error_code')}] {s.get('error')}")
        time.sleep(poll)
    raise TimeoutError(f"task {task_id} chưa xong trong {timeout}s")

# Ảnh
urls = generate("image", {
    "prompt": "a modern minimalist house, golden hour",
    "model": "nano_banana_pro",
    "aspect_ratio": "16:9",
    "upscale": ["2K"],
})

# Tải về
for i, u in enumerate(urls):
    data = requests.get(u, timeout=120).content   # /api/files không cần key
    open(f"out_{i}{u[u.rfind('.'):]}" if '.' in u else f"out_{i}.bin", "wb").write(data)

# Ảnh→Ảnh qua Grok
grok_urls = generate("grok", {
    "prompt": "same character, sunset lighting",
    "mode": "i2i",
    "aspect_ratio": "1:1",
    "reference_images": [b64("char.png")],
})
```

### 10.3 JavaScript (Node, fetch)

```js
const BASE = "http://127.0.0.1:8765";
const KEY  = "YOUR_API_KEY";
const H = { "X-API-Key": KEY, "Content-Type": "application/json" };

async function generate(endpoint, body, { poll = 4000, timeout = 900000 } = {}) {
  const r = await fetch(`${BASE}/api/${endpoint}/generate`, {
    method: "POST", headers: H, body: JSON.stringify(body),
  });
  if (!r.ok) throw new Error(`submit ${r.status}`);
  const { task_id } = await r.json();

  const end = Date.now() + timeout;
  while (Date.now() < end) {
    const s = await (await fetch(`${BASE}/api/status/${task_id}`, { headers: H })).json();
    if (s.status === "completed") return s.results;          // URL file
    if (s.status === "failed") throw new Error(`[${s.error_code}] ${s.error}`);
    await new Promise(r => setTimeout(r, poll));
  }
  throw new Error(`task ${task_id} hết thời gian chờ`);
}

// Video, văn bản→video
const urls = await generate("video", {
  prompt: "neon city at night, drone shot",
  model: "veo_31_fast",
  aspect_ratio: "16:9",
  resolution: ["720p"],
});
console.log(urls);
```

---

## 11. Checklist nhanh cho người tích hợp / AI agent

1. Bật máy chủ Webhook trong app; sao chép **port** và **API key**.
2. Luôn gửi `X-API-Key` ở các call generate/status/result/tasks/stop.
3. `POST /api/{image|video|grok|meta|openai}/generate` với body hợp lệ (`prompt` bắt buộc -
   trừ `upscale` của `omni_vids`), hoặc `POST /api/upscale/generate` với `image_path` /
   `image` và **không** có `prompt`.
4. Đọc `task_id` từ response `202`.
5. Hỏi `GET /api/status/{task_id}` mỗi 3-5 giây tới khi `completed` hoặc `failed`.
6. Khi `completed`: `GET` từng URL trong `results` để tải file.
7. Khi `failed`: xem `error_code` (vd `429` = hết quota) và `error` / `error_detail`.
8. Tôn trọng tỉ lệ theo từng model, số ảnh tham chiếu theo từng mode, và các tính
   năng chỉ dành cho ULTRA. Google Vids và Google Pics từ chối giá trị sai bằng mã `400` có
   tên lỗi, không tự đổi về mặc định.
9. Muốn huỷ: `POST /api/stop/{task_id}` (hoặc `/api/stop` cho tất cả) - task chuyển ngay sang
   `failed` với `499 STOPPED_BY_CLIENT`.
