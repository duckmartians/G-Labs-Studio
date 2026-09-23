<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>แอปเดสก์ท็อปเดียวสำหรับสร้างภาพและวิดีโอแบบเป็นชุดข้าม AI รายใหญ่ทุกเจ้า — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI และ ChatGPT GPT Image 2</b></p>

<p align="center">
  <a href="README.en.md">English</a> ·
  <a href="../../README.md">Tiếng Việt</a> ·
  <a href="README.zh.md">简体中文</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.pt.md">Português</a> ·
  <a href="README.ru.md">Русский</a> ·
  <a href="README.hi.md">हिन्दी</a> ·
  <a href="README.bn.md">বাংলা</a> ·
  <b>ไทย</b> ·
  <a href="README.tr.md">Türkçe</a> ·
  <a href="README.ur.md">اردو</a> ·
  <a href="README.ar.md">العربية</a> ·
  <a href="README.de.md">Deutsch</a> ·
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="ดาวน์โหลด — Windows" src="https://img.shields.io/badge/%E0%B8%94%E0%B8%B2%E0%B8%A7%E0%B8%99%E0%B9%8C%E0%B9%82%E0%B8%AB%E0%B8%A5%E0%B8%94-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="ดาวน์โหลด — macOS (Apple Silicon)" src="https://img.shields.io/badge/%E0%B8%94%E0%B8%B2%E0%B8%A7%E0%B8%99%E0%B9%8C%E0%B9%82%E0%B8%AB%E0%B8%A5%E0%B8%94-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="ดาวน์โหลด — macOS (Intel)" src="https://img.shields.io/badge/%E0%B8%94%E0%B8%B2%E0%B8%A7%E0%B8%99%E0%B9%8C%E0%B9%82%E0%B8%AB%E0%B8%A5%E0%B8%94-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## การติดตั้ง

### ขั้นที่ 1 — เลือกไฟล์ให้ตรงกับเครื่องของคุณ

ดาวน์โหลดเวอร์ชันล่าสุดจาก **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** แล้วเลือกไฟล์ที่ตรงกับเครื่องของคุณ:

