<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>تطبيق سطح مكتب واحد لتوليد الصور ومقاطع الفيديو دفعةً واحدة عبر كل نماذج الذكاء الاصطناعي الكبرى — Google Flow (Veo 3.1 وOmni Flash وNano Banana) وGrok Imagine وMeta AI وChatGPT GPT Image 2.</b></p>

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
  <b>العربية</b> ·
  <a href="README.de.md">Deutsch</a> ·
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Download for Windows" src="https://img.shields.io/badge/Download-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Download for macOS (Apple Silicon)" src="https://img.shields.io/badge/Download-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Download for macOS (Intel)" src="https://img.shields.io/badge/Download-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

![G-Labs Studio](../screenshots/01-image.png)

---

## التثبيت

نزّل أحدث إصدار من **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**:

| المنصة | الملف |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-win.exe` — شغّل المُثبِّت (مسؤول/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-mac-intel.dmg` |

**التشغيل الأول على macOS** — التطبيق غير موقّع من Apple، لذا يضعه macOS في الحجر الصحي. افتحه في المرة الأولى بـ **النقر بالزر الأيمن ← Open**، أو امسح العلامة من الطرفية (Terminal):

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**تحتاج إلى حساب G-Labs.** افتح التطبيق، وسجّل الدخول عبر Google، واختر خطة. تفتح الخطط (**FREE / PLUS / MAX**) أدوات ونماذج مختلفة؛ ويمكنك شراء واحدة من داخل التطبيق (رمز QR للبنك، أو PayPal، أو USDT). يعمل الحساب الواحد على **جهاز واحد في كل مرة** — تسجيل الدخول في مكان آخر يُسجّل خروج الجهاز السابق. تعرض الشارة في أسفل يسار الشريط الجانبي مستواك الحالي.

يقوم التطبيق **بتحديث نفسه**: يتحقق من GitHub Releases عند التشغيل ويمكنه تنزيل الإصدار الجديد وتثبيته من داخل التطبيق.

---

## التشغيل الأول

1. **افتح التطبيق وسجّل الدخول عبر Google.** تؤكد شارة المستوى (أسفل اليسار) خطتك.
2. **اربط الحسابات الخاصة بالأدوات التي ستستخدمها** (Settings ← علامة تبويب الحساب المطابقة):
   - حسابات **Google** ← Flow Image / Flow Video
   - حسابات **ChatGPT** ← GPT Image 2
   - حسابات **Meta** ← Meta Media
   - **Grok** ← يعمل عبر علامة التبويب `grok.com` التي سجّلت الدخول فيها من خلال إضافة المتصفح المرافقة (Auth Helper) — لا يوجد تجمّع حسابات
   تعرض كل علامة تبويب للحساب **"Active: N accounts"** على شريط عنوانها لتعرف عدد الحسابات القابلة للاستخدام.
3. **اختر صفحة من الشريط الجانبي الأيسر** وابدأ التوليد. تتّبع كل صفحة توليد الإيقاع نفسه: اكتب المطالبات أو استوردها على اليسار، فتظهر في **جدول** على اليمين، ثم اضغط **Run**.

يحمل رأس كل صفحة **شريط حالة** حيًّا — *Running · Queued · Done · Failed · Accounts* — لترى الدفعة بلمحة. انقر **Queued** لفتح مدير الطابور، و**Accounts** للانتقال إلى إعدادات الحسابات.

---

## المزايا

- **كل مولّد كبير في تطبيق واحد** — Google Flow (صورة + فيديو) وGrok Imagine وMeta AI (vibes.ai) وOpenAI GPT Image 2، كلٌّ في صفحته الخاصة مع النماذج والنسب التي يدعمها ذلك المزوّد.
- **الدفعات من صميم التصميم** — الصق قائمة مطالبات (واحدة لكل سطر) أو استورد ملف `.txt`/Excel؛ يصبح كلٌّ منها صفًّا. تتطابق الصور المرجعية تلقائيًا حسب اسم الملف. شغّل القائمة كاملةً بمستوى تزامن تختاره.
- **أضِف أولًا، وشغّل عند الجاهزية** — تذهب الصفوف إلى طابور؛ **Run / Pause / Stop** منفصلة. لا يبدأ شيء حتى تأمر به، ويتيح لك مدير الطابور إعادة الترتيب والفحص.
- **مكتبة الشخصيات** — احفظ شخصية مرة واحدة (صورة مرجعية + صوتها الخاص + ملاحظات) وأدرجها في أي مطالبة بـ `@name`؛ يحتفظ الفيديو بمظهر تلك الشخصية وصوتها.
- **Workflow (رسم بياني للعقد)** — اربط العقد في خط أنابيب: مطالبة ← صورة ← فيديو ← استخراج الإطار الأخير ← الفيديو التالي، بالإضافة إلى عقدة **Merge Video** التي تجمع مقطعين مع اقتطاعات وانتقالات (crossfade، wipe، slide، dissolve…). تكرّر عقد الدفعات السلسلة كاملةً لكل مطالبة أو لكل صورة.
- **Webhook API** — خادم REST محلي حتى تتمكن السكربتات ووكلاء الذكاء الاصطناعي من إرسال مهام الصور/الفيديو/Grok/Meta/OpenAI واستطلاع النتائج.
- **Image Upscaler** و**Video Editor** (قص، دمج، عرض شرائح) للمسات النهائية.
- **متين** — يتم التحقق من النتائج وحفظها تلقائيًا؛ وتُستعاد الجلسات؛ وتُعاد محاولة الصفوف الفاشلة.
- **سمة داكنة / فاتحة**، وواجهة مدركة للمستوى، و**15 لغة**.

---

## الصفحات

### 🖼 Flow Image — توليد الصور عبر Google Flow

