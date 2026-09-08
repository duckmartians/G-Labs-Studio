<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>ہر بڑے AI پر بیک وقت بہت سی تصاویر اور ویڈیوز بنانے کے لیے ایک ڈیسک ٹاپ ایپ — Google Flow (Veo 3.1، Omni Flash، Nano Banana)، Grok Imagine، Meta AI اور ChatGPT GPT Image 2۔</b></p>

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
  <b>اردو</b> ·
  <a href="README.ar.md">العربية</a> ·
  <a href="README.de.md">Deutsch</a> ·
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

![G-Labs Studio](../screenshots/01-image.png)

---

## انسٹال

تازہ ترین بلڈ **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** سے ڈاؤن لوڈ کریں:

| پلیٹ فارم | فائل |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-v<version>-win.exe` — انسٹالر چلائیں (ایڈمن/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-v<version>-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-v<version>-mac-intel.dmg` |

**macOS پہلی بار کھولنا** — ایپ Apple کی طرف سے دستخط شدہ نہیں ہے، اس لیے macOS اسے قرنطینہ میں ڈال دیتا ہے۔ پہلی بار اسے **رائٹ کلک → Open** سے کھولیں، یا Terminal سے فلیگ صاف کریں:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**آپ کو ایک G-Labs اکاؤنٹ درکار ہے۔** ایپ کھولیں، Google سے سائن اِن کریں، اور ایک پلان چنیں۔ پلانز (**FREE / PLUS / MAX**) مختلف ٹولز اور ماڈلز کھولتے ہیں؛ آپ ایک پلان ایپ کے اندر سے خرید سکتے ہیں (بینک QR، PayPal، یا USDT)۔ ایک اکاؤنٹ **ایک وقت میں ایک مشین** پر چلتا ہے — کہیں اور سائن اِن کرنے سے پچھلی مشین سائن آؤٹ ہو جاتی ہے۔ سائیڈبار کے نیچے بائیں جانب بیج آپ کا موجودہ ٹیئر دکھاتا ہے۔

ایپ **خود کو اپ ڈیٹ کرتی ہے**: یہ لانچ پر GitHub Releases چیک کرتی ہے اور نئی ورژن ایپ کے اندر سے ڈاؤن لوڈ اور انسٹال کر سکتی ہے۔

---

## پہلی بار چلانا

1. **ایپ کھولیں اور Google سے سائن اِن کریں۔** ٹیئر بیج (نیچے بائیں) آپ کے پلان کی تصدیق کرتا ہے۔
2. **جو ٹولز آپ استعمال کریں گے ان کے لیے اکاؤنٹس جوڑیں** (Settings → متعلقہ اکاؤنٹ ٹیب):
   - **Google** اکاؤنٹس → Flow Image / Flow Video
   - **ChatGPT** اکاؤنٹس → GPT Image 2
   - **Meta** اکاؤنٹس → Meta Media
   - **Grok** → آپ کے لاگ اِن `grok.com` ٹیب کے ذریعے companion براؤزر ایکسٹینشن (Auth Helper) سے چلتا ہے — کوئی اکاؤنٹ پول نہیں
   ہر اکاؤنٹ ٹیب اپنی ٹائٹل بار پر **"Active: N accounts"** دکھاتا ہے تاکہ آپ جان سکیں کہ کتنے قابلِ استعمال ہیں۔
3. **بائیں سائیڈبار سے ایک صفحہ چنیں** اور بنانا شروع کریں۔ ہر جنریشن صفحہ ایک ہی تال رکھتا ہے: بائیں جانب پرومپٹ ٹائپ یا امپورٹ کریں، وہ دائیں جانب ایک **ٹیبل** میں آ جاتے ہیں، پھر **Run** دبائیں۔

ہر صفحے کے ہیڈر میں ایک لائیو **اسٹیٹس بار** ہوتا ہے — *Running · Queued · Done · Failed · Accounts* — تاکہ آپ بیچ کو ایک نظر میں دیکھ سکیں۔ کیو مینیجر کھولنے کے لیے **Queued** پر کلک کریں، اکاؤنٹ سیٹنگز پر جانے کے لیے **Accounts** پر۔

---

## خصوصیات

