<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Satu aplikasi desktop untuk menghasilkan gambar &amp; video secara massal di seluruh AI besar - Google Flow (Veo 3.1, Omni Flash, Nano Banana), Google Vids, Google Pics, ChatGPT GPT Image 2, Meta Vibes, dan Grok - ditambah alat video, workflow node, dan Webhook API.</b></p>

<p align="center">
  <a href="README.en.md">English</a> ·
  <a href="../../README.md">Tiếng Việt</a> ·
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

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Unduh - Windows" src="https://img.shields.io/badge/Unduh-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Unduh - macOS (Apple Silicon)" src="https://img.shields.io/badge/Unduh-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Unduh - macOS (Intel)" src="https://img.shields.io/badge/Unduh-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Instalasi

### Langkah 1 - Pilih versi yang tepat untuk perangkatmu

Unduh versi terbaru dari **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**, lalu pilih berkas yang cocok dengan perangkatmu:

| Perangkatmu | Unduh | Google Drive | Catatan |
|---|---|---|---|
| 🪟 **Windows 10/11 (64-bit)** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | Untuk PC Windows apa pun |
| 🍎 **Mac dengan chip Apple (M1/M2/M3/M4)** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Mac dari sekitar akhir 2020 ke atas |
| 🍎 **Mac dengan chip Intel** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Mac lama (sebelum 2020) |

**Tidak yakin chip Mac-mu apa?** Klik menu  (kiri atas) → **About This Mac**:
- Baris **Chip** bertuliskan “Apple M1 / M2 / M3…” → unduh versi **arm64**.
- Baris **Processor** bertuliskan “Intel…” → unduh versi **intel**.

> Versi **Intel** tetap jalan di Mac chip Apple (hanya lebih lambat), tapi versi **arm64** **tidak bisa dibuka** di Mac Intel - jadi pilih yang tepat.

### Langkah 2 - Instal

<details open>
<summary><b>🪟 Di Windows</b></summary>

1. Buka **`G-Labs-Studio-win.exe`** yang sudah diunduh.
2. Jika muncul **“Windows protected your PC”** (SmartScreen): klik **More info** → **Run anyway**. *(Aplikasi belum ditandatangani dengan sertifikat Microsoft, jadi ditandai - bukan virus.)*
3. Klik **Yes** pada permintaan admin (UAC), lalu ikuti pemasang sampai selesai.
4. Jalankan dari **Start Menu** atau pintasan **Desktop**.

</details>

<details open>
<summary><b>🍎 Di macOS</b></summary>

1. Buka **`.dmg`** yang diunduh, lalu **seret G-Labs Studio ke folder Applications**.
2. Buka **Applications**, **klik kanan** (atau Control-klik) **G-Labs Studio** → **Open** → klik **Open** lagi di dialog. *(Aplikasi tidak ditandatangani Apple, jadi kamu harus membukanya begini pada **kali pertama**; setelahnya terbuka normal.)*
3. Jika macOS bilang aplikasi **“rusak / tidak bisa dibuka”**, atau tidak ada tombol Open, buka **Terminal** dan tempel:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   Lalu buka aplikasi lagi.

</details>

### Langkah 3 - Masuk & pilih paket

**Kamu butuh akun G-Labs.** Buka aplikasi, masuk dengan Google, dan pilih paket. Paket (**BASIC / PLUS / MAX**) membuka alat dan model yang berbeda; kamu bisa membeli dari dalam aplikasi (QR bank, PayPal, atau USDT). Satu akun berjalan di **satu mesin dalam satu waktu** - masuk di tempat lain akan mengeluarkan mesin sebelumnya. Lencana di kiri bawah bilah sisi menunjukkan tingkatmu saat ini. Butuh beberapa perangkat sekaligus? Kamu bisa membeli paket **Team** (harganya naik sesuai jumlah perangkat tambahan yang kamu pilih).

> **Baru pindah dari versi lama (G-Labs Automation)?** Versi baru **tidak** membawa akunmu. Kamu perlu **masuk ke semua akun lagi** (Google/Flow, ChatGPT, Meta…) di G-Labs Studio yang baru.

Aplikasi **memperbarui dirinya sendiri**: memeriksa GitHub Releases saat dibuka dan bisa mengunduh serta memasang versi baru dari dalam aplikasi.

---

## Menjalankan pertama kali

