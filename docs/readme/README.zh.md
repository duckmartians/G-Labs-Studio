<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>一款桌面应用，在所有主流 AI 上批量生成图像与视频 —— Google Flow（Veo 3.1、Omni Flash、Nano Banana）、Grok Imagine、Meta AI 和 ChatGPT GPT Image 2。</b></p>

<p align="center">
  <a href="README.en.md">English</a> ·
  <a href="../../README.md">Tiếng Việt</a> ·
  <b>简体中文</b> ·
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
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="下载 — Windows" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="下载 — macOS (Apple Silicon)" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="下载 — macOS (Intel)" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## 安装

### 第 1 步 — 为你的电脑选择正确的版本

从 **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** 下载最新版本，然后选择与你电脑匹配的文件：

| 你的电脑 | 下载 | Google Drive | 说明 |
|---|---|---|---|
| 🪟 **Windows 10/11（64 位）** | [`G-Labs-Studio-win.exe`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | 适用于所有 Windows 电脑 |
| 🍎 **搭载 Apple 芯片的 Mac（M1/M2/M3/M4）** | [`G-Labs-Studio-mac-arm64.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | 约 2020 年底及以后的 Mac |
| 🍎 **搭载 Intel 芯片的 Mac** | [`G-Labs-Studio-mac-intel.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | 较旧的 Mac（2020 年前） |

**不确定你的 Mac 是什么芯片？** 点击左上角  菜单 → **About This Mac**：
- 有 **Chip**（芯片）一行显示 “Apple M1 / M2 / M3…” → 下载 **arm64** 版本。
- 有 **Processor**（处理器）一行显示 “Intel…” → 下载 **intel** 版本。

> **Intel** 版本在 Apple 芯片的 Mac 上仍可运行（只是较慢），但 **arm64** 版本在 Intel Mac 上**无法打开** —— 所以请选对。

### 第 2 步 — 安装

<details open>
<summary><b>🪟 在 Windows 上</b></summary>

1. 打开下载好的 **`G-Labs-Studio-win.exe`**。
2. 如果出现 **“Windows protected your PC”**（SmartScreen）：点击 **More info** → **Run anyway**。*（该应用尚未用微软证书签名，所以会被提示——并非病毒。）*
3. 在管理员（UAC）提示中点击 **Yes**，然后按照安装程序完成安装。
4. 从 **Start Menu** 或 **Desktop** 快捷方式启动它。

</details>

<details open>
<summary><b>🍎 在 macOS 上</b></summary>

1. 打开下载好的 **`.dmg`**，然后**把 G-Labs Studio 拖到 Applications 文件夹**。
2. 进入 **Applications**，**右键点击**（或按住 Control 点击）**G-Labs Studio** → **Open** → 在对话框中再次点击 **Open**。*（该应用未经 Apple 签名，所以**第一次**必须这样打开；之后就能正常打开。）*
3. 如果 macOS 提示应用**“已损坏 / 无法打开”**，或没有 Open 按钮，打开 **Terminal** 粘贴：
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   然后再次打开应用。

</details>

### 第 3 步 — 登录并选择套餐

**你需要一个 G-Labs 账号。** 打开应用，用 Google 登录并选择套餐。套餐（**FREE / PLUS / MAX**）解锁不同的工具和模型；你可以在应用内购买（银行二维码、PayPal 或 USDT）。一个账号同一时间只能在**一台电脑**上运行——在别处登录会让上一台电脑退出登录。侧边栏左下角的徽章显示你当前的等级。 需要多台设备同时使用，可以购买 **Team** 套餐（价格会随你额外增加的设备数量而上涨）。

> **刚从旧版（G-Labs Automation）切换过来？** 新版**不会**带过来旧版的账号。你需要在新的 G-Labs Studio 中**重新登录所有账号**（Google/Flow、ChatGPT、Meta……）。

应用会**自动更新**：启动时检查 GitHub Releases，并可在应用内下载并安装新版本。

---

## 首次运行

1. **打开应用并用 Google 登录。** 等级徽章（左下角）确认你的套餐。
2. **为你将使用的工具连接账户**（Settings → 对应的账户标签页）：
   - **Google** 账户 → Flow Image / Flow Video
   - **ChatGPT** 账户 → GPT Image 2
   - **Meta** 账户 → Meta Media
   - **Grok** → 通过配套浏览器扩展（Auth Helper）在你已登录的 `grok.com` 标签页中运行 —— 无需账户池
   每个账户标签页在标题栏上显示 **"Active: N accounts"**，让你知道有多少个账户可用。
3. **从左侧边栏选择一个页面**并开始生成。每个生成页面都遵循相同的节奏：在左侧输入或导入提示词，它们落入右侧的**表格**，然后按 **Run**。

每个页面标题都带有一个实时**状态栏** —— *Running · Queued · Done · Failed · Accounts* —— 让你一眼看清整批任务。点击 **Queued** 打开队列管理器，点击 **Accounts** 跳转到账户设置。

---

## 功能

![G-Labs Studio](../screenshots/01-image.png)

- **所有主流生成器，一款应用** —— Google Flow（图像 + 视频）、Grok Imagine、Meta AI（vibes.ai）和 OpenAI GPT Image 2，各自拥有独立页面，配备该提供商所支持的模型和比例。
- **为批量而生** —— 粘贴一列提示词（每行一条）或导入 `.txt`/Excel 文件；每条成为一行。参考图像按文件名自动匹配。以你选择的并发数运行整个列表。
- **先添加，就绪再运行** —— 各行进入队列；**Run / Pause / Stop** 相互独立。在你下令之前不会启动任何任务，队列管理器让你可以重新排序和检查。
- **角色库** —— 一次保存一个角色（参考图像 + 专属语音 + 备注），用 `@name` 将其放入任何提示词；视频会保留该角色的外观和声音。
- **Workflow（节点图）** —— 将节点连成一条流水线：提示词 → 图像 → 视频 → 提取末帧 → 下一段视频，还有一个 **Merge Video** 节点通过裁剪和转场（crossfade、wipe、slide、dissolve……）拼接两段片段。批处理节点会按每条提示词或每张图像循环整条链。
- **Webhook API** —— 一个本地 REST 服务器，让脚本和 AI 代理可以提交 image/video/Grok/Meta/OpenAI 任务并轮询结果。
- **Image Upscaler** 和一个 **Video Editor**（剪切、拼接、幻灯片）用于收尾。
- **稳健可靠** —— 结果经过校验并自动保存；会话可恢复；失败的行会重试。
- **深色 / 浅色主题**、感知等级的 UI，以及 **15 种语言**。

---

## 页面

### 🖼 Flow Image —— Google Flow 图像生成

![Flow Image](../screenshots/01-image.png)

使用 **Nano Banana Pro / 2 / Lite** 批量生成图像。选择模型、宽高比和分辨率（**1K / 2K / 4K** —— 2K/4K 使用模型的放大器），设置同时运行的行数以及它们之间的延迟。粘贴提示词（或导入文件），为每行附加参考图像（拖入一个文件夹，它们会按文件名自动匹配），并用 `@name` 引入角色。**Run** 将整个列表发送到队列。

### 🎬 Flow Video —— Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

三个标签页：**Text / Frames → Video**（一条文本提示词，或首/尾帧）、**Image / Video ingredients → Video**（参考图像或参考视频），以及 **Scene stitch → Video**。模型：**Veo 3.1 Fast / Lite / Quality** 和 **Omni Flash**。选择宽高比、放大（720p / 1080p / 4K）和 seed。将鼠标悬停在标签栏上的 **?** 上，可获得关于 frames 与 ingredients 的通俗解释。

### 🤖 Grok Media —— Grok Imagine

![Grok Media](../screenshots/03-grok.png)

通过 Grok Imagine 进行 text-to-image、image-to-image、text-to-video 和 image-to-video（通过 Auth Helper 扩展在你已登录的 `grok.com` 标签页中运行）。图像提供 **8 种宽高比**（含 4:3、21:9、5:2）；视频以 **480p / 720p / 1080p** 生成。Image-to-video 有两种模式：**First frame**（图像作为片段的开头）和 **Reference**（最多 14 张引导图像）。

### 🎨 Meta Media —— Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

通过 Meta AI 生成图像和视频。模式：text-to-image、image-to-image（Character / Scene / Style 组件）、text-to-video 和 image-to-video（首 / 尾帧）。

### ✨ GPT Image 2 —— OpenAI

![GPT Image 2](../screenshots/05-openai.png)

使用你的 ChatGPT 账户通过 OpenAI **GPT Image 2** 生成，最多可用 5 张参考图像。选择比例（10 个选项，含 21:9、4:5 和 **custom** —— 你在提示词中写出比例）、质量、提示词模式、推理强度和网页搜索。

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

在本地放大一整个文件夹的图像 —— 选择目标并让它处理队列，带有每行的进度和状态（processing / done / error）。

### 👤 Characters

![Characters](../screenshots/07-character.png)

构建一个可复用角色库：一张参考图像、一个可选的自定义语音，以及外观/性格备注。在任何 Flow 提示词中用 `@name` 标记它们，生成时会保留该身份。

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

一块可视化节点画布。右键点击某个节点的接口，菜单只会提供合适的节点 —— 选中一个，它会自动连线。将 提示词 → generate → video → **Extract Frame** → 下一段视频 连成链，并用 **Merge Video** 拼接两段片段（裁剪每一端，选择转场）。将整张图保存/加载为 `.json` 文件；**Run Flow** 会端到端执行它。

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

把应用变成一个本地自动化服务器。启动它，复制你的 API key，向 `/api/image/generate`、`/api/video/generate`、`/api/grok/generate`、`/api/meta/generate` 或 `/api/openai/generate` POST 任务，然后轮询 `/api/status/<id>`。该页面列出每个模型及其支持的宽高比。完整架构：[`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md)。

---

## 文件存放位置

| 内容 | macOS | Windows |
|---|---|---|
| 输出（图像 / 视频） | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| 设置、会话、账户 | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

你的设置、提示词列表、会话、角色库和账户列表会被保存，并在下次打开应用时恢复。

---

## 故障排查

**一切都被锁定 / 购买界面不断弹出** —— 你的套餐已过期，或该账户在另一台设备上登录了。检查等级徽章（左下角）并续期。

**Grok 生成没有反应** —— Grok 通过你的 `grok.com` 标签页运行。安装/启用 **Auth Helper** 浏览器扩展（Settings → Grok），并确保你已登录 grok.com。

**某页面显示 "Active: 0 accounts"** —— 在该页面的账户标签页（Settings）中添加或重新启用一个账户，或者它的 token 已过期 —— 按 **Refresh all**。

**macOS 提示应用已损坏 / 无法打开** —— 它未经 Apple 签名。首次请右键 → **Open**，或运行 `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`。

**更新无法安装** —— 从 [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) 手动下载最新版本。
