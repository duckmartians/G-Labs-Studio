<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Her büyük yapay zekâda toplu görsel ve video üretmek için tek bir masaüstü uygulaması — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Google Vids, Google Pics, ChatGPT GPT Image 2, Meta Vibes ve Grok — ayrıca video araçları, düğüm tabanlı bir workflow ve bir Webhook API.</b></p>

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
| 🪟 **Windows 10/11 (64 bit)** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | Her Windows PC için |
| 🍎 **Apple çipli Mac (M1/M2/M3/M4)** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Yaklaşık 2020 sonundan itibaren Mac'ler |
| 🍎 **Intel çipli Mac** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Daha eski Mac'ler (2020 öncesi) |

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

**Bir G-Labs hesabına ihtiyacın var.** Uygulamayı aç, Google ile giriş yap ve bir plan seç. Planlar (**BASIC / PLUS / MAX**) farklı araç ve modelleri açar; uygulama içinden satın alabilirsin (banka QR, PayPal veya USDT). Bir hesap **aynı anda tek makinede** çalışır — başka yerde giriş yapmak önceki makinenin oturumunu kapatır. Kenar çubuğunun sol alt köşesindeki rozet mevcut seviyeni gösterir. Aynı anda birden fazla cihaz mı gerekiyor? **Team** planı satın alabilirsin (fiyat, eklediğin ek cihaz sayısına göre artar).

> **Az önce eski sürümden (G-Labs Automation) mi geçtin?** Yeni sürüm hesaplarını **taşımaz**. Yeni G-Labs Studio'da **tüm hesaplara yeniden giriş yapman** gerekir (Google/Flow, ChatGPT, Meta…).

Uygulama **kendini günceller**: açılışta GitHub Releases'i kontrol eder ve yeni sürümü uygulama içinden indirip kurabilir.

---

## İlk çalıştırma

1. **Uygulamayı açın ve Google ile oturum açın.** Kademe rozeti (sol alt: **BASIC / PLUS / MAX**) planınızı doğrular.
2. **Kullanacağınız araçlar için hesapları bağlayın** (**Ayarlar** → ilgili hesap sekmesi):
   - **Flow Hesapları** → Flow Görsel / Flow Video
   - **Google Hesapları** → **Google Vids** ve **Google Pics** (iki sayfa da bu Google hesaplarını paylaşır; her hesap Vids videoları ve Pics görselleri için ayrı ayrı açılır)
   - **ChatGPT Hesabı** → GPT Image 2
   - **Vibes Hesabı** → Meta Vibes
   - **Grok Hesabı** → hesap deposu yok: bu sekme **Auth Helper** tarayıcı uzantısını kurmanızda size yol gösterir, ardından Grok, Chrome'da oturum açtığınız `grok.com` sekmesi üzerinden çalışır

   Her hesap sekmesi başlık çubuğunda **"Aktif: N hesap"** gösterir, böylece kaç tanesinin kullanılabilir olduğunu bilirsiniz.
3. **Soldaki kenar çubuğundan bir sayfa seçin** ve üretmeye başlayın. Her üretim sayfası aynı ritmi izler: solda istemleri yazın veya içe aktarın, sağdaki bir **tabloya** düşerler, sonra **Run**'a basın.

Her sayfa başlığında canlı bir **durum şeridi** bulunur — *Çalışıyor · Sırada · Bitti · Hata · Hesaplar* — böylece tüm toplu işi bir bakışta görürsünüz. Kuyruk yöneticisini açmak için **Sırada**'a, hesap ayarlarına atlamak için **Hesaplar**'a tıklayın.

---

