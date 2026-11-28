# G-Labs Studio — Hướng dẫn tích hợp Webhook API

> Đối tượng đọc: lập trình viên, người tích hợp kỹ thuật, và AI agent.
> Mục tiêu: cung cấp đầy đủ mọi thứ cần để tích hợp đúng Webhook REST API nội bộ —
> danh sách endpoint, xác thực, schema request/response, model, tham số, xử lý lỗi,
> và quy trình bất đồng bộ (gửi yêu cầu → hỏi trạng thái → tải kết quả).

Tài liệu này mô tả API do tab **Webhook** của ứng dụng desktop G-Labs Studio
(v5.0.3+; danh mục model `/api/models` và API chuẩn OpenAI `/v1/*` cần bản mới hơn 5.0.6) cung cấp. Nó cho phép các công cụ bên ngoài (n8n, Make.com, script tự
viết, AI agent) điều khiển việc tạo ảnh (Flow, Google Pics, Meta Muse, Dreamina) / video (Veo, Omni Flash, Google Vids, Meta Muse, Dreamina) / Grok /
Meta AI / OpenAI — và nâng cấp ảnh cục bộ — qua REST API đơn giản.

---

## Dành cho AI agent - đọc phần này trước

Bạn là AI agent (Antigravity, Claude Code, Cursor, Codex...) được người dùng gửi link tài liệu này? Phần này đủ
để bắt đầu; các mục đánh số bên dưới là phần tra cứu chi tiết.

- **Lấy bản đầy đủ.** Tài liệu dài. Nếu công cụ đọc web của bạn chỉ trả về bản tóm tắt hoặc bị cắt, hãy tải bản thô
  về thư mục làm việc rồi đọc từ file:
  `https://raw.githubusercontent.com/duckmartians/G-Labs-Studio/main/WEBHOOK_INTEGRATION.vi.md`
- **Cần hai thứ: cổng (mặc định `8765`) và API key** ở trang Webhook API của app. Khi bạn chạy **cùng máy với app** và
  người dùng đồng ý, đọc cả hai từ file cấu hình của app (trường `port` và `api_key`), khỏi phải chép tay:
  Windows `%APPDATA%\G-Labs Studio\webhook_config.json`, macOS
  `~/Library/Application Support/G-Labs Studio/webhook_config.json`. Không đọc được thì hỏi người dùng, không đoán.
  Chỉ dùng key để gọi app trên máy này; không in key ra câu trả lời, không gửi key đi nơi khác.
- **Đọc từ file, không đọc từ trang web.** Sau khi tải bản thô ở trên, lưu thành một file trong thư mục làm việc và
  tra từ file đó mỗi khi cần một trường hay một mã lỗi.
- **Tài liệu này chỉ nói cách gọi app.** Làm phim gì, phong cách nào, quy trình ra sao là do người dùng chỉ đạo.
  Chưa được yêu cầu thì chưa tạo gì (mỗi lần tạo tốn hạn mức tài khoản của người dùng).

**Cách làm việc**

1. `GET /api/health` (không cần key) để biết app đang mở và máy chủ Webhook đang bật. Không kết nối được → bảo người
   dùng mở G-Labs Studio, vào trang Webhook API và bật server.
2. `GET /api/models` để lấy danh sách model **đang dùng được trên máy này**, kèm giới hạn của từng model: số ảnh tham
   chiếu tối đa và cách gắn (`reference_binding`: `tag` hoặc `position`), các `modes`, tỉ lệ, độ phân giải, thời
   lượng, và thứ cần hạng tài khoản cao hơn (`requires`). Đọc trước khi chọn model; đừng giả định giới hạn (§5.7, §7).
   Danh mục không có giá: đừng nêu giá hay số credit.
3. Gửi `POST /api/<endpoint>/generate` → nhận `task_id` → hỏi `GET /api/status/<task_id>` mỗi 3-5 giây tới khi
   `completed` hoặc `failed` → tải từng link trong `results` (§4). Video có thể mất nhiều phút: chờ bằng **một lệnh
   chạy lâu**, đừng gọi lẻ từng lần hỏi trạng thái.
4. Chỉ dùng các trường có trong §5. Google Vids, Google Pics, Meta Muse và Dreamina từ chối giá trị sai bằng `400`
   kèm tên lỗi (§8), không tự đổi về mặc định.

**Mẹo khi chạy cùng máy với app (trường hợp thường gặp)**

- Ảnh / video tham chiếu: gửi `{"path": "D:/duong/dan/anh.png"}` thay vì base64 (§6). Đường dẫn tuyệt đối.
- Viết body JSON ra **file UTF-8** rồi gửi file đó (`curl --data-binary @body.json`, hoặc đọc byte trong PowerShell).
  Nhét JSON có tiếng Việt, dấu nháy vào thẳng dòng lệnh rất dễ hỏng.
- Viết **một script nhỏ dùng lại** (gửi → chờ → tải về, mỗi ảnh / clip một file body) ngay từ đầu, thay vì gõ tay từng
  lệnh. Windows không cần cài gì: mẫu PowerShell ở §10.4; có Python thì §10.2.
- Kết quả đã tải thì đừng tạo lại. Một mục lỗi thì sửa và chạy lại riêng mục đó, không chạy lại cả lô.
- `429` hoặc "No active accounts" = tài khoản của nền tảng đó trong app không chạy được lúc này: báo người dùng, không
  thử lại liên tục. Mỗi nền tảng (Flow, Google, Dreamina, Grok, Meta, ChatGPT) dùng tài khoản riêng do người dùng thêm
  trong app.

**Giữ nhân vật đồng nhất (cơ chế của app, chi tiết ở §6)**

- Ảnh tham chiếu có `name` được gọi trong prompt bằng `@tên`, đặt **trong câu, đúng chỗ của thứ nó vẽ**
  (`"@lan đi qua @cho"`), với model gắn theo `tag` (§6.1). Model gắn theo `position` dùng ảnh theo thứ tự, `@tên`
  không có tác dụng.
- Thư viện nhân vật của app: thêm bằng `POST /api/characters` (§5.8), dùng bằng `@Tên` trong prompt kèm
  `"use_characters": true` (§6.3). Tên trùng trả `409`: chọn tên khác, không ghi đè nhân vật người dùng đã có.
- Video từ ảnh: `mode` `start_image` (ảnh đầu), `start_end_image` (ảnh đầu + ảnh cuối), `components` (ghép từ ảnh
  thành phần). Mode nào có ở model nào xem trong `/api/models` và §5.2.

---

## Bắt đầu nhanh

1. Trong app: tab **Webhook** → **Bật**. Chép lại **cổng** (mặc định `8765`) và **API key**.
2. Kiểm tra máy chủ có trả lời (không cần khoá):
   ```bash
   curl http://127.0.0.1:8765/api/health
   ```
3. Xem các model dùng được, kèm giới hạn của chúng:
   ```bash
   curl http://127.0.0.1:8765/api/models -H "X-API-Key: YOUR_API_KEY"
   ```
4. Yêu cầu tạo một ảnh. Kết quả trả về là `task_id`, chưa phải ảnh:
   ```bash
   curl -X POST http://127.0.0.1:8765/api/image/generate -H "Content-Type: application/json" \
     -H "X-API-Key: YOUR_API_KEY" -d '{"prompt": "a cat wearing sunglasses", "model": "nano_banana_2"}'
   ```
5. Vài giây hỏi trạng thái một lần tới khi `"status": "completed"`, rồi tải từng link trong `results`:
   ```bash
   curl http://127.0.0.1:8765/api/status/<task_id> -H "X-API-Key: YOUR_API_KEY"
   curl -o cat.png "<một link trong results>"
   ```

Đang dùng thư viện hoặc tool OpenAI? Trỏ nó tới `http://127.0.0.1:8765/v1` và đọc §12.
Đọc tiếp: các trường request của từng trang (§5), ảnh tham chiếu và `@tag` (§6), lỗi (§8), ví dụ
đầy đủ bằng cURL / Python / JavaScript (§10).

---

## 1. Tổng quan & khái niệm chính

- **Yêu cầu gói MAX.** Máy chủ Webhook chỉ bật được với license **MAX**.
- **Địa chỉ bind (mặc định loopback).** API chạy ở `http://<host>:<port>`. Mặc định
  `host` là `127.0.0.1` (chỉ máy này). Bạn đổi được trong tab Webhook: đặt `0.0.0.0`
  (mọi interface) hoặc một **IP LAN** cụ thể để máy khác trong mạng truy cập được.
  **Đừng dùng `127.0.0.0`** — đó là địa chỉ *network* của loopback, không client nào
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
- **Hai kiểu API, chung một bộ máy.** Ngoài `/api/*` (gửi → hỏi trạng thái → tải, như trên), máy chủ
  còn nói **chuẩn OpenAI** ở `/v1/*` (§12) - giống API "tương thích OpenAI" của Gemini hay DeepSeek, thư viện
  hoặc tool viết cho OpenAI chỉ cần đổi base URL. Hai kiểu dùng chung hàng chờ, tài khoản và giới hạn.
- **Đồng thời.** Máy chủ nhận nhiều request cùng lúc. Tối đa **10 task được bóc
  tách song song**; còn *chạy tạo* được bao nhiêu cái một lúc thì theo số tài khoản: mọi
  endpoint có tài khoản (Ảnh/Video, Meta AI, OpenAI, Grok, Google Vids, Google Pics, Meta Muse, Dreamina)
  chạy tối đa **số tài khoản dùng được × số việc mỗi tài khoản do máy chủ cấp** (hiện là 5, chỉ
  gói MAX). Grok ở chế độ extension tính là 1 tài khoản. Google Vids, Google Pics, Meta Muse và Dreamina chờ
  slot trống (Meta Muse và Dreamina tối đa 900 giây),
  riêng Upscale chạy **lần lượt từng cái** (chỉ có một GPU — xem §5.6).
- **Giới hạn theo từng tài khoản (từ bản 6.0.0).** Ở mọi endpoint có tài khoản, một tài khoản không bao giờ
  chạy quá số việc mỗi tài khoản do máy chủ cấp (hiện là 5; Grok là 4), kể cả khi chuyển tài khoản để thử lại.
  Tài khoản đã đủ việc thì task sang tài khoản khác còn chỗ; mọi tài khoản dùng được đều đủ việc thì task
  **chờ** chỗ trống. Meta AI và OpenAI chờ tối đa 3 giờ rồi báo `503 NO_FREE_SLOT`;
  Ảnh/Video (Flow) chờ tới khi có chỗ. Trước bản 6.0.0, Ảnh/Video, Meta AI và OpenAI chỉ giới hạn tổng số việc
  rồi chia xoay vòng, nên một tài khoản có thể nhận nhiều hơn phần của nó.
- **Độ trễ giữa các yêu cầu (từ bản 6.0.0).** Tab Webhook có ô **Độ trễ giữa các yêu cầu**: khoảng nghỉ giữa
  hai lần *bắt đầu* liên tiếp của cùng một nền tảng. Các mốc: **Ngay lập tức** (2-3 giây, mặc định),
  `5-10s`, `10-20s`, `20-30s`, `30-60s`, `60-90s`, `90-120s`; mỗi lần nghỉ lấy ngẫu nhiên trong khoảng đã chọn.
  - Áp dụng **riêng cho từng nền tảng** (Ảnh Flow, Video Flow, Meta AI, OpenAI, Grok, Google Vids, Google Pics,
    Meta Muse, Dreamina mỗi nơi một hàng chạy riêng), không áp cho Upscale.
  - Đây là cài đặt trong app, **không phải** trường của request: không có tham số API nào để đổi nó. Lựa chọn
    được lưu và dùng lại ở lần mở app sau.
  - Task đang chờ tới lượt vẫn ở trạng thái `pending`; độ trễ dài + nhiều request dồn thì hàng chờ dài tương
    ứng (ví dụ `90-120s` với 10 request là khoảng 15-20 phút cho request cuối bắt đầu). Hãy đặt thời gian chờ
    phía client cho phù hợp.
  - Đổi lúc đang chạy có hiệu lực với các request đến sau; request đã được hẹn giờ giữ giờ cũ. Riêng Ảnh Flow
    nhận độ trễ mới khi hàng chạy hiện tại xong và hàng mới bắt đầu.
  - **Thời gian chờ chỗ trống theo độ trễ:** các mốc "tối đa 15 phút" (900 giây) nêu ở từng endpoint áp dụng khi
    để **Ngay lập tức**. Chọn độ trễ dài hơn thì task được chờ chỗ tới **3 giờ** trước khi báo
    `503 NO_FREE_SLOT`, vì chỗ trên tài khoản được giữ cả trong lúc nghỉ theo độ trễ.
  - Khi gặp lỗi tạo quá nhanh của Google (`USER_REQUESTS_THROTTLED` / `TOO_MUCH_TRAFFIC`), hãy tăng độ trễ.
  - Trước bản 6.0.0 khoảng nghỉ này cố định 1-3 giây và không chỉnh được.
- **Tạo nội dung dùng tài khoản đã đăng nhập trong app.** Ảnh/Video dùng tài khoản
  Google (Flow/Veo) cấu hình trong app; Grok dùng các tài khoản Grok ở Cài đặt → Grok
  (hoặc tab grok.com qua extension nếu chọn cách chạy Extension, xem §5.3);
  **Meta AI** dùng tài khoản Meta (vibes.ai) đã đăng nhập; **OpenAI (GPT Image)**
  dùng tài khoản ChatGPT/OpenAI đã đăng nhập; **Google Vids** (`omni_vids`) và **Google Pics**
  (`nano_pics`) dùng tài khoản Google ở Cài đặt → Tài khoản Google; **Meta Muse** (`meta_muse`) dùng
  tài khoản Muse ở Cài đặt → Tài khoản Muse (muse.ai, đăng nhập bằng tài khoản Meta); **Dreamina** (`dreamina`) dùng
  tài khoản Dreamina ở Cài đặt → Tài khoản Dreamina (CapCut). Nếu không có tài khoản hợp lệ, task sẽ
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
- Các đường chuẩn OpenAI (`/v1/*`, §12) nhận thêm `Authorization: Bearer <api-key-của-bạn>` - thứ client
  OpenAI gửi - và trả lỗi theo dạng OpenAI:
  `401 {"error": {"message": "Invalid or missing API key", "type": "authentication_error", "code": "invalid_api_key"}}`.

CORS đã bật (`Access-Control-Allow-Origin: *`) và có xử lý preflight `OPTIONS`, nên
client trên trình duyệt cũng dùng được.

---

## 3. Danh sách Endpoint

| Method | Path | Auth | Mục đích |
|--------|------|:----:|----------|
| `GET`  | `/api/health` | ❌ | Tình trạng máy chủ / uptime / số task trong hàng đợi |
| `POST` | `/api/image/generate` | ✅ | Đưa task tạo **ảnh** vào hàng đợi (Flow, Google Pics với `model: "nano_pics"`, Meta Muse với `model: "meta_muse"`, hoặc Dreamina với `model: "dreamina"`) |
| `POST` | `/api/video/generate` | ✅ | Đưa task tạo **video** vào hàng đợi (Veo / Omni Flash / Google Vids, Meta Muse với `model: "meta_muse"`, hoặc Dreamina với `model: "dreamina"`) |
| `POST` | `/api/grok/generate`  | ✅ | Đưa task **Grok** (ảnh/video) vào hàng đợi |
| `POST` | `/api/meta/generate`  | ✅ | Đưa task **Meta AI** (ảnh/video) vào hàng đợi |
| `POST` | `/api/openai/generate` | ✅ | Đưa task **OpenAI GPT Image** vào hàng đợi (model mặc định của máy chủ, hiện là GPT-6 Luna) |
| `POST` | `/api/upscale/generate` | ✅ | Nâng cấp ảnh bằng engine **Real-ESRGAN chạy local** |
| `GET`  | `/api/status/{task_id}` | ✅ | Hỏi trạng thái task; trả kết quả hoặc lỗi |
| `GET`  | `/api/result/{task_id}` | ✅ | Lấy kết quả (chỉ khi đã `completed`) |
| `GET`  | `/api/files/{filename}` | ❌ | Tải file kết quả đã tạo |
| `GET`  | `/api/tasks` | ✅ | Liệt kê 50 task gần nhất |
| `GET`  | `/api/models` | ✅ | **Danh mục model mọi trang** theo dạng OpenAI (cũng là `/v1/models`, `/v1/models/{id}`) - xem §7 |
| `POST` | `/api/stop` | ✅ | **Dừng** mọi task đang chờ / đang chạy — hoặc một task: `/api/stop/{task_id}` hay body `{"task_id": "..."}`. Chỉ cần API key (không kiểm tra gói MAX), nên client luôn huỷ được. |
| `POST` | `/v1/images/generations` | ✅ | Tạo ảnh **theo chuẩn OpenAI** (chờ xong, trả `url` / `b64_json`) - xem §12 |
| `POST` | `/v1/images/edits` | ✅ | Sửa ảnh từ ảnh tham chiếu **theo chuẩn OpenAI** (JSON hoặc multipart) - §12 |
| `POST` | `/v1/videos` | ✅ | Tạo video **theo chuẩn OpenAI** (trả đối tượng video) - §12 |
| `GET`  | `/v1/videos`, `/v1/videos/{id}`, `/v1/videos/{id}/content` | ✅ | Danh sách / trạng thái / tải video **theo chuẩn OpenAI** - §12 |
| `DELETE` | `/v1/videos/{id}` | ✅ | **Chuẩn OpenAI**: dừng video và bỏ khỏi danh sách - §12 |
| `GET`  | `/api/characters` | ✅ | Liệt kê **thư viện nhân vật** (§5.8) |
| `GET`  | `/api/characters/{name}` | ✅ | Một nhân vật (tên không phân biệt hoa thường, mã hoá URL) |
| `GET`  | `/api/characters/{name}/image` | ✅ | Ảnh của nhân vật (cũng cần API key) |
| `POST` | `/api/characters` | ✅ | Thêm nhân vật (tên, ảnh, giọng có sẵn, ghi chú) → `201` |
| `PUT` / `PATCH` | `/api/characters/{name}` | ✅ | Sửa nhân vật: đổi tên (`new_name`), ảnh mới, giọng có sẵn, ghi chú |
| `DELETE` | `/api/characters/{name}` | ✅ | Xoá nhân vật và ảnh của nó |
| `POST` | `/api/characters/preupload` | ✅ | **Upload trước** ảnh nhân vật lên các tài khoản (§5.9) → `202` + `task_id` |
| `POST` | `/api/preupload` | ✅ | **Upload trước** ảnh tham chiếu lên các tài khoản (§5.9) → `202` + `task_id` |