1. **Buka aplikasi dan masuk dengan Google.** Lencana tingkat (kiri bawah: **BASIC / PLUS / MAX**) mengonfirmasi paket Anda.
2. **Hubungkan akun untuk alat yang akan Anda gunakan** (**Pengaturan** → tab akun yang sesuai):
   - **Akun Flow** → Flow Image / Flow Video
   - **Akun Google** → **Google Vids** dan **Google Pics** (kedua halaman berbagi akun Google ini; setiap akun diaktifkan terpisah untuk video Vids dan untuk gambar Pics)
   - **Akun ChatGPT** → GPT Image 2
   - **Akun Vibes** → Meta Vibes
   - **Akun Grok** → tanpa penyimpanan akun: tab ini memandu Anda memasang ekstensi browser **Auth Helper**, lalu Grok berjalan melalui tab `grok.com` tempat Anda sudah masuk di Chrome

   Setiap tab akun menampilkan **"Aktif: N akun"** di bilah judulnya sehingga Anda tahu berapa banyak yang dapat dipakai.
3. **Pilih halaman dari bilah sisi kiri** dan mulai menghasilkan. Setiap halaman generasi mengikuti ritme yang sama: ketik atau impor prompt di kiri, prompt itu masuk ke **tabel** di kanan, lalu tekan **Run**.

Setiap kepala halaman membawa **bilah status** langsung - *Berjalan · Antre · Selesai · Gagal · Akun* - sehingga Anda dapat melihat seluruh batch sekilas. Klik **Antre** untuk membuka pengelola antrean, klik **Akun** untuk melompat ke pengaturan akun.

---

## Fitur

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **Setiap generator besar, satu aplikasi** - Google Flow (gambar + video), Google Vids, Google Pics, GPT Image 2, Meta Vibes, dan Grok, masing-masing di halamannya sendiri dengan model dan rasio yang didukung penyedia tersebut.
- **Dirancang untuk batch** - tempel daftar prompt (satu per baris) atau impor `.txt`/Excel; setiap prompt menjadi satu baris. Gambar referensi dicocokkan otomatis berdasarkan nama berkas. Jalankan seluruh daftar dengan jumlah thread paralel yang Anda pilih.
- **Tambahkan dulu, jalankan saat siap** - baris masuk ke antrean; **Run / Pause / Stop** terpisah. Tidak ada yang dimulai sampai Anda memerintahkannya, dan pengelola antrean memungkinkan Anda menyusun ulang dan memeriksa.
- **Penghapusan otomatis logo Gemini ✦** - gambar Google Pics dan video Google Vids dibersihkan tepat setelah diunduh (aktifkan **Tampilkan logo Gemini** untuk mempertahankannya). Berkas tanpa logo dibiarkan apa adanya.
- **Perpustakaan karakter** - simpan sebuah karakter sekali (gambar referensi + suara + catatan) dan panggil dengan `@name` di prompt Flow Image, Flow Video, dan Google Vids agar adegan tetap konsisten.
- **Workflow (graf node)** - hubungkan node menjadi sebuah pipeline: prompt → gambar → video → ekstrak frame terakhir → video berikutnya, ditambah node **Gabung Video** yang menggabungkan dua klip dengan transisi.
- **Alat Video** - edit video berbasis timeline, slideshow gambar yang sinkron dengan subtitle, pembagian video, ekstraksi frame, dan penghapusan logo video, langsung di dalam aplikasi.
- **Upscaler Gambar** di komputer Anda sendiri dan **Webhook API** untuk otomasi.
- **Tangguh** - hasil diverifikasi dan disimpan otomatis; sesi dipulihkan; baris yang gagal dicoba ulang.
- **Tema terang / gelap**, antarmuka yang peka terhadap tingkat, dan **15 bahasa**.

---

## Halaman

### 🖼 Flow Image - generasi gambar Google Flow

![Flow Image](../screenshots/en/flow-image.webp)

Hasilkan gambar secara massal dengan **Nano Banana Pro / 2 / 2 Lite**. Pilih model, rasio aspek, dan resolusi (**1K / 2K / 4K** - 2K/4K menggunakan upscaler model), atur berapa banyak baris yang berjalan sekaligus dan jeda di antaranya. Tempel prompt (atau impor berkas), lampirkan gambar referensi per baris (jatuhkan satu folder dan gambar dicocokkan otomatis berdasarkan nama berkas), dan gunakan `@name` untuk memasukkan karakter. Sakelar **Tampilkan logo Veo / Gemini** (mati secara default) digunakan bersama dengan halaman Flow Video. **Run** mengirim seluruh daftar ke antrean.

### 🎬 Flow Video - Veo &amp; Omni Flash

![Flow Video](../screenshots/en/flow-video.webp)