## Özellikler

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **Her büyük üreteç, tek uygulama** — Google Flow (görsel + video), Google Vids, Google Pics, GPT Image 2, Meta Vibes ve Grok, her biri kendi sayfasında, o sağlayıcının desteklediği modeller ve oranlarla.
- **Toplu iş için tasarlandı** — bir istem listesi yapıştırın (satır başına bir tane) veya `.txt`/Excel içe aktarın; her istem bir satır olur. Referans görseller dosya adına göre otomatik eşleşir. Tüm listeyi seçtiğiniz sayıda paralel iş parçacığıyla çalıştırın.
- **Önce ekle, hazır olunca çalıştır** — satırlar bir kuyruğa gider; **Run / Pause / Stop** ayrıdır. Siz söyleyene kadar hiçbir şey başlamaz ve kuyruk yöneticisi yeniden sıralayıp incelemenizi sağlar.
- **Otomatik Gemini ✦ logosu kaldırma** — Google Pics görselleri ve Google Vids videoları indirmenin hemen ardından temizlenir (logoyu korumak için **Gemini logosunu göster**'i açın). Logosuz dosyalara dokunulmaz.
- **Karakter kütüphanesi** — bir karakteri bir kez kaydedin (referans görsel + ses + notlar) ve sahneleri tutarlı tutmak için Flow Görsel, Flow Video ve Google Vids istemlerinde `@name` ile çağırın.
- **Workflow (düğüm grafiği)** — düğümleri bir işlem hattına bağlayın: istem → görsel → video → son kareyi çıkar → sonraki video, artı iki klibi bir geçişle birleştiren bir **Video Birleştir** düğümü.
- **Video Araçları** — zaman çizelgesinde video düzenleme, altyazıyla senkronize görsel slayt gösterileri, video bölme, kare çıkarma ve video logosu kaldırma, doğrudan uygulamanın içinde.
- Kendi bilgisayarınızda **Görüntü Büyütme** ve otomasyon için bir **Webhook API**.
- **Dayanıklı** — sonuçlar doğrulanır ve otomatik kaydedilir; oturumlar geri yüklenir; başarısız satırlar yeniden denenir.
- **Açık / koyu tema**, kademeye duyarlı arayüz ve **15 dil**.

---

## Sayfalar

### 🖼 Flow Görsel — Google Flow görsel üretimi

![Flow Görsel](../screenshots/en/flow-image.webp)

**Nano Banana Pro / 2 / 2 Lite** ile toplu görsel üretin. Modeli, en boy oranını ve çözünürlüğü (**1K / 2K / 4K** — 2K/4K modelin büyütücüsünü kullanır) seçin, aynı anda kaç satırın çalışacağını ve aralarındaki gecikmeyi ayarlayın. İstemleri yapıştırın (veya bir dosya içe aktarın), satır başına referans görseller ekleyin (bir klasör bırakın, dosya adına göre otomatik eşleşirler) ve bir karakteri çekmek için `@name` kullanın. **Veo / Gemini logosunu göster** anahtarı (varsayılan olarak kapalı) Flow Video sayfasıyla ortaktır. **Run** tüm listeyi kuyruğa gönderir.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/en/flow-video.webp)

Üç sekme: **Metin / Kare → Video** (bir metin istemi veya başlangıç/bitiş kareleri), **Görsel / Video Bileşenleri → Video** (referans görseller veya bir referans video) ve **Sahne Zinciri → Video**. Modeller: **Veo 3.1 Fast / Lite / Quality** ve **Omni Flash**. En boy oranını, büyütmeyi (720p / 1080p / 4K) ve seed'i seçin. Kareler ile bileşenler arasındaki farkın sade dille açıklaması için sekme çubuğundaki **?** üzerine gelin.

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

Google hesabınızla üç sekmede video yapın: **Metin → Video**, **Görsel → Video** (tek bir açılış görseli) ve **Bileşenler → Video** (en fazla 3 bileşen görseli). Yatay/dikey, 720p / 1080p ve 3–10 saniyelik bir süre seçin — ya da her satıra kendi uzunluğunu vermek için isteme `[4s]` gibi bir etiket koyun. Biten videolar doğrudan tablodan 1080p'ye büyütülebilir. Her hesabın video saniyesi cinsinden ölçülen bir kotası vardır; daha hızlı çalıştırmak için daha fazla hesap ekleyin. İndirilen videolardaki (720p / 1080p) Gemini ✦ logosu, **Gemini logosunu göster**'i açmadığınız sürece otomatik olarak kaldırılır.

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

