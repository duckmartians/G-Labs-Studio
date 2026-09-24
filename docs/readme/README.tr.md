<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Her büyük yapay zekâda toplu görüntü ve video üretmek için tek bir masaüstü uygulaması — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI ve ChatGPT GPT Image 2.</b></p>

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
  <b>Türkçe</b> ·
  <a href="README.ur.md">اردو</a> ·
  <a href="README.ar.md">العربية</a> ·
  <a href="README.de.md">Deutsch</a> ·
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="İndir — Windows" src="https://img.shields.io/badge/%C4%B0ndir-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="İndir — macOS (Apple Silicon)" src="https://img.shields.io/badge/%C4%B0ndir-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="İndir — macOS (Intel)" src="https://img.shields.io/badge/%C4%B0ndir-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Kurulum

### Adım 1 — Makinen için doğru sürümü seç

En son sürümü **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** üzerinden indir, sonra makinene uygun dosyayı seç:

| Makinen | İndir | Google Drive | Notlar |
|---|---|---|---|
| 🪟 **Windows 10/11 (64 bit)** | [`G-Labs-Studio-win.exe`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | Her Windows PC için |
| 🍎 **Apple çipli Mac (M1/M2/M3/M4)** | [`G-Labs-Studio-mac-arm64.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Yaklaşık 2020 sonundan itibaren Mac'ler |
| 🍎 **Intel çipli Mac** | [`G-Labs-Studio-mac-intel.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Daha eski Mac'ler (2020 öncesi) |

**Mac'inin hangi çipe sahip olduğundan emin değil misin?**  menüsü (sol üst) → **About This Mac**:
- “Apple M1 / M2 / M3…” yazan bir **Chip** satırı → **arm64** sürümünü indir.
- “Intel…” yazan bir **Processor** satırı → **intel** sürümünü indir.

> **Intel** sürümü Apple çipli bir Mac'te yine de çalışır (sadece daha yavaş), ama **arm64** sürümü bir Intel Mac'te **açılmaz** — o yüzden doğru olanı seç.

### Adım 2 — Kur

<details open>
<summary><b>🪟 Windows'ta</b></summary>

1. İndirdiğin **`G-Labs-Studio-win.exe`** dosyasını aç.
2. **“Windows protected your PC”** (SmartScreen) çıkarsa: **More info** → **Run anyway** tıkla. *(Uygulama henüz bir Microsoft sertifikasıyla imzalanmadı, bu yüzden uyarı çıkıyor — virüs değil.)*
3. Yönetici (UAC) isteminde **Yes** tıkla, sonra kurulumu sonuna kadar tamamla.
4. **Start Menu** ya da **Desktop** kısayolundan aç.

</details>

<details open>
<summary><b>🍎 macOS'ta</b></summary>

1. İndirdiğin **`.dmg`** dosyasını aç, sonra **G-Labs Studio'yu Applications klasörüne sürükle**.
2. **Applications**'a git, **G-Labs Studio**'ya **sağ tıkla** (veya Control-tıkla) → **Open** → iletişim kutusunda tekrar **Open** tıkla. *(Uygulama Apple tarafından imzalı değil, bu yüzden **ilk kez** böyle açman gerekir; sonrasında normal açılır.)*
3. macOS uygulamanın **“hasarlı / açılamıyor”** olduğunu söylerse ya da Open düğmesi yoksa, **Terminal**'i açıp yapıştır:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   Sonra uygulamayı tekrar aç.

</details>

### Adım 3 — Giriş yap ve bir plan seç

**Bir G-Labs hesabına ihtiyacın var.** Uygulamayı aç, Google ile giriş yap ve bir plan seç. Planlar (**FREE / PLUS / MAX**) farklı araç ve modelleri açar; uygulama içinden satın alabilirsin (banka QR, PayPal veya USDT). Bir hesap **aynı anda tek makinede** çalışır — başka yerde giriş yapmak önceki makinenin oturumunu kapatır. Kenar çubuğunun sol alt köşesindeki rozet mevcut seviyeni gösterir. Aynı anda birden fazla cihaz mı gerekiyor? **Team** planı satın alabilirsin (fiyat, eklediğin ek cihaz sayısına göre artar).

> **Az önce eski sürümden (G-Labs Automation) mi geçtin?** Yeni sürüm hesaplarını **taşımaz**. Yeni G-Labs Studio'da **tüm hesaplara yeniden giriş yapman** gerekir (Google/Flow, ChatGPT, Meta…).

Uygulama **kendini günceller**: açılışta GitHub Releases'i kontrol eder ve yeni sürümü uygulama içinden indirip kurabilir.

---

## İlk çalıştırma

1. **Uygulamayı açın ve Google ile oturum açın.** Kademe rozeti (sol alt) planınızı doğrular.
2. **Kullanacağınız araçlar için hesapları bağlayın** (Ayarlar → ilgili hesap sekmesi):
   - **Google** hesapları → Flow Image / Flow Video
   - **ChatGPT** hesapları → GPT Image 2
   - **Meta** hesapları → Meta Media
   - **Grok** → refakatçi tarayıcı uzantısı (Auth Helper) aracılığıyla oturum açtığınız `grok.com` sekmesi üzerinden çalışır — hesap havuzu yok
   Her hesap sekmesi başlık çubuğunda **"Active: N accounts"** gösterir, böylece kaç tanesinin kullanılabilir olduğunu bilirsiniz.
3. **Soldaki kenar çubuğundan bir sayfa seçin** ve üretmeye başlayın. Her üretim sayfası aynı ritmi paylaşır: solda istemleri yazın veya içe aktarın, sağdaki bir **tabloya** düşerler, sonra **Run**'a basın.

Her sayfa başlığında canlı bir **durum çubuğu** bulunur — *Running · Queued · Done · Failed · Accounts* — böylece toplu işi bir bakışta görebilirsiniz. Kuyruk yöneticisini açmak için **Queued**'a, hesap ayarlarına atlamak için **Accounts**'a tıklayın.

---

## Özellikler

![G-Labs Studio](../screenshots/01-image.png)

- **Her büyük üreteç, tek uygulama** — Google Flow (görüntü + video), Grok Imagine, Meta AI (vibes.ai) ve OpenAI GPT Image 2, her biri kendi sayfasında, o sağlayıcının desteklediği modeller ve oranlarla.
- **Tasarımı gereği toplu** — bir istem listesini yapıştırın (satır başına bir tane) veya bir `.txt`/Excel dosyası içe aktarın; her biri bir satır olur. Referans görüntüler dosya adına göre otomatik eşleşir. Seçtiğiniz bir eşzamanlılıkla tüm listeyi çalıştırın.
- **Önce ekle, hazır olunca çalıştır** — satırlar bir kuyruğa gider; **Run / Pause / Stop** ayrıdır. Siz söyleyene kadar hiçbir şey başlamaz ve bir kuyruk yöneticisi yeniden sıralayıp incelemenizi sağlar.
- **Karakter kütüphanesi** — bir karakteri bir kez kaydedin (referans görüntü + kendi sesi + notlar) ve `@name` ile herhangi bir isteme bırakın; video o karakterin görünümünü ve sesini korur.
- **Workflow (düğüm grafiği)** — düğümleri bir işlem hattına bağlayın: istem → görüntü → video → son kareyi çıkar → sonraki video, artı iki klibi kırpma ve geçişlerle (crossfade, wipe, slide, dissolve…) birleştiren bir **Merge Video** düğümü. Toplu düğümler tüm zinciri istem başına veya görüntü başına döngüye alır.
- **Webhook API** — betiklerin ve yapay zekâ ajanlarının görüntü/video/Grok/Meta/OpenAI işleri göndermesi ve sonuçları sorgulaması için yerel bir REST sunucusu.
- Tamamlama için **Image Upscaler** ve bir **Video Editor** (kesme, birleştirme, slayt gösterisi).
- **Dayanıklı** — sonuçlar doğrulanır ve otomatik kaydedilir; oturumlar geri yüklenir; başarısız satırlar yeniden denenir.
- **Koyu / açık tema**, kademeye duyarlı arayüz ve **15 dil**.

---

## Sayfalar

### 🖼 Flow Image — Google Flow görüntü üretimi

![Flow Image](../screenshots/01-image.png)

**Nano Banana Pro / 2 / Lite** ile toplu görüntü üretin. Modeli, en boy oranını ve çözünürlüğü (**1K / 2K / 4K** — 2K/4K modelin büyütücüsünü kullanır) seçin, aynı anda kaç satırın çalışacağını ve aralarındaki gecikmeyi ayarlayın. İstemleri yapıştırın (veya bir dosya içe aktarın), satır başına referans görüntüler ekleyin (bir klasörü sürükleyin, dosya adına göre otomatik eşleşirler) ve karakterleri çekmek için `@name` kullanın. **Run** tüm listeyi kuyruğa gönderir.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Üç sekme: **Text / Frames → Video** (bir metin istemi veya bir başlangıç/bitiş karesi), **Image / Video ingredients → Video** (referans görüntüler veya bir referans video) ve **Scene stitch → Video**. Modeller: **Veo 3.1 Fast / Lite / Quality** ve **Omni Flash**. En boy oranını, büyütmeyi (720p / 1080p / 4K) ve seed'i seçin. Kareler ve içerikler arasındaki farkın sade dille açıklaması için sekme çubuğundaki **?** üzerine gelin.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Grok Imagine aracılığıyla metinden görüntüye, görüntüden görüntüye, metinden videoya ve görüntüden videoya (Auth Helper uzantısı ile oturum açtığınız `grok.com` sekmesi). Görüntüler **8 en boy oranı** sunar (4:3, 21:9, 5:2 dahil); video **480p / 720p / 1080p** olarak üretilir. Görüntüden videoya iki modu vardır: **First frame** (görüntü klibi açar) ve **Reference** (14'e kadar yönlendirici görüntü).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Meta AI aracılığıyla görüntü ve video üretimi. Modlar: metinden görüntüye, görüntüden görüntüye (Character / Scene / Style bileşenleri), metinden videoya ve görüntüden videoya (başlangıç / bitiş karesi).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

ChatGPT hesaplarınızı kullanarak, en fazla 5 referans görüntüyle OpenAI **GPT Image 2** ile üretin. Oranı (21:9, 4:5 ve **özel** dahil 10 seçenek — özel olanda oranı isteme yazarsınız), kaliteyi, istem modunu, akıl yürütme çabasını ve web aramasını seçin.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Bir görüntü klasörünü yerel olarak büyütün — hedefi seçin ve kuyruğu işlemesine izin verin; satır başına ilerleme ve durum (işleniyor / bitti / hata) ile.

### 👤 Characters

![Characters](../screenshots/07-character.png)

Yeniden kullanılabilir karakterlerden bir kütüphane oluşturun: bir referans görüntü, isteğe bağlı özel bir ses ve görünüm/kişilik notları. Herhangi bir Flow isteminde `@name` ile etiketleyin, üretim o kimliği korur.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Görsel bir düğüm tuvali. Bir düğümün soketine sağ tıklayın, menü yalnızca uyan düğümleri sunar — birini seçin, otomatik olarak bağlanır. İstem → üret → video → **Extract Frame** → sonraki video zincirleyin ve iki klibi birleştirmek için **Merge Video** kullanın (her ucu kırpın, bir geçiş seçin). Tüm grafiği bir `.json` dosyası olarak kaydedin/yükleyin; **Run Flow** onu baştan sona çalıştırır.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Uygulamayı yerel bir otomasyon sunucusuna dönüştürün. Başlatın, API anahtarınızı kopyalayın ve `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` veya `/api/openai/generate` adreslerine iş POST edin, ardından `/api/status/<id>` sorgulayın. Sayfa her modeli ve desteklediği en boy oranlarını listeler. Tam şema: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Dosyalar nerede

| Ne | macOS | Windows |
|---|---|---|
| Çıktı (görüntüler / videolar) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Ayarlar, oturumlar, hesaplar | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Ayarlarınız, istem listeleriniz, oturumlarınız, karakter kütüphaneniz ve hesap listeniz kaydedilir ve uygulamayı bir sonraki açışınızda geri yüklenir.

---

## Sorun giderme

**Her şey kilitli / satın alma ekranı sürekli açılıyor** — planınızın süresi doldu veya hesap başka bir makinede oturum açtı. Kademe rozetini (sol alt) kontrol edin ve yenileyin.

**Bir Grok üretimi hiçbir şey yapmıyor** — Grok, `grok.com` sekmeniz üzerinden çalışır. **Auth Helper** tarayıcı uzantısını kurun/etkinleştirin (Ayarlar → Grok) ve grok.com'da oturum açtığınızdan emin olun.

**Bir sayfada "Active: 0 accounts"** — o sayfanın hesap sekmesinde (Ayarlar) bir hesap ekleyin veya yeniden etkinleştirin ya da token'ı süresi dolmuştur — **Refresh all**'a basın.

**macOS uygulamanın hasarlı olduğunu / açılamadığını söylüyor** — Apple tarafından imzalanmamıştır. İlk seferinde sağ tıkla → **Open** yapın veya `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` çalıştırın.

**Bir güncelleme kurulmuyor** — en son sürümü [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) sayfasından manuel olarak indirin.
