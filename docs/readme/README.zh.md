<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>一款桌面应用，在所有主流 AI 上批量生成图像与视频 -- Google Flow（Veo 3.1、Omni Flash、Nano Banana）、Google Vids、Google Pics、ChatGPT GPT Image 2、Meta Vibes 和 Grok -- 另有视频工具、节点工作流和 Webhook API。</b></p>

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
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="下载 - Windows" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="下载 - macOS (Apple Silicon)" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="下载 - macOS (Intel)" src="https://img.shields.io/badge/%E4%B8%8B%E8%BD%BD-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## 安装

### 第 1 步 - 为你的电脑选择正确的版本

从 **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** 下载最新版本，然后选择与你电脑匹配的文件：

| 你的电脑 | 下载 | Google Drive | 说明 |
|---|---|---|---|
| 🪟 **Windows 10/11（64 位）** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | 适用于所有 Windows 电脑 |
| 🍎 **搭载 Apple 芯片的 Mac（M1/M2/M3/M4）** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | 约 2020 年底及以后的 Mac |
| 🍎 **搭载 Intel 芯片的 Mac** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | 较旧的 Mac（2020 年前） |

**不确定你的 Mac 是什么芯片？** 点击左上角  菜单 → **About This Mac**：
- 有 **Chip**（芯片）一行显示 “Apple M1 / M2 / M3…” → 下载 **arm64** 版本。
- 有 **Processor**（处理器）一行显示 “Intel…” → 下载 **intel** 版本。

> **Intel** 版本在 Apple 芯片的 Mac 上仍可运行（只是较慢），但 **arm64** 版本在 Intel Mac 上**无法打开** -- 所以请选对。

### 第 2 步 - 安装

<details open>
<summary><b>🪟 在 Windows 上</b></summary>

1. 打开下载好的 **`G-Labs-Studio-win.exe`**。
2. 如果出现 **“Windows protected your PC”**（SmartScreen）：点击 **More info** → **Run anyway**。*（该应用尚未用微软证书签名，所以会被提示--并非病毒。）*
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

### 第 3 步 - 登录并选择套餐

**你需要一个 G-Labs 账号。** 打开应用，用 Google 登录并选择套餐。套餐（**BASIC / PLUS / MAX**）解锁不同的工具和模型；你可以在应用内购买（银行二维码、PayPal 或 USDT）。一个账号同一时间只能在**一台电脑**上运行--在别处登录会让上一台电脑退出登录。侧边栏左下角的徽章显示你当前的等级。 需要多台设备同时使用，可以购买 **Team** 套餐（价格会随你额外增加的设备数量而上涨）。

> **刚从旧版（G-Labs Automation）切换过来？** 新版**不会**带过来旧版的账号。你需要在新的 G-Labs Studio 中**重新登录所有账号**（Google/Flow、ChatGPT、Meta……）。

应用会**自动更新**：启动时检查 GitHub Releases，并可在应用内下载并安装新版本。

---

## 首次运行

1. **打开应用并用 Google 登录。** 等级徽章（左下角：**BASIC / PLUS / MAX**）确认你的套餐。
2. **为你将使用的工具连接账户**（**设置** → 对应的账户标签页）：
   - **Flow 账户** → Flow 图片 / Flow 视频
   - **Google 账号** → **Google Vids** 和 **Google Pics**（两个页面共用这些 Google 账号；每个账号分别为 Vids 视频和 Pics 图像单独开启）
   - **ChatGPT 账号** → GPT Image 2
   - **Vibes 账号** → Meta Vibes
   - **Grok 账户** → 无账户存储：该标签页会引导你安装 **Auth Helper** 浏览器扩展，之后 Grok 通过你在 Chrome 中已登录的 `grok.com` 标签页运行

   每个账户标签页在标题栏上显示 **"活跃中：N 个账号"**，让你知道有多少个账户可用。
3. **从左侧边栏选择一个页面**并开始生成。每个生成页面都遵循相同的节奏：在左侧输入或导入提示词，它们落入右侧的**表格**，然后按 **Run**。

每个页面标题都带有一个实时**状态栏** -- *运行中 · 队列 · 完成 · 失败 · 账号* -- 让你一眼看清整批任务。点击 **队列** 打开队列管理器，点击 **账号** 跳转到账户设置。

---

