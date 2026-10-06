<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>One desktop app to batch-generate images &amp; videos across every major AI - Google Flow (Veo 3.1, Omni Flash, Nano Banana), Google Vids, Google Pics, ChatGPT GPT Image 2, Meta Vibes and Grok - plus video tools, a node workflow and a Webhook API.</b></p>

<p align="center">
  <b>English</b> ·
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
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Download for Windows" src="https://img.shields.io/badge/Download-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Download for macOS (Apple Silicon)" src="https://img.shields.io/badge/Download-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Download for macOS (Intel)" src="https://img.shields.io/badge/Download-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Install

### Step 1 - Pick the right build for your machine

Download the latest build from **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**, then choose the file that matches your machine:

| Your machine | Download | Google Drive | Notes |
|---|---|---|---|
| 🪟 **Windows 10/11 (64-bit)** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | For any Windows PC |
| 🍎 **Mac with Apple chip (M1/M2/M3/M4)** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Macs from ~late 2020 onward |
| 🍎 **Mac with Intel chip** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Older Macs (before 2020) |

**Not sure which chip your Mac has?** Click the  menu (top-left) → **About This Mac**:
- A **Chip** line reading "Apple M1 / M2 / M3…" → download the **arm64** build.
- A **Processor** line reading "Intel…" → download the **intel** build.

> The **Intel** build still runs on an Apple-chip Mac (just slower), but the **arm64** build will **not open** on an Intel Mac - so pick the right one.

### Step 2 - Install

<details open>
<summary><b>🪟 On Windows</b></summary>