Dấu `/` ở cuối được chấp nhận (vd `/api/health/`).

**Dừng việc đang làm.** Client đổi ý (tạo lại, prompt sai, người dùng bấm huỷ) nên gọi
`POST /api/stop` thay vì để hàng đợi chạy tiếp: mọi task được nhắm tới lỗi ngay với
`error_code 499` / `STOPPED_BY_CLIENT`, việc đang xếp hàng không bao giờ bắt đầu, provider đang
chạy được yêu cầu dừng, và kết quả về sau của một request đã gửi tới provider bị bỏ (request đó
vẫn bị tính phí — một cuộc gọi HTTP không huỷ ngang được).

---

## 4. Quy trình bất đồng bộ (từng bước)

### Bước 1 — Gửi yêu cầu

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

### Bước 2 — Hỏi trạng thái

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

> Khoảng thời gian hỏi đề xuất: mỗi 3–5 giây. Ảnh thường xong trong vài giây tới vài
> phút; video có thể mất vài phút (dịch vụ phía trên có thể xếp hàng). Máy chủ có cơ
> chế watchdog để báo thất bại cho task bị treo quá lâu không có kết quả.

### Bước 3 — Tải kết quả

`results` là mảng URL dạng `http://<host>:<port>/api/files/<tên-đã-url-encode>`.
`<host>` khớp với địa chỉ đã bind của máy chủ, nên client vào bằng IP LAN sẽ nhận link
tải trên đúng IP đó (khi bind `0.0.0.0`, máy chủ tự quảng bá IP LAN chính). `GET` từng
URL (không cần API key) để tải dữ liệu thô. `Content-Type` được đặt theo phần mở rộng
file (`image/png`, `image/jpeg`, `video/mp4`, …). File lưu nội bộ trên máy đang chạy app.

**Trả về bao nhiêu file (và ở độ phân giải nào):**

- **Ảnh, không `upscale`** → 1 file (ảnh gốc).
- **Google Pics** (`nano_pics`) → tối đa `keep` file (mặc định 1; `keep: 0` = mọi ảnh của lượt,
  3–9).
- **Ảnh có `upscale`** → một file **cho mỗi độ phân giải upscale yêu cầu**, theo thứ
  tự tăng dần — vd `["2K"]` → `[2K]`, `["2K","4K"]` → `[2K, 4K]`. Ảnh gốc
  (không upscale) **không** được kèm khi đã yêu cầu `upscale`.
- **Video** → một file **cho mỗi độ phân giải tạo được** — vd `["720p","1080p"]` →
  tối đa 2 file.
- **Grok** → luôn đúng 1 file.
- **Meta AI** → `count` file (1–4): `count` ảnh (một lô) hoặc `count` clip video.
- **OpenAI** (GPT Image) → luôn đúng 1 file.
- **Google Vids** (`omni_vids`) → đúng 1 file ở độ phân giải đã yêu cầu; task `upscale` của
  `omni_vids` → 1 file (clip 1080p).
- **Meta Muse** (`meta_muse`) → `count` file: ảnh (JPG, 1–4) hoặc video (MP4, 1–2); chỉ ít hơn khi
  lượt bị dừng / lỗi sau khi đã lưu được một số file (`meta.partial`).
- **Dreamina** (`dreamina`) → `count` file (ảnh hoặc video, mặc định 1); chỉ ít hơn khi lượt bị dừng /
  lỗi sau khi đã lưu được một số file (`meta.partial`).
- **Upscale** → luôn đúng 1 file (một ảnh vào, một ảnh ra).

(Nên `len(results)` và thứ tự khớp với các độ phân giải bạn yêu cầu.)

---

## 5. Schema body của request

Mọi body đều là JSON. `prompt` là **bắt buộc** cho mọi endpoint tạo nội dung; prompt
rỗng/thiếu sẽ làm task thất bại với lỗi `Missing required field: prompt`. Ngoại lệ duy
nhất là `/api/upscale/generate` (§5.6) — nhận ảnh, không có prompt.

**Trần kích thước body: 50 MB** cho mọi endpoint. Base64 làm dữ liệu nhị phân phình
~4/3, nên một request chứa được khoảng 37 MB dữ liệu ảnh thô. Vượt trần thì chính lệnh
`POST` trả `413` — task không được tạo. Cách hay vấp nhất là nhét nhiều ảnh tham chiếu
lớn vào cùng một request.

### 5.1 Ảnh — `POST /api/image/generate`

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | — | Mô tả ảnh. |
| `model` | string | ❌ | `nano_banana_2` | Một trong `nano_banana_pro`, `nano_banana_2`, `nano_banana_2_lite`, `nano_pics`, `meta_muse`, `dreamina`. Không hợp lệ → `nano_banana_2`. **`nano_pics`** = Google Pics, có trường riêng (`mode`, `keep`, `remove_logo`) và kiểm tra chặt — xem ghi chú Google Pics bên dưới. **`meta_muse`** = Meta Muse, có trường riêng (`mode`, `count`) và kiểm tra chặt - xem ghi chú Meta Muse bên dưới. **`dreamina`** = Dreamina (CapCut), có trường riêng (`dreamina_model`, `mode`, `resolution`, `count`, `quality`) - xem ghi chú Dreamina bên dưới. Danh sách sống kèm giới hạn từng model: `GET /v1/models` (§5.7). |
| `aspect_ratio` | string | ❌ | `1:1` | Một trong `1:1`, `3:4`, `4:3`, `9:16`, `16:9`. Không hợp lệ → `1:1`. |
| `reference_images` | array | ❌ | `[]` | Tối đa **10** ảnh base64 (xem §6). Mỗi ảnh có thể kèm `name` để gắn theo `@tên` trong prompt (§6.1). |
| `upscale` | array | ❌ | `[]` | Bất kỳ `"2K"`, `"4K"`. **4K cần tài khoản ULTRA** và model hỗ trợ upscale. Giá trị sai bị bỏ. |
| `use_characters` | bool | ❌ | (công tắc app) | Dùng (`true`) hay bỏ qua (`false`) **thư viện nhân vật** cho **riêng task này** - công tắc Nhân vật chung của app không đổi, task khác / lượt chạy trong app không bị ảnh hưởng. Không gửi hoặc `null` → theo công tắc (như trước khi có trường này). Riêng `nano_pics` và `meta_muse` chỉ dùng nhân vật khi gửi **rõ `true`** - công tắc app không áp dụng cho hai model này (§6.3). Không phải boolean → `400 INVALID_FIELD`. |
| `auto_fix_prompt` | bool | ❌ | `true` | Máy chủ chặn yêu cầu vì **prompt** (người nổi tiếng, nội dung nhạy cảm, trẻ em, bản quyền...) thì app nhờ LLM viết lại rồi chạy lại, tối đa 2 lần, task vẫn `running` (chỉ model Flow; cần gói PLUS+ và bật Cài đặt → Trợ lý LLM). **Ảnh tham chiếu / ảnh đầu vào** bị chặn thì không sửa. `false` → báo lỗi 400 gốc ngay (cho client tự viết lại prompt). Task đã được sửa có thêm `prompt_rewrites`, `original_prompt`, `final_prompt` trong `/api/status` và `/api/result` (`prompt` vẫn là prompt bạn gửi). Không phải boolean → `400 INVALID_FIELD`. |

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
> báo **failed** kèm lý do — **không** âm thầm trả về ảnh gốc độ phân giải thấp hơn.

> **Tự đổi model khi hết giới hạn (Flow: `nano_banana_pro`, `nano_banana_2`, `nano_banana_2_lite`)** - khi bật công
> tắc "Tự đổi model khi hết giới hạn" (trang Flow Ảnh → Cấu hình nâng cao; áp dụng cho cả Webhook): nếu model của
> request đã hết giới hạn ngày trên mọi tài khoản, app tự tạo bằng model thuộc hạn mức khác (Nano Banana Pro ⇄
> Nano Banana 2.1; Nano Banana 2 Lite → Nano Banana Pro) thay vì trả `429`. Khi đó phản hồi trạng thái có thêm
> `meta`: `{"model": "<model thật đã tạo>", "model_requested": "<model bạn gửi>", "model_fallback": true}`. Không đổi
> model thì không có `meta`. Mọi hạn mức đều hết → `429` như trước. Tắt công tắc → luôn dùng đúng model của request.

> **Google Pics (`model: "nano_pics"`)** — trình tạo ảnh của Google (docs.google.com/images), chạy
> bằng **tài khoản Google** ở Cài đặt → Tài khoản Google (cùng tài khoản với Google Vids; gói
> PLUS/MAX). Cùng endpoint, có trường và quy tắc riêng:
> - `mode` (không phân biệt hoa thường, không bắt buộc): `text_to_image` hoặc `image_to_image`
>   (bí danh `t2i` / `i2i`). Bỏ trống → `image_to_image` nếu có gửi `reference_images`, ngược lại
>   `text_to_image`. Giá trị khác → `400 INVALID_MODE`; `image_to_image` mà không có ảnh →
>   `400 MISSING_REFERENCE`; `text_to_image` bỏ qua mọi ảnh gửi kèm.
> - `reference_images`: **1–14** ảnh (base64 hoặc `path`, §6), theo vị trí — Google Pics **không
>   có** gắn `@tag`, `name` / `category` bị bỏ qua. Vượt giới hạn máy chủ (14) →
>   `400 TOO_MANY_REFERENCES` (không bao giờ lặng lẽ cắt bớt).
> - **Nhân vật trong thư viện** (chỉ khi yêu cầu gửi `use_characters: true` - riêng công tắc app không
>   áp dụng ở đây): mọi nhân vật mà prompt nhắc tới - cùng luật với trang Google Pics: tên nhân vật
>   đóng vai tên file trong tự động gán ảnh, theo chế độ khớp chung (Cài đặt chung) - được thêm làm
>   ảnh tham chiếu **sau ảnh của bạn**, chỉ vào các ô còn trống (không bao giờ vượt 14, không bao giờ
>   gây `TOO_MANY_REFERENCES`). Ảnh **bạn gửi** có `name` (tên file) trùng tên nhân vật được ưu tiên.
>   Không gửi `mode` mà có nhân vật khớp → thành `image_to_image`; `text_to_image` gửi rõ thì không
>   bao giờ thêm nhân vật.
> - `aspect_ratio`: một giá trị trong danh sách máy chủ — hiện là `16:9, 9:16, 1:1, 4:3, 3:4, 3:2,
>   2:3, 5:4, 4:5, 21:9` (bảng model ở tab Webhook hiện danh sách đang dùng). Mặc định `1:1`. Giá
>   trị khác → `400 INVALID_ASPECT_RATIO` (không tự đổi về mặc định như các model Flow).
> - `keep`: số ảnh của lượt cần trả về. Google trả **3–9 ảnh mỗi lượt**; `keep` là số nguyên, một
>   trong `1`, `2`, `3`, `4` hoặc `0` (= mọi ảnh của lượt). Bỏ trống hoặc `null` → `1`. Giá trị
>   khác (kể cả `true`, `2.7` hay chuỗi `"2"`) → `400 INVALID_KEEP`.
> - `remove_logo`: `true` xoá logo ✦ Gemini khỏi mọi ảnh (khôi phục điểm ảnh sạch, không làm mờ);
>   `false` giữ nguyên ảnh như Google tạo. **Không gửi** (hoặc `null`) → theo nút **"Hiển thị logo
>   Gemini"** của trang Google Pics (mặc định nút tắt = xoá). Không phải boolean → `400 INVALID_FIELD`.
> - Không hỗ trợ `upscale` (bị bỏ qua).
> - **Hạn mức:** một task = **một lượt = 1 đơn vị** hạn mức Pics của tài khoản, bất kể ra bao nhiêu
>   ảnh. Hạn mức đọc thật từ Google (còn / tổng), tách riêng với số giây của Vids.
> - **Tài khoản:** chỉ dùng tài khoản đang **BẬT** và đang tích ô **Ảnh** ở Cài đặt → Tài khoản
>   Google, còn ít nhất 1 lượt Pics (tài khoản chưa từng đọc hạn mức vẫn được thử — việc sẽ đọc
>   trước khi tạo). Mỗi tài khoản nhận tối đa số việc đồng thời máy chủ cấp. Xoay vòng round-robin,
>   lỗi auth / hạn mức / giới hạn tốc độ / máy chủ, hoặc tài khoản không dùng được Google Pics thì
>   chuyển sang tài khoản kế; cookie chết được làm mới từ profile trước. Cookie không làm mới được
>   thì tài khoản bị **TẮT** (cả cho Vids). Tài khoản cookie vẫn sống nhưng không có Google Pics (bị
>   từ chối ngay cả khi vừa làm mới cookie) chỉ bị **bỏ qua** — không bao giờ bị tắt. Hết lượt Pics
>   cũng **không** tắt tài khoản: khi bật *Tự động tắt tài khoản bị hết giới hạn* chỉ ô **Ảnh** bị
>   bỏ tích; qua mốc reset hạn mức Pics thì tài khoản được thử lại và ô được tích lại — Google Vids
>   vẫn dùng tiếp suốt thời gian đó. Khi mọi tài khoản dùng được đều bận, task trở về `pending` và
>   **chờ** slot trống (tối đa 15 phút), kể cả sau khi đã chuyển tài khoản.
> - **Kết quả:** `results` = các ảnh được giữ (PNG), tối đa `keep` file (ít hơn nếu có ảnh tải
>   lỗi). Task hoàn thành có thêm `meta`: `mode` (`t2i` / `i2i`), `aspect_ratio`, `images` (số file
>   trả về), `logo_removed` (số ảnh thực sự đã được xoá logo Gemini — `0` khi `remove_logo: false`),
>   `account` (email tài khoản Google) và `partial: true` khi lượt bị dừng
>   / lỗi sau khi đã lưu được một số ảnh.
> - Prompt bị từ chối → `400 CONTENT_POLICY` (không tốn hạn mức, không thử lại trên tài khoản khác).

Ví dụ Google Pics — ảnh sang ảnh, 16:9, giữ 2 ảnh:

```json
{
  "prompt": "the same girl reading in a cozy cafe",
  "model": "nano_pics",
  "aspect_ratio": "16:9",
  "keep": 2,
  "reference_images": ["data:image/png;base64,..."]
}
```

> **Meta Muse (`model: "meta_muse"`)** - Muse của Meta (muse.ai), chạy bằng **tài khoản Muse** ở
> Cài đặt → Tài khoản Muse (đăng nhập bằng tài khoản Meta; gói PLUS/MAX). Cùng endpoint, có trường
> và quy tắc riêng. Muse là một AI agent: prompt được gửi nguyên văn, còn các tuỳ chọn bên dưới
> được chuyển thành lời trong yêu cầu.
> - `mode` (không phân biệt hoa thường, không bắt buộc): `text_to_image` hoặc `image_to_image`
>   (bí danh `t2i` / `i2i`). Bỏ trống → `image_to_image` nếu có gửi `reference_images`, ngược lại
>   `text_to_image`. Giá trị khác → `400 INVALID_MODE`; `image_to_image` mà không có ảnh →
>   `400 MISSING_REFERENCE`; `text_to_image` bỏ qua mọi ảnh gửi kèm.
> - `reference_images`: **1–14** ảnh (base64 hoặc `path`, §6), theo vị trí - Meta Muse **không
>   có** gắn `@tag`, `name` / `category` bị bỏ qua. Vượt giới hạn máy chủ (14) →
>   `400 TOO_MANY_REFERENCES` (không bao giờ lặng lẽ cắt bớt).
> - **Nhân vật trong thư viện**: cùng luật với Google Pics ở trên (khớp như trang Meta Muse, chỉ vào
>   ô trống, ảnh bạn gửi cùng tên được ưu tiên, không gửi `mode` → `image_to_image` khi có nhân vật
>   khớp, không bao giờ với `text_to_image`). Áp dụng cả `image_to_video` trên `/api/video/generate`
>   (trong giới hạn ảnh của video).
> - `aspect_ratio`: một giá trị trong danh sách máy chủ - hiện là `1:1, 16:9, 9:16, 4:3, 3:4, 3:2,
>   2:3, 21:9, 5:4, 4:5` (bảng model ở tab Webhook hiện danh sách đang dùng). Mặc định `1:1`. Giá
>   trị khác → `400 INVALID_ASPECT_RATIO` (không tự đổi về mặc định).
> - `count`: số ảnh mỗi prompt, số nguyên trong danh sách máy chủ - hiện là `1`, `2`, `3`, `4`.
>   Bỏ trống → `1`. Nhận cả bí danh `num_images`. Giá trị khác (kể cả `true` hay chuỗi `"2"`) →
>   `400 INVALID_COUNT`.
> - Không hỗ trợ `upscale` và `remove_logo` (bị bỏ qua) - ảnh Muse không có logo.
> - **Hạn mức:** token Muse của tài khoản (dùng gói theo tuần trước, sau đó tới token mua thêm).
> - **Tài khoản:** chỉ dùng tài khoản đang bật ở Cài đặt → Tài khoản Muse và còn hạn mức. Mỗi tài
>   khoản nhận tối đa số việc đồng thời máy chủ cấp (hiện là 5). Xoay vòng round-robin, lỗi auth /
>   hạn mức / bị vô hiệu / lỗi tạm thời thì chuyển sang tài khoản kế chưa thử cho task này. Khi mọi
>   tài khoản dùng được đều bận, task **chờ** slot trống (tối đa 15 phút), quá thời gian thì lỗi
>   `503 NO_FREE_SLOT`.
> - **Kết quả:** `results` = `count` ảnh (JPG). Task hoàn thành có thêm `meta`: `mode`
>   (`t2i` / `i2i`), `aspect_ratio`, `count` (số file trả về), `account` (tài khoản Muse đã tạo ảnh)
>   và `partial: true` khi lượt bị dừng / lỗi sau khi đã lưu được một số ảnh.
> - Các danh sách của máy chủ (tỉ lệ, số lượng, số ảnh tham chiếu tối đa) có thể thay đổi; bảng
>   model ở tab Webhook hiện giá trị đang dùng.