İki sekme: **Metin → Görsel** ve **en fazla 14 referans görselle** (karakterler, nesneler, sahneler, stil) **Görsel → Görsel**. Her çalıştırmada Google 3–9 görsel döndürür; **Çalıştırma başına saklanacak görsel** kaç tanesinin saklanacağını belirler (1–4 veya tümü). 21:9, 3:2 ve 5:4 dahil 10 en boy oranı. Her çalıştırma, görsel sayısı ne olursa olsun 1 Google Pics çalıştırması harcar; içerik politikası tarafından reddedilen bir istem hiçbir şeye mal olmaz. Pics, **Google Hesapları**'nı Google Vids ile paylaşır.

**Otomatik Gemini ✦ logosu kaldırma:** indirilen Pics görsellerinin sağ alt köşesindeki ✦ işareti, özellikle Google Pics için ölçülmüş bir logo haritası kullanılarak indirmenin hemen ardından kaldırılır — logo karışımı tersine çevrilir, böylece altındaki orijinal doku bulanıklaştırılmak yerine geri kazanılır. Logo algılanmayan görseller olduğu gibi bırakılır. Logoyu korumak için **Gemini logosunu göster**'i açın.

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

ChatGPT hesabınızı kullanarak, en fazla 5 referans görselle OpenAI **GPT Image 2** ile üretin. Oranı (21:9, 4:5 ve **custom** dahil 10 seçenek — custom'da oranı isteme yazarsınız), kaliteyi, istem modunu, akıl yürütme düzeyini ve web aramasını seçin.

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

Meta Vibes'ta dört sekmede görsel ve video oluşturun: **Metin → Görsel**, **Metin → Video**, **Görsel → Görsel** (karakter / sahne / stil görselleri) ve **Görsel → Video** (başlangıç / bitiş karesi). Kuyruğa alma ve indirme otomatiktir.

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

Grok Imagine aracılığıyla Metin → Görsel, Görsel → Görsel, Metin → Video ve Görsel → Video (Auth Helper uzantısı ile oturum açtığınız `grok.com` sekmeniz). Görseller **8 en boy oranında** gelir (4:3, 21:9, 5:2 dahil); videolar **480p / 720p / 1080p** olarak işlenir. Görsel → Video'nun iki modu vardır: **İlk kare** (görsel klibi açar) ve **Referans görselleri** (en fazla 14 yönlendirici görsel).

### 👤 Karakterler

![Karakterler](../screenshots/en/characters.webp)

Yeniden kullanılabilir bir oyuncu kadrosu oluşturun: bir referans görsel, bir ses (Flow'un hazır seslerinden biri, isteğe bağlı bir anlatım açıklamasıyla) ve görünüm/kişilik notları. Flow Görsel, Flow Video ve Google Vids istemlerinde `@name` ile etiketleyin, üretim o kimliği korur (ses yalnızca Flow Video tarafından kullanılır; Google Vids görseli kullanır).

### 🔗 Workflow

![Workflow](../screenshots/en/workflow.webp)

Görsel bir düğüm tuvali. Bir düğümün soketine sağ tıklayın, menü yalnızca uyan düğümleri sunar — birini seçin, kendiliğinden bağlanır. Flow Görsel, Flow Video, Grok, Meta ve GPT Image 2 için düğümler vardır. İstem → görsel → video → **Kare Çıkar** → sonraki video zincirleyin ve iki klibi birleştirmek için **Video Birleştir** kullanın (her ucu kırpın, bir geçiş seçin). Tüm grafiği bir `.json` dosyası olarak kaydedin/yükleyin (biçim: [`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)); **Run Flow** onu baştan sona çalıştırır.

### 🎞 Video Araçları

Tek sayfada beş sekme:

**Video Düzenleme** — video, SRT altyazıları ve ses için bir zaman çizelgesi: kesin, bölün, yeniden sıralayın, otomatik sığdırın, sonra tek bir bitmiş video dışa aktarın.

![Video Düzenleme](../screenshots/en/vt-video.webp)

**Altyazıya uygun görsel slayt gösterisi** — görselleri ve bir `.srt` dosyasını yükleyin; her görsel otomatik olarak bir altyazı satırıyla eşleşir, hareket efektleri, katmanlar ve altyazı stiliyle.

![Altyazıya uygun görsel slayt gösterisi](../screenshots/en/vt-slideshow.webp)

**Videoyu bölümlere ayır** — parça sayısına, sabit veya rastgele uzunluğa, bir zaman damgası listesine veya bir A–B aralıkları listesine göre; tek dosya veya bütün bir toplu iş, mümkün olduğunda GPU hızlandırmalı.

![Videoyu bölümlere ayır](../screenshots/en/vt-slicer.webp)

**Videodan kareleri çıkar** — toplam sayıya, zaman aralığına, kare aralığına veya harekete göre; tek dosya veya bütün bir klasör.

![Videodan kareleri çıkar](../screenshots/en/vt-extractor.webp)

**Video logosunu kaldır** — 720p ve 1080p (yatay veya dikey) Google Vids videolarından ✦ logosunu kaldırır, uygulamada önce/sonra önizlemesiyle. Logosuz videolar atlanır; orijinaller korunur ve sonuçlar `<ad>_nologo.mp4` olarak kaydedilir.

![Video logosunu kaldır](../screenshots/en/vt-logo.webp)

### 🔍 Görüntü Büyütme

![Görüntü Büyütme](../screenshots/en/upscaler.webp)

Görselleri doğrudan bilgisayarınızda büyütün ve keskinleştirin — tek tek görseller veya bütün bir klasör ekleyin, bir yapay zekâ modeli (Real-ESRGAN, UltraSharp, Remacri…) ve 2x–8x ölçek seçin, satır başına ilerlemeyi izleyin ve önce/sonra karşılaştırın.

### 🌐 Webhook API

![Webhook API](../screenshots/en/webhook.webp)

Uygulamayı yerel bir otomasyon sunucusuna dönüştürün (MAX planı); böylece n8n, Make, Zapier, betikler veya yapay zekâ ajanları uygulamanın kuyruğuna iş gönderebilir. Başlatın, API anahtarınızı kopyalayın ve `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate`, `/api/openai/generate` veya `/api/upscale/generate` adreslerine iş POST edin, ardından `/api/status/<id>` sorgulayın. Sayfa her modeli ve desteklediği en boy oranlarını listeler. Tam şema: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Dosyalar nerede

| Ne | macOS | Windows |
|---|---|---|
| Çıktılar (görseller / videolar) | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| Ayarlar, oturumlar, hesaplar, karakterler | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Her sayfanın `output` içinde kendi alt klasörü vardır (her çalıştırma için daha küçük bir klasör); kayıt klasörünü her sayfada değiştirebilirsiniz. Ayarlarınız, istem listeleriniz, oturumlarınız, karakter kütüphaneniz ve hesap listeniz kaydedilir ve uygulamayı bir sonraki açışınızda geri yüklenir.

---

## Sorun giderme

**Her şey kilitli / satın alma ekranı sürekli açılıyor** — planınızın süresi doldu veya hesap başka bir makinede oturum açtı. Kademe rozetini (sol alt) kontrol edin ve yenileyin. Google Vids ve Google Pics için PLUS/MAX planı gerekir; Webhook API için MAX gerekir.

**Bir Grok üretimi hiçbir şey yapmıyor** — Grok, `grok.com` sekmeniz üzerinden çalışır. **Auth Helper** tarayıcı uzantısını kurun/etkinleştirin (Ayarlar → Grok Hesabı) ve grok.com'da oturum açtığınızdan emin olun.

**Google Pics hesap olmadığını söylüyor** — Pics, Google Vids hesaplarını kullanır. Ayarlar → **Google Hesapları** bölümünden bir hesap ekleyin.

**Bir sayfada "Aktif: 0 hesap"** — o sayfanın hesap sekmesinde (Ayarlar) bir hesap ekleyin veya yeniden etkinleştirin ya da token'ının süresi dolmuştur — **Tümünü Yenile**'ye basın.

**Windows "Windows protected your PC" uyarısıyla engelliyor** — **More info → Run anyway**'e tıklayın. Uygulama henüz bir Microsoft sertifikasıyla kod imzalı olmadığı için işaretlenir — virüs değildir.

**macOS uygulamanın hasarlı olduğunu / açılamadığını söylüyor** — henüz Apple tarafından imzalanmamıştır. İlk seferinde sağ tıkla → **Open** yapın veya `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` çalıştırın.

**Bir güncelleme kurulmadı** — en son sürümü [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) sayfasından manuel olarak indirin.
