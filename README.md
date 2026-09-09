<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>One desktop app to batch-generate images &amp; videos across every major AI — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI and ChatGPT GPT Image 2.</b></p>

<p align="center">
  <b>English</b> ·
  <a href="docs/readme/README.vi.md">Tiếng Việt</a> ·
  <a href="docs/readme/README.zh.md">简体中文</a> ·
  <a href="docs/readme/README.es.md">Español</a> ·
  <a href="docs/readme/README.pt.md">Português</a> ·
  <a href="docs/readme/README.ru.md">Русский</a> ·
  <a href="docs/readme/README.hi.md">हिन्दी</a> ·
  <a href="docs/readme/README.bn.md">বাংলা</a> ·
  <a href="docs/readme/README.th.md">ไทย</a> ·
  <a href="docs/readme/README.tr.md">Türkçe</a> ·
  <a href="docs/readme/README.ur.md">اردو</a> ·
  <a href="docs/readme/README.ar.md">العربية</a> ·
  <a href="docs/readme/README.de.md">Deutsch</a> ·
  <a href="docs/readme/README.id.md">Bahasa Indonesia</a> ·
  <a href="docs/readme/README.ko.md">한국어</a>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Download for Windows" src="https://img.shields.io/badge/Download-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Download for macOS (Apple Silicon)" src="https://img.shields.io/badge/Download-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Download for macOS (Intel)" src="https://img.shields.io/badge/Download-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

![G-Labs Studio](docs/screenshots/01-image.png)

---

## Install

Download the latest build from **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**:

| Platform | File |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-win.exe` — run the installer (admin/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-mac-intel.dmg` |

**macOS first launch** — the app is not signed by Apple, so macOS quarantines it. Open it the first time with **right-click → Open**, or clear the flag from Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**You need a G-Labs account.** Open the app, sign in with Google, and pick a plan. Plans (**FREE / PLUS / MAX**) unlock different tools and models; you can buy one from inside the app (bank QR, PayPal, or USDT). One account runs on **one machine at a time** — signing in elsewhere signs the previous machine out. The badge at the bottom-left of the sidebar shows your current tier.

The app **updates itself**: it checks GitHub Releases on launch and can download and install the new version from inside the app.

---

## First run

1. **Open the app and sign in with Google.** The tier badge (bottom-left) confirms your plan.
2. **Connect the accounts for the tools you'll use** (Settings → the matching account tab):
   - **Google** accounts → Flow Image / Flow Video
   - **ChatGPT** accounts → GPT Image 2
   - **Meta** accounts → Meta Media
   - **Grok** → runs through your logged-in `grok.com` tab via the companion browser extension (Auth Helper) — no account pool
   Each account tab shows **"Active: N accounts"** on its title bar so you know how many are usable.
3. **Pick a page from the left sidebar** and start generating. Every generation page shares the same rhythm: type or import prompts on the left, they land in a **table** on the right, then press **Run**.

Every page header carries a live **status bar** — *Running · Queued · Done · Failed · Accounts* — so you can see the batch at a glance. Click **Queued** to open the queue manager, **Accounts** to jump to account settings.

---

## Features

- **Every major generator, one app** — Google Flow (image + video), Grok Imagine, Meta AI (vibes.ai) and OpenAI GPT Image 2, each on its own page with the models and ratios that provider supports.
- **Batch by design** — paste a list of prompts (one per line) or import a `.txt`/Excel file; each becomes a row. Reference images auto-match by filename. Run the whole list with a concurrency you choose.
- **Add first, run when ready** — rows go to a queue; **Run / Pause / Stop** are separate. Nothing starts until you say so, and a queue manager lets you reorder and inspect.
- **Character library** — save a character once (reference image + its own voice + notes) and drop it into any prompt with `@name`; the video keeps that character's look and voice.
- **Workflow (node graph)** — wire nodes into a pipeline: prompt → image → video → extract last frame → next video, plus a **Merge Video** node that joins two clips with trims and transitions (crossfade, wipe, slide, dissolve…). Batch nodes loop the whole chain per prompt or per image.
- **Webhook API** — a local REST server so scripts and AI agents can submit image/video/Grok/Meta/OpenAI jobs and poll for results.
- **Image Upscaler** and a **Video Editor** (cut, stitch, slideshow) for finishing.
- **Resilient** — results are verified and auto-saved; sessions restore; failed rows retry.
- **Dark / light theme**, tier-aware UI, and **15 languages**.