Ví dụ Meta Muse - ảnh sang ảnh, 16:9, 2 ảnh:

```json
{
  "prompt": "the same girl reading in a cozy cafe",
  "model": "meta_muse",
  "mode": "image_to_image",
  "aspect_ratio": "16:9",
  "count": 2,
  "reference_images": ["data:image/png;base64,..."]
}
```

> **Dreamina (`model: "dreamina"`)** - Dreamina của CapCut, chạy bằng **tài khoản Dreamina** ở
> Cài đặt → Tài khoản Dreamina (gói PLUS/MAX). Cùng endpoint, có trường và quy tắc riêng; mọi lựa
> chọn được kiểm theo đúng danh sách của model trên Dreamina (giá trị không có → `400`, không tự đổi).
> - `dreamina_model` (không bắt buộc): khoá model Dreamina (vd `high_aes_general_v50`) hoặc tên hiển
>   thị (vd `Seedream 5.0 Lite`). Bỏ trống → model đầu tiên hỗ trợ chế độ. Không có / không hợp chế
>   độ → `400 INVALID_MODEL` (lỗi liệt kê các khoá dùng được).
> - `mode`: `text_to_image` hoặc `image_to_image` (bí danh `t2i` / `i2i` / `reference`). Bỏ trống →
>   `image_to_image` nếu có ảnh tham chiếu (hoặc prompt `@` gọi tên nhân vật thư viện), ngược lại
>   `text_to_image`. `text_to_image` bỏ qua ảnh gửi kèm.
> - `reference_images`: ảnh tham chiếu, tối đa theo model (GPT Image 16, Nano Banana 14, Seedream 5.0
>   Pro / Flash 10, Seedream 5.0 Lite 6 ...). Có `@tag`: `@luna` trong prompt trỏ tới ảnh có
>   `"name": "luna"` (§6.1). Với `{"path": ...}` thì tên `@` là tên của chính file và `name` bị bỏ
>   qua; `name` chỉ áp dụng cho phần tử base64 / `data`. Quá trần → `400 TOO_MANY_REFERENCES`.
> - `aspect_ratio` (mặc định `1:1`), `resolution` (vd `1k` / `2k` / `4k`, mặc định `2k`), `count`
>   (số ảnh, theo danh sách của model, mặc định `1`), `quality` (chỉ model GPT Image: `low` /
>   `medium` / `high` ...). Sai → `400 INVALID_ASPECT_RATIO` / `INVALID_RESOLUTION` / `INVALID_COUNT`
>   / `INVALID_QUALITY`.
> - Tên trường thay thế cũng được nhận: `model_key` = `dreamina_model`, `num_images` = `count`.
> - **Tài khoản:** tài khoản Dreamina đang bật (cột Ảnh bật) và chưa hết credit; trần số việc mỗi tài
>   khoản do máy chủ cấp; xoay vòng; cookie hết hạn / hết credit trước khi tạo ra file thì chuyển sang
>   tài khoản kế; mọi tài khoản bận thì chờ slot tối đa 15 phút (`503 NO_FREE_SLOT`).
> - **Kết quả:** `results` = các ảnh; `meta`: `mode` (`img_t2i` / `img_ref`), `model`, `aspect_ratio`,
>   `resolution`, `count`, `account`, `partial`.

Ví dụ Dreamina - ảnh tham chiếu có `@tag`:

```json
{
  "prompt": "@luna reading in a cozy cafe",
  "model": "dreamina",
  "aspect_ratio": "16:9",
  "resolution": "2k",
  "reference_images": [{"data": "data:image/png;base64,...", "name": "luna"}]
}
```

### 5.2 Video — `POST /api/video/generate`

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | — | Mô tả chuyển động / khung cảnh. Chỉ không bắt buộc với request `upscale` của `omni_vids`. |
| `model` | string | ✅ | — | Một trong `veo_31_lite`, `veo_31_lite_relaxed`, `omni_flash_12`, `veo_31_fast`, `veo_31_quality`, `omni_flash`, `omni_vids`, `meta_muse`, `dreamina`. Thiếu → `400 MISSING_MODEL`; tên Veo lạ → model mặc định của máy chủ (`veo_31_fast`; từ 05/12/2026 là `veo_31_lite`). **Model Google đã tắt** (từ 05/12/2026: `veo_31_fast`, `veo_31_quality` → dùng `veo_31_lite`; `omni_flash` → dùng `omni_flash_12`) trả `400 MODEL_RETIRED` kèm tên id thay thế. **`omni_vids`** = Google Vids (xem ghi chú Google Vids bên dưới). **`meta_muse`** = Meta Muse (xem ghi chú Meta Muse bên dưới). **`dreamina`** = Dreamina, nhận thêm `reference_videos` / `reference_audios` ở chế độ `omni` (xem ghi chú Dreamina bên dưới). `veo_31_lite_relaxed` cần tài khoản **ULTRA**. **`omni_flash`** / **`omni_flash_12`**: xem ghi chú `mode`. Danh sách sống kèm giới hạn từng model: `GET /v1/models` (§5.7). |
| `aspect_ratio` | string | ❌ | `16:9` | `16:9` hoặc `9:16`. |
| `mode` | string | ❌ | `text_to_video` | `text_to_video` (0 ảnh) · `start_image` (1 ảnh) · `start_end_image` (2 ảnh: khung đầu + khung cuối) · `components` (Veo tối đa 3 ảnh, Omni Flash tối đa 7; hỗ trợ `voice` và `reference_video`). **Mọi mode dùng được cho cả Veo lẫn Omni Flash** (`start_end_image` của Omni Flash cần server config có mapping `i2v_end` — thiếu sẽ bị từ chối kèm lý do rõ). |
| `reference_images` | array | ❌ | `[]` | Tối đa **3** ảnh base64 (Veo); **Omni Flash `components` tối đa 7** (có `reference_video` thì tối đa **5**). **Bắt buộc khi `mode != text_to_video`** — riêng `components` có thể thay bằng `reference_video`, hoặc chỉ `@Tên` của nhân vật trong thư viện khi đang dùng nhân vật (§6.3). Mỗi ảnh có thể kèm `name` để gắn theo `@tên` trong prompt — Veo (§6.1). |
| `reference_video` | string/object | ❌ | — | **Chỉ Omni Flash + mode `components`** — luồng **edit video**: clip (≤ **10s**; Omni Flash 1.2 ≤ **15s**) được dựng lại theo prompt, có thể kèm tối đa 5 ảnh thành phần. Nhận chuỗi base64/data-URI (`data:video/mp4;base64,...`) hoặc `{"path": "...", "name": "..."}` (file có sẵn trên máy chạy app). Luôn xuất **720p** (không dùng cùng `"360p"`). Clip dài quá mức (10s, Omni Flash 1.2 là 15s) bị từ chối — cắt trước khi gửi. |
| `resolution` | array | ❌ | `["720p"]` | Bất kỳ `"360p"`, `"720p"`, `"1080p"`, `"4K"`. **`360p` chỉ có ở Omni Flash** (server config quyết định) — bản gốc tạo ở 360p, rẻ credit hơn; **nguồn 360p chỉ upscale được lên 720p** nên tổ hợp hợp lệ là `["360p"]` hoặc `["360p", "720p"]` (kèm `1080p`/`4K` sẽ bị từ chối). `1080p`/`4K` tạo bằng upscale từ nguồn 720p; **chỉ `4K` cần tài khoản ULTRA**. Giá trị sai → `720p`. Mỗi độ phân giải tạo ra một file: `results` trả **mọi** độ phân giải đã yêu cầu theo thứ tự xử lý (trước 07/10/2026 chỉ trả file của độ phân giải cuối). |
| `voice` | string | ❌ | `""` | Tên giọng (chữ thường). Chỉ dùng ở mode `components`. |
| `video_length` | int | ❌ | (mặc định model) | Độ dài clip (giây). Veo: `4`/`6`/`8`; Omni Flash: `4`/`6`/`8`/`10`; Omni Flash 1.2: `3`–`15` (`11`–`15` cần gói Google AI trả phí; `start_end_image` quá 10s thì chỉ dùng ảnh đầu, giống web Flow). Mode `components` của Veo chỉ chạy `8` (giá trị khác → 8s). Giá trị không hỗ trợ → dùng mặc định (8s). **Veo `4`/`6` cần tài khoản ULTRA** (Omni Flash không cần); không có tài khoản ULTRA (Veo `4`/`6`) hoặc không có tài khoản trả phí (Omni Flash 1.2 `11`–`15`) → dùng mặc định 8s. Luồng edit (`reference_video`) bỏ qua trường này — độ dài theo clip gốc. |
| `remove_logo` | bool | ❌ | (theo công tắc trang Flow Video) | Xoá logo khỏi video tạo bằng tài khoản **Pro/Free**: chữ "Veo" (Veo) hoặc dấu ✦ (Omni Flash), cho 720p và 1080p (360p / 4K giữ nguyên). `true` xoá, `false` giữ; không gửi → theo công tắc "Hiển thị logo Veo / Gemini" của trang Flow Video (tắt = xoá) **và** công tắc tổng "Tự động xoá logo khi tải video" (tab Xoá logo video; tắt = không xoá). `true` gửi rõ thì xoá dù công tắc tổng tắt. Tài khoản **ULTRA**: khi không gửi, Google tắt logo tận gốc theo công tắc đó (app không xử lý thêm); gửi `true` thì app vẫn kiểm tra và xoá nếu video còn logo. Sai kiểu → `400 INVALID_FIELD`. Các video xoá logo chạy lần lượt từng cái (thêm ~1–4 giây/video). |
| `use_characters` | bool | ❌ | (công tắc app) | Dùng / bỏ qua **thư viện nhân vật** cho riêng task này (Veo, Omni Flash, `omni_vids`, `meta_muse`, `dreamina`) - xem §5.1 và §6.3. Dreamina theo công tắc app khi không gửi trường này (không cần `true` rõ ràng, khác `meta_muse`); `false` tắt cho riêng tác vụ đó. Không phải boolean → `400 INVALID_FIELD`. |
| `auto_fix_prompt` | bool | ❌ | `true` | Máy chủ chặn yêu cầu vì **prompt** (người nổi tiếng, nội dung nhạy cảm, trẻ em, bản quyền...) thì app nhờ LLM viết lại rồi chạy lại, tối đa 2 lần, task vẫn `running` (chỉ model Flow; cần gói PLUS+ và bật Cài đặt → Trợ lý LLM). **Ảnh tham chiếu / ảnh đầu vào** bị chặn thì không sửa. `false` → báo lỗi 400 gốc ngay (cho client tự viết lại prompt). Task đã được sửa có thêm `prompt_rewrites`, `original_prompt`, `final_prompt` trong `/api/status` và `/api/result` (`prompt` vẫn là prompt bạn gửi). Không phải boolean → `400 INVALID_FIELD`. |

