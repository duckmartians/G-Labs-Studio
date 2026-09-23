<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>모든 주요 AI에서 이미지 &amp; 비디오를 일괄 생성하는 하나의 데스크톱 앱 — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI 및 ChatGPT GPT Image 2.</b></p>

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
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <b>한국어</b>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="다운로드 — Windows" src="https://img.shields.io/badge/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="다운로드 — macOS (Apple Silicon)" src="https://img.shields.io/badge/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="다운로드 — macOS (Intel)" src="https://img.shields.io/badge/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## 설치

### 1단계 — 내 컴퓨터에 맞는 버전 선택

**[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** 에서 최신 버전을 내려받은 뒤, 내 컴퓨터에 맞는 파일을 선택하세요:

| 내 컴퓨터 | 다운로드 | 비고 |
|---|---|---|
| 🪟 **Windows 10/11 (64비트)** | [`G-Labs-Studio-win.exe`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | 모든 Windows PC용 |
| 🍎 **Apple 칩 Mac (M1/M2/M3/M4)** | [`G-Labs-Studio-mac-arm64.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | 2020년 말 이후 출시된 Mac |
| 🍎 **Intel 칩 Mac** | [`G-Labs-Studio-mac-intel.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | 구형 Mac (2020년 이전) |

**Mac 칩이 무엇인지 잘 모르겠나요?** 왼쪽 위  메뉴 → **About This Mac** 클릭:
- **Chip** 줄에 “Apple M1 / M2 / M3…” 표시 → **arm64** 버전 다운로드.
- **Processor** 줄에 “Intel…” 표시 → **intel** 버전 다운로드.

> **Intel** 버전은 Apple 칩 Mac에서도 실행됩니다(다만 느림). 하지만 **arm64** 버전은 Intel Mac에서 **열리지 않으므로** 올바른 것을 선택하세요.

### 2단계 — 설치

<details open>
<summary><b>🪟 Windows에서</b></summary>

1. 내려받은 **`G-Labs-Studio-win.exe`** 를 엽니다.
2. **“Windows protected your PC”**(SmartScreen)가 뜨면: **More info** → **Run anyway** 를 클릭하세요. *(아직 Microsoft 인증서로 서명되지 않아 경고가 뜨는 것이며 바이러스가 아닙니다.)*
3. 관리자(UAC) 창에서 **Yes** 를 클릭한 뒤 설치를 끝까지 진행합니다.
4. **Start Menu** 또는 **Desktop** 바로가기에서 실행합니다.

</details>

<details open>
<summary><b>🍎 macOS에서</b></summary>

1. 내려받은 **`.dmg`** 를 열고 **G-Labs Studio 를 Applications 폴더로 드래그**합니다.
2. **Applications** 에서 **G-Labs Studio** 를 **우클릭**(또는 Control-클릭) → **Open** → 대화상자에서 다시 **Open** 클릭. *(Apple 서명이 없어 **처음 한 번**은 이렇게 열어야 하며, 이후에는 정상적으로 열립니다.)*
3. macOS가 앱이 **“손상됨 / 열 수 없음”**이라고 하거나 Open 버튼이 없으면, **Terminal** 을 열고 붙여넣으세요:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   그런 다음 앱을 다시 엽니다.

</details>

### 3단계 — 로그인하고 요금제 선택

**G-Labs 계정이 필요합니다.** 앱을 열고 Google로 로그인한 뒤 요금제를 선택하세요. 요금제(**FREE / PLUS / MAX**)에 따라 열리는 도구와 모델이 다르며, 앱 안에서 구매할 수 있습니다(은행 QR, PayPal 또는 USDT). 한 계정은 **한 번에 한 대**에서만 실행됩니다 — 다른 곳에서 로그인하면 이전 기기는 로그아웃됩니다. 사이드바 왼쪽 아래 배지가 현재 등급을 보여 줍니다. 여러 기기를 동시에 써야 하나요? **Team** 요금제를 구매할 수 있습니다(추가하는 기기 수에 따라 가격이 올라갑니다).

> **방금 구버전(G-Labs Automation)에서 옮겨 오셨나요?** 새 버전은 계정을 **가져오지 않습니다**. 새 G-Labs Studio에서 **모든 계정에 다시 로그인**해야 합니다(Google/Flow, ChatGPT, Meta…).

앱은 **스스로 업데이트**합니다: 실행 시 GitHub Releases를 확인하고 앱 안에서 새 버전을 내려받아 설치할 수 있습니다.

---

## 처음 실행

1. **앱을 열고 Google로 로그인하세요.** 등급 배지(왼쪽 아래)가 요금제를 확인해 줍니다.
2. **사용할 도구의 계정을 연결하세요** (Settings → 해당 계정 탭):
   - **Google** 계정 → Flow Image / Flow Video
   - **ChatGPT** 계정 → GPT Image 2
   - **Meta** 계정 → Meta Media
   - **Grok** → 컴패니언 브라우저 확장(Auth Helper)을 통해 로그인된 `grok.com` 탭으로 실행됩니다 — 계정 풀 없음
   각 계정 탭은 제목 표시줄에 **"Active: N accounts"** 를 표시하여 사용 가능한 계정 수를 알려줍니다.
3. **왼쪽 사이드바에서 페이지를 선택**하고 생성을 시작하세요. 모든 생성 페이지는 같은 흐름을 공유합니다: 왼쪽에 프롬프트를 입력하거나 가져오면 오른쪽 **표**에 들어가고, 그다음 **Run**을 누릅니다.

모든 페이지 헤더에는 실시간 **상태 표시줄** — *Running · Queued · Done · Failed · Accounts* — 이 있어 배치를 한눈에 볼 수 있습니다. **Queued**를 클릭하면 대기열 관리자가 열리고, **Accounts**를 클릭하면 계정 설정으로 이동합니다.

---

## 기능

![G-Labs Studio](../screenshots/01-image.png)

- **모든 주요 생성기, 하나의 앱** — Google Flow (이미지 + 비디오), Grok Imagine, Meta AI (vibes.ai) 및 OpenAI GPT Image 2. 각각 해당 제공자가 지원하는 모델과 비율과 함께 자체 페이지에 있습니다.
- **처음부터 배치 설계** — 프롬프트 목록을 붙여넣거나(한 줄에 하나씩) `.txt`/Excel 파일을 가져오면, 각각이 하나의 행이 됩니다. 참조 이미지는 파일명으로 자동 매칭됩니다. 원하는 동시 실행 수로 전체 목록을 실행하세요.
- **먼저 추가, 준비되면 실행** — 행은 대기열로 들어가고, **Run / Pause / Stop**은 분리되어 있습니다. 지시하기 전에는 아무것도 시작되지 않으며, 대기열 관리자로 순서를 바꾸고 검토할 수 있습니다.
- **캐릭터 라이브러리** — 캐릭터를 한 번 저장하면(참조 이미지 + 자체 음성 + 메모) `@name`으로 어느 프롬프트에나 넣을 수 있습니다. 비디오는 해당 캐릭터의 외모와 음성을 유지합니다.
- **Workflow (노드 그래프)** — 노드를 파이프라인으로 연결하세요: 프롬프트 → 이미지 → 비디오 → 마지막 프레임 추출 → 다음 비디오, 그리고 두 클립을 트림과 전환(crossfade, wipe, slide, dissolve…)으로 이어 붙이는 **Merge Video** 노드가 있습니다. 배치 노드는 프롬프트별 또는 이미지별로 전체 체인을 반복합니다.
- **Webhook API** — 로컬 REST 서버로 스크립트와 AI 에이전트가 이미지/비디오/Grok/Meta/OpenAI 작업을 제출하고 결과를 폴링할 수 있습니다.
- 마무리를 위한 **Image Upscaler** 와 **Video Editor** (자르기, 이어붙이기, 슬라이드쇼).
- **안정적** — 결과는 검증되고 자동 저장되며, 세션이 복원되고, 실패한 행은 재시도됩니다.
- **다크 / 라이트 테마**, 등급 인식 UI, **15개 언어**.

---

## 페이지

### 🖼 Flow Image — Google Flow 이미지 생성

![Flow Image](../screenshots/01-image.png)

**Nano Banana Pro / 2 / Lite** 로 이미지를 일괄 생성하세요. 모델, 종횡비, 해상도(**1K / 2K / 4K** — 2K/4K는 모델의 업스케일러 사용)를 선택하고, 한 번에 실행할 행 수와 그 사이의 지연을 설정하세요. 프롬프트를 붙여넣거나(또는 파일 가져오기), 행마다 참조 이미지를 첨부하고(폴더를 끌어다 놓으면 파일명으로 자동 매칭됨), `@name`으로 캐릭터를 불러오세요. **Run**은 전체 목록을 대기열로 보냅니다.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

세 개의 탭: **Text / Frames → Video** (텍스트 프롬프트, 또는 시작/끝 프레임), **Image / Video ingredients → Video** (참조 이미지 또는 참조 비디오), 그리고 **Scene stitch → Video**. 모델: **Veo 3.1 Fast / Lite / Quality** 및 **Omni Flash**. 종횡비, 업스케일(720p / 1080p / 4K), 시드를 선택하세요. 탭 바의 **?** 위에 마우스를 올리면 frames와 ingredients의 차이를 쉬운 말로 설명해 줍니다.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Grok Imagine을 통한 text-to-image, image-to-image, text-to-video 및 image-to-video (Auth Helper 확장을 통해 로그인된 `grok.com` 탭). 이미지는 **8가지 종횡비**(4:3, 21:9, 5:2 포함)를 제공하며, 비디오는 **480p / 720p / 1080p** 로 생성됩니다. Image-to-video에는 두 가지 모드가 있습니다: **First frame** (이미지가 클립을 시작함)과 **Reference** (최대 14개의 가이드 이미지).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Meta AI를 통한 이미지 및 비디오 생성. 모드: text-to-image, image-to-image (Character / Scene / Style 구성 요소), text-to-video 및 image-to-video (시작 / 끝 프레임).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

ChatGPT 계정을 사용하여 OpenAI **GPT Image 2** 로 생성하며, 최대 5개의 참조 이미지를 쓸 수 있습니다. 비율(21:9, 4:5 및 **custom** — 프롬프트에 비율을 직접 쓰는 방식 — 을 포함한 10가지 옵션), 품질, 프롬프트 모드, reasoning effort, 웹 검색을 선택하세요.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

이미지 폴더를 로컬에서 업스케일하세요 — 목표를 선택하면 대기열을 처리하며, 행별 진행 상황과 상태(processing / done / error)를 보여줍니다.

### 👤 Characters

![Characters](../screenshots/07-character.png)

재사용 가능한 캐릭터 라이브러리를 구축하세요: 참조 이미지, 선택적 커스텀 음성, 외모/성격 메모. 어느 Flow 프롬프트에서든 `@name`으로 태그하면 생성이 그 정체성을 유지합니다.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

시각적 노드 캔버스. 노드의 소켓을 마우스 오른쪽 클릭하면 메뉴가 적합한 노드만 제공합니다 — 하나를 고르면 자동으로 연결됩니다. 프롬프트 → 생성 → 비디오 → **Extract Frame** → 다음 비디오를 체인으로 연결하고, **Merge Video** 로 두 클립을 이어 붙이세요(각 끝을 트림하고 전환을 선택). 전체 그래프를 `.json` 파일로 저장/불러오기; **Run Flow** 는 처음부터 끝까지 실행합니다.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

앱을 로컬 자동화 서버로 바꾸세요. 서버를 시작하고 API 키를 복사한 뒤, `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` 또는 `/api/openai/generate` 로 작업을 POST하고, `/api/status/<id>` 를 폴링하세요. 이 페이지는 모든 모델과 지원되는 종횡비를 나열합니다. 전체 스키마: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## 파일 위치

| 항목 | macOS | Windows |
|---|---|---|
| 출력 (이미지 / 비디오) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| 설정, 세션, 계정 | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

설정, 프롬프트 목록, 세션, 캐릭터 라이브러리 및 계정 목록은 저장되어 다음에 앱을 열 때 복원됩니다.

---

## 문제 해결

**모든 것이 잠겨 있음 / 구매 화면이 계속 열림** — 요금제가 만료되었거나 계정이 다른 기기에서 로그인되었습니다. 등급 배지(왼쪽 아래)를 확인하고 갱신하세요.

**Grok 생성이 아무것도 하지 않음** — Grok은 `grok.com` 탭을 통해 실행됩니다. **Auth Helper** 브라우저 확장을 설치/활성화하고(Settings → Grok) grok.com에 로그인되어 있는지 확인하세요.

**페이지에 "Active: 0 accounts"** — 해당 페이지의 계정 탭(Settings)에서 계정을 추가하거나 다시 활성화하세요. 또는 토큰이 만료되었을 수 있으니 **Refresh all** 을 누르세요.

**macOS가 앱이 손상되었다 / 열 수 없다고 함** — Apple 서명이 없어서입니다. 처음에는 마우스 오른쪽 클릭 → **열기**로 열거나, `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` 를 실행하세요.

**업데이트가 설치되지 않음** — [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) 에서 최신 빌드를 수동으로 다운로드하세요.