1. Open the downloaded **`G-Labs-Studio-win.exe`**.
2. If **"Windows protected your PC"** (SmartScreen) appears: click **More info** → **Run anyway**. *(The app isn't code-signed with a Microsoft certificate yet, so it's flagged - it isn't a virus.)*
3. Click **Yes** on the admin (UAC) prompt, then follow the installer to the end.
4. Launch it from the **Start Menu** or the **Desktop** shortcut.

</details>

<details open>
<summary><b>🍎 On macOS</b></summary>

1. Open the downloaded **`.dmg`**, then **drag G-Labs Studio into the Applications folder**.
2. Go to **Applications**, **right-click** (or Control-click) **G-Labs Studio** → **Open** → click **Open** again in the dialog. *(The app isn't signed by Apple, so you must open it this way the **first time**; afterwards it opens normally.)*
3. If macOS says the app is **"damaged / can't be opened"**, or there's no Open button, open **Terminal** and paste:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   Then open the app again.

</details>

### Step 3 - Sign in &amp; pick a plan

**You need a G-Labs account.** Open the app, sign in with Google, and pick a plan. Plans (**BASIC / PLUS / MAX**) unlock different tools and models; you can buy one from inside the app (bank QR, PayPal, or USDT). One account runs on **one machine at a time** - signing in elsewhere signs the previous machine out. The badge at the bottom-left of the sidebar shows your current tier. Need **several devices at once**? You can buy a **Team** plan (the price scales with the number of extra devices you add).

> **Just switched from the old version (G-Labs Automation)?** The new version does **not** carry your accounts over. You'll need to **sign in to all your accounts again** (Google/Flow, ChatGPT, Meta…) in the new G-Labs Studio.

The app **updates itself**: it checks GitHub Releases on launch and can download and install the new version from inside the app.

---

## First run

1. **Open the app and sign in with Google.** The tier badge (bottom-left: **BASIC / PLUS / MAX**) confirms your plan.
2. **Connect accounts for the tools you'll use** (**Settings** → the matching accounts tab):
   - **Flow Accounts** → Flow Image / Flow Video
   - **Google Accounts** → **Google Vids** and **Google Pics** (both pages share these Google accounts; each account is switched on separately for Vids video and for Pics images)
   - **ChatGPT Account** → GPT Image 2
   - **Vibes Account** → Meta Vibes
   - **Grok Account** → no account store: this tab walks you through installing the **Auth Helper** browser extension, then Grok runs through your signed-in `grok.com` tab in Chrome

   Each accounts tab shows **"Active: N accounts"** in its title bar so you know how many are usable.
3. **Pick a page from the left sidebar** and start generating. Every generation page follows the same rhythm: type or import prompts on the left, they land in a **table** on the right, then hit **Run**.

Every page header carries a live **status strip** - *Running · Queued · Done · Failed · Accounts* - so you see the whole batch at a glance. Click **Queued** to open the queue manager, click **Accounts** to jump to account settings.

---

## Features

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **Every major generator, one app** - Google Flow (image + video), Google Vids, Google Pics, GPT Image 2, Meta Vibes and Grok, each on its own page with the models and ratios that provider supports.
- **Built for batches** - paste a prompt list (one per line) or import `.txt`/Excel; each prompt becomes a row. Reference images auto-match by file name. Run the whole list with the number of parallel threads you choose.
- **Add first, run when ready** - rows go into a queue; **Run / Pause / Stop** are separate. Nothing starts until you say so, and the queue manager lets you reorder and inspect.
- **Automatic Gemini ✦ logo removal** - Google Pics images and Google Vids videos are cleaned right after download (turn on **Show Gemini logo** to keep it). Files without the logo are left untouched.
- **Character library** - save a character once (reference image + voice + notes) and call it with `@name` in Flow Image, Flow Video and Google Vids prompts to keep scenes consistent.
- **Workflow (node graph)** - wire nodes into a pipeline: prompt → image → video → extract the last frame → next video, plus a **Merge Video** node that joins two clips with a transition.
- **Video Tools** - timeline video editing, subtitle-synced image slideshows, video splitting, frame extraction and video logo removal, right inside the app.
- **Image Upscaler** on your own machine and a **Webhook API** for automation.
- **Resilient** - results are verified and auto-saved; sessions are restored; failed rows retry.
- **Light / Dark theme**, tier-aware UI, and **15 languages**.

---

## Pages

### 🖼 Flow Image - Google Flow image generation

![Flow Image](../screenshots/en/flow-image.webp)

Batch-generate images with **Nano Banana Pro / 2 / 2 Lite**. Pick the model, aspect ratio and resolution (**1K / 2K / 4K** - 2K/4K use the model's upscaler), set how many rows run at once and the delay between them. Paste prompts (or import a file), attach reference images per row (drop a folder and they auto-match by file name), and use `@name` to pull in a character. The **Show Veo / Gemini logo** switch (off by default) is shared with the Flow Video page. **Run** sends the whole list to the queue.

### 🎬 Flow Video - Veo &amp; Omni Flash

![Flow Video](../screenshots/en/flow-video.webp)

Three tabs: **Text / Frame → Video** (a text prompt, or start/end frames), **Image / Video Ingredients → Video** (reference images or a reference video) and **Scene Chain → Video**. Models: **Veo 3.1 Fast / Lite / Quality** and **Omni Flash**. Choose aspect ratio, upscale (720p / 1080p / 4K) and seed. Hover the **?** on the tab bar for a plain-language explanation of frames vs. ingredients.

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

Make videos with your Google account in three tabs: **Text → Video**, **Image → Video** (one opening image) and **Components → Video** (up to 3 component images). Choose landscape/portrait, 720p / 1080p and a 3-10 second duration - or put a tag like `[4s]` in the prompt to give each row its own length. Finished videos can be upscaled to 1080p straight from the table. Each account has a quota measured in seconds of video; add more accounts to run faster. The Gemini ✦ logo on downloaded videos (720p / 1080p) is removed automatically unless you turn on **Show Gemini logo**.

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

Two tabs: **Text → Image** and **Image → Image** with **up to 14 reference images** (characters, objects, scenes, style). Each run Google returns 3-9 images; **Keep images per run** decides how many to keep (1-4 or all). 10 aspect ratios, including 21:9, 3:2 and 5:4. Every run costs 1 Google Pics run whatever the number of images; a prompt refused by the content policy costs nothing. Pics shares the **Google Accounts** with Google Vids.

**Automatic Gemini ✦ logo removal:** downloaded Pics images have the ✦ mark in the bottom-right corner removed right after download, using a logo map measured specifically for Google Pics - the logo blend is reversed, so the original texture under it is restored instead of blurred. Images where no logo is detected are left as they are. To keep the logo, turn on **Show Gemini logo**.

### ✨ GPT Image 2 - OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

Generate with OpenAI **GPT Image 2** using your ChatGPT account, with up to 5 reference images. Choose the ratio (10 options including 21:9, 4:5 and **custom** - where you write the ratio in the prompt), quality, prompt mode, reasoning level and web search.

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

Create images and videos on Meta Vibes in four tabs: **Text → Image**, **Text → Video**, **Image → Image** (character / scene / style images) and **Image → Video** (start / end frame). Queued and downloaded automatically.

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

Text → Image, Image → Image, Text → Video and Image → Video through Grok Imagine (your signed-in `grok.com` tab, via the Auth Helper extension). Images come in **8 aspect ratios** (including 4:3, 21:9, 5:2); videos render at **480p / 720p / 1080p**. Image → Video has two modes: **First frame** (the image opens the clip) and **Reference images** (up to 14 guide images).

### 👤 Characters

![Characters](../screenshots/en/characters.webp)

Build a reusable cast: a reference image, a voice (one of Flow's preset voices, with an optional delivery description), and notes on look/personality. Tag them with `@name` in Flow Image, Flow Video and Google Vids prompts and the generation keeps that identity (the voice is used by Flow Video only; Google Vids uses the image).

### 🔗 Workflow

![Workflow](../screenshots/en/workflow.webp)

A visual node canvas. Right-click a node's socket and the menu offers only the nodes that fit - pick one and it wires itself in. There are nodes for Flow Image, Flow Video, Grok, Meta and GPT Image 2. Chain prompt → image → video → **Extract Frame** → next video, and use **Merge Video** to join two clips (trim each end, pick a transition). Save/load the whole graph as a `.json` file (format: [`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)); **Run Flow** executes it end-to-end.

### 🎞 Video Tools

Five tabs on one page:

**Video Edit** - a timeline for video, SRT subtitles and audio: cut, split, reorder, auto-fit, then export one finished video.

![Video Edit](../screenshots/en/vt-video.webp)

**Image slideshow matching subtitle file** - load images and an `.srt` file; each image matches a subtitle line automatically, with motion effects, overlays and subtitle styling.

![Image slideshow matching subtitle file](../screenshots/en/vt-slideshow.webp)

**Split video into segments** - by number of parts, fixed or random length, a list of timestamps or a list of A-B ranges; one file or a whole batch, GPU-accelerated when available.

![Split video into segments](../screenshots/en/vt-slicer.webp)

**Extract frames from video** - by total count, time interval, frame interval or motion; one file or an entire folder.

![Extract frames from video](../screenshots/en/vt-extractor.webp)

**Remove video logo** - removes the ✦ logo from Google Vids videos at 720p and 1080p (landscape or portrait), with a before/after preview in the app. Videos without the logo are skipped; originals are kept and results are saved as `<name>_nologo.mp4`.

![Remove video logo](../screenshots/en/vt-logo.webp)

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/en/upscaler.webp)

Enlarge and sharpen images right on your computer - add single images or a whole folder, pick an AI model (Real-ESRGAN, UltraSharp, Remacri…) and a 2x-8x scale, follow per-row progress and compare before/after.

### 🌐 Webhook API

![Webhook API](../screenshots/en/webhook.webp)

Turn the app into a local automation server (MAX plan) so n8n, Make, Zapier, scripts or AI agents can push jobs into the app's queue. Start it, copy your API key, and POST jobs to `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate`, `/api/openai/generate` or `/api/upscale/generate`, then poll `/api/status/<id>`. The page lists every model and its supported aspect ratios. Full schema: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Where things live

| What | macOS | Windows |
|---|---|---|
| Outputs (images / videos) | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| Settings, sessions, accounts, characters | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Each page has its own subfolder inside `output` (one smaller folder per run); you can change the save folder on each page. Your settings, prompt lists, sessions, character library and account list are saved and restored the next time you open the app.

---

## Troubleshooting

**Everything is locked / the purchase screen keeps opening** - your plan expired, or the account signed in on another machine. Check the tier badge (bottom-left) and renew. Google Vids and Google Pics need a PLUS/MAX plan; the Webhook API needs MAX.

**A Grok generation does nothing** - Grok runs through your `grok.com` tab. Install/enable the **Auth Helper** browser extension (Settings → Grok Account) and make sure you're signed in to grok.com.

**Google Pics says there is no account** - Pics uses the Google Vids accounts. Add one in Settings → **Google Accounts**.

**"Active: 0 accounts" on a page** - add or re-enable an account in that page's accounts tab (Settings), or its token expired - hit **Refresh All**.

**Windows blocks it at "Windows protected your PC"** - click **More info → Run anyway**. The app isn't code-signed with a Microsoft certificate yet, so it's flagged - it isn't a virus.

**macOS says the app is damaged / can't be opened** - it isn't Apple-signed yet. Right-click → **Open** the first time, or run `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**An update didn't install** - download the latest build manually from [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