![Flow Image](../screenshots/01-image.png)

ولّد الصور دفعةً واحدة بـ **Nano Banana Pro / 2 / Lite**. اختر النموذج ونسبة العرض إلى الارتفاع والدقة (**1K / 2K / 4K** — تستخدم 2K/4K مُكبِّر النموذج)، وحدّد عدد الصفوف التي تعمل في آنٍ واحد والتأخير بينها. الصِق المطالبات (أو استورد ملفًا)، وأرفِق صورًا مرجعية لكل صف (اسحب مجلدًا فتتطابق تلقائيًا حسب اسم الملف)، واستخدم `@name` لجلب الشخصيات. يرسل **Run** القائمة كاملةً إلى الطابور.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

ثلاث علامات تبويب: **Text / Frames → Video** (مطالبة نصية، أو إطار بداية/نهاية)، و**Image / Video ingredients → Video** (صور مرجعية أو فيديو مرجعي)، و**Scene stitch → Video**. النماذج: **Veo 3.1 Fast / Lite / Quality** و**Omni Flash**. اختر نسبة العرض إلى الارتفاع، والتكبير (720p / 1080p / 4K)، والبذرة (seed). مرّر المؤشر فوق **?** في شريط علامات التبويب لشرح مبسّط للفرق بين الإطارات والمكوّنات (frames vs. ingredients).

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

من نص إلى صورة، ومن صورة إلى صورة، ومن نص إلى فيديو، ومن صورة إلى فيديو عبر Grok Imagine (علامة التبويب `grok.com` التي سجّلت الدخول فيها من خلال إضافة Auth Helper). تتيح الصور **8 نسب للعرض إلى الارتفاع** (بما في ذلك 4:3 و21:9 و5:2)؛ ويُولَّد الفيديو بدقة **480p / 720p / 1080p**. لتحويل الصورة إلى فيديو وضعان: **First frame** (تفتتح الصورة المقطع) و**Reference** (حتى 14 صورة موجِّهة).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

توليد الصور والفيديو عبر Meta AI. الأوضاع: من نص إلى صورة، ومن صورة إلى صورة (مكوّنات Character / Scene / Style)، ومن نص إلى فيديو، ومن صورة إلى فيديو (إطار بداية / نهاية).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

ولّد باستخدام OpenAI **GPT Image 2** عبر حسابات ChatGPT الخاصة بك، مع ما يصل إلى 5 صور مرجعية. اختر النسبة (10 خيارات منها 21:9 و4:5 و**custom** — حيث تكتب النسبة في المطالبة)، والجودة، ووضع المطالبة، وجهد الاستدلال (reasoning effort)، والبحث على الويب.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

كبّر مجلدًا من الصور محليًا — اختر الهدف ودعه يعالج الطابور، مع تقدُّم وحالة لكل صف (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

ابنِ مكتبة من الشخصيات القابلة لإعادة الاستخدام: صورة مرجعية، وصوت مخصّص اختياري، وملاحظات عن المظهر/الشخصية. ضع علامة عليها بـ `@name` في أي مطالبة Flow ويحافظ التوليد على تلك الهوية.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

لوحة عقد مرئية. انقر بالزر الأيمن على مقبس عقدة فتعرض القائمة العقد المناسبة فقط — اختر واحدة فتُربط تلقائيًا. اربط سلسلة مطالبة ← generate ← video ← **Extract Frame** ← الفيديو التالي، واستخدم **Merge Video** لدمج مقطعين (اقتطع كل طرف، واختر انتقالًا). احفظ/حمّل الرسم البياني كاملًا كملف `.json`؛ ويُنفّذه **Run Flow** من البداية إلى النهاية.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

حوّل التطبيق إلى خادم أتمتة محلي. شغّله، وانسخ مفتاح API الخاص بك، وأرسِل المهام عبر POST إلى `/api/image/generate` أو `/api/video/generate` أو `/api/grok/generate` أو `/api/meta/generate` أو `/api/openai/generate`، ثم استطلِع `/api/status/<id>`. تسرد الصفحة كل نموذج ونسب العرض إلى الارتفاع التي يدعمها. المخطط الكامل: [`docs/WEBHOOK_INTEGRATION.en.md`](../WEBHOOK_INTEGRATION.en.md).

---

## أين توجد الأشياء

| ماذا | macOS | Windows |
|---|---|---|
| المخرجات (الصور / مقاطع الفيديو) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| الإعدادات، الجلسات، الحسابات | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

تُحفظ إعداداتك وقوائم مطالباتك وجلساتك ومكتبة شخصياتك وقائمة حساباتك وتُستعاد في المرة التالية التي تفتح فيها التطبيق.

---

## استكشاف الأخطاء وإصلاحها

**كل شيء مقفل / شاشة الشراء تظل تُفتح** — انتهت صلاحية خطتك، أو سُجِّل دخول الحساب على جهاز آخر. تحقق من شارة المستوى (أسفل اليسار) وجدِّد.

**توليد Grok لا يفعل شيئًا** — يعمل Grok عبر علامة التبويب `grok.com` الخاصة بك. ثبّت/فعّل إضافة المتصفح **Auth Helper** (Settings ← Grok) وتأكد من تسجيل دخولك إلى grok.com.

**"Active: 0 accounts" على صفحة** — أضِف حسابًا أو أعِد تفعيله في علامة تبويب حساب تلك الصفحة (Settings)، أو انتهت صلاحية رمزه — اضغط **Refresh all**.

**يقول macOS إن التطبيق تالف / يتعذر فتحه** — إنه غير موقّع من Apple. انقر بالزر الأيمن ← **Open** في المرة الأولى، أو شغّل `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**التحديث لا يُثبَّت** — نزّل أحدث إصدار يدويًا من [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