Tiga tab: **Teks / Frame → Video** (prompt teks, atau frame awal/akhir), **Bahan Gambar / Video → Video** (gambar referensi atau video referensi), dan **Rantai Adegan → Video**. Model: **Veo 3.1 Fast / Lite / Quality** dan **Omni Flash**. Pilih rasio aspek, upscale (720p / 1080p / 4K), dan seed. Arahkan kursor ke **?** pada bilah tab untuk penjelasan sederhana tentang frame vs. bahan.

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

Buat video dengan akun Google Anda dalam tiga tab: **Teks → Video**, **Gambar → Video** (satu gambar pembuka), dan **Komponen → Video** (hingga 3 gambar komponen). Pilih lanskap/potret, 720p / 1080p, dan durasi 3-10 detik - atau tulis tag seperti `[4s]` di prompt untuk memberi setiap baris durasinya sendiri. Video yang sudah jadi dapat di-upscale ke 1080p langsung dari tabel. Setiap akun memiliki kuota yang diukur dalam detik video; tambahkan lebih banyak akun untuk berjalan lebih cepat. Logo Gemini ✦ pada video yang diunduh (720p / 1080p) dihapus otomatis kecuali Anda mengaktifkan **Tampilkan logo Gemini**.

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

Dua tab: **Teks → Gambar** dan **Gambar → Gambar** dengan **hingga 14 gambar referensi** (karakter, objek, adegan, gaya). Setiap putaran Google mengembalikan 3-9 gambar; **Gambar disimpan per putaran** menentukan berapa yang disimpan (1-4 atau semua). 10 rasio aspek, termasuk 21:9, 3:2, dan 5:4. Setiap putaran memakan 1 putaran Google Pics berapa pun jumlah gambarnya; prompt yang ditolak oleh kebijakan konten tidak memakan apa pun. Pics berbagi **Akun Google** dengan Google Vids.

**Penghapusan otomatis logo Gemini ✦:** gambar Pics yang diunduh dihapus tanda ✦ di sudut kanan bawahnya tepat setelah diunduh, menggunakan peta logo yang diukur khusus untuk Google Pics - campuran logo dibalik, sehingga tekstur asli di bawahnya dipulihkan alih-alih dikaburkan. Gambar yang tidak terdeteksi logo dibiarkan apa adanya. Untuk mempertahankan logo, aktifkan **Tampilkan logo Gemini**.

### ✨ GPT Image 2 - OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

Hasilkan dengan OpenAI **GPT Image 2** menggunakan akun ChatGPT Anda, dengan hingga 5 gambar referensi. Pilih rasio (10 opsi termasuk 21:9, 4:5, dan **custom** - di mana Anda menuliskan rasio dalam prompt), kualitas, mode prompt, tingkat reasoning, dan pencarian web.

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

Buat gambar dan video di Meta Vibes dalam empat tab: **Teks → Gambar**, **Teks → Video**, **Gambar → Gambar** (gambar karakter / adegan / gaya), dan **Gambar → Video** (frame awal / akhir). Diantrekan dan diunduh secara otomatis.

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

Teks → Gambar, Gambar → Gambar, Teks → Video, dan Gambar → Video melalui Grok Imagine (tab `grok.com` tempat Anda sudah masuk, lewat ekstensi Auth Helper). Gambar tersedia dalam **8 rasio aspek** (termasuk 4:3, 21:9, 5:2); video dirender pada **480p / 720p / 1080p**. Gambar → Video memiliki dua mode: **Bingkai pertama** (gambar membuka klip) dan **Gambar referensi** (hingga 14 gambar pemandu).

### 👤 Karakter

![Karakter](../screenshots/en/characters.webp)

Bangun pemeran yang dapat dipakai ulang: sebuah gambar referensi, suara (salah satu suara bawaan Flow, dengan deskripsi cara bicara opsional), serta catatan penampilan/kepribadian. Tandai dengan `@name` di prompt Flow Image, Flow Video, dan Google Vids dan generasi mempertahankan identitas itu (suara hanya dipakai oleh Flow Video; Google Vids memakai gambarnya).

### 🔗 Workflow

![Workflow](../screenshots/en/workflow.webp)