```json
{
  "prompt": "water flowing over rocks, cinematic",
  "model": "veo_31_lite",
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
> `text_to_video` (bỏ qua ảnh tham chiếu). Giá trị phân biệt hoa thường: `"Components"` hay
> `"START_IMAGE"` là mode lạ và chạy như `text_to_video` - hãy gửi chữ thường. Chỉ `components` đọc trường `voice`
> (Veo tối đa 3 ảnh tham chiếu, Omni Flash tối đa 7). **Riêng `omni_vids`** kiểm tra chặt
> `mode`, `resolution`, `video_length`, `aspect_ratio` và trả `400` kèm tên lỗi (xem ghi chú Google Vids).
>
> **Dùng được cả Veo lẫn Omni Flash.** Omni Flash (`model: "omni_flash"` hoặc `"omni_flash_12"`) hỗ trợ
> đủ `text_to_video`, `start_image`, `start_end_image`, `components` — và riêng nó
> có thêm: mốc `video_length` **10s** (Omni Flash 1.2: **3–15s**), độ phân giải **360p**, và luồng **edit video**
> (`reference_video` trong mode `components`). Nó không cần tài khoản ULTRA.
>
> `resolution` có thể liệt kê nhiều giá trị; mỗi giá trị được tạo nếu hạng tài khoản
> cho phép.

Ví dụ Omni Flash 1.2 — khung đầu + khung cuối, bản nháp 360p:

```json
{
  "prompt": "animate",
  "model": "omni_flash_12",
  "mode": "start_end_image",
  "reference_images": ["data:image/png;base64,...", "data:image/png;base64,..."],
  "resolution": ["360p"]
}
```

Ví dụ Omni Flash 1.2 — edit video (dựng lại clip ≤15s theo prompt):

```json
{
  "prompt": "make it snow heavily",
  "model": "omni_flash_12",
  "mode": "components",
  "reference_video": "data:video/mp4;base64,...",
  "reference_images": ["data:image/png;base64,..."]
}
```

> **Google Vids (`model: "omni_vids"`)** chạy bằng tài khoản Google thêm ở Cài đặt → Tài khoản Google
> (gói PLUS/MAX). Cùng dạng request với Veo, với các quy tắc:
> - `mode` (không phân biệt hoa thường): `text_to_video` (không ảnh, mặc định), `start_image`
>   (1 ảnh = khung hình đầu; ảnh thừa bị bỏ qua), `components` (1–3 ảnh làm nguyên liệu),
>   `video_to_video` (xem dưới) hoặc `upscale` (xem dưới). Nhận cả tên tắt `t2v` / `i2v` / `r2v` / `v2v`. Giá trị khác — kể cả
>   `start_end_image` → `400 INVALID_MODE`.
> - `resolution`: **một** giá trị trong danh sách máy chủ (hiện `720p` / `1080p`), chuỗi hoặc list một
>   phần tử — tạo thẳng, không qua bước upscale. Bỏ trống → giá trị đầu tiên của danh sách máy chủ.
>   Hai giá trị, `360p`, `4K` hay giá trị lạ → `400 INVALID_RESOLUTION`.
> - `video_length`: số nguyên **3–15** giây (mặc định 5); 1 giây video trừ 1 giây hạn mức tài khoản.
>   Ngoài khoảng → `400 INVALID_VIDEO_LENGTH`.
> - `orientation` (`landscape` / `portrait`) hoặc `aspect_ratio` (`16:9` / `9:16`); gửi cả hai thì
>   `orientation` được ưu tiên. Mặc định `16:9`. Giá trị khác → `400 INVALID_ASPECT_RATIO`.
> - `reference_video` chỉ dùng với mode `video_to_video`; mode khác → `400 INVALID_FIELD`. `voice` và `category` bị bỏ qua.
> - **Video → Video** (`"mode": "video_to_video"`): biến đổi một video có sẵn theo prompt (đổi phong cách, thêm
>   nhân vật, đổi bối cảnh), giữ chuyển động gốc. **Chỉ chạy bằng giây gói trả phí** của Google Vids - tài khoản
>   miễn phí không có chế độ này nên bị bỏ qua; không còn tài khoản trả phí đủ giây → `503 NO_VIDS_PAID_ACCOUNT`.
>   - `reference_video` (bắt buộc): 1 video `mp4` / `m4v` / `mov` / `webm`, base64 / data-URI hoặc
>     `{"path": "..."}` trên máy chạy app; tối đa **10 giây** (trần máy chủ) - dài hơn → `400 VIDEO_TOO_LONG`,
>     thiếu → `400 MISSING_REFERENCE`, đuôi khác → `400 INVALID_VIDEO_FORMAT`, không đọc được → `400 BAD_VIDEO`.
>   - Clip ra **dài bằng video nguồn**, cùng hướng với video nguồn, và trừ đúng số giây đó (`video_length` /
>     `aspect_ratio` không dùng). `resolution` như các mode khác.
>   - `reference_images` (tuỳ chọn): tối đa 3 ảnh thành phần, gọi bằng `@tên` như `components` (kể cả nhân vật thư viện).
> - Ở mode `components`, đặt `"name"` cho từng ảnh và viết `@tên` trong prompt để đặt ảnh đúng vị trí
>   (`"@luna gặp @grandpa"`); ảnh không được @ vẫn được gửi kèm ở đầu. **Nhân vật trong thư viện**
>   (Cài đặt → Nhân vật) gọi được cùng cách — `@Anna` thêm ảnh của nhân vật làm nguyên liệu
>   (Google Vids chỉ đồng nhất hình ảnh — không đồng nhất giọng nói). Quy tắc: phải đang dùng nhân
>   vật (công tắc Nhân vật, hoặc `use_characters: true` cho task này; `false` thì tắt cho task đó); tag phải là **đúng tên đầy đủ** của nhân vật (không phân biệt hoa thường); nhân
>   vật chỉ được thêm khi request còn dưới 3 ảnh; ảnh **bạn gửi** có cùng `name` được ưu tiên hơn
>   nhân vật. Tổng tối đa 3 nguyên liệu; không có nguyên liệu nào → `400 MISSING_REFERENCE`.
> - **Tài khoản:** chỉ dùng tài khoản đang **BẬT** ở Cài đặt → Tài khoản Google (và đang tích ô Video) và còn ít
>   nhất `video_length` giây; mỗi tài khoản nhận tối đa số việc đồng thời máy chủ cấp, và số giây
>   được giữ chỗ trong lúc việc chạy. Xoay vòng round-robin, lỗi auth / hạn mức / giới hạn tốc độ /
>   máy chủ thì chuyển sang tài khoản kế; cookie chết được làm mới từ profile trước. Tài khoản không
>   làm mới được cookie bị **TẮT** trong app; tài khoản hết giây chỉ bị bỏ tích ô **Video** (khi bật
>   *Tự động tắt tài khoản bị hết giới hạn*) — Google Pics vẫn dùng tiếp (giống trang Vids). Khi mọi tài
>   khoản dùng được đều bận, task giữ trạng thái `pending` và **chờ** slot trống (tối đa 15 phút)
>   thay vì lỗi.
> - **Kết quả:** task hoàn thành có thêm `meta` trong `GET /api/status/{task_id}` và
>   `GET /api/result/{task_id}`:
>   `mode` (`t2v` / `i2v` / `r2v` / `v2v` / `upscale`), `resolution` (`720p` / `1080p`), `orientation`
>   (`landscape` / `portrait`), `duration` (giây), `account` (email tài khoản Google Vids đã tạo
>   clip), `clip_temp_id` (id mà request upscale cần), `upscale_available` (`true` khi clip
>   còn nâng phân giải được — chưa phải 1080p) và `logo_removed` (`true` khi logo ✦ Gemini đã
>   được xoá khỏi file trả về).
> - `remove_logo` (tuỳ chọn, cả request tạo lẫn `upscale`): `true` xoá logo ✦ Gemini khỏi video
>   (720p / 1080p; bản 1080p là bản nâng cấp nên đôi khi còn vết rất mờ trên nền nhiều vân);
>   `false` giữ nguyên video như Google tạo. **Không gửi** (hoặc `null`) → theo nút **"Hiển thị
>   logo Gemini"** của trang Google Vids (mặc định nút tắt = xoá) **và** công tắc tổng **"Tự động xoá logo khi
>   tải video"** ở tab Công cụ Video → Xoá logo video (tắt công tắc tổng = không xoá). Không phải boolean →
>   `400 INVALID_FIELD`. Video không có logo, hoặc xoá lỗi, được trả nguyên bản (`logo_removed: false`).
> - **Upscale:** `{"model": "omni_vids", "mode": "upscale", "clip_temp_id": "<meta.clip_temp_id>"}`
>   (không cần `prompt`) tạo bản 1080p của clip do **một task webhook `omni_vids` đã hoàn thành
>   trong cùng phiên chạy app** tạo ra — clip tạo ở trang Vids không dùng được. Chỉ chạy trên đúng
>   tài khoản đã tạo clip, giữ nguyên độ dài và hướng, không bao giờ chuyển sang tài khoản khác
>   (tài khoản đó đang bận thì task chờ). Kết quả là một task mới với file riêng. Id lạ →
>   `400 UNKNOWN_CLIP`, đã 1080p → `400 ALREADY_UPSCALED`, tài khoản đó đang tắt hoặc đã lỗi →
>   `409 CLIP_ACCOUNT_UNAVAILABLE`, clip đã hết hạn phía Google → `400 CLIP_GONE`.

Ví dụ Google Vids — thành phần với @tên:

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

Ví dụ Google Vids - video → video (tài khoản trả phí, video nguồn ≤ 10 giây):

```json
{
  "prompt": "@luna đi cạnh chú chó, phong cách tranh màu nước",
  "model": "omni_vids",
  "mode": "video_to_video",
  "resolution": ["720p"],
  "reference_video": {"path": "D:/clips/dog.mp4"},
  "reference_images": [{"data": "data:image/png;base64,...", "name": "luna"}]
}
```

Ví dụ Google Vids — nâng phân giải clip của một task đã xong:

```json
{
  "model": "omni_vids",
  "mode": "upscale",
  "clip_temp_id": "ABCD...WXYZ"
}
```

> **Meta Muse (`model: "meta_muse"`)** chạy bằng tài khoản Muse thêm ở Cài đặt → Tài khoản Muse
> (đăng nhập bằng tài khoản Meta; gói PLUS/MAX) - cùng model `meta_muse` như ở `/api/image/generate`.
> Muse là một AI agent: prompt được gửi nguyên văn, còn các tuỳ chọn bên dưới được chuyển thành lời
> trong yêu cầu.
> - `mode` (không phân biệt hoa thường): `text_to_video` hoặc `image_to_video` (bí danh `t2v` /
>   `i2v`; `start_image` được hiểu là `image_to_video`). Bỏ trống → `image_to_video` nếu có gửi
>   `reference_images`, ngược lại `text_to_video`. Giá trị khác → `400 INVALID_MODE`;
>   `image_to_video` mà không có ảnh → `400 MISSING_REFERENCE`; `text_to_video` bỏ qua mọi ảnh gửi
>   kèm.
> - `reference_images` (`image_to_video`): **1** ảnh = khung hình đầu; **từ 2** ảnh = ảnh tham chiếu
>   (nhân vật / đồ vật / bối cảnh), tối đa theo trần máy chủ (hiện **7**). Theo vị trí, không có
>   `@tag`. Quá trần → `400 TOO_MANY_REFERENCES`.
> - `aspect_ratio`: một giá trị trong danh sách máy chủ - hiện là `16:9, 9:16, 1:1, 4:3, 3:4, 21:9`.
>   Mặc định `16:9`. Giá trị khác → `400 INVALID_ASPECT_RATIO`.
> - `count`: số video mỗi prompt, `1` hoặc `2` (mặc định `1`). Giá trị khác → `400 INVALID_COUNT`.
> - `video_length` (không bắt buộc): số giây nguyên, **1–60**; được thêm vào yêu cầu dưới dạng
>   `"N second video."`. Cũng có thể ghi thẳng độ dài trong prompt (`"an 8 second video ..."`).
>   Không phải số nguyên hoặc ngoài khoảng → `400 INVALID_VIDEO_LENGTH`.
> - `meta_muse` không hỗ trợ: `resolution`, `voice`, `reference_video`, `remove_logo`, `upscale`
>   (bị bỏ qua).
> - **Tài khoản / hạn mức:** giống bên ảnh (ghi chú Meta Muse ở §5.1): tài khoản Muse đang bật còn
>   hạn mức, xoay vòng round-robin, trần số việc mỗi tài khoản do máy chủ cấp (hiện là 5), chuyển
>   sang tài khoản kế chưa thử, chờ slot trống tối đa 15 phút.
> - **Kết quả:** `results` = `count` video (MP4 có tiếng). Task hoàn thành có thêm `meta`: `mode`
>   (`t2v` / `i2v`), `aspect_ratio`, `count` (số file trả về), `account` và `partial: true` khi đã
>   lưu được một số video trước khi lượt bị dừng / lỗi.

Ví dụ Meta Muse - ảnh sang video (khung hình đầu, 8 giây, 9:16):

```json
{
  "prompt": "slow push in, steam rising",
  "model": "meta_muse",
  "mode": "image_to_video",
  "aspect_ratio": "9:16",
  "video_length": 8,
  "reference_images": ["data:image/png;base64,..."]
}
```

> **Dreamina (`model: "dreamina"`)** chạy bằng tài khoản Dreamina (cột Video bật; gói PLUS/MAX) -
> cùng model `dreamina` như ở `/api/image/generate`, cùng trường `dreamina_model`.
> - `mode`: `text_to_video` (bí danh `t2v`), `image_to_video` (bí danh `i2v` / `frames` /
>   `start_image` / `first_last_frames`: 1 ảnh = khung đầu, 2 ảnh = khung đầu + khung cuối khi model có khung cuối), `omni`
>   (bí danh `omni_reference` / `reference`: ảnh + video + âm thanh tham chiếu, gọi tên bằng `@tag`).
>   Bỏ trống → `omni` khi có video / âm thanh hoặc từ 3 ảnh, `image_to_video` với 1-2 ảnh, ngược lại
>   `text_to_video`.
> - `reference_videos` / `reference_audios` (**chỉ `omni`**): danh sách cùng dạng phần tử với
>   `reference_images` - chuỗi base64 / data-URI, hoặc `{"data": "...", "name": "beat"}`, hoặc
>   `{"path": "D:/..."}` (file trên máy chạy app). Video: mp4 / mov / webm / m4v; âm thanh: mp3 / wav
>   / m4a / aac / ogg. `"name"` là tên `@` trong prompt (`@beat`); không có `name` thì dùng tên file.
>   Với `{"path": ...}` (cả ảnh) thì tên `@` luôn là tên của chính file và `name` bị bỏ qua - `name`
>   chỉ áp dụng cho phần tử base64 / `data`.
>   Gửi ở chế độ khác → `400 INVALID_FIELD`; base64 hỏng / file không đúng loại → `400`.
> - Trần tham chiếu Omni theo model, **từng loại và tổng** (vd Seedance 2.5: 30 ảnh, 10 video, 10 âm
>   thanh, tổng 50; Seedance 2.0: 9 / 3 / 3, tổng 12, cần ít nhất 1 ảnh hoặc video). Quá trần →
>   `400 TOO_MANY_REFERENCES`; thiếu loại bắt buộc → `400 MISSING_REFERENCE`.
> - `aspect_ratio` (mặc định `16:9`, hoặc tỉ lệ đầu tiên của model khi model không có `16:9`;
>   `image_to_video` nhận `auto` = theo ảnh khi model hỗ trợ, và trên model đó mặc định của
>   `image_to_video` là `adaptive`, giống `auto`), `resolution` (mặc định `720p` khi model có, không thì
>   độ phân giải đầu tiên của model), `video_length` (giây, trong khoảng của model, mặc định theo model),
>   `count` (số video 1-4, mặc định 1 - mỗi video là một lần tạo, tính credit riêng).
> - Tên trường thay thế cũng được nhận: `model_key` = `dreamina_model`, `duration` = `video_length`,
>   `num_videos` = `count`.
> - Dreamina đã nhận lệnh tạo mà tạo hỏng → `502 DREAMINA_FAILED`, **không** tự gửi lại (có thể đã trừ
>   credit).
> - **Kết quả:** `results` = các video MP4; `meta`: `mode` (`vid_t2v` / `vid_frames` / `vid_omni`),
>   `model`, `aspect_ratio`, `resolution`, `video_length`, `count`, `account`, `partial`.

Ví dụ Dreamina - Omni với một ảnh, một video và một âm thanh tham chiếu:

```json
{
  "prompt": "@luna dances to @beat, camera moves like @move",
  "model": "dreamina",
  "mode": "omni",
  "video_length": 5,
  "reference_images": [{"data": "data:image/png;base64,...", "name": "luna"}],
  "reference_videos": [{"path": "D:/clips/move.mp4"}],
  "reference_audios": [{"path": "D:/audio/beat.mp3"}]
}
```

### 5.3 Grok — `POST /api/grok/generate`

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | — | Prompt. |
| `mode` | string | ❌ | `t2v` | `t2i` (văn bản→ảnh) · `i2i` (ảnh→ảnh) · `t2v` (văn bản→video) · `i2v` (ảnh→video). Mode sai → task thất bại. |
| `aspect_ratio` | string | ❌ | `9:16` | Ảnh (`t2i`/`i2i`): `9:16, 16:9, 1:1, 2:3, 3:2, 4:3, 21:9, 5:2`. Video (`t2v`/`i2v`): `9:16, 16:9, 1:1, 2:3, 3:2`. Không hợp lệ → `9:16`. |
| `reference_images` | array | ❌ | `[]` | `i2i` tối đa **5** ảnh; `i2v` tối đa **14** ảnh thành phần (với `first_frame: true` tối đa **3** khung). Base64 hoặc `path` (§6); gửi quá → `400 TOO_MANY_REFERENCES`. **Bắt buộc cho `i2i` và `i2v`** (≥1, không có thì task thất bại). Bị bỏ qua với `t2i` / `t2v`. |
| `video_length` | int | ❌ | `6` | `6`, `10` hoặc `15` (giây). **Chỉ mode video** (`t2v`/`i2v`). Giá trị khác → `6`. |
| `resolution` | string | ❌ | `480p` | `480p`, `720p` hoặc `1080p`. **Chỉ mode video.** Mode ảnh (`t2i`/`i2i`) luôn xuất **1K**. |
| `first_frame` | bool | ❌ | `false` | **Chỉ `i2v`.** `true` = ảnh làm khung hình: 1 ảnh = khung đầu, 2 ảnh = khung đầu + cuối, 3 ảnh = khung đầu + giữa + cuối (gửi quá 3 → `400 TOO_MANY_REFERENCES`); `false` = ảnh thành phần tham chiếu (nhiều ảnh). |

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
> - **Tài khoản** (cách chạy ở Cài đặt → Grok):
>   - **Tài khoản Grok** (mặc định): chỉ dùng tài khoản đang bật, tích ô **Ảnh** cho `t2i`/`i2i`
>     và ô **Video** cho `t2v`/`i2v`. Xoay vòng, mỗi tài khoản nhận tối đa số việc đồng thời máy chủ
>     cấp; dư thì chờ tới lượt. Grok báo hết giới hạn → task chuyển sang tài khoản khác (tài khoản đó
>     nghỉ 30 phút, hoặc bị bỏ tích ô Ảnh/Video nếu bật "Tự động tắt tài khoản bị hết giới hạn");
>     tài khoản bị đăng xuất bị đánh dấu hết hạn và task chuyển tài khoản. Mọi tài khoản đều đang
>     nghỉ → task `failed` (Limit Reached).
>   - **Extension** (dự phòng): một tài khoản - tài khoản đang đăng nhập trên tab grok.com, chạy qua
>     extension. Extension chưa kết nối → task `failed`.
> - Tài khoản không được Grok cho phép tùy chọn đã chọn (ví dụ `1080p`) → task `failed` ngay,
>   không thử lại.

### 5.4 Meta AI — `POST /api/meta/generate`

Tạo nội dung trên **Meta AI (vibes.ai)** bằng tài khoản Meta đã đăng nhập. Khác với
các endpoint kia, ảnh tham chiếu được truyền qua **trường có tên** (không phải mảng
`reference_images`) — xem §6.2.

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | — | Prompt. |
| `mode` | string | ❌ | `t2i` | `t2i` (văn bản→ảnh) · `t2v` (văn bản→video) · `i2i` (ảnh→ảnh, thành phần) · `i2v` (ảnh→video). Mode sai → task thất bại. |
| `aspect_ratio` | string | ❌ | `9:16` | Một trong `9:16`, `16:9`, `1:1`. Không hợp lệ → `9:16`. |
| `resolution` | string | ❌ | `720p` | `480p` hoặc `720p`. **Chỉ mode video** (`t2v`/`i2v`). Ảnh tự suy theo site: `1:1` → 1280p, còn lại → 720p. |
| `count` | int | ❌ | `1` | Số đầu ra mỗi prompt, **1–4** (kẹp về khoảng này). Ảnh: `count` ảnh trong một lô; video: `count` clip. |
| `remove_logo` | bool | ❌ | (theo công tắc trang Meta AI) | **Chỉ ảnh** (`t2i` / `i2i`): xoá logo "◯ Meta AI" góc dưới phải (khôi phục điểm ảnh, ảnh 810×1440 / 1440×810 / 1280×1280). `true` xoá, `false` giữ; không gửi → theo công tắc "Hiển thị logo Meta AI" của trang Meta AI (tắt = xoá). Ảnh không có logo được giữ nguyên. Sai kiểu → `400 INVALID_FIELD`. |
| `character_image` | base64 | i2i¹ | — | Thành phần nhân vật/chủ thể (§6.2). Cũng chấp nhận `subject_image`. |
| `scene_image` | base64 | i2i¹ | — | Thành phần bối cảnh. |
| `style_image` | base64 | i2i¹ | — | Thành phần phong cách. |
| `start_image` | base64 | i2v | — | **Bắt buộc cho `i2v`** — khung đầu. |
| `end_image` | base64 | ❌ | — | Khung cuối tùy chọn cho `i2v` (nội suy đầu→cuối). |

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

### 5.5 OpenAI (GPT Image) — `POST /api/openai/generate`

Tạo ảnh bằng **model ảnh OpenAI mặc định của máy chủ** (hiện là **GPT-6 Luna**; bản app cũ: GPT Image 2)
bằng tài khoản ChatGPT/OpenAI đã đăng nhập. `GET /api/models` cho biết model đang dùng (`openai/...`). Luôn
ra **đúng một ảnh** mỗi request (như Grok/Meta trả kết quả đầu). Ảnh tham chiếu đi
theo **VỊ TRÍ** (không có `@tag`).

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|--------|------|:--------:|----------|---------|
| `prompt` | string | ✅ | — | Mô tả ảnh. |
| `aspect_ratio` | string | ❌ | `1:1` | Một trong `1:1`, `3:2`, `4:3`, `16:9`, `21:9`, `2:3`, `3:4`, `4:5`, `9:16`, `custom`. Không hợp lệ → `1:1`. |
| `quality` | string | ❌ | `high` | Một trong `low`, `medium`, `high`. Không hợp lệ → `high`. |
| `prompt_mode` | string | ❌ | `auto` | `auto` (model tinh chỉnh prompt) hoặc `direct` (dùng nguyên văn). Không hợp lệ → `auto`. |
| `reasoning` | string | ❌ | `none` | Mức suy luận: `none`, `low`, `medium`, `high`, `xhigh`, `max`. Không hợp lệ → `none`. |
| `web_search` | bool | ❌ | `false` | Cho phép tra cứu web trước khi tạo. |
| `reference_images` | array | ❌ | `[]` | Tối đa theo model mặc định trên máy chủ (hiện **15** ảnh), base64 hoặc `path` (xem §6); gửi quá → `400 TOO_MANY_REFERENCES`. Truyền theo **vị trí** — GPT Image **không** hỗ trợ `@tag`. |

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

> **Không cần trường `model`** — endpoint chạy model mặc định của máy chủ. Gửi `model`
> cũng bị bỏ qua.
> **Độ phân giải native bị cap ~1.57 MP** ở backend OpenAI (giữ đúng tỉ lệ, không ra
> đủ 2K/4K theo số pixel tuyệt đối). Endpoint này **không** có `upscale`. Xem §9.

### 5.6 Nâng cấp ảnh — `POST /api/upscale/generate`

Phóng to một ảnh bằng **engine Real-ESRGAN chạy local** — đúng engine của tab
**Image Upscaler**. Không cần tài khoản, không tốn credit, không đụng quota: chạy
trên GPU của chính máy bạn.

Khác mọi endpoint còn lại, endpoint này **không có `prompt`** — ảnh chính là toàn bộ
nội dung request.

| Trường | Kiểu | Bắt buộc | Mặc định | Ghi chú |
|-------|------|:--------:|---------|-------|
| `image_path` | string | ⚠️ | — | Đường dẫn tuyệt đối tới ảnh nguồn **trên máy đang chạy G-Labs**. Dùng cái này *hoặc* `image`. |
| `image` | string | ⚠️ | — | Ảnh nguồn dạng base64 (xem §6). Dùng khi client nằm ở máy khác. |
| `filename` | string | ❌ | — | Chỉ dùng kèm `image`: làm gốc tên cho ảnh ra — xem quy tắc đặt tên bên dưới. Không có thì ảnh ra tên `wh_ups_<ngẫu nhiên>_upscaled_x4.png`. |
| `model` | string | ❌ | model đang chọn ở tab Upscaler | Phải là model đã cài, ví dụ `upscayl-standard-4x`, `remacri-4x`, `digital-art-4x`. Model lạ → `400 UNKNOWN_MODEL` kèm danh sách model *đang có*. |
| `scale` | int | ❌ | `4` | Tỉ lệ cuối, `2`–`8`. Model chạy gốc 4x; giá trị khác được resize từ kết quả 4x. Ngoài khoảng → `4`. |
| `format` | string | ❌ | `auto` | `auto` (theo ảnh gốc), `png`, `jpg`, `webp`. |
| `suffix` | string | ❌ | `_upscaled` | Nối vào tên ảnh ra, trước phần `_x<scale>`. Chuỗi rỗng → quay về `_upscaled`. |
| `tile` | int | ❌ | `0` | Kích thước ô xử lý của engine; `0` = tự động. Hạ xuống nếu GPU hết VRAM. |
| `tta` | bool | ❌ | `false` | Chế độ TTA — đẹp hơn chút, chậm hơn **rất** nhiều. |

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

**Mỗi request một ảnh.** Muốn chạy lô thì gửi nhiều request — mỗi cái có `task_id`
riêng.

> ⚠️ **Các request chạy lần lượt, không song song.** Engine là một tiến trình GPU;
> chạy nhiều cái cùng lúc là tranh nhau VRAM. Request thừa nằm trong hàng đợi FIFO,
> báo `pending` rồi chuyển `running` khi tới lượt. Đây là endpoint duy nhất **không**
> song song hoá — các endpoint khác chia tải theo *tài khoản*, còn cái này bị buộc
> vào một GPU.

> 💡 **Cùng máy thì nên dùng `image_path`** (n8n, script chạy local). Base64 làm
> payload phình ~4/3 mà trần body là 50 MB, nên một ảnh PNG 4K lớn có thể vượt trần.
> `image_path` không giới hạn kích thước và bỏ qua luôn bước mã hoá.

#### File nằm ở đâu và được đặt tên thế nào

**Thư mục**, xét theo thứ tự:

1. **Thư mục lưu** đã đặt ở tab **Image Upscaler** trong app, nếu không để trống.
2. Không thì `<thư mục output của G-Labs>/upscale_output` — nằm cạnh `image_output`,
   `veo_output`…

Không bao giờ lưu cạnh ảnh nguồn (đó là cách *tab* Upscaler làm): nguồn qua webhook
thường là file tạm, để vậy thì ảnh kết quả rơi vào thư mục temp của hệ điều hành rồi
bị dọn mất. Tuỳ chọn **Chế độ lưu / thư mục con theo lượt** ở tab Upscaler cũng
**không** được áp dụng — kết quả qua webhook luôn đi thẳng vào thư mục trên.

**Tên file:**

```
<base><suffix>_x<scale>.<ext>
```

| Thành phần | Lấy từ đâu |
|------|---------------------|
| `<base>` | Dùng `image_path`: tên file nguồn, bỏ phần mở rộng. Dùng `image`: tên bạn gửi ở `filename`, cộng thêm một chuỗi ngẫu nhiên ngắn (payload được ghi ra file tạm trước). Không gửi cả hai → `wh_ups_<ngẫu nhiên>`. |
| `<suffix>` | Trường `suffix` — mặc định `_upscaled`. Gửi **chuỗi rỗng thì vẫn quay về `_upscaled`**, giống hệt khi bỏ trống ô ở tab Upscaler; không có cách nào ra tên không hậu tố. |
| `<scale>` | Trường `scale` — mặc định `4`. |
| `<ext>` | Trường `format`. `auto` (mặc định) lấy theo phần mở rộng ảnh nguồn, thứ gì không phải png/jpg/webp thì về `png`; `jpeg` quy về `jpg`. |

Ví dụ:

```
image_path=E:/anh/meo.png, scale=4                 → meo_upscaled_x4.png
image_path=E:/anh/meo.heic, scale=2, format=webp   → meo_upscaled_x2.webp
image + filename="meo.png", scale=4                → meo_a1b2c3d4_upscaled_x4.png
```

**Trùng tên không bao giờ ghi đè.** Nếu tên đích đã tồn tại, phần mở rộng sẽ được chèn
thêm `_2`, `_3`, … phía trước — nên nâng cùng một ảnh hai lần bạn nhận được
`meo_upscaled_x4.png` và `meo_upscaled_x4_2.png`, chứ không phải một file bị lặng lẽ
thay thế.

API chỉ trả URL `/api/files/...`, **không** lộ đường dẫn cục bộ. Tên file trong URL
chính là tên dựng theo quy tắc trên nên bạn nhận ra được — nhưng hãy tải qua URL thay
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
| 500 | `WRITE_FAILED` | Upscale xong nhưng không chép được kết quả vào thư mục đích (đầy ổ, file bị khoá, không có quyền ghi). |
| 499 | `CANCELLED` | Upscale bị dừng trước khi xong (vd dừng từ app hoặc app đang đóng). |

`name` được nhận như tên khác của `filename`.

### 5.7 Bảng tham chiếu Model

**Danh sách model và giới hạn của chúng không ghi cứng trong tài liệu này**: Google, Dreamina và các nhà cung
cấp khác thêm, đổi tên, ngừng model, G-Labs theo cấu hình server. Đọc danh sách sống ở **`GET /v1/models`**
(= `/api/models`, dạng OpenAI, §7) - bảng model ở tab Webhook hiển thị đúng dữ liệu đó. Mỗi mục cho biết gọi
`endpoint` nào và đưa những trường nào (`params`) vào body.

| `id` trong danh mục | Nhà cung cấp | `endpoint` · `params` | Ghi chú |
|------|---------|--------|--------|
| `flow/<model>` (vd `flow/nano_banana_2`, `flow/veo_31_lite`, `flow/omni_flash_12`) | Google Flow - ảnh Nano Banana, video Veo / Omni Flash | `/api/image/generate` hoặc `/api/video/generate` · `model` | tham chiếu theo `@tag` (§6.1); upscale 2K/4K (4K cần ULTRA); Veo `components` chỉ 8 s |
| `pics/nano_pics` | Google Pics | `/api/image/generate` · `model: nano_pics` | tham chiếu theo vị trí; tài khoản Google trong Cài đặt |
| `vids/omni_vids` | Google Vids Omni | `/api/video/generate` · `model: omni_vids` | 720p / 1080p tạo thẳng; tài khoản Google trong Cài đặt |
| `muse/image`, `muse/video` | Meta Muse | `/api/image/generate`, `/api/video/generate` · `model: meta_muse` | tham chiếu theo vị trí; tài khoản Muse trong Cài đặt |
| `grok/image`, `grok/video` | Grok Imagine | `/api/grok/generate` · `mode` | `t2i` / `i2i` / `t2v` / `i2v` (§5.3) |
| `meta/image`, `meta/video` | Meta AI (Vibes) | `/api/meta/generate` · `mode` | các trường tham chiếu có tên (§6.2) |
| `openai/<model>` | GPT Image (tài khoản ChatGPT) | `/api/openai/generate` | chạy model GPT Image mặc định của server; tham chiếu theo vị trí |
| `dreamina/image/<key>`, `dreamina/video/<key>` | Dreamina (CapCut) | endpoint ảnh / video · `model: dreamina`, `dreamina_model` | danh sách sống của tài khoản Dreamina; `@tag`; Omni nhận ảnh + video + âm thanh tham chiếu |
| `upscale/<model>` | Real-ESRGAN trên máy | `/api/upscale/generate` · `model` | model cài trong `bin/realesrgan/models/`; tỉ lệ 2-8 |

Model Google đã ngừng nằm trong bảng `retired` của danh mục kèm model thay thế, gửi vào nhận
`400 MODEL_RETIRED`. Từ **2026-12-05**: `veo_31_fast`, `veo_31_quality` → `veo_31_lite`; `omni_flash` →
`omni_flash_12`.

### 5.8 Thư viện nhân vật - `/api/characters`

Chính là thư viện ở Cài đặt → Nhân vật trong app (mỗi nhân vật một bản ghi; ảnh được sao vào thư
mục riêng của app nên vẫn còn khi bạn xoá file đã gửi). Mọi lệnh cần `X-API-Key` và gói MAX, như
generate. Thay đổi hiện ngay trong app (trang Nhân vật tải lại, thumbnail `@Tên` trên các trang
được làm mới).

**Đối tượng nhân vật** (list / get / create / update trả về):

```json
{
  "name": "Luna",
  "character_id": "3f2b6a4e-...",
  "voice_preset_id": "kore",
  "has_custom_voice": false,
  "personality_notes": "dũng cảm, tò mò",
  "has_image": true,
  "image_url": "http://127.0.0.1:8765/api/characters/Luna/image?v=1761550000"
}
```

`image_url` cũng cần header `X-API-Key` (không phải link công khai); `?v=` đổi khi ảnh đổi.
`GET /api/characters` → `{"characters": [...], "count": n}`, sắp theo tên.

**Tạo - `POST /api/characters` → `201`**

| Trường | Kiểu | Bắt buộc | Ghi chú |
|-------|------|:--------:|-------|
| `name` | string | ✅ | Chỉ chữ và số (chữ Unicode được, vd `Ông2`; không dấu cách, dấu câu hay ký hiệu - đây là `@tag`), tối đa 64. Không trùng, **không phân biệt hoa thường** (`luna` = `Luna`) → nếu trùng `409 NAME_TAKEN`. |
| `image` | string / object | ✅ | Như một mục `reference_images`: chuỗi base64 / data-URI, `{"data": "...", "name": "..."}` hoặc `{"path": "..."}` (file trên máy chạy app, được sao). Phải là ảnh PNG / JPEG / WEBP / GIF / BMP thật → nếu không `400 INVALID_IMAGE`. |
| `voice_preset_id` | string | ❌ | Một trong 30 giọng có sẵn của Flow (`achernar`, `kore`, `puck`, ...; không phân biệt hoa thường), `""` = không giọng. Sai → `400 INVALID_VOICE`. |
| `personality_notes` | string | ❌ | Văn bản tự do, tối đa 4000. |

**Giọng tuỳ chỉnh** (`voice_performance` / `voice_dialog`) không tạo được qua webhook - cần nghe thử
(và captcha) trong app → `400 CUSTOM_VOICE_UNSUPPORTED`. Trường lạ → `400 UNKNOWN_FIELD`.

**Sửa - `PUT` hoặc `PATCH /api/characters/{name}` → `200`** - chỉ gửi phần đổi: `new_name` (đổi
tên; `@tag` đổi theo; `name` trong body cũng được hiểu là tên mới), `image` (ảnh mới, cùng dạng như
trên), `voice_preset_id`, `personality_notes`. Không có gì để đổi → `400 NOTHING_TO_UPDATE`. Đổi
giọng có sẵn của nhân vật đang có giọng tuỳ chỉnh → `409 CUSTOM_VOICE_LOCKED` (đổi trong app). Đổi
tên hoặc ảnh sẽ bỏ các entity Flow của nhân vật để lần chạy sau tạo lại theo tên / ảnh mới.

**Xoá - `DELETE /api/characters/{name}` → `200`** `{"deleted": "Luna", "character_id": "..."}`
(bản sao ảnh cũng bị xoá).

Ví dụ:

```bash
# Thêm nhân vật từ ảnh gửi dạng base64 (client ở máy khác)
curl -X POST http://127.0.0.1:8765/api/characters -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"name": "Luna", "image": {"data": "data:image/png;base64,...", "name": "luna.png"}, "voice_preset_id": "kore", "personality_notes": "dũng cảm, tò mò"}'
# → 201 {"name": "Luna", "character_id": "3f2b...", "voice_preset_id": "kore", "has_image": true, "image_url": "...", ...}

