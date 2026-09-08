<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Satu aplikasi desktop untuk menghasilkan gambar &amp; video secara massal di seluruh AI besar — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI, dan ChatGPT GPT Image 2.</b></p>

<p align="center">
  <a href="../../README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
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
  <b>Bahasa Indonesia</b> ·
  <a href="README.ko.md">한국어</a>
</p>

![G-Labs Studio](../screenshots/01-image.png)

---

## Instalasi

Unduh build terbaru dari **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**:

| Platform | Berkas |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-v<version>-win.exe` — jalankan installer (admin/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-v<version>-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-v<version>-mac-intel.dmg` |

**Peluncuran pertama di macOS** — aplikasi ini tidak ditandatangani oleh Apple, sehingga macOS mengarantinanya. Buka pertama kali dengan **klik kanan → Open**, atau hapus penanda tersebut dari Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**Anda memerlukan akun G-Labs.** Buka aplikasi, masuk dengan Google, dan pilih paket. Paket (**FREE / PLUS / MAX**) membuka berbagai alat dan model; Anda dapat membelinya dari dalam aplikasi (QR bank, PayPal, atau USDT). Satu akun berjalan di **satu mesin pada satu waktu** — masuk di tempat lain akan mengeluarkan mesin sebelumnya. Lencana di kiri bawah bilah sisi menampilkan tingkat Anda saat ini.

Aplikasi ini **memperbarui dirinya sendiri**: ia memeriksa GitHub Releases saat diluncurkan dan dapat mengunduh serta memasang versi baru dari dalam aplikasi.

---

## Menjalankan pertama kali

1. **Buka aplikasi dan masuk dengan Google.** Lencana tingkat (kiri bawah) mengonfirmasi paket Anda.
2. **Hubungkan akun untuk alat yang akan Anda gunakan** (Settings → tab akun yang sesuai):
   - Akun **Google** → Flow Image / Flow Video
   - Akun **ChatGPT** → GPT Image 2
   - Akun **Meta** → Meta Media
   - **Grok** → berjalan melalui tab `grok.com` tempat Anda masuk lewat ekstensi browser pendamping (Auth Helper) — tanpa kumpulan akun
   Setiap tab akun menampilkan **"Active: N accounts"** di bilah judulnya sehingga Anda tahu berapa banyak yang dapat dipakai.
3. **Pilih halaman dari bilah sisi kiri** dan mulai menghasilkan. Setiap halaman generasi memiliki ritme yang sama: ketik atau impor prompt di kiri, prompt itu masuk ke **tabel** di kanan, lalu tekan **Run**.

Setiap kepala halaman membawa **bilah status** langsung — *Running · Queued · Done · Failed · Accounts* — sehingga Anda dapat melihat seluruh batch sekilas. Klik **Queued** untuk membuka pengelola antrean, **Accounts** untuk melompat ke pengaturan akun.

---

## Fitur

- **Setiap generator besar, satu aplikasi** — Google Flow (gambar + video), Grok Imagine, Meta AI (vibes.ai) dan OpenAI GPT Image 2, masing-masing di halamannya sendiri dengan model dan rasio yang didukung penyedia tersebut.
- **Dirancang untuk batch** — tempel daftar prompt (satu per baris) atau impor berkas `.txt`/Excel; masing-masing menjadi satu baris. Gambar referensi dicocokkan otomatis berdasarkan nama berkas. Jalankan seluruh daftar dengan konkurensi yang Anda pilih.
- **Tambahkan dulu, jalankan saat siap** — baris masuk ke antrean; **Run / Pause / Stop** terpisah. Tidak ada yang dimulai sampai Anda memerintahkannya, dan pengelola antrean memungkinkan Anda menyusun ulang dan memeriksa.
- **Perpustakaan karakter** — simpan sebuah karakter sekali (gambar referensi + suaranya sendiri + catatan) dan sisipkan ke prompt mana pun dengan `@name`; video mempertahankan tampilan dan suara karakter itu.
- **Workflow (graf node)** — hubungkan node menjadi sebuah pipeline: prompt → gambar → video → ekstrak bingkai terakhir → video berikutnya, ditambah node **Merge Video** yang menggabungkan dua klip dengan pemangkasan dan transisi (crossfade, wipe, slide, dissolve…). Node batch mengulang seluruh rantai per prompt atau per gambar.
- **Webhook API** — server REST lokal sehingga skrip dan agen AI dapat mengirim pekerjaan gambar/video/Grok/Meta/OpenAI dan memeriksa hasilnya.
- **Image Upscaler** dan **Video Editor** (potong, gabung, slideshow) untuk penyelesaian.
- **Tangguh** — hasil diverifikasi dan disimpan otomatis; sesi dipulihkan; baris yang gagal dicoba ulang.
- **Tema gelap / terang**, antarmuka yang peka terhadap tingkat, dan **15 bahasa**.