- **ہر بڑا جنریٹر، ایک ایپ** — Google Flow (تصویر + ویڈیو)، Grok Imagine، Meta AI (vibes.ai) اور OpenAI GPT Image 2، ہر ایک اپنے صفحے پر ان ماڈلز اور تناسبات کے ساتھ جو وہ فراہم کنندہ سپورٹ کرتا ہے۔
- **ڈیزائن ہی سے بیچ** — پرومپٹ کی فہرست پیسٹ کریں (فی لائن ایک) یا ایک `.txt`/Excel فائل امپورٹ کریں؛ ہر ایک ایک قطار بن جاتی ہے۔ ریفرنس تصاویر فائل نام سے خودکار میچ ہو جاتی ہیں۔ اپنی منتخب کردہ concurrency کے ساتھ پوری فہرست چلائیں۔
- **پہلے شامل کریں، تیار ہونے پر چلائیں** — قطاریں ایک کیو میں جاتی ہیں؛ **Run / Pause / Stop** الگ الگ ہیں۔ جب تک آپ نہ کہیں کچھ شروع نہیں ہوتا، اور ایک کیو مینیجر آپ کو دوبارہ ترتیب دینے اور معائنہ کرنے دیتا ہے۔
- **کریکٹر لائبریری** — ایک کریکٹر ایک بار محفوظ کریں (ریفرنس تصویر + اس کی اپنی آواز + نوٹس) اور اسے `@name` کے ساتھ کسی بھی پرومپٹ میں ڈراپ کریں؛ ویڈیو اس کریکٹر کی شکل اور آواز برقرار رکھتی ہے۔
- **Workflow (node graph)** — نوڈز کو ایک پائپ لائن میں جوڑیں: پرومپٹ → تصویر → ویڈیو → آخری فریم نکالیں → اگلی ویڈیو، مزید ایک **Merge Video** نوڈ جو دو کلپس کو ٹرمز اور ٹرانزیشنز (crossfade، wipe، slide، dissolve…) کے ساتھ جوڑتا ہے۔ بیچ نوڈز پوری چین کو فی پرومپٹ یا فی تصویر لوپ کرتے ہیں۔
- **Webhook API** — ایک مقامی REST سرور تاکہ اسکرپٹس اور AI ایجنٹس تصویر/ویڈیو/Grok/Meta/OpenAI جابز جمع کرا سکیں اور نتائج کے لیے پول کر سکیں۔
- تکمیل کے لیے **Image Upscaler** اور ایک **Video Editor** (کاٹنا، جوڑنا، سلائیڈ شو)۔
- **مضبوط** — نتائج تصدیق اور خودکار محفوظ ہوتے ہیں؛ سیشنز بحال ہوتے ہیں؛ ناکام قطاریں دوبارہ کوشش کرتی ہیں۔
- **ڈارک / لائٹ تھیم**، ٹیئر سے آگاہ UI، اور **15 زبانیں**۔

---

## صفحات

### 🖼 Flow Image — Google Flow تصویر جنریشن

![Flow Image](../screenshots/01-image.png)

**Nano Banana Pro / 2 / Lite** کے ساتھ بیچ میں تصاویر بنائیں۔ ماڈل، ایسپیکٹ ریشو اور ریزولوشن (**1K / 2K / 4K** — 2K/4K ماڈل کے اپ اسکیلر کا استعمال کرتے ہیں) چنیں، طے کریں کہ ایک وقت میں کتنی قطاریں چلیں اور ان کے درمیان تاخیر۔ پرومپٹ پیسٹ کریں (یا ایک فائل امپورٹ کریں)، فی قطار ریفرنس تصاویر منسلک کریں (ایک فولڈر ڈریگ کریں اور وہ فائل نام سے خودکار میچ ہو جائیں گی)، اور کریکٹرز شامل کرنے کے لیے `@name` استعمال کریں۔ **Run** پوری فہرست کو کیو میں بھیجتا ہے۔

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

تین ٹیبز: **Text / Frames → Video** (ایک ٹیکسٹ پرومپٹ، یا ایک اسٹارٹ/اینڈ فریم)، **Image / Video ingredients → Video** (ریفرنس تصاویر یا ایک ریفرنس ویڈیو)، اور **Scene stitch → Video**۔ ماڈلز: **Veo 3.1 Fast / Lite / Quality** اور **Omni Flash**۔ ایسپیکٹ ریشو، اپ اسکیل (720p / 1080p / 4K) اور seed چنیں۔ frames بمقابلہ ingredients کی سادہ زبان میں وضاحت کے لیے ٹیب بار پر **?** پر ہوور کریں۔

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Grok Imagine کے ذریعے text-to-image، image-to-image، text-to-video اور image-to-video (Auth Helper ایکسٹینشن کے ذریعے آپ کا لاگ اِن `grok.com` ٹیب)۔ تصاویر **8 ایسپیکٹ ریشوز** پیش کرتی ہیں (بشمول 4:3، 21:9، 5:2)؛ ویڈیو **480p / 720p / 1080p** پر بنتی ہے۔ image-to-video کے دو موڈ ہیں: **First frame** (تصویر کلپ کا آغاز کرتی ہے) اور **Reference** (14 تک رہنمائی کرنے والی تصاویر)۔

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Meta AI کے ذریعے تصویر اور ویڈیو جنریشن۔ موڈز: text-to-image، image-to-image (Character / Scene / Style اجزاء)، text-to-video اور image-to-video (اسٹارٹ / اینڈ فریم)۔

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