# Xem một nhân vật, rồi tải ảnh của nhân vật đó (link ảnh cũng cần khoá)
curl http://127.0.0.1:8765/api/characters/luna -H "X-API-Key: YOUR_API_KEY"
curl -o luna.png "http://127.0.0.1:8765/api/characters/Luna/image" -H "X-API-Key: YOUR_API_KEY"

# Đổi ảnh và ghi chú (chỉ gửi phần thay đổi)
curl -X PATCH http://127.0.0.1:8765/api/characters/Luna -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"image": {"path": "E:/chars/luna_v2.png"}, "personality_notes": "dũng cảm, tò mò, mê biển"}'
```

Lỗi: `{"error": "...", "error_code": "..."}` với `400` (`INVALID_NAME`, `INVALID_IMAGE`,
`MISSING_IMAGE`, `INVALID_VOICE`, `INVALID_FIELD`, `UNKNOWN_FIELD`, `CUSTOM_VOICE_UNSUPPORTED`,
`NOTHING_TO_UPDATE`), `404 NOT_FOUND`, `409` (`NAME_TAKEN`, `CUSTOM_VOICE_LOCKED`). Tạo song song an
toàn: hai request cùng một tên không bao giờ cùng thành công.

### 5.9 Upload trước - `/api/characters/preupload` và `/api/preupload`

Upload ảnh lên các tài khoản **từ trước** và ghi vào cache upload bền của từng nền tảng, để lần tạo
sau (có thể qua proxy / VPN chậm) chỉ việc trúng cache. Nền tảng: `flow` (tài khoản Flow của trang
Ảnh; mỗi lần upload tốn 1 captcha) và `grok`. Không có Meta AI: token upload của Meta hết hạn sau vài
phút nên upload trước không sống tới lúc tạo. Ảnh đã có trong cache được bỏ qua. Mỗi
lúc một lượt (tính cả lượt chạy từ app) → `409 BUSY` khi đang có lượt khác.

| Trường body | Kiểu | Mặc định | Ghi chú |
|-------|------|---------|-------|
| `names` | array | mọi nhân vật | Chỉ `/api/characters/preupload`: tên nhân vật (không phân biệt hoa thường). Tên không có → `404`. Nhân vật không còn ảnh trên đĩa nằm trong `skipped`. |
| `images` | array | - | Chỉ `/api/preupload`, bắt buộc: các mục kiểu `reference_images`. Cache Flow theo **đường dẫn file**, nên khi có `flow` hãy gửi `{"path": "..."}` - đúng đường dẫn bạn sẽ dùng trong `reference_images` sau này. Grok cache theo **nội dung** file nên gửi base64 được; base64 mà `providers` có `flow` → `400 BASE64_NOT_CACHEABLE`. Tối đa 200. |
| `providers` | array | `["flow", "grok"]` (nhân vật: `["flow"]`) | `/api/preupload`: bất kỳ `flow`, `grok`. `/api/characters/preupload`: chỉ `flow` - kho nhân vật dùng ở các trang Flow, trang Grok không đọc kho nhân vật. Sai / rỗng → `400 INVALID_PROVIDERS`. |
| `raw_network` | bool | `false` | `true` = upload không qua proxy của tài khoản (nhanh hơn; mọi tài khoản lộ cùng một IP). |

Trả `202`: `{"task_id", "status": "running", "type": "preupload", "files", "providers",
"raw_network", "poll_url"}` (+ `characters` / `skipped` với bản nhân vật). Hỏi
`GET /api/status/{task_id}`: khi đang chạy có `progress` `{done, total, info}`; khi `completed`,
`meta` = `{files, raw_network, providers: {flow: {uploaded, cached, failed: [{account, file, error}],
accounts, seconds}, ...}}` (+ `characters` / `skipped`). `POST /api/stop/{task_id}` dừng nó giữa hai
file.

Ví dụ - upload trước hai ảnh tham chiếu lên Flow và Grok, lần sau dùng lại đúng đường dẫn đó:

```bash
curl -X POST http://127.0.0.1:8765/api/preupload -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"images": [{"path": "E:/refs/car.png"}, {"path": "E:/refs/house.png"}], "providers": ["flow", "grok"]}'
# → 202 {"task_id": "p1q2r3s4", "status": "running", "type": "preupload", "files": 2,
#        "providers": ["flow", "grok"], "raw_network": false, "poll_url": "/api/status/p1q2r3s4"}
curl http://127.0.0.1:8765/api/status/p1q2r3s4 -H "X-API-Key: YOUR_API_KEY"   # progress, rồi meta
# lần sau: cùng các đường dẫn đó trong reference_images sẽ dùng bản đã upload
curl -X POST http://127.0.0.1:8765/api/image/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt": "the @car in front of the @house", "reference_images": [{"path": "E:/refs/car.png"}, {"path": "E:/refs/house.png"}]}'
```

> Lưu ý: ảnh đã upload trước lên Flow được task ảnh và task video Veo qua webhook dùng lại khi tham
> chiếu là file cố định: nhân vật trong thư viện, hoặc tham chiếu `{"path": ...}`. Tham chiếu base64
> được ghi ra file tạm mới mỗi lần gọi nên không dùng lại được bản upload trước (Veo vẫn khử trùng
> theo nội dung trong lúc app đang chạy).

---

## 6. Định dạng ảnh tham chiếu

Mọi endpoint có nhận ảnh đều chấp nhận **hai kiểu** — base64 nhúng thẳng, hoặc đường
dẫn tới file đã có sẵn trên máy đang chạy G-Labs. Dạng `{"path": ...}` bên dưới giống nhau ở
`/api/image`, `/api/video`, `/api/grok` và `/api/meta`. `/api/upscale` thì khác: nhận đường dẫn qua
trường `image_path` (hoặc base64 trong `image`), không phải `{"path": ...}` (§5.6).

> ⚠️ **`path` chỉ dùng được khi client và app nằm CÙNG một thiết bị.** App mở đường dẫn
> đó trên hệ thống file của chính nó — nó không tải file từ phía bạn về. Client ở máy
> khác (hoặc trong container) bắt buộc phải gửi base64; đường dẫn không tồn tại bên đó
> sẽ làm hỏng cả task với lỗi `reference path not found: <đường dẫn>`.

Mỗi phần tử trong `reference_images` là một trong ba dạng:

1. **Chuỗi base64** — data URI hoặc base64 thô:
   - `"data:image/png;base64,iVBORw0KGgo..."`
   - `"data:image/jpeg;base64,/9j/4AAQ..."`
   - base64 thô `"iVBORw0KGgo..."` (được coi là PNG)
2. **Object có `data`**: `{"data": "data:image/...;base64,...", "category": "subject", "name": "red_car.png"}`
3. **Object có `path`**: `{"path": "E:/anh/xe_do.png", "category": "subject"}`
   - File được đọc tại chỗ — không copy, không xoá. Ảnh gốc của bạn an toàn: chỉ
     những ảnh G-Labs tự giải mã từ base64 mới bị dọn sau khi task xong.
   - Không cần `name` ở dạng này — cơ chế `@tag` (§6.1) dùng luôn tên file thật.

`category` và `name` áp dụng như nhau cho cả hai:
- `category` không bắt buộc: `subject` | `scene` | `style`. Được chấp nhận nhưng
  **bị bỏ qua với model ảnh Flow** (chúng dùng một ô tham chiếu chung).
- `name` (hoặc `filename`) không bắt buộc, dành cho dạng **base64**: tên file gốc của
  ảnh, dùng để gắn vào prompt bằng `@<từ_khoá>` (xem §6.1).

**Chuỗi trần luôn được hiểu là base64**, không bao giờ là đường dẫn — base64 dùng cả
`/` lẫn `+` nên không có cách nào phân biệt chắc chắn. Muốn truyền đường dẫn thì phải
dùng dạng object.

Trộn cả hai dạng trong cùng một request cũng được.

Ràng buộc:
- Kiểu giải mã hỗ trợ: PNG, JPG/JPEG, WEBP (nhận diện qua header data-URI; mặc định
  PNG khi không có header). Dạng `path` thì trỏ tới định dạng nào engine đọc được cũng được.
- Base64 giải mã ra dưới ~100 byte sẽ bị bỏ (coi là không hợp lệ). Ngược lại, `path`
  không tồn tại sẽ **làm hỏng task** — gõ nhầm đường dẫn mà vẫn lặng lẽ render thiếu
  một ảnh tham chiếu thì tệ hơn nhiều.
- Số lượng tối đa theo endpoint: **ảnh = 10** (**Google Pics = 14**, **Meta Muse = 14**), **grok** = `i2i` 5 /
  `i2v` 14 / `i2v` với `first_frame: true` 3, **openai = 15** (trần của model trên máy chủ), **Dreamina** = trần của model,
  **video = 3** (**Omni Flash = 7** - chỉ `components` dùng quá 2; **Google Vids = 3**; **Meta Muse = 7** (trần máy chủ): 1 = khung hình đầu, từ 2 = ảnh tham chiếu).
  Phần dư vượt mức tối đa bị bỏ lặng lẽ **chỉ** với ảnh / video Flow và Google Vids.
  Google Pics, Meta Muse, Grok, OpenAI và Dreamina từ chối bằng `400 TOO_MANY_REFERENCES`.
- **Vì sao nên dùng `path`:** base64 làm payload phình ~4/3 và mỗi request bị chặn ở
  50 MB (§5). Đường dẫn cục bộ không giới hạn kích thước và bỏ qua luôn khâu mã hoá/
  giải mã ở cả hai đầu.

### 6.1 Gắn ảnh theo tên bằng `@tag`

Khi một ảnh tham chiếu có `name` (hoặc `filename`), bạn có thể trỏ tới nó **ngay trong
prompt** bằng `@<từ_khoá>` — **đúng cùng cơ chế** ở trang Image / Veo trong app (tín hiệu
webhook đi qua chính các hàm xử lý đó nên payload gửi Flow API khớp y như tạo trực tiếp).

- **Khớp**: `<từ_khoá>` là **chuỗi con** không phân biệt hoa thường của tên file (đã bỏ
  đuôi). Vd `name: "red_car.png"` → `@red_car`, `@car`, `@red` đều trúng; ảnh đầu tiên theo
  thứ tự trong `reference_images` thắng.
- **Tác dụng**: gắn đúng ảnh đó vào đúng vị trí danh từ trong câu (Flow structured prompt
  "Mode-2"), thay vì truyền tất cả ảnh như tham chiếu chung vô danh.
- **Phạm vi**: dùng cho **image (Flow)**, **video (Veo)** và **Google Vids `components`** (`omni_vids`, ở đó tên nhân vật trong thư viện cũng là tag hợp lệ), **Dreamina** (`dreamina`: ảnh tham chiếu và Omni - tag trỏ được tới ảnh, video, âm thanh theo `name`, và nhân vật thư viện theo tên); **Grok**, **OpenAI (GPT Image)**, **Google Pics** và **Meta Muse** (`meta_muse`) **không hỗ trợ** `@tag` (ref đi theo vị trí).
- Tên file được làm sạch (bỏ thành phần thư mục và ký tự không hợp lệ) trước khi dùng.
- **Tag không khớp** được giữ nguyên là văn bản — không gây lỗi.
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

**Video (Veo) — mode `components`** (ghép nhiều "nguyên liệu" theo tên; cũng áp dụng cho
`start_image` / `start_end_image`):
```json
{
  "prompt": "the @character walks through the @forest at dawn",
  "model": "veo_31_lite",
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
`{"path": "..."}` — cùng hai dạng như `reference_images`, và cũng kèm điều kiện phải
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
- `t2i` / `t2v` **không** nhận ảnh — ảnh gửi kèm sẽ bị bỏ qua.
- Meta AI **không có `@tag`**; tên trường quyết định vai trò.

---

### 6.3 Nhân vật trong thư viện và `use_characters`

Nhân vật trong thư viện (Cài đặt → Nhân vật, hoặc `/api/characters` §5.8) được dùng khi task **đang
dùng nhân vật**: `use_characters: true`, hoặc - khi không gửi trường này - công tắc Nhân vật chung của
app. `use_characters: false` bỏ qua nhân vật cho task đó kể cả khi công tắc đang bật. Lựa chọn chỉ
áp dụng cho task đó.

- **Ảnh (Flow)** và **Video (Veo / Omni Flash)**: `@Tên` (đúng tên, không phân biệt hoa thường) dùng
  nhân vật - ảnh của nó làm ảnh tham chiếu, hoặc entity Flow khi nó có giọng tuỳ chỉnh (video
  `components`). Nhân vật lấy các ô tham chiếu mà ảnh của bạn để trống. `components` chỉ có `@Tên`
  (không `reference_images`) được chấp nhận khi prompt gắn tag ít nhất một nhân vật trong thư viện.
- **Google Vids `components`**: `@Tên` thêm ảnh làm nguyên liệu (§5.2).
- **Dreamina** (chế độ ảnh tham chiếu và Omni): `@Tên` thêm ảnh của nhân vật làm tham chiếu sau ảnh
  của bạn mỗi khi đang dùng nhân vật - chỉ cần công tắc app, không bắt buộc gửi `use_characters: true`
  (khác Pics / Muse). `use_characters: false` tắt cho riêng tác vụ đó. Khi không gửi `mode`, prompt gọi
  tên một nhân vật thư viện sẽ chuyển `text_to_image` thành `image_to_image`.
- **Google Pics / Meta Muse**: chỉ khi yêu cầu gửi `use_characters: true` (riêng công tắc app không áp
  dụng ở đây, để tích hợp đang chạy giữ nguyên hành vi). Không cần `@tag` - mọi nhân vật prompt nhắc tới
  (luật trang Pics / Muse, chế độ khớp chung) được thêm sau ảnh của bạn, chỉ vào ô trống (§5.1).
- Grok, Meta AI (`/api/meta/generate`), OpenAI và Upscale không dùng thư viện (trường bị bỏ qua).

```json
{ "prompt": "@Luna đọc sách bên lò sưởi", "model": "nano_banana_2", "use_characters": true }
```

## 7. Tham chiếu Response & trạng thái

### POST generate → `202`
```json
{ "task_id": "abc12345", "status": "pending", "message": "...", "poll_url": "/api/status/abc12345" }
```

### GET `/api/status/{task_id}` → `200`
- `pending` / `running`: `{ task_id, type, status, prompt, created_at }`
- `type`: `image`, `video`, `grok`, `vibes` (task Meta AI), `openai`, `upscale` hoặc `preupload` (§5.9;
  kèm thêm `progress` `{done, total, info}`).
- `completed`: thêm `results` (mảng URL file) và `completed_at` (unix giây); task Google Vids
  còn có thêm `meta` (§5.2), task Google Pics cũng vậy (§5.1), task Meta Muse thêm `meta`
  `{mode, aspect_ratio, count, account, partial}` (§5.1 / §5.2).
- `failed`: thêm `error_code` (int), `error` (string), `error_detail` (string).
- task_id không tồn tại → `404 {"error": "Task <id> not found"}`. Máy chủ giữ 200 task **đã
  xong** gần nhất; task cũ hơn bị xoá và cũng trả `404`.

### GET `/api/result/{task_id}` → `200`
- Nếu chưa xong: `{ task_id, status, message: "Task not yet completed" }` — task `failed` cũng
  nhận đúng dạng này, **không** có trường lỗi: đọc lỗi ở `GET /api/status/{task_id}`.
- Nếu đã xong: `{ task_id, status: "completed", results: [...], completed_at }` (thêm `meta`
  với Google Vids / Google Pics / Meta Muse).
### GET `/api/health` → `200`
```json
{ "status": "ok", "server": "G-Labs Webhook", "uptime": 123, "tasks_pending": 0, "tasks_running": 1 }
```

### GET `/api/tasks` → `200`
```json
{ "tasks": [ { "task_id": "...", "type": "image", "status": "completed", "prompt": "50 ký tự đầu...", "created_at": 1707782400.0 } ] }
```
(Mới nhất trước, tối đa 50.)

### GET `/api/models` (= `/v1/models`) → `200`
Mọi model webhook chạy - Flow ảnh / video, Google Pics, Google Vids, Meta Muse, Grok, Meta AI, GPT Image,
Dreamina, upscale trên máy - theo **dạng "list models" của OpenAI**: client OpenAI đọc được ngay, còn client
dựng ô chọn và giới hạn từ đây thay vì cứng danh sách. Giá trị lấy từ đúng cấu hình các trang đang dùng (đa số
do server G-Labs gửi), nên model mới, đổi tên hay bị ngừng đều tự hiện mà không cần client ra bản mới. Nhà cung
cấp chưa có cấu hình (hoặc gói chưa mở) thì vắng mặt, không đoán. Xác thực: `X-API-Key`, hoặc
`Authorization: Bearer <khoá>` như OpenAI.
```json
{ "object": "list",
  "data": [
    { "id": "flow/veo_31_lite", "object": "model", "created": 0, "owned_by": "google-flow",
      "name": "Veo 3.1 Lite", "type": "video",
      "endpoint": "/api/video/generate", "params": { "model": "veo_31_lite" },
      "modes": ["text_to_video", "start_image", "start_end_image", "components"],
      "aspect_ratios": ["16:9", "9:16"], "resolutions": ["720p", "1080p", "4K"],
      "durations": [4, 6, 8], "component_durations": [8], "max_reference_images": 3,
      "reference_binding": "tag", "end_frame": true,
      "requires": { "4K": "ULTRA", "durations": { "ULTRA": [4, 6] } } },
    { "id": "dreamina/video/dreamina_seedance_40", "object": "model", "created": 0, "owned_by": "dreamina",
      "name": "Dreamina Seedance 2.0 Fast", "type": "video",
      "endpoint": "/api/video/generate", "params": { "model": "dreamina", "dreamina_model": "dreamina_seedance_40" },
      "modes": ["text_to_video", "image_to_video", "omni"], "duration_range": [4, 15], "...": "..." }
  ],
  "retired": { "flow/veo_31_fast": "flow/veo_31_lite" } }
```
- `id` = `<nhà cung cấp>/<model>`. Muốn chạy model: POST tới `endpoint`, thêm các trường trong `params` vào body.
- `type`: `image`, `video` hoặc `upscale`. `owned_by`: `google-flow`, `google-pics`, `google-vids`, `meta-muse`,
  `grok`, `meta-ai`, `openai`, `dreamina`, `local`.
- Giới hạn (chỉ có khi áp dụng): `modes`, `aspect_ratios`, `resolutions`, `durations` (các giá trị
  `video_length` được nhận) hoặc `duration_range` ([ngắn nhất, dài nhất]), `component_durations` (Flow
  `components`), `max_reference_images`, `max_frames`, `end_frame` (nhận khung cuối), `counts`, `qualities`,
  `upscale`, `keep`, `scale_range`, `reference_video_max_seconds`.
- `reference_binding`: `tag` = ảnh gắn theo `@tên` (§6.1), `position` = theo thứ tự gửi, `named` = các trường
  có tên của Meta AI (§6.2).
- `requires`: yêu cầu gói, vd `{"model": "ULTRA"}`, `{"4K": "ULTRA"}`, `{"durations": {"ULTRA": [4, 6], "paid": [11, 12]}}`.
- `dreamina`: mục Dreamina gốc (`modes`, `secs`, trần `omni` theo loại, `accounts`, `live` - `false` = danh sách
  dự phòng của trang vì chưa tải được danh sách sống).
- `openai_endpoints`: các endpoint chuẩn OpenAI (§12) nhận `id` này làm `model`.
- `retired`: id Google đã ngừng → model thay thế (`null` = không có); gửi id này nhận `400 MODEL_RETIRED`.
- `GET /v1/models/{id}` (id mã hoá URL) → một mục; không có → `404`
  `{"error": {"message": "...", "type": "invalid_request_error", "param": "model", "code": "model_not_found"}}`.

### POST `/api/stop` (hoặc `/api/stop/{task_id}`) → `200`
```json
{ "stopped": ["a1b2c3d4", "e5f6a7b8"], "skipped": [], "count": 2 }
```
`stopped` = các task đang chờ / đang chạy nay đã `failed` (`499 STOPPED_BY_CLIENT`);
`skipped` = task được gọi đích danh nhưng đã xong từ trước. `task_id` không tồn tại → `404`.
Lệnh này chỉ cần API key. Body không phải JSON object → `400 {"error": "Body must be a JSON
object"}`; body quá 64 KB → `413` — cả hai đều không dừng gì cả.

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
| `413` | `{"error": "Payload too large (max 52428800 bytes)"}` | Body vượt trần **50 MB** — xem §5 |
| `500` | `{"error": "Failed to read file"}` | File kết quả có trong registry nhưng không đọc được |
| `400` / `404` / `409` | `{"error": "...", "error_code": "NAME_TAKEN"}` | Lệnh thư viện nhân vật / upload trước (§5.8, §5.9) trả lời ngay với `error_code` có tên |
| `409` | `{"error": "A pre-upload is already running ...", "error_code": "BUSY"}` | Đang có một lượt upload trước |

Đây là các lỗi ở **tầng truyền tải**, do chính lệnh `POST`/`GET` trả về. Request đã đi
qua được các lỗi này sẽ nhận `202`, và mọi trục trặc sau đó hiện ra dưới dạng task
`failed` kèm `error_code` / `error` (§8) chứ không phải lỗi HTTP.

---

## 8. Mã lỗi (`error_code` / `error` / `error_detail`)

Khi task thất bại, response trạng thái mang ba trường:

- **`error_code`** — số nguyên. Với lỗi từ API phía trên, nó phản ánh mã kiểu HTTP
  (`400`, `403`, `429`, `500`, …). **`429` nghĩa là hết quota / giới hạn tần suất**
  (vd hết giới hạn tạo trong ngày). Bằng `0` khi không có mã số phù hợp (vd lỗi
  validate, "không có tài khoản").
- **`error`** — thông điệp dễ đọc. Với các status đã biết từ phía trên, đây là status
  tiếng Anh ổn định (vd `PERMISSION_DENIED`, `RESOURCE_EXHAUSTED`). Với các thông điệp
  thân thiện (quota, upscale thất bại, timeout), phần chữ **theo ngôn ngữ giao diện
  của app** (vd tiếng Việt nếu app đang để tiếng Việt).
- **`error_detail`** — chuỗi lỗi gốc đầy đủ (vd `"429: Đã hết giới hạn tạo ảnh trong ngày (user@gmail.com)"`).

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
> `"INVALID_MODE — omni_vids supports text_to_video, …"`. Hãy so **phần đầu** của `error`
> (`error.startswith("INVALID_MODE")`), đừng so cả chuỗi.

Lưu ý riêng của app này:
- **Video** yêu cầu độ phân giải không tạo được (vd `4K` mà không có tài khoản ULTRA)
  → `failed`.
- **Ảnh** yêu cầu `upscale` (`2K`/`4K`) không tạo được → `failed` kèm lý do upscale
  (không trả về ảnh gốc nhỏ hơn).
- **Upscale** có mã riêng (`503 ENGINE_MISSING`, `503 NO_VULKAN_DEVICE`,
  `507 GPU_OUT_OF_MEMORY`, `400 UNKNOWN_MODEL`, …) — xem bảng ở §5.6. Không bao giờ trả
  `429`: không có quota nào để hết.
- **Meta AI**: cookie tài khoản hết hạn → `failed` `401` (`Meta cookie expired`);
  hết quota → `429` (`Meta quota exhausted`); không có tài khoản Meta đang bật cho
  loại yêu cầu → `error_code 0` (`No enabled Meta account for image/video`); không
  tạo ra gì → `Meta produced no output`.
- **Task bất kỳ** bị dừng qua `POST /api/stop` → `failed` với `499` / `STOPPED_BY_CLIENT`.
- **Flow Video** (Veo / Omni Flash): thiếu `model` → `400 MISSING_MODEL`; model Google đã tắt →
  `400 MODEL_RETIRED` (`error` nêu id thay thế, vd `use 'veo_31_lite'`).
- **Google Vids** (`omni_vids`): request bị từ chối → `400` `INVALID_MODE` / `INVALID_RESOLUTION` /
  `INVALID_VIDEO_LENGTH` / `INVALID_ASPECT_RATIO` / `INVALID_FIELD` / `MISSING_REFERENCE` /
  `UNKNOWN_CLIP` / `ALREADY_UPSCALED`; gói thấp → `403 PLAN_REQUIRED`; thiếu config máy chủ →
  `503 VIDS_CONFIG` / `503 RUNTIME_CONFIG`; không tài khoản nào đủ giây → `503 NO_VIDS_ACCOUNT`;
  mọi tài khoản bận suốt 15 phút → `503 NO_FREE_SLOT`; sau một lỗi mà không còn tài khoản nào nhận được task → `502 ALL_ACCOUNTS_FAILED` (còn lại là lỗi của chính tài khoản cuối, bên dưới);
  việc tự lỗi → `401 VIDS_COOKIE_EXPIRED`, `429 VIDS_QUOTA_EXHAUSTED`, `429 RATE_LIMITED`,
  `400 CONTENT_POLICY`, `400 BAD_REQUEST`, `400 CLIP_GONE` (upscale), `409 CLIP_ACCOUNT_UNAVAILABLE`
  (upscale), `504 VIDS_TIMEOUT` (đã gửi yêu cầu mà không nhận được trả lời - có thể đã trừ giây nên
  KHÔNG tự thử lại), `502 UPSTREAM`, `502 NO_OUTPUT`; máy chủ webhook bị tắt khi task đang chờ hoặc đang chạy
  → `503 SERVER_STOPPED`.
  `video_to_video` có thêm: `400 MISSING_REFERENCE` (thiếu `reference_video`), `400 INVALID_VIDEO_FORMAT`
  (không phải mp4 / m4v / mov / webm), `400 BAD_VIDEO` (không đọc được độ dài / kích thước khung hình),
  `400 VIDEO_TOO_LONG` (dài hơn giới hạn của máy chủ), `503 NO_VIDS_PAID_ACCOUNT` (không tài khoản
  đang bật nào đủ giây của gói trả phí) và `429 VIDS_PAID_SECONDS_REQUIRED` (tác vụ cần giây của gói
  trả phí mà không tài khoản nào đủ).
- **Google Pics** (`nano_pics`): request bị từ chối → `400` `INVALID_MODE` / `MISSING_REFERENCE` /
  `TOO_MANY_REFERENCES` / `INVALID_ASPECT_RATIO` / `INVALID_KEEP` / `INVALID_FIELD`; gói thấp →
  `403 PLAN_REQUIRED`; thiếu config máy chủ → `503 PICS_CONFIG` / `503 RUNTIME_CONFIG`; không tài
  khoản nào dùng được còn lượt → `503 NO_PICS_ACCOUNT`; mọi tài khoản bận suốt 15 phút →
  `503 NO_FREE_SLOT`; sau một lỗi mà không còn tài khoản nào nhận được task →
  `502 ALL_ACCOUNTS_FAILED` (còn lại là lỗi của chính tài khoản cuối, bên dưới); việc tự lỗi →
  `401 PICS_COOKIE_EXPIRED`, `403 PICS_NO_ACCESS` (tài khoản không dùng được Google Pics; vẫn
  được giữ bật), `504 PICS_TIMEOUT` (đã gửi yêu cầu mà không nhận được trả lời — có thể đã trừ lượt
  nên KHÔNG tự thử lại, không chuyển tài khoản khác), `429 PICS_QUOTA_EXHAUSTED`, `429 RATE_LIMITED`, `400 CONTENT_POLICY`,
  `400 BAD_REQUEST`, `502 UPSTREAM`, `502 NO_OUTPUT`; máy chủ webhook bị tắt → `503 SERVER_STOPPED`.
- **Meta Muse** (`meta_muse`, cả ảnh lẫn video): request bị từ chối → `400` `INVALID_MODE` /
  `MISSING_REFERENCE` / `TOO_MANY_REFERENCES` (quá trần máy chủ - hiện 14 với ảnh, 7 với video) /
  `INVALID_ASPECT_RATIO` / `INVALID_COUNT` / `INVALID_VIDEO_LENGTH`; chưa nhận được config máy chủ →
  `503 MUSE_CONFIG`; gói thấp → `403 PLAN_REQUIRED`; không có tài khoản Muse đang bật còn hạn mức →
  `503 NO_MUSE_ACCOUNT`; mọi tài khoản bận suốt 15 phút → `503 NO_FREE_SLOT`; mọi tài khoản đã thử
  đều lỗi → `502 ALL_ACCOUNTS_FAILED`; việc tự lỗi → `401 MUSE_COOKIE_EXPIRED`,
  `403 MUSE_DISCONNECTED` (Meta đã ngắt Muse trên tài khoản), `403 MUSE_REGION_BLOCKED` (Muse chặn
  lượt tạo này theo quốc gia / khu vực của tài khoản), `429 MUSE_QUOTA_EXHAUSTED`,
  `504 MUSE_TIMEOUT` (đã gửi yêu cầu mà không nhận được kết quả - có thể đã tốn token nên KHÔNG tự
  thử lại), `400 CONTENT_POLICY` (Muse trả lời mà không có ảnh / video), `502 DOWNLOAD_FAILED`,
  `502 UPSTREAM`, `502 NO_OUTPUT`; máy chủ webhook bị tắt → `503 SERVER_STOPPED`.
- **Dreamina** (`dreamina`, cả ảnh lẫn video): request bị từ chối → `400` `INVALID_MODE` /
  `INVALID_MODEL` / `INVALID_FIELD` / `MISSING_REFERENCE` / `TOO_MANY_REFERENCES` /
  `INVALID_ASPECT_RATIO` / `INVALID_RESOLUTION` / `INVALID_VIDEO_LENGTH` / `INVALID_COUNT` /
  `INVALID_QUALITY`; gói thấp → `403 PLAN_REQUIRED`; không có tài khoản Dreamina dùng được →
  `503 NO_DREAMINA_ACCOUNT`; máy chủ chưa cấp trần luồng → `503 RUNTIME_CONFIG`; mọi tài khoản bận
  suốt 15 phút → `503 NO_FREE_SLOT`; mọi tài khoản đã thử đều lỗi → `502 ALL_ACCOUNTS_FAILED`; việc tự
  lỗi → `401 DREAMINA_COOKIE_EXPIRED`, `429 DREAMINA_CREDIT` (không đủ credit), `503 DREAMINA_CONFIG`,
  `502 DREAMINA_FAILED` (Dreamina tạo hỏng - không tự gửi lại), `400 CONTENT_REJECTED` (Dreamina từ
  chối nội dung - ảnh tham chiếu hoặc prompt - thường là mặt người thật hoặc nội dung bị cấm; không tự
  thử lại); máy chủ webhook bị tắt →
  `503 SERVER_STOPPED`.

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
  - `video_length` Veo `4`/`6` cần **ULTRA**; Omni Flash 1.2 `11`–`15` cần tài khoản **không phải FREE**.
    Không có tài khoản như vậy thì dùng độ dài mặc định 8s (task vẫn chạy).
  - Tài khoản đã **TẮT** trong app sẽ không được dùng.
- **Grok** cần ít nhất một tài khoản Grok đang bật ở Cài đặt → Grok (cách chạy **Tài khoản**,
  mặc định), hoặc extension đang kết nối với tab grok.com đã đăng nhập (cách chạy **Extension**,
  một tài khoản). Chi tiết xoay vòng / hết giới hạn ở §5.3.
- **Mỗi request Grok trả 1 kết quả** (ảnh/video đầu tiên được tạo).
- **Meta AI** cần tài khoản Meta (vibes.ai) đã đăng nhập và **đang bật** trong app
  (tab Meta AI) — `image_enabled` cho `t2i`/`i2i`, `video_enabled` cho `t2v`/`i2v`.
  Tài khoản dùng **xoay vòng** (round-robin), lỗi ở mức tài khoản (cookie hết hạn / hết hạn mức) thì
  chuyển sang tài khoản chưa thử kế tiếp; trần luồng = số tài khoản đang bật × số việc mỗi tài khoản
  máy chủ cấp. Từ bản 6.0.0 mỗi tài khoản không chạy quá số việc đó; mọi tài khoản đủ việc thì task chờ
  tối đa 3 giờ rồi báo `503 NO_FREE_SLOT`.
- **OpenAI (GPT Image)** cần tài khoản ChatGPT/OpenAI đã đăng nhập và **đang bật**
  trong app (trang GPT Image → tài khoản ChatGPT). Tài khoản dùng **xoay vòng** (round-robin)
  và **fail-over** sang tài khoản kế khi lỗi ở mức tài khoản (hết hạn/quota/5xx). Token
  được làm mới tự động trước mỗi lượt. Trần luồng = số tài khoản đang bật × số việc mỗi tài
  khoản máy chủ cấp (hiện là 5), như mọi endpoint. Từ bản 6.0.0 mỗi tài khoản không chạy quá số việc đó;
  mọi tài khoản đủ việc thì task chờ tối đa 3 giờ rồi báo `503 NO_FREE_SLOT`. Ảnh ra bị cap ~1.57 MP
  (không 2K/4K, không upscale).
- **Google Vids** (`omni_vids`) cần gói **PLUS/MAX** và ít nhất một tài khoản Google ở
  Cài đặt → Tài khoản Google đang BẬT (tích ô Video) và còn giây. Số giây là hạn mức riêng của tài khoản (1 giây video =
  1 giây). Upscale chỉ chạy trên đúng tài khoản đã tạo clip.
- **Google Pics** (`nano_pics`) cần gói **PLUS/MAX** và ít nhất một tài khoản Google ở Cài đặt →
  Tài khoản Google đang BẬT (tích ô Ảnh) và còn lượt Pics. Một task = một lượt = 1 đơn vị hạn
  mức Pics của tài khoản, bất kể lượt đó ra bao nhiêu ảnh.
- **Meta Muse** (`meta_muse`) cần gói **PLUS/MAX** và ít nhất một tài khoản Muse đang bật ở
  Cài đặt → Tài khoản Muse còn hạn mức. Hạn mức = token Muse của tài khoản (gói theo tuần trước,
  sau đó tới token mua thêm). Mỗi tài khoản chạy tối đa số việc máy chủ cấp (hiện là 5).
- **Dreamina** (`dreamina`) cần gói **PLUS/MAX** và ít nhất một tài khoản Dreamina đang bật ở
  Cài đặt → Tài khoản Dreamina (cột Ảnh / Video tương ứng bật) còn credit. Lệnh tạo được gửi từ
  Chrome ngầm của tài khoản (mở khi cần, tự đóng sau 90 giây rảnh).
- **Upscale** không cần tài khoản, không cần hạng nào — engine Real-ESRGAN chạy trên
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
  -d '{"prompt":"flowing water","model":"veo_31_lite","mode":"start_image","reference_images":["data:image/png;base64,..."],"resolution":["1080p"]}'

# --- Video (mode components + voice) ---
curl -X POST http://127.0.0.1:8765/api/video/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"she says hello","model":"veo_31_lite","mode":"components","reference_images":["data:image/png;base64,..."],"voice":"aoede"}'

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

# --- OpenAI GPT Image: văn bản → ảnh ---
curl -X POST http://127.0.0.1:8765/api/openai/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a modern minimalist house, golden hour","aspect_ratio":"16:9","quality":"high"}'

# --- OpenAI GPT Image: kèm ảnh tham chiếu (theo vị trí, không @tag) ---
curl -X POST http://127.0.0.1:8765/api/openai/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"same subject on a beach","aspect_ratio":"1:1","reference_images":["data:image/png;base64,..."]}'

# --- Ảnh kèm tham chiếu đọc thẳng từ đĩa (cùng máy, khỏi base64) ---
curl -X POST http://127.0.0.1:8765/api/image/generate   -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY"   -d '{"prompt":"chiếc @xe trên đường đèo","reference_images":[{"path":"E:/anh/xe.png"}]}'

# --- Upscale: ảnh nguồn có sẵn trên máy này (không giới hạn cỡ, khỏi mã hoá) ---
curl -X POST http://127.0.0.1:8765/api/upscale/generate   -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY"   -d '{"image_path":"E:/anh/meo.png","scale":4,"model":"upscayl-standard-4x"}'

# --- Upscale: gửi ảnh dạng base64 (client ở máy khác) ---
curl -X POST http://127.0.0.1:8765/api/upscale/generate   -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY"   -d '{"image":"data:image/png;base64,...","filename":"meo.png","scale":2,"format":"png"}'

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

# --- Meta Muse: văn bản → ảnh (16:9, 2 ảnh) ---
curl -X POST http://127.0.0.1:8765/api/image/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a red fox in the snow","model":"meta_muse","aspect_ratio":"16:9","count":2}'

# --- Meta Muse: ảnh → video (khung hình đầu, 8 giây, 9:16) ---
curl -X POST http://127.0.0.1:8765/api/video/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"slow push in, steam rising","model":"meta_muse","mode":"image_to_video","aspect_ratio":"9:16","video_length":8,"reference_images":["data:image/png;base64,..."]}'

# --- Dreamina: văn bản → ảnh (Seedream 5.0 Lite, 2 ảnh 16:9) ---
curl -X POST http://127.0.0.1:8765/api/image/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"a red fox in the snow","model":"dreamina","dreamina_model":"high_aes_general_v50","aspect_ratio":"16:9","count":2}'

# --- Dreamina: Omni (ảnh + video + âm thanh tham chiếu, @tag) ---
curl -X POST http://127.0.0.1:8765/api/video/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"@luna dances to @beat, camera like @move","model":"dreamina","mode":"omni","video_length":5,"reference_images":[{"path":"D:/refs/luna.png"}],"reference_videos":[{"path":"D:/clips/move.mp4"}],"reference_audios":[{"path":"D:/audio/beat.mp3"}]}'

# --- Các model dùng được (kèm giới hạn) ---
curl http://127.0.0.1:8765/api/models -H "X-API-Key: YOUR_API_KEY"

# --- Omni Flash 1.2: khung đầu + khung cuối, 6 giây ---
curl -X POST http://127.0.0.1:8765/api/video/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"the door slowly opens","model":"omni_flash_12","mode":"start_end_image","video_length":6,"reference_images":["data:image/png;base64,...","data:image/png;base64,..."]}'

# --- Dreamina: ảnh → video (khung đầu, Seedance 2.0 Fast, 720p, 5 giây) ---
curl -X POST http://127.0.0.1:8765/api/video/generate -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt":"she turns and smiles","model":"dreamina","dreamina_model":"dreamina_seedance_40","mode":"image_to_video","resolution":"720p","video_length":5,"reference_images":[{"path":"D:/refs/luna.png"}]}'

# --- Dừng một task / dừng tất cả ---
curl -X POST http://127.0.0.1:8765/api/stop/abc12345 -H "X-API-Key: YOUR_API_KEY"
curl -X POST http://127.0.0.1:8765/api/stop -H "X-API-Key: YOUR_API_KEY"

# --- Thư viện nhân vật: thêm, liệt kê, đổi tên, xoá ---
curl -X POST http://127.0.0.1:8765/api/characters \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"name": "Luna", "image": {"path": "E:/chars/luna.png"}, "voice_preset_id": "kore"}'
curl http://127.0.0.1:8765/api/characters -H "X-API-Key: YOUR_API_KEY"
curl -X PATCH http://127.0.0.1:8765/api/characters/Luna \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"new_name": "Selene"}'
curl -X DELETE http://127.0.0.1:8765/api/characters/Selene -H "X-API-Key: YOUR_API_KEY"

# --- Dùng thư viện cho riêng task này (công tắc app giữ nguyên) ---
curl -X POST http://127.0.0.1:8765/api/image/generate \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"prompt": "@Luna đọc sách bên lò sưởi", "model": "nano_banana_2", "use_characters": true}'

# --- Upload trước mọi ảnh nhân vật lên Flow, rồi hỏi trạng thái task ---
curl -X POST http://127.0.0.1:8765/api/characters/preupload \
  -H "Content-Type: application/json" -H "X-API-Key: YOUR_API_KEY" \
  -d '{"providers": ["flow"]}'

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
  model: "veo_31_lite",
  aspect_ratio: "16:9",
  resolution: ["720p"],
});
console.log(urls);
```

---

### 10.4 PowerShell trên Windows (không cần cài gì: gửi → chờ → tải về)

Body là một file JSON UTF-8 (đúng các trường ở §5). Key lấy từ biến môi trường `GLABS_API_KEY` hoặc tham số `-Key`.

```powershell
# glabs.ps1  -  powershell -ExecutionPolicy Bypass -File glabs.ps1 -Endpoint image -Body job.json -Out output -Name scene01
param([string]$Endpoint, [string]$Body, [string]$Out = ".", [string]$Name = "result",
      [string]$Base = "http://127.0.0.1:8765", [string]$Key = $env:GLABS_API_KEY, [int]$Timeout = 2400, [int]$Poll = 5)