Kanvas node visual. Klik kanan soket sebuah node dan menu hanya menawarkan node yang cocok - pilih satu dan ia terhubung sendiri. Tersedia node untuk Flow Image, Flow Video, Grok, Meta, dan GPT Image 2. Rantai prompt → gambar → video → **Ekstrak Frame** → video berikutnya, dan gunakan **Gabung Video** untuk menggabungkan dua klip (pangkas setiap ujung, pilih transisi). Simpan/muat seluruh graf sebagai berkas `.json` (format: [`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)); **Run Flow** menjalankannya dari awal hingga akhir.

### 🎞 Alat Video

Lima tab dalam satu halaman:

**Edit Video** - timeline untuk video, subtitle SRT, dan audio: potong, bagi, susun ulang, sesuaikan otomatis, lalu ekspor satu video jadi.

![Edit Video](../screenshots/en/vt-video.webp)

**Slideshow gambar yang cocok dengan file subtitle** - muat gambar dan berkas `.srt`; setiap gambar otomatis dicocokkan dengan satu baris subtitle, dengan efek gerak, overlay, dan gaya subtitle.

![Slideshow gambar yang cocok dengan file subtitle](../screenshots/en/vt-slideshow.webp)

**Bagi video menjadi segmen** - berdasarkan jumlah bagian, durasi tetap atau acak, daftar stempel waktu, atau daftar rentang A-B; satu berkas atau satu batch penuh, dengan akselerasi GPU bila tersedia.

![Bagi video menjadi segmen](../screenshots/en/vt-slicer.webp)

**Ekstrak frame dari video** - berdasarkan jumlah total, interval waktu, interval frame, atau gerakan; satu berkas atau satu folder penuh.

![Ekstrak frame dari video](../screenshots/en/vt-extractor.webp)

**Hapus logo video** - menghapus logo ✦ dari video Google Vids pada 720p dan 1080p (lanskap atau potret), dengan pratinjau sebelum/sesudah di aplikasi. Video tanpa logo dilewati; berkas asli dipertahankan dan hasilnya disimpan sebagai `<nama>_nologo.mp4`.

![Hapus logo video](../screenshots/en/vt-logo.webp)

### 🔍 Upscaler Gambar

![Upscaler Gambar](../screenshots/en/upscaler.webp)

Perbesar dan pertajam gambar langsung di komputer Anda - tambahkan gambar satu per satu atau satu folder penuh, pilih model AI (Real-ESRGAN, UltraSharp, Remacri…) dan skala 2x-8x, pantau kemajuan per baris, dan bandingkan sebelum/sesudah.

### 🌐 Webhook API

![Webhook API](../screenshots/en/webhook.webp)

Ubah aplikasi menjadi server otomasi lokal (paket MAX) sehingga n8n, Make, Zapier, skrip, atau agen AI dapat mengirim pekerjaan ke antrean aplikasi. Jalankan, salin API key Anda, dan POST pekerjaan ke `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate`, `/api/openai/generate` atau `/api/upscale/generate`, lalu periksa `/api/status/<id>`. Halaman ini mencantumkan setiap model dan rasio aspek yang didukungnya. Skema lengkap: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Tempat penyimpanan

| Apa | macOS | Windows |
|---|---|---|
| Keluaran (gambar / video) | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| Pengaturan, sesi, akun, karakter | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Setiap halaman memiliki subfolder sendiri di dalam `output` (satu folder lebih kecil per putaran); Anda dapat mengubah folder penyimpanan di setiap halaman. Pengaturan, daftar prompt, sesi, perpustakaan karakter, dan daftar akun Anda disimpan dan dipulihkan saat berikutnya Anda membuka aplikasi.

---

## Pemecahan masalah

**Semuanya terkunci / layar pembelian terus terbuka** - paket Anda kedaluwarsa, atau akun sedang masuk di mesin lain. Periksa lencana tingkat (kiri bawah) dan perpanjang. Google Vids dan Google Pics memerlukan paket PLUS/MAX; Webhook API memerlukan MAX.

**Generasi Grok tidak melakukan apa pun** - Grok berjalan melalui tab `grok.com` Anda. Pasang/aktifkan ekstensi browser **Auth Helper** (Pengaturan → Akun Grok) dan pastikan Anda sudah masuk ke grok.com.

**Google Pics mengatakan tidak ada akun** - Pics memakai akun Google Vids. Tambahkan satu di Pengaturan → **Akun Google**.

**"Aktif: 0 akun" di sebuah halaman** - tambahkan atau aktifkan kembali akun di tab akun halaman itu (Pengaturan), atau tokennya kedaluwarsa - tekan **Segarkan Semua**.

**Windows memblokirnya dengan "Windows protected your PC"** - klik **More info → Run anyway**. Aplikasi ini belum ditandatangani dengan sertifikat Microsoft, jadi ditandai - ini bukan virus.

**macOS mengatakan aplikasi rusak / tidak dapat dibuka** - aplikasi belum ditandatangani oleh Apple. Klik kanan → **Open** pertama kali, atau jalankan `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Pembaruan tidak terpasang** - unduh build terbaru secara manual dari [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