---

## Pages

### 🖼 Flow Image — Google Flow image generation

![Flow Image](docs/screenshots/01-image.png)

Batch-generate images with **Nano Banana Pro / 2 / Lite**. Pick the model, aspect ratio, and resolution (**1K / 2K / 4K** — 2K/4K use the model's upscaler), set how many rows run at once and the delay between them. Paste prompts (or import a file), attach reference images per row (drag a folder and they auto-match by filename), and use `@name` to pull in characters. **Run** sends the whole list to the queue.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](docs/screenshots/02-flow-video.png)

Three tabs: **Text / Frames → Video** (a text prompt, or a start/end frame), **Image / Video ingredients → Video** (reference images or a reference video), and **Scene stitch → Video**. Models: **Veo 3.1 Fast / Lite / Quality** and **Omni Flash**. Choose aspect ratio, upscale (720p / 1080p / 4K) and seed. Hover the **?** on the tab bar for a plain-language explainer of frames vs. ingredients.

### 🤖 Grok Media — Grok Imagine

![Grok Media](docs/screenshots/03-grok.png)

Text-to-image, image-to-image, text-to-video and image-to-video through Grok Imagine (your logged-in `grok.com` tab via the Auth Helper extension). Images offer **8 aspect ratios** (incl. 4:3, 21:9, 5:2); video generates at **480p / 720p / 1080p**. Image-to-video has two modes: **First frame** (the image opens the clip) and **Reference** (up to 14 guiding images).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](docs/screenshots/04-meta.png)

Image and video generation via Meta AI. Modes: text-to-image, image-to-image (Character / Scene / Style components), text-to-video and image-to-video (start / end frame).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](docs/screenshots/05-openai.png)

Generate with OpenAI **GPT Image 2** using your ChatGPT accounts, with up to 5 reference images. Choose the ratio (10 options including 21:9, 4:5 and **custom** — where you write the ratio in the prompt), quality, prompt mode, reasoning effort and web search.

### 🔍 Image Upscaler

![Image Upscaler](docs/screenshots/06-upscaler.png)

Upscale a folder of images locally — pick the target and let it process the queue, with per-row progress and status (processing / done / error).

### 👤 Characters

![Characters](docs/screenshots/07-character.png)

Build a library of reusable characters: a reference image, an optional custom voice, and appearance/personality notes. Tag them with `@name` in any Flow prompt and the generation keeps that identity.

### 🔗 Workflow

![Workflow](docs/screenshots/08-workflow.png)

A visual node canvas. Right-click a node's socket and the menu offers only the nodes that fit — pick one and it wires up automatically. Chain prompt → generate → video → **Extract Frame** → next video, and use **Merge Video** to join two clips (trim each end, pick a transition). Save/load the whole graph as a `.json` file; **Run Flow** executes it end to end.

### 🌐 Webhook API

![Webhook API](docs/screenshots/09-webhook.png)

Turn the app into a local automation server. Start it, copy your API key, and POST jobs to `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` or `/api/openai/generate`, then poll `/api/status/<id>`. The page lists every model and its supported aspect ratios. Full schema: [`docs/WEBHOOK_INTEGRATION.en.md`](docs/WEBHOOK_INTEGRATION.en.md).

---

## Where things live

| What | macOS | Windows |
|---|---|---|
| Output (images / videos) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Settings, sessions, accounts | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Your settings, prompt lists, sessions, character library and account list are saved and restored the next time you open the app.

---

## Troubleshooting

**Everything is locked / the buy screen keeps opening** — your plan expired, or the account signed in on another machine. Check the tier badge (bottom-left) and renew.

**A Grok generation does nothing** — Grok runs through your `grok.com` tab. Install/enable the **Auth Helper** browser extension (Settings → Grok) and make sure you're logged in to grok.com.

**"Active: 0 accounts" on a page** — add or re-enable an account in that page's account tab (Settings), or its token expired — press **Refresh all**.

**macOS says the app is damaged / can't be opened** — it isn't signed by Apple. Right-click → **Open** the first time, or run `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**An update won't install** — download the latest build manually from [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