$ErrorActionPreference = "Stop"
$utf8 = New-Object System.Text.UTF8Encoding($false)
$h = @{ "X-API-Key" = $Key }
function Call($method, $url, $bytes) {
  $a = @{ Uri = $url; Method = $method; Headers = $h; UseBasicParsing = $true; TimeoutSec = 120 }
  if ($bytes) { $a.Body = $bytes; $a.ContentType = "application/json; charset=utf-8" }
  try { $r = Invoke-WebRequest @a; return $utf8.GetString($r.RawContentStream.ToArray()) | ConvertFrom-Json }
  catch [System.Net.WebException] {
    if (-not $_.Exception.Response) { throw "cannot reach $url - is G-Labs Studio open with the Webhook server on?" }
    $ms = New-Object System.IO.MemoryStream; $_.Exception.Response.GetResponseStream().CopyTo($ms)
    throw "HTTP $([int]$_.Exception.Response.StatusCode): $($utf8.GetString($ms.ToArray()))"
  }
}
$job = Call "POST" "$Base/api/$Endpoint/generate" ([System.IO.File]::ReadAllBytes($Body))   # body = UTF-8 JSON file
$t0 = Get-Date
while ($true) {
  Start-Sleep -Seconds $Poll
  $s = Call "GET" "$Base/api/status/$($job.task_id)"
  if ($s.status -eq "completed") { break }
  if ($s.status -eq "failed") { throw "[$($s.error_code)] $($s.error)" }
  if (((Get-Date) - $t0).TotalSeconds -gt $Timeout) { throw "task $($job.task_id) not finished after $Timeout s" }
}
New-Item -ItemType Directory -Force $Out | Out-Null
$i = 0
foreach ($u in @($s.results)) {
  $i++; $ext = [System.IO.Path]::GetExtension(([uri]$u).AbsolutePath)
  $file = Join-Path $Out ($(if (@($s.results).Count -gt 1) { "${Name}_$i" } else { $Name }) + $ext)
  Invoke-WebRequest -Uri $u -OutFile $file -UseBasicParsing -TimeoutSec 600      # /api/files needs no key
  Write-Host "saved $file"
}
```

---

## 11. Checklist nhanh cho người tích hợp / AI agent

1. Bật máy chủ Webhook trong app; sao chép **port** và **API key**.
2. Luôn gửi `X-API-Key` ở các call generate/status/result/tasks/stop.
3. `POST /api/{image|video|grok|meta|openai}/generate` với body hợp lệ (`prompt` bắt buộc —
   trừ `upscale` của `omni_vids`), hoặc `POST /api/upscale/generate` với `image_path` /
   `image` và **không** có `prompt`.
4. Đọc `task_id` từ response `202`.
5. Hỏi `GET /api/status/{task_id}` mỗi 3–5 giây tới khi `completed` hoặc `failed`.
6. Khi `completed`: `GET` từng URL trong `results` để tải file.
7. Khi `failed`: xem `error_code` (vd `429` = hết quota) và `error` / `error_detail`.
8. Tôn trọng tỉ lệ theo từng model, số ảnh tham chiếu theo từng mode, và các tính
   năng chỉ dành cho ULTRA. Google Vids, Google Pics, Meta Muse và Dreamina từ chối giá trị sai bằng mã `400` có
   tên lỗi, không tự đổi về mặc định.
9. Muốn huỷ: `POST /api/stop/{task_id}` (hoặc `/api/stop` cho tất cả) — task chuyển ngay sang
   `failed` với `499 STOPPED_BY_CLIENT`.
10. Nhân vật: quản lý bằng `/api/characters` (§5.8), chọn theo từng task bằng `use_characters`
    (§6.3), upload trước ảnh của chúng bằng `/api/characters/preupload` (§5.9).
11. Dùng thư viện OpenAI hoặc tool "OpenAI-compatible"? Đặt base URL `http://<host>:<port>/v1`, API key =
    khoá webhook, `model` = id trong `GET /v1/models` - rồi theo §12 (ảnh trả luôn trong response, video thì
    hỏi trạng thái bằng `GET /v1/videos/{id}`).