---

## Halaman

### 🖼 Flow Image — generasi gambar Google Flow

![Flow Image](../screenshots/01-image.png)

Hasilkan gambar secara massal dengan **Nano Banana Pro / 2 / Lite**. Pilih model, rasio aspek, dan resolusi (**1K / 2K / 4K** — 2K/4K menggunakan upscaler model), atur berapa banyak baris yang berjalan sekaligus dan jeda di antaranya. Tempel prompt (atau impor berkas), lampirkan gambar referensi per baris (seret satu folder dan mereka dicocokkan otomatis berdasarkan nama berkas), dan gunakan `@name` untuk memasukkan karakter. **Run** mengirim seluruh daftar ke antrean.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Tiga tab: **Text / Frames → Video** (prompt teks, atau bingkai awal/akhir), **Image / Video ingredients → Video** (gambar referensi atau video referensi), dan **Scene stitch → Video**. Model: **Veo 3.1 Fast / Lite / Quality** dan **Omni Flash**. Pilih rasio aspek, upscale (720p / 1080p / 4K), dan seed. Arahkan kursor ke **?** pada bilah tab untuk penjelasan sederhana tentang frames vs. ingredients.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Text-to-image, image-to-image, text-to-video, dan image-to-video melalui Grok Imagine (tab `grok.com` tempat Anda masuk lewat ekstensi Auth Helper). Gambar menawarkan **8 rasio aspek** (termasuk 4:3, 21:9, 5:2); video dihasilkan pada **480p / 720p / 1080p**. Image-to-video memiliki dua mode: **First frame** (gambar membuka klip) dan **Reference** (hingga 14 gambar pemandu).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Generasi gambar dan video melalui Meta AI. Mode: text-to-image, image-to-image (komponen Character / Scene / Style), text-to-video, dan image-to-video (bingkai awal / akhir).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

Hasilkan dengan OpenAI **GPT Image 2** menggunakan akun ChatGPT Anda, dengan hingga 5 gambar referensi. Pilih rasio (10 opsi termasuk 21:9, 4:5 dan **custom** — di mana Anda menuliskan rasio dalam prompt), kualitas, mode prompt, reasoning effort, dan pencarian web.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Tingkatkan resolusi satu folder gambar secara lokal — pilih target dan biarkan ia memproses antrean, dengan kemajuan dan status per baris (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

Bangun perpustakaan karakter yang dapat dipakai ulang: sebuah gambar referensi, suara kustom opsional, serta catatan penampilan/kepribadian. Tandai dengan `@name` di prompt Flow mana pun dan generasi mempertahankan identitas itu.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Kanvas node visual. Klik kanan soket sebuah node dan menu hanya menawarkan node yang cocok — pilih satu dan ia terhubung otomatis. Rantai prompt → generate → video → **Extract Frame** → video berikutnya, dan gunakan **Merge Video** untuk menggabungkan dua klip (pangkas setiap ujung, pilih transisi). Simpan/muat seluruh graf sebagai berkas `.json`; **Run Flow** menjalankannya dari awal hingga akhir.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Ubah aplikasi menjadi server otomasi lokal. Jalankan, salin API key Anda, dan POST pekerjaan ke `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` atau `/api/openai/generate`, lalu periksa `/api/status/<id>`. Halaman ini mencantumkan setiap model dan rasio aspek yang didukungnya. Skema lengkap: [`docs/WEBHOOK_INTEGRATION.en.md`](../WEBHOOK_INTEGRATION.en.md).

---

## Tempat penyimpanan

| Apa | macOS | Windows |
|---|---|---|
| Keluaran (gambar / video) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Pengaturan, sesi, akun | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Pengaturan, daftar prompt, sesi, perpustakaan karakter, dan daftar akun Anda disimpan dan dipulihkan saat berikutnya Anda membuka aplikasi.

---

## Pemecahan masalah

**Semuanya terkunci / layar pembelian terus terbuka** — paket Anda kedaluwarsa, atau akun sedang masuk di mesin lain. Periksa lencana tingkat (kiri bawah) dan perpanjang.

**Generasi Grok tidak melakukan apa pun** — Grok berjalan melalui tab `grok.com` Anda. Pasang/aktifkan ekstensi browser **Auth Helper** (Settings → Grok) dan pastikan Anda masuk ke grok.com.

**"Active: 0 accounts" di sebuah halaman** — tambahkan atau aktifkan kembali akun di tab akun halaman itu (Settings), atau tokennya kedaluwarsa — tekan **Refresh all**.

**macOS mengatakan aplikasi rusak / tidak dapat dibuka** — aplikasi tidak ditandatangani oleh Apple. Klik kanan → **Open** pertama kali, atau jalankan `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Pembaruan tidak mau terpasang** — unduh build terbaru secara manual dari [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