| เครื่องของคุณ | ดาวน์โหลด | หมายเหตุ |
|---|---|---|
| 🪟 **Windows 10/11 (64 บิต)** | [`G-Labs-Studio-win.exe`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | สำหรับพีซี Windows ทุกเครื่อง |
| 🍎 **Mac ชิป Apple (M1/M2/M3/M4)** | [`G-Labs-Studio-mac-arm64.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | Mac ตั้งแต่ราวปลายปี 2020 เป็นต้นมา |
| 🍎 **Mac ชิป Intel** | [`G-Labs-Studio-mac-intel.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | Mac รุ่นเก่า (ก่อนปี 2020) |

**ไม่แน่ใจว่า Mac ของคุณใช้ชิปอะไร?** คลิกเมนู  (มุมบนซ้าย) → **About This Mac**:
- มีบรรทัด **Chip** ระบุ “Apple M1 / M2 / M3…” → ดาวน์โหลดไฟล์ **arm64**
- มีบรรทัด **Processor** ระบุ “Intel…” → ดาวน์โหลดไฟล์ **intel**

> ไฟล์ **Intel** ยังรันบน Mac ชิป Apple ได้ (แค่ช้ากว่า) แต่ไฟล์ **arm64** จะ **เปิดไม่ได้** บน Mac Intel — จึงควรเลือกให้ถูก

### ขั้นที่ 2 — ติดตั้ง

<details open>
<summary><b>🪟 บน Windows</b></summary>

1. เปิดไฟล์ **`G-Labs-Studio-win.exe`** ที่ดาวน์โหลดมา
2. ถ้าขึ้น **“Windows protected your PC”** (SmartScreen): คลิก **More info** → **Run anyway** *(แอปยังไม่ได้เซ็นด้วยใบรับรองของ Microsoft จึงถูกเตือน — ไม่ใช่ไวรัส)*
3. คลิก **Yes** ที่หน้าต่างสิทธิ์ผู้ดูแล (UAC) แล้วทำตามตัวติดตั้งจนเสร็จ
4. เปิดจาก **Start Menu** หรือทางลัดบน **Desktop**

</details>

<details open>
<summary><b>🍎 บน macOS</b></summary>

1. เปิดไฟล์ **`.dmg`** ที่ดาวน์โหลดมา แล้ว **ลาก G-Labs Studio ไปไว้ในโฟลเดอร์ Applications**
2. ไปที่ **Applications**, **คลิกขวา** (หรือกด Control แล้วคลิก) ที่ **G-Labs Studio** → **Open** → คลิก **Open** อีกครั้งในกล่องโต้ตอบ *(แอปยังไม่ได้เซ็นโดย Apple จึงต้องเปิดแบบนี้ใน **ครั้งแรก**; หลังจากนั้นเปิดได้ตามปกติ)*
3. ถ้า macOS แจ้งว่าแอป **“เสียหาย / เปิดไม่ได้”** หรือไม่มีปุ่ม Open ให้เปิด **Terminal** แล้ววาง:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   จากนั้นเปิดแอปอีกครั้ง

</details>

### ขั้นที่ 3 — ลงชื่อเข้าใช้และเลือกแพ็กเกจ

**คุณต้องมีบัญชี G-Labs** เปิดแอป ลงชื่อเข้าใช้ด้วย Google แล้วเลือกแพ็กเกจ แพ็กเกจ (**FREE / PLUS / MAX**) ปลดล็อกเครื่องมือและโมเดลต่างกัน ซื้อได้ในแอป (QR ธนาคาร, PayPal หรือ USDT) หนึ่งบัญชีใช้ได้ **ครั้งละหนึ่งเครื่อง** — ลงชื่อเข้าใช้ที่อื่นจะทำให้เครื่องก่อนหน้าออกจากระบบ ป้ายมุมล่างซ้ายของแถบข้างแสดงระดับปัจจุบันของคุณ ต้องใช้หลายอุปกรณ์พร้อมกันใช่ไหม? สามารถซื้อแพ็กเกจ **Team** ได้ (ราคาจะเพิ่มตามจำนวนอุปกรณ์ที่คุณเพิ่ม)

> **เพิ่งย้ายจากเวอร์ชันเก่า (G-Labs Automation)?** เวอร์ชันใหม่ **ไม่** ยกบัญชีจากเวอร์ชันเก่ามาให้ คุณต้อง **ลงชื่อเข้าใช้ทุกบัญชีใหม่** (Google/Flow, ChatGPT, Meta…) ใน G-Labs Studio ใหม่

แอป **อัปเดตตัวเองอัตโนมัติ**: ตรวจ GitHub Releases เมื่อเปิด และดาวน์โหลดพร้อมติดตั้งเวอร์ชันใหม่ได้จากในแอป

---

## การใช้งานครั้งแรก

1. **เปิดแอปและลงชื่อเข้าใช้ด้วย Google** ป้ายระดับ (มุมล่างซ้าย) ยืนยันแพ็กเกจของคุณ
2. **เชื่อมต่อบัญชีสำหรับเครื่องมือที่คุณจะใช้** (Settings → แท็บบัญชีที่ตรงกัน):
   - บัญชี **Google** → Flow Image / Flow Video
   - บัญชี **ChatGPT** → GPT Image 2
   - บัญชี **Meta** → Meta Media
   - **Grok** → ทำงานผ่านแท็บ `grok.com` ที่คุณล็อกอินไว้ ด้วยส่วนขยายเบราว์เซอร์คู่หู (Auth Helper) — ไม่มีพูลบัญชี
   แท็บบัญชีแต่ละแท็บแสดง **"Active: N accounts"** บนแถบชื่อ เพื่อให้คุณรู้ว่ามีกี่บัญชีที่ใช้งานได้
3. **เลือกหน้าจากแถบด้านข้างซ้าย** แล้วเริ่มสร้าง ทุกหน้าการสร้างมีจังหวะเดียวกัน: พิมพ์หรือนำเข้าพรอมป์ทางซ้าย พวกมันจะไปอยู่ใน **ตาราง** ทางขวา จากนั้นกด **Run**

ส่วนหัวของทุกหน้ามี **แถบสถานะ** แบบเรียลไทม์ — *Running · Queued · Done · Failed · Accounts* — เพื่อให้คุณเห็นชุดงานได้ในพริบตา คลิก **Queued** เพื่อเปิดตัวจัดการคิว **Accounts** เพื่อไปยังการตั้งค่าบัญชี

---

## คุณสมบัติ

![G-Labs Studio](../screenshots/01-image.png)

- **ตัวสร้างรายใหญ่ทุกเจ้า ในแอปเดียว** — Google Flow (ภาพ + วิดีโอ), Grok Imagine, Meta AI (vibes.ai) และ OpenAI GPT Image 2 แต่ละตัวอยู่บนหน้าของตัวเองพร้อมโมเดลและอัตราส่วนที่ผู้ให้บริการนั้นรองรับ
- **ออกแบบมาเพื่อทำเป็นชุด** — วางรายการพรอมป์ (บรรทัดละหนึ่ง) หรือนำเข้าไฟล์ `.txt`/Excel แต่ละรายการจะกลายเป็นหนึ่งแถว ภาพอ้างอิงจับคู่อัตโนมัติตามชื่อไฟล์ รันทั้งรายการด้วยจำนวนการทำงานพร้อมกัน (concurrency) ที่คุณเลือก
- **เพิ่มก่อน รันเมื่อพร้อม** — แถวต่าง ๆ เข้าสู่คิว **Run / Pause / Stop** แยกกัน ไม่มีอะไรเริ่มจนกว่าคุณจะสั่ง และตัวจัดการคิวให้คุณจัดลำดับใหม่และตรวจสอบได้
- **คลังตัวละคร** — บันทึกตัวละครครั้งเดียว (ภาพอ้างอิง + เสียงของตัวเอง + บันทึก) แล้วใส่ลงในพรอมป์ใดก็ได้ด้วย `@name` วิดีโอจะคงหน้าตาและเสียงของตัวละครนั้นไว้
- **Workflow (โหนดกราฟ)** — เชื่อมโหนดเข้าเป็นไปป์ไลน์: พรอมป์ → ภาพ → วิดีโอ → ดึงเฟรมสุดท้าย → วิดีโอถัดไป พร้อมโหนด **Merge Video** ที่รวมสองคลิปด้วยการตัดและทรานซิชัน (crossfade, wipe, slide, dissolve…) โหนดแบบชุดวนทำทั้งเชนต่อพรอมป์หรือต่อภาพ
- **Webhook API** — เซิร์ฟเวอร์ REST ในเครื่อง เพื่อให้สคริปต์และเอเจนต์ AI ส่งงาน image/video/Grok/Meta/OpenAI และดึงผลลัพธ์ได้
- **Image Upscaler** และ **Video Editor** (ตัด, ต่อ, สไลด์โชว์) สำหรับงานเก็บรายละเอียด
- **ทนทาน** — ผลลัพธ์ถูกตรวจสอบและบันทึกอัตโนมัติ เซสชันถูกกู้คืน แถวที่ล้มเหลวลองใหม่
- **ธีมมืด / สว่าง**, UI ที่รับรู้ระดับ (tier) และ **15 ภาษา**

---

## หน้าต่าง ๆ

### 🖼 Flow Image — การสร้างภาพด้วย Google Flow

![Flow Image](../screenshots/01-image.png)

สร้างภาพเป็นชุดด้วย **Nano Banana Pro / 2 / Lite** เลือกโมเดล อัตราส่วนภาพ และความละเอียด (**1K / 2K / 4K** — 2K/4K ใช้ตัวอัปสเกลของโมเดล) ตั้งค่าว่าจะรันกี่แถวพร้อมกันและดีเลย์ระหว่างแถว วางพรอมป์ (หรือนำเข้าไฟล์) แนบภาพอ้างอิงต่อแถว (ลากโฟลเดอร์เข้ามาแล้วจะจับคู่อัตโนมัติตามชื่อไฟล์) และใช้ `@name` เพื่อดึงตัวละครเข้ามา **Run** จะส่งทั้งรายการเข้าคิว

### 🎬 Flow Video — Veo และ Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

สามแท็บ: **Text / Frames → Video** (พรอมป์ข้อความ หรือเฟรมเริ่ม/จบ), **Image / Video ingredients → Video** (ภาพอ้างอิงหรือวิดีโออ้างอิง) และ **Scene stitch → Video** โมเดล: **Veo 3.1 Fast / Lite / Quality** และ **Omni Flash** เลือกอัตราส่วนภาพ อัปสเกล (720p / 1080p / 4K) และ seed วางเมาส์เหนือ **?** บนแถบแท็บเพื่อดูคำอธิบายภาษาง่าย ๆ ว่า frames ต่างจาก ingredients อย่างไร

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

ข้อความเป็นภาพ, ภาพเป็นภาพ, ข้อความเป็นวิดีโอ และภาพเป็นวิดีโอ ผ่าน Grok Imagine (แท็บ `grok.com` ที่คุณล็อกอินไว้ผ่านส่วนขยาย Auth Helper) ภาพมี **8 อัตราส่วน** (รวมถึง 4:3, 21:9, 5:2) วิดีโอสร้างที่ **480p / 720p / 1080p** ภาพเป็นวิดีโอมีสองโหมด: **First frame** (ภาพเปิดคลิป) และ **Reference** (ภาพนำทางได้สูงสุด 14 ภาพ)

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

การสร้างภาพและวิดีโอผ่าน Meta AI โหมด: ข้อความเป็นภาพ, ภาพเป็นภาพ (คอมโพเนนต์ Character / Scene / Style), ข้อความเป็นวิดีโอ และภาพเป็นวิดีโอ (เฟรมเริ่ม / จบ)

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

สร้างด้วย OpenAI **GPT Image 2** โดยใช้บัญชี ChatGPT ของคุณ พร้อมภาพอ้างอิงได้สูงสุด 5 ภาพ เลือกอัตราส่วน (10 ตัวเลือก รวมถึง 21:9, 4:5 และ **custom** — ที่คุณเขียนอัตราส่วนในพรอมป์) คุณภาพ โหมดพรอมป์ reasoning effort และการค้นหาเว็บ

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

อัปสเกลโฟลเดอร์ภาพในเครื่อง — เลือกเป้าหมายแล้วให้มันประมวลผลคิว พร้อมความคืบหน้าและสถานะรายแถว (processing / done / error)

### 👤 Characters

![Characters](../screenshots/07-character.png)

สร้างคลังตัวละครที่นำกลับมาใช้ซ้ำได้: ภาพอ้างอิง เสียงกำหนดเองแบบไม่บังคับ และบันทึกหน้าตา/บุคลิก แท็กพวกเขาด้วย `@name` ในพรอมป์ Flow ใดก็ได้ แล้วการสร้างจะคงอัตลักษณ์นั้นไว้

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

แคนวาสโหนดแบบภาพ คลิกขวาที่ซ็อกเก็ตของโหนด เมนูจะเสนอเฉพาะโหนดที่เข้ากันได้ — เลือกหนึ่งแล้วมันจะเชื่อมต่อโดยอัตโนมัติ ต่อเชน พรอมป์ → generate → วิดีโอ → **Extract Frame** → วิดีโอถัดไป และใช้ **Merge Video** เพื่อรวมสองคลิป (ตัดปลายแต่ละด้าน เลือกทรานซิชัน) บันทึก/โหลดกราฟทั้งหมดเป็นไฟล์ `.json` **Run Flow** รันตั้งแต่ต้นจนจบ

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

เปลี่ยนแอปให้เป็นเซิร์ฟเวอร์อัตโนมัติในเครื่อง เริ่มมัน คัดลอก API key ของคุณ แล้ว POST งานไปยัง `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` หรือ `/api/openai/generate` จากนั้นดึงสถานะที่ `/api/status/<id>` หน้านี้แสดงรายการทุกโมเดลและอัตราส่วนภาพที่รองรับ สคีมาฉบับเต็ม: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md)

---

## ไฟล์ต่าง ๆ อยู่ที่ไหน

| อะไร | macOS | Windows |
|---|---|---|
| เอาต์พุต (ภาพ / วิดีโอ) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| การตั้งค่า, เซสชัน, บัญชี | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

การตั้งค่า รายการพรอมป์ เซสชัน คลังตัวละคร และรายการบัญชีของคุณจะถูกบันทึกและกู้คืนในครั้งถัดไปที่คุณเปิดแอป

---

## การแก้ปัญหา

**ทุกอย่างถูกล็อก / หน้าจอซื้อเปิดขึ้นมาเรื่อย ๆ** — แพ็กเกจของคุณหมดอายุ หรือบัญชีถูกลงชื่อเข้าใช้บนเครื่องอื่น ตรวจสอบป้ายระดับ (มุมล่างซ้าย) แล้วต่ออายุ

**การสร้าง Grok ไม่ทำอะไรเลย** — Grok ทำงานผ่านแท็บ `grok.com` ของคุณ ติดตั้ง/เปิดใช้งานส่วนขยายเบราว์เซอร์ **Auth Helper** (Settings → Grok) และตรวจสอบว่าคุณล็อกอิน grok.com อยู่

**"Active: 0 accounts" บนหน้าหนึ่ง** — เพิ่มหรือเปิดใช้งานบัญชีอีกครั้งในแท็บบัญชีของหน้านั้น (Settings) หรือโทเคนหมดอายุ — กด **Refresh all**

**macOS บอกว่าแอปเสียหาย / เปิดไม่ได้** — มันไม่ได้เซ็นโดย Apple คลิกขวา → **Open** ในครั้งแรก หรือรัน `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`

**อัปเดตติดตั้งไม่ได้** — ดาวน์โหลดบิลด์ล่าสุดด้วยตนเองจาก [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)