## 功能

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **所有主流生成器，一款应用** -- Google Flow（图像 + 视频）、Google Vids、Google Pics、GPT Image 2、Meta Vibes 和 Grok，各自拥有独立页面，配备该提供商所支持的模型和比例。
- **为批量而生** -- 粘贴一列提示词（每行一条）或导入 `.txt`/Excel；每条提示词成为一行。参考图像按文件名自动匹配。以你选择的并行线程数运行整个列表。
- **先添加，就绪再运行** -- 各行进入队列；**Run / Pause / Stop** 相互独立。在你下令之前不会启动任何任务，队列管理器让你可以重新排序和检查。
- **自动去除 Gemini ✦ 徽标** -- Google Pics 图像和 Google Vids 视频在下载后立即被清理（开启 **显示 Gemini 徽标** 即可保留）。没有徽标的文件保持原样。
- **角色库** -- 一次保存一个角色（参考图像 + 语音 + 备注），在 Flow 图片、Flow 视频和 Google Vids 的提示词中用 `@name` 调用，让各个场景保持一致。
- **Workflow（节点图）** -- 将节点连成一条流水线：提示词 → 图像 → 视频 → 提取末帧 → 下一段视频，还有一个 **合并视频** 节点，用转场拼接两段片段。
- **视频工具** -- 时间轴视频编辑、与字幕同步的图片幻灯片、视频分割、帧提取和视频去水印，全部在应用内完成。
- 在你自己电脑上运行的 **图片放大**，以及用于自动化的 **Webhook API**。
- **稳健可靠** -- 结果经过校验并自动保存；会话可恢复；失败的行会重试。
- **浅色 / 深色主题**、感知等级的 UI，以及 **15 种语言**。

---

## 页面

### 🖼 Flow 图片 -- Google Flow 图像生成

![Flow 图片](../screenshots/en/flow-image.webp)

使用 **Nano Banana Pro / 2 / 2 Lite** 批量生成图像。选择模型、宽高比和分辨率（**1K / 2K / 4K** -- 2K/4K 使用模型的放大器），设置同时运行的行数以及它们之间的延迟。粘贴提示词（或导入文件），为每行附加参考图像（拖入一个文件夹，它们会按文件名自动匹配），并用 `@name` 引入角色。**显示 Veo / Gemini 徽标** 开关（默认关闭）与 Flow 视频页面共用。**Run** 将整个列表发送到队列。

### 🎬 Flow 视频 -- Veo &amp; Omni Flash

![Flow 视频](../screenshots/en/flow-video.webp)

三个标签页：**文本 / 画面 → 视频**（一条文本提示词，或首/尾帧）、**图片 / 视频组件 → 视频**（参考图像或参考视频），以及 **场景连接 → 视频**。模型：**Veo 3.1 Fast / Lite / Quality** 和 **Omni Flash**。选择宽高比、放大（720p / 1080p / 4K）和 seed。将鼠标悬停在标签栏上的 **?** 上，可获得关于帧与组件区别的通俗解释。

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

用你的 Google 账号在三个标签页中制作视频：**文本 → 视频**、**图片 → 视频**（一张开场图像）和 **素材 → 视频**（最多 3 张素材图像）。选择横屏/竖屏、720p / 1080p 以及 3-10 秒的时长 -- 或在提示词中加入 `[4s]` 这样的标签，为每一行设定各自的长度。生成好的视频可直接在表格中放大到 1080p。每个账号都有以视频秒数计算的配额；添加更多账号即可运行得更快。下载的视频（720p / 1080p）上的 Gemini ✦ 徽标会被自动去除，除非你开启 **显示 Gemini 徽标**。

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

两个标签页：**文本 → 图像** 和 **图像 → 图像**，支持 **最多 14 张参考图像**（角色、物体、场景、风格）。每次运行 Google 会返回 3-9 张图像；**每次保留图像数** 决定保留多少张（1-4 张或全部）。10 种宽高比，包括 21:9、3:2 和 5:4。无论生成多少张图像，每次运行都消耗 1 次 Google Pics 运行额度；被内容政策拒绝的提示词不消耗额度。Pics 与 Google Vids 共用 **Google 账号**。

**自动去除 Gemini ✦ 徽标：** 下载的 Pics 图像会在下载后立即去除右下角的 ✦ 标记，所用的徽标贴图是专门针对 Google Pics 测量的 -- 徽标的混合被反向还原，因此其下方的原始纹理得以恢复，而不是被模糊处理。未检测到徽标的图像保持原样。如需保留徽标，请开启 **显示 Gemini 徽标**。

### ✨ GPT Image 2 -- OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

使用你的 ChatGPT 账号通过 OpenAI **GPT Image 2** 生成，最多可用 5 张参考图像。选择比例（10 个选项，含 21:9、4:5 和 **custom** -- 你在提示词中写出比例）、质量、提示词模式、推理强度和网页搜索。

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

在四个标签页中于 Meta Vibes 上创作图像和视频：**文本 → 图像**、**文本 → 视频**、**图像 → 图像**（角色 / 场景 / 风格图像）和 **图像 → 视频**（首 / 尾帧）。自动排队并下载。

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

通过 Grok Imagine 进行 文本 → 图像、图像 → 图像、文本 → 视频 和 图像 → 视频（在你已登录的 `grok.com` 标签页中运行，借助 Auth Helper 扩展）。图像提供 **8 种宽高比**（含 4:3、21:9、5:2）；视频以 **480p / 720p / 1080p** 渲染。图像 → 视频有两种模式：**首帧**（图像作为片段的开头）和 **参考图片**（最多 14 张引导图像）。