اپنے ChatGPT اکاؤنٹس کا استعمال کرتے ہوئے OpenAI **GPT Image 2** کے ساتھ بنائیں، 5 تک ریفرنس تصاویر کے ساتھ۔ ریشو (21:9، 4:5 اور **custom** سمیت 10 اختیارات — جہاں آپ ریشو پرومپٹ میں لکھتے ہیں)، کوالٹی، پرومپٹ موڈ، reasoning effort اور ویب سرچ چنیں۔

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

تصاویر کے ایک فولڈر کو مقامی طور پر اپ اسکیل کریں — ہدف چنیں اور اسے کیو پروسیس کرنے دیں، فی قطار پیش رفت اور اسٹیٹس (processing / done / error) کے ساتھ۔

### 👤 Characters

![Characters](../screenshots/07-character.png)

دوبارہ قابلِ استعمال کریکٹرز کی ایک لائبریری بنائیں: ایک ریفرنس تصویر، ایک اختیاری کسٹم آواز، اور شکل/شخصیت کے نوٹس۔ انہیں کسی بھی Flow پرومپٹ میں `@name` سے ٹیگ کریں اور جنریشن اس شناخت کو برقرار رکھے گی۔

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

ایک بصری نوڈ کینوس۔ کسی نوڈ کے ساکٹ پر رائٹ کلک کریں اور مینیو صرف وہی نوڈز پیش کرتا ہے جو فِٹ ہوں — ایک چنیں اور یہ خودکار طور پر جُڑ جاتا ہے۔ پرومپٹ → generate → video → **Extract Frame** → اگلی ویڈیو کو چین کریں، اور دو کلپس کو جوڑنے کے لیے **Merge Video** استعمال کریں (ہر سرے کو ٹرم کریں، ایک ٹرانزیشن چنیں)۔ پورے گراف کو ایک `.json` فائل کے طور پر محفوظ/لوڈ کریں؛ **Run Flow** اسے شروع سے آخر تک چلاتا ہے۔

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

ایپ کو ایک مقامی آٹومیشن سرور میں بدل دیں۔ اسے شروع کریں، اپنی API کلید کاپی کریں، اور `/api/image/generate`، `/api/video/generate`، `/api/grok/generate`، `/api/meta/generate` یا `/api/openai/generate` پر جابز POST کریں، پھر `/api/status/<id>` پول کریں۔ صفحہ ہر ماڈل اور اس کے سپورٹ کردہ ایسپیکٹ ریشوز کی فہرست دیتا ہے۔ مکمل شیما: [`docs/WEBHOOK_INTEGRATION.en.md`](../WEBHOOK_INTEGRATION.en.md)۔

---

## چیزیں کہاں رہتی ہیں

| کیا | macOS | Windows |
|---|---|---|
| آؤٹ پٹ (تصاویر / ویڈیوز) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| سیٹنگز، سیشنز، اکاؤنٹس | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

آپ کی سیٹنگز، پرومپٹ فہرستیں، سیشنز، کریکٹر لائبریری اور اکاؤنٹ فہرست محفوظ ہوتی ہیں اور اگلی بار ایپ کھولنے پر بحال ہو جاتی ہیں۔

---

## مسائل کا حل

**سب کچھ لاک ہے / خریداری کی اسکرین بار بار کھلتی ہے** — آپ کا پلان ختم ہو گیا، یا اکاؤنٹ کسی اور مشین پر سائن اِن ہو گیا۔ ٹیئر بیج (نیچے بائیں) چیک کریں اور تجدید کریں۔

**Grok جنریشن کچھ نہیں کرتی** — Grok آپ کے `grok.com` ٹیب کے ذریعے چلتا ہے۔ **Auth Helper** براؤزر ایکسٹینشن انسٹال/فعال کریں (Settings → Grok) اور یقینی بنائیں کہ آپ grok.com پر لاگ اِن ہیں۔

**کسی صفحے پر "Active: 0 accounts"** — اس صفحے کے اکاؤنٹ ٹیب (Settings) میں ایک اکاؤنٹ شامل یا دوبارہ فعال کریں، یا اس کا ٹوکن ختم ہو گیا ہے — **Refresh all** دبائیں۔

**macOS کہتا ہے ایپ خراب ہے / کھولی نہیں جا سکتی** — یہ Apple کی طرف سے دستخط شدہ نہیں ہے۔ پہلی بار رائٹ کلک → **Open** کریں، یا `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` چلائیں۔

**اپ ڈیٹ انسٹال نہیں ہوتی** — تازہ ترین بلڈ دستی طور پر [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) سے ڈاؤن لوڈ کریں۔