---

## 12. API tương thích OpenAI (`/v1/*`)

Một API thứ hai, **chạy song song**, theo đúng dạng OpenAI: thư viện OpenAI (Python / JS) hay tool hỗ trợ
"OpenAI-compatible" (n8n, LiteLLM...) chỉ cần đổi base URL là dùng được. **Không thay thế** `/api/*`: hai bên
dùng chung hàng chờ, tài khoản, giới hạn và log; task tạo qua `/v1` vẫn xem được ở `/api/status/{id}`,
`/api/tasks` và dừng được bằng `/api/stop/{id}`. Tích hợp đang chạy không phải sửa gì.

```python
from openai import OpenAI
client = OpenAI(base_url="http://127.0.0.1:8765/v1", api_key="<API key của webhook>")
img = client.images.generate(model="flow/nano_banana_2", prompt="a red car", size="1536x1024")
print(img.data[0].url)
video = client.videos.create(model="flow/veo_31_lite", prompt="waves at sunset", seconds="8", size="1280x720")
```

- **Xác thực**: `Authorization: Bearer <API key>` (hoặc `X-API-Key`). Cần gói MAX như `/api/*`.
- **`model`**: một `id` trong `GET /v1/models` (§7) - vd `flow/nano_banana_2`, `flow/veo_31_lite`, `grok/video`,
  `dreamina/image/high_aes_general_v50`. Giá trị cũ của `/api/*` cũng nhận (`nano_banana_2`, `veo_31_lite`).
  Mỗi mục danh mục ghi các endpoint `/v1` dùng được trong `openai_endpoints`.