### 👤 角色

![角色](../screenshots/en/characters.webp)

打造一套可复用的角色阵容：一张参考图像、一个语音（Flow 的预设语音之一，可选填语气描述），以及外观/性格备注。在 Flow 图片、Flow 视频和 Google Vids 的提示词中用 `@name` 标记它们，生成时会保留该身份（语音仅由 Flow 视频使用；Google Vids 使用图像）。

### 🔗 Workflow

![Workflow](../screenshots/en/workflow.webp)

一块可视化节点画布。右键点击某个节点的接口，菜单只会提供合适的节点 -- 选中一个，它会自动连线。提供 Flow 图片、Flow 视频、Grok、Meta 和 GPT Image 2 的节点。将 提示词 → 图像 → 视频 → **提取帧** → 下一段视频 连成链，并用 **合并视频** 拼接两段片段（裁剪每一端，选择转场）。将整张图保存/加载为 `.json` 文件（格式：[`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)）；**Run Flow** 会端到端执行它。

### 🎞 视频工具

一个页面上的五个标签页：

**视频编辑** -- 用于视频、SRT 字幕和音频的时间轴：剪切、分割、重新排序、自动适配，然后导出一个成品视频。

![视频编辑](../screenshots/en/vt-video.webp)

**匹配字幕文件的图片幻灯片** -- 载入图像和一个 `.srt` 文件；每张图像自动匹配一行字幕，并带有动态效果、叠加层和字幕样式。

![匹配字幕文件的图片幻灯片](../screenshots/en/vt-slideshow.webp)

**将视频分割成多段** -- 按段数、固定或随机长度、时间戳列表或 A-B 区间列表分割；可处理单个文件或整批文件，条件允许时使用 GPU 加速。

![将视频分割成多段](../screenshots/en/vt-slicer.webp)

**从视频中提取帧** -- 按总数量、时间间隔、帧间隔或运动提取；可处理单个文件或整个文件夹。

![从视频中提取帧](../screenshots/en/vt-extractor.webp)

**去除视频水印** -- 去除 Google Vids 视频（720p 和 1080p，横屏或竖屏）上的 ✦ 徽标，并在应用内提供前后对比预览。没有徽标的视频会被跳过；原始文件会被保留，结果保存为 `<名称>_nologo.mp4`。

![去除视频水印](../screenshots/en/vt-logo.webp)

### 🔍 图片放大

![图片放大](../screenshots/en/upscaler.webp)

直接在你的电脑上放大并锐化图像 -- 添加单张图像或整个文件夹，选择 AI 模型（Real-ESRGAN、UltraSharp、Remacri……）和 2x-8x 倍数，查看每行的进度并对比前后效果。

### 🌐 Webhook API

![Webhook API](../screenshots/en/webhook.webp)

把应用变成一个本地自动化服务器（MAX 套餐），让 n8n、Make、Zapier、脚本或 AI 代理可以把任务推送到应用的队列中。启动它，复制你的 API key，向 `/api/image/generate`、`/api/video/generate`、`/api/grok/generate`、`/api/meta/generate`、`/api/openai/generate` 或 `/api/upscale/generate` POST 任务，然后轮询 `/api/status/<id>`。该页面列出每个模型及其支持的宽高比。完整架构：[`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md)。

---

## 文件存放位置

| 内容 | macOS | Windows |
|---|---|---|
| 输出（图像 / 视频） | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| 设置、会话、账户、角色 | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

每个页面在 `output` 内都有自己的子文件夹（每次运行一个更小的文件夹）；你可以在每个页面上更改保存文件夹。你的设置、提示词列表、会话、角色库和账户列表会被保存，并在下次打开应用时恢复。

---

## 故障排查

**一切都被锁定 / 购买界面不断弹出** -- 你的套餐已过期，或该账户在另一台设备上登录了。检查等级徽章（左下角）并续期。Google Vids 和 Google Pics 需要 PLUS/MAX 套餐；Webhook API 需要 MAX。

**Grok 生成没有反应** -- Grok 通过你的 `grok.com` 标签页运行。安装/启用 **Auth Helper** 浏览器扩展（设置 → Grok 账户），并确保你已登录 grok.com。

**Google Pics 提示没有账号** -- Pics 使用 Google Vids 的账号。在 设置 → **Google 账号** 中添加一个。

**某页面显示 "活跃中：0 个账号"** -- 在该页面的账户标签页（设置）中添加或重新启用一个账户，或者它的 token 已过期 -- 按 **全部刷新**。

**Windows 在 "Windows protected your PC" 处拦截** -- 点击 **More info → Run anyway**。该应用尚未使用 Microsoft 证书进行代码签名，因此会被标记 -- 它不是病毒。

**macOS 提示应用已损坏 / 无法打开** -- 它尚未经过 Apple 签名。首次请右键 → **Open**，或运行 `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`。

**更新没有安装成功** -- 从 [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) 手动下载最新版本。