- **Lỗi** theo dạng OpenAI, đúng mã HTTP của lỗi:
  `{"error": {"message": "...", "type": "invalid_request_error", "param": "model", "code": "model_not_found"}}`.
  Lượt tạo bị lỗi giữ mã lỗi webhook, viết thường (`400 TOO_MANY_REFERENCES` → `"code": "too_many_references"`).
- **Mở rộng**: trường nào không thuộc chuẩn OpenAI được chuyển nguyên vào request `/api/*`, nên mọi tuỳ chọn
  của webhook vẫn dùng được: `reference_images` (có `name` để gắn `@tag`), `upscale`, `mode`, `use_characters`,
  `auto_fix_prompt`, `count`, `first_frame`, `reference_video`... (§5).

### 12.1 `POST /v1/images/generations` và `/v1/images/edits`

| Trường | Ý nghĩa |
|------|---------|
| `model` | id trong danh mục (bắt buộc). Gửi model video vào đây → `400 model_type_mismatch`. |
| `prompt` | Bắt buộc. |
| `n` | 1-10 (mặc định 1). Mỗi ảnh là một task riêng trong hàng chờ. |
| `size` | `RỘNGxCAO` hoặc `auto`. Đổi sang **tỉ lệ gần nhất mà model có** (`1792x1024` → `16:9`; `1536x1024` → `3:2` trên model có `3:2`, nhưng `4:3` trên `flow/nano_banana_2`, vốn không có `3:2`). Độ phân giải đầu ra là của model (Flow 2K / 4K dùng trường mở rộng `upscale`). |
| `quality` | GPT Image (`low` / `medium` / `high`; `standard` → medium, `hd` / `auto` → high) và Dreamina. Model khác bỏ qua. |
| `response_format` | `url` (mặc định - link `/api/files/...`) hoặc `b64_json`. |
| `image` / `images` (edits) | Tệp multipart (`image` hoặc `image[]`, **tên tệp** thành tên `@tag`) hoặc JSON: chuỗi data URI / base64, `{"image_url": "data:..."}`, hoặc một mục `reference_images`. **Link http(s) bị từ chối** - G-Labs không tự tải ảnh. Meta AI điền lần lượt `character_image`, `scene_image`, `style_image`. |
| `wait` (mở rộng) | Số giây chờ kết quả, 10-3600 (mặc định 600). Quá hạn → `504 timeout`; câu lỗi ghi id các task, task vẫn chạy tiếp (hỏi `/api/status/{id}`). |
| `mask`, `stream` | Không hỗ trợ → `400`. `background`, `style`, `output_format`, `moderation`, `user` được nhận và bỏ qua. |

Response `200` (dạng OpenAI + `task_ids`; `errors` liệt kê ảnh lỗi khi `n` > 1 mà có ảnh thành công):
```json
{ "created": 1794890977, "data": [ { "url": "http://127.0.0.1:8765/api/files/....png" } ], "task_ids": ["a1b2c3d4"] }
```

### 12.2 `POST /v1/videos`, `GET /v1/videos[/{id}[/content]]`, `DELETE /v1/videos/{id}`

| Trường | Ý nghĩa |
|------|---------|
| `model`, `prompt` | Bắt buộc (id danh mục; model ảnh → `400`). |
| `seconds` | `"8"` hoặc `8`. Phải là một giá trị trong `durations` / nằm trong `duration_range` của model, không thì `400 invalid_seconds`. Không gửi → mặc định của model. |
| `size` | `RỘNGxCAO` → **tỉ lệ** gần nhất + **độ phân giải** của model gần cạnh ngắn nhất (`1280x720` → 16:9, 720p). |
| `input_reference` | Một ảnh = **khung đầu** (tệp multipart, data URI, hoặc `{"image_url": "data:..."}`). Nhiều ảnh → trường mở rộng `reference_images` (kèm `mode`, vd `"components"` / `"omni"`). |

`POST` trả đối tượng video ngay; lỗi request mà webhook bắt được trong vài giây đầu (model, mode, ảnh sai...)
trả luôn `4xx`:
```json
{ "id": "0043608a", "object": "video", "model": "flow/veo_31_lite", "status": "queued", "progress": 0,
  "created_at": 1794890977, "completed_at": null, "expires_at": null, "prompt": "waves at sunset",
  "seconds": "8", "size": "1280x720", "remixed_from_video_id": null, "error": null }
```
- `status`: `queued` → `in_progress` → `completed` | `failed` (`error: {code, message}`); `progress` 0 / 50 / 100.
  Video xong có thêm `urls` (mở rộng): link tải, như `/api/status`.
- `GET /v1/videos/{id}/content` trả tệp MP4 (chỉ `variant=video`). `GET /v1/videos?limit=20&order=desc&after=<id>`
  liệt kê các video tạo qua `/v1/videos`.
- `DELETE /v1/videos/{id}` dừng video nếu còn chạy (như `/api/stop`) và bỏ khỏi danh sách →
  `{"id": "...", "object": "video.deleted", "deleted": true}`. Tệp đã lưu trong thư mục output vẫn giữ nguyên.
- Không hỗ trợ `remix_video_id`. Lưu ý: OpenAI báo API video (Sora) của họ ngừng từ 24/09/2026; SDK chính thức
  vẫn có `client.videos` (kèm cảnh báo) và endpoint này giữ đúng dạng đó, dạng các cổng OpenAI-compatible khác
  cũng dùng.

### 12.3 Từng nhà cung cấp đọc các trường OpenAI thế nào

| id model | Ảnh (`/v1/images/*`) | Video (`/v1/videos`) |
|------|---------|--------|
| `flow/*` | `size` → `aspect_ratio`; ảnh → `reference_images` (`@tag`) | không ảnh → `text_to_video`, `input_reference` → `start_image`; `size` → `aspect_ratio` + `resolution`; `seconds` → `video_length` |
| `pics/nano_pics` | `text_to_image` / `image_to_image`, `keep: 1` | - |
| `vids/omni_vids` | - | `text_to_video` / `start_image`, `resolution`, `video_length` |
| `muse/*` | `text_to_image` / `image_to_image`, `count: 1` | `text_to_video` / `image_to_video`, `count: 1`, `video_length` |
| `dreamina/*` | `text_to_image` / `image_to_image`, `count: 1`, chuyển `quality` | `text_to_video` / `image_to_video`, `count: 1`, `resolution`, `video_length` |
| `grok/*` | `t2i` / `i2i` | `t2v` / `i2v` (`input_reference` = khung đầu), `resolution`, `video_length` |
| `meta/*` | `t2i` / `i2i`; ảnh điền `character_image`, `scene_image`, `style_image` | `t2v` / `i2v` (`input_reference` = `start_image`); bỏ qua `seconds` (độ dài cố định) |
| `openai/*` | `size` → một tỉ lệ của model; `quality` low / medium / high | - |

Những thứ khác (khung cuối, components / Omni nhiều ảnh, giọng, sửa video, upscale 2K / 4K, nhân vật
thư viện) dùng các trường mở rộng ở §5 - vd `"mode": "components"` + `"reference_images": [...]` trên
`/v1/videos`.

### 12.4 Mã lỗi của `/v1/*`

| HTTP | `code` | Khi nào |
|------|------|--------|
| 400 | `missing_model`, `missing_prompt`, `missing_image` | Thiếu trường bắt buộc (`image` của edits) |
| 404 | `model_not_found` | `model` không có trong `GET /v1/models` |
| 400 | `model_type_mismatch` | Model video gửi vào `/v1/images/*`, hoặc model ảnh vào `/v1/videos` |
| 400 | `invalid_size`, `invalid_seconds`, `invalid_n`, `invalid_wait`, `invalid_response_format` | Giá trị sai (câu lỗi ghi các giá trị model nhận) |
| 400 | `image_url_not_supported`, `invalid_image`, `too_many_references` | Link ảnh http(s), ảnh không đọc được, hơn một `input_reference` |
| 400 | `mask_not_supported`, `stream_not_supported`, `remix_not_supported` | Tính năng OpenAI mà G-Labs không có |
| 401 / 403 | `invalid_api_key` / `plan_required` | Sai khoá / gói không phải MAX |
| 404 | `video_not_found`, `variant_not_available`, `file_not_found` | Sai id video, `variant` khác `video`, tệp không còn |
| 400 | `video_not_ready` | Gọi `/content` khi video chưa `completed` |
| 504 | `timeout` | Ảnh vẫn đang tạo sau `wait` giây - task vẫn chạy tiếp |
| 4xx / 5xx | mã lỗi webhook, viết thường | Lượt tạo bị lỗi: `too_many_references`, `resource_exhausted` (429), `rate_limited`, `stopped_by_client` (499)... - cùng nguyên nhân như §8 |

### 12.5 Ví dụ

**cURL - tạo ảnh, sửa ảnh (multipart), video (tạo → hỏi → tải)**
```bash
KEY=<api-key-của-bạn>; BASE=http://127.0.0.1:8765/v1
curl $BASE/models -H "Authorization: Bearer $KEY"
curl $BASE/images/generations -H "Authorization: Bearer $KEY" -H "Content-Type: application/json" \
  -d '{"model": "flow/nano_banana_2", "prompt": "a red car on a beach", "size": "1536x1024"}'
curl $BASE/images/edits -H "Authorization: Bearer $KEY" \
  -F model=flow/nano_banana_2 --form-string "prompt=@car parked in front of @house" \
  -F "image[]=@car.png" -F "image[]=@house.png"
curl $BASE/videos -H "Authorization: Bearer $KEY" -H "Content-Type: application/json" \
  -d '{"model": "flow/veo_31_lite", "prompt": "waves at sunset", "seconds": "8", "size": "1280x720"}'
curl $BASE/videos/<id> -H "Authorization: Bearer $KEY"                      # tới khi "status": "completed"
curl $BASE/videos/<id>/content -H "Authorization: Bearer $KEY" -o waves.mp4
```

**Python (gói `openai` chính thức)**
```python
import time
from openai import OpenAI
client = OpenAI(base_url="http://127.0.0.1:8765/v1", api_key="<api-key-của-bạn>", timeout=700)

img = client.images.edit(model="dreamina/image/high_aes_general_v50", prompt="@cat sleeping on @sofa",
                         image=[open("cat.png", "rb"), open("sofa.png", "rb")])
print(img.data[0].url)

video = client.videos.create(model="flow/veo_31_lite", prompt="a cat jumps", seconds="8", size="720x1280",
                             input_reference=open("cat.png", "rb"),
                             extra_body={"use_characters": False})       # trường mở rộng bất kỳ của webhook
while video.status in ("queued", "in_progress"):
    time.sleep(5)
    video = client.videos.retrieve(video.id)
if video.status == "completed":
    client.videos.download_content(video.id).write_to_file("cat.mp4")
else:
    print(video.error)
```

**JavaScript (gói `openai` chính thức)**
```js
import OpenAI from "openai";
const client = new OpenAI({ baseURL: "http://127.0.0.1:8765/v1", apiKey: "<api-key-của-bạn>", timeout: 700_000 });
const img = await client.images.generate({ model: "grok/image", prompt: "a lighthouse", size: "1024x1536" });
console.log(img.data[0].url);
```

### 12.6 Lưu ý

- **Dùng `/api/*` hay `/v1/*`?** Dùng `/v1/*` khi thư viện / tool đã nói chuẩn OpenAI. Dùng `/api/*` cho các
  trường hợp còn lại và khi cần điều khiển chi tiết từng trang (đủ trường ở §5, nhận `202` rồi tự hỏi trạng
  thái, không giữ kết nối trong lúc tạo ảnh).
- **Thời gian chờ.** `/v1/images/*` giữ kết nối tới khi ảnh xong (tối đa `wait`, mặc định 600 s): đặt timeout
  của client HTTP lớn hơn `wait` (ví dụ Python dùng 700 s). Cần nhiều ảnh? Dùng `n` (một request) thay vì nhiều
  request song song cùng chờ.
- **Tool.** Ở tool có thông tin đăng nhập "OpenAI" (n8n, Make, LiteLLM, Open WebUI...), đặt base URL là
  `http://<host>:<port>/v1` và API key là khoá webhook; chọn model theo id trong danh mục.
- **Máy khác.** Dùng host hiện ở tab Webhook (IP LAN) trong base URL; link kết quả cũng dùng host đó.
- **Trường mở rộng trong SDK.** Trường ngoài chuẩn OpenAI đặt trong `extra_body` (Python) hoặc thêm thẳng vào
  body (JS / cURL).
