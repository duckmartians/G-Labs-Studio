<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>모든 주요 AI에서 이미지 &amp; 비디오를 일괄 생성하는 하나의 데스크톱 앱 — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Google Vids, Google Pics, ChatGPT GPT Image 2, Meta Vibes 및 Grok — 여기에 동영상 도구, 노드 워크플로, Webhook API까지.</b></p>

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

| 내 컴퓨터 | 다운로드 | Google Drive | 비고 |
|---|---|---|---|
| 🪟 **Windows 10/11 (64비트)** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | 모든 Windows PC용 |
| 🍎 **Apple 칩 Mac (M1/M2/M3/M4)** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | 2020년 말 이후 출시된 Mac |
| 🍎 **Intel 칩 Mac** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | 구형 Mac (2020년 이전) |

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

**G-Labs 계정이 필요합니다.** 앱을 열고 Google로 로그인한 뒤 요금제를 선택하세요. 요금제(**BASIC / PLUS / MAX**)에 따라 열리는 도구와 모델이 다르며, 앱 안에서 구매할 수 있습니다(은행 QR, PayPal 또는 USDT). 한 계정은 **한 번에 한 대**에서만 실행됩니다 — 다른 곳에서 로그인하면 이전 기기는 로그아웃됩니다. 사이드바 왼쪽 아래 배지가 현재 등급을 보여 줍니다. 여러 기기를 동시에 써야 하나요? **Team** 요금제를 구매할 수 있습니다(추가하는 기기 수에 따라 가격이 올라갑니다).

> **방금 구버전(G-Labs Automation)에서 옮겨 오셨나요?** 새 버전은 계정을 **가져오지 않습니다**. 새 G-Labs Studio에서 **모든 계정에 다시 로그인**해야 합니다(Google/Flow, ChatGPT, Meta…).

앱은 **스스로 업데이트**합니다: 실행 시 GitHub Releases를 확인하고 앱 안에서 새 버전을 내려받아 설치할 수 있습니다.

---

## 처음 실행

1. **앱을 열고 Google로 로그인하세요.** 등급 배지(왼쪽 아래: **BASIC / PLUS / MAX**)가 요금제를 확인해 줍니다.
2. **사용할 도구의 계정을 연결하세요** (**설정** → 해당 계정 탭):
   - **Flow 계정** → Flow 이미지 / Flow 동영상
   - **Google 계정** → **Google Vids** 및 **Google Pics** (두 페이지가 이 Google 계정을 함께 사용하며, 각 계정은 Vids 동영상용과 Pics 이미지용으로 따로 켭니다)
   - **ChatGPT 계정** → GPT Image 2
   - **Vibes 계정** → Meta Vibes
   - **Grok 계정** → 계정 저장소 없음: 이 탭에서 **Auth Helper** 브라우저 확장 설치를 안내하며, 이후 Grok은 Chrome에서 로그인된 `grok.com` 탭을 통해 실행됩니다

   각 계정 탭은 제목 표시줄에 **"활성: 계정 N개"** 를 표시하여 사용 가능한 계정 수를 알려줍니다.
3. **왼쪽 사이드바에서 페이지를 선택**하고 생성을 시작하세요. 모든 생성 페이지는 같은 흐름을 따릅니다: 왼쪽에 프롬프트를 입력하거나 가져오면 오른쪽 **표**에 들어가고, 그다음 **Run**을 누릅니다.

모든 페이지 헤더에는 실시간 **상태 표시줄** — *실행 중 · 대기 중 · 완료 · 실패 · 계정* — 이 있어 배치 전체를 한눈에 볼 수 있습니다. **대기 중**를 클릭하면 대기열 관리자가 열리고, **계정**를 클릭하면 계정 설정으로 이동합니다.

---

## 기능

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **모든 주요 생성기, 하나의 앱** — Google Flow (이미지 + 동영상), Google Vids, Google Pics, GPT Image 2, Meta Vibes 및 Grok. 각각 해당 제공자가 지원하는 모델과 비율과 함께 자체 페이지에 있습니다.
- **배치를 위해 설계** — 프롬프트 목록을 붙여넣거나(한 줄에 하나씩) `.txt`/Excel을 가져오면, 각 프롬프트가 하나의 행이 됩니다. 참조 이미지는 파일명으로 자동 매칭됩니다. 원하는 병렬 스레드 수로 전체 목록을 실행하세요.
- **먼저 추가, 준비되면 실행** — 행은 대기열로 들어가고, **Run / Pause / Stop**은 분리되어 있습니다. 지시하기 전에는 아무것도 시작되지 않으며, 대기열 관리자로 순서를 바꾸고 검토할 수 있습니다.
- **Gemini ✦ 로고 자동 제거** — Google Pics 이미지와 Google Vids 동영상은 다운로드 직후 정리됩니다(로고를 유지하려면 **Gemini 로고 표시** 를 켜세요). 로고가 없는 파일은 그대로 둡니다.
- **캐릭터 라이브러리** — 캐릭터를 한 번 저장하고(참조 이미지 + 음성 + 메모) Flow 이미지, Flow 동영상, Google Vids 프롬프트에서 `@name`으로 불러와 장면을 일관되게 유지하세요.
- **워크플로 (노드 그래프)** — 노드를 파이프라인으로 연결하세요: 프롬프트 → 이미지 → 동영상 → 마지막 프레임 추출 → 다음 동영상, 그리고 두 클립을 전환 효과로 이어 붙이는 **동영상 합치기** 노드가 있습니다.
- **동영상 도구** — 타임라인 동영상 편집, 자막에 맞춘 이미지 슬라이드쇼, 동영상 분할, 프레임 추출, 동영상 로고 제거를 앱 안에서 바로 할 수 있습니다.
- 내 컴퓨터에서 실행되는 **이미지 업스케일러** 와 자동화를 위한 **Webhook API**.
- **안정적** — 결과는 검증되고 자동 저장되며, 세션이 복원되고, 실패한 행은 재시도됩니다.
- **라이트 / 다크 테마**, 등급 인식 UI, **15개 언어**.

---

## 페이지

### 🖼 Flow 이미지 — Google Flow 이미지 생성

![Flow 이미지](../screenshots/en/flow-image.webp)

**Nano Banana Pro / 2 / 2 Lite** 로 이미지를 일괄 생성하세요. 모델, 종횡비, 해상도(**1K / 2K / 4K** — 2K/4K는 모델의 업스케일러 사용)를 선택하고, 한 번에 실행할 행 수와 그 사이의 지연을 설정하세요. 프롬프트를 붙여넣거나(또는 파일 가져오기), 행마다 참조 이미지를 첨부하고(폴더를 끌어다 놓으면 파일명으로 자동 매칭됨), `@name`으로 캐릭터를 불러오세요. **Veo / Gemini 로고 표시** 스위치(기본값 꺼짐)는 Flow 동영상 페이지와 공유됩니다. **Run**은 전체 목록을 대기열로 보냅니다.

### 🎬 Flow 동영상 — Veo &amp; Omni Flash

![Flow 동영상](../screenshots/en/flow-video.webp)

세 개의 탭: **텍스트 / 프레임 → 동영상** (텍스트 프롬프트, 또는 시작/끝 프레임), **이미지 / 동영상 재료 → 동영상** (참조 이미지 또는 참조 동영상), 그리고 **장면 체인 → 동영상**. 모델: **Veo 3.1 Fast / Lite / Quality** 및 **Omni Flash**. 종횡비, 업스케일(720p / 1080p / 4K), 시드를 선택하세요. 탭 바의 **?** 위에 마우스를 올리면 프레임과 재료의 차이를 쉬운 말로 설명해 줍니다.

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

Google 계정으로 세 개의 탭에서 동영상을 만드세요: **텍스트 → 동영상**, **이미지 → 동영상** (시작 이미지 한 장), **구성 요소 → 동영상** (구성 요소 이미지 최대 3장). 가로/세로, 720p / 1080p, 3–10초 길이를 선택하거나 — 프롬프트에 `[4s]` 같은 태그를 넣어 행마다 길이를 따로 지정하세요. 완성된 동영상은 표에서 바로 1080p로 업스케일할 수 있습니다. 각 계정에는 동영상 초 단위로 측정되는 할당량이 있으며, 계정을 더 추가하면 더 빠르게 실행됩니다. 다운로드한 동영상(720p / 1080p)의 Gemini ✦ 로고는 **Gemini 로고 표시** 를 켜지 않는 한 자동으로 제거됩니다.

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

두 개의 탭: **텍스트 → 이미지** 와 **이미지 → 이미지** (**최대 14장의 참조 이미지**: 캐릭터, 사물, 장면, 스타일). 실행할 때마다 Google은 3–9장의 이미지를 반환하며, **회당 보관할 이미지** 가 몇 장을 보관할지 결정합니다(1–4장 또는 전부). 21:9, 3:2, 5:4를 포함한 10가지 종횡비. 이미지 수와 관계없이 실행마다 Google Pics 실행 1회가 소모되며, 콘텐츠 정책에 의해 거부된 프롬프트는 소모되지 않습니다. Pics는 Google Vids와 **Google 계정** 을 공유합니다.

**Gemini ✦ 로고 자동 제거:** 다운로드한 Pics 이미지는 Google Pics 전용으로 측정한 로고 맵을 사용해 다운로드 직후 오른쪽 아래의 ✦ 표시가 제거됩니다 — 로고 합성을 역으로 되돌리므로, 그 아래의 원래 질감이 흐려지는 대신 복원됩니다. 로고가 감지되지 않은 이미지는 그대로 둡니다. 로고를 유지하려면 **Gemini 로고 표시** 를 켜세요.

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

ChatGPT 계정을 사용하여 OpenAI **GPT Image 2** 로 생성하며, 최대 5개의 참조 이미지를 쓸 수 있습니다. 비율(21:9, 4:5 및 **custom** — 프롬프트에 비율을 직접 쓰는 방식 — 을 포함한 10가지 옵션), 품질, 프롬프트 모드, 추론 수준, 웹 검색을 선택하세요.

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

네 개의 탭에서 Meta Vibes로 이미지와 동영상을 만드세요: **텍스트 → 이미지**, **텍스트 → 동영상**, **이미지 → 이미지** (캐릭터 / 장면 / 스타일 이미지), **이미지 → 동영상** (시작 / 끝 프레임). 자동으로 대기열에 넣고 다운로드합니다.

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

Grok Imagine을 통한 텍스트 → 이미지, 이미지 → 이미지, 텍스트 → 동영상 및 이미지 → 동영상 (Auth Helper 확장을 통해 로그인된 `grok.com` 탭). 이미지는 **8가지 종횡비**(4:3, 21:9, 5:2 포함)를 제공하며, 동영상은 **480p / 720p / 1080p** 로 렌더링됩니다. 이미지 → 동영상에는 두 가지 모드가 있습니다: **첫 프레임** (이미지가 클립을 시작함)과 **참조 이미지** (최대 14장의 가이드 이미지).

### 👤 캐릭터

![캐릭터](../screenshots/en/characters.webp)

재사용 가능한 출연진을 만드세요: 참조 이미지, 음성(Flow의 프리셋 음성 중 하나, 선택적으로 말투 설명 추가), 외모/성격 메모. Flow 이미지, Flow 동영상, Google Vids 프롬프트에서 `@name`으로 태그하면 생성이 그 정체성을 유지합니다(음성은 Flow 동영상에서만 사용되며, Google Vids는 이미지를 사용합니다).

### 🔗 워크플로

![워크플로](../screenshots/en/workflow.webp)

시각적 노드 캔버스. 노드의 소켓을 마우스 오른쪽 클릭하면 메뉴가 적합한 노드만 제공합니다 — 하나를 고르면 자동으로 연결됩니다. Flow 이미지, Flow 동영상, Grok, Meta, GPT Image 2용 노드가 있습니다. 프롬프트 → 이미지 → 동영상 → **프레임 추출** → 다음 동영상을 체인으로 연결하고, **동영상 합치기** 로 두 클립을 이어 붙이세요(각 끝을 트림하고 전환을 선택). 전체 그래프를 `.json` 파일로 저장/불러오기(형식: [`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)); **Run Flow** 는 처음부터 끝까지 실행합니다.

### 🎞 동영상 도구

한 페이지에 다섯 개의 탭:

**영상 편집** — 동영상, SRT 자막, 오디오를 위한 타임라인: 자르기, 분할, 순서 변경, 자동 맞춤 후 완성된 동영상 하나로 내보내기.

![영상 편집](../screenshots/en/vt-video.webp)

**자막 파일에 맞춘 이미지 슬라이드쇼** — 이미지와 `.srt` 파일을 불러오면 각 이미지가 자막 한 줄에 자동으로 맞춰지며, 모션 효과, 오버레이, 자막 스타일을 적용할 수 있습니다.

![자막 파일에 맞춘 이미지 슬라이드쇼](../screenshots/en/vt-slideshow.webp)

**영상을 구간으로 분할** — 구간 수, 고정 또는 무작위 길이, 타임스탬프 목록 또는 A–B 범위 목록으로 분할; 파일 하나 또는 일괄 처리, 가능하면 GPU 가속.

![영상을 구간으로 분할](../screenshots/en/vt-slicer.webp)

**영상에서 프레임 추출** — 총 개수, 시간 간격, 프레임 간격 또는 움직임 기준; 파일 하나 또는 폴더 전체.

![영상에서 프레임 추출](../screenshots/en/vt-extractor.webp)

**동영상 로고 제거** — 720p 및 1080p(가로 또는 세로) Google Vids 동영상에서 ✦ 로고를 제거하며, 앱 안에서 전/후 미리보기를 제공합니다. 로고가 없는 동영상은 건너뛰고, 원본은 보존되며 결과는 `<이름>_nologo.mp4` 로 저장됩니다.

![동영상 로고 제거](../screenshots/en/vt-logo.webp)

### 🔍 이미지 업스케일러

![이미지 업스케일러](../screenshots/en/upscaler.webp)

내 컴퓨터에서 바로 이미지를 확대하고 선명하게 만드세요 — 이미지 한 장이나 폴더 전체를 추가하고, AI 모델(Real-ESRGAN, UltraSharp, Remacri…)과 2x–8x 배율을 선택한 뒤, 행별 진행 상황을 확인하고 전/후를 비교하세요.

### 🌐 Webhook API

![Webhook API](../screenshots/en/webhook.webp)

앱을 로컬 자동화 서버(MAX 요금제)로 바꿔 n8n, Make, Zapier, 스크립트 또는 AI 에이전트가 앱의 대기열로 작업을 보낼 수 있게 하세요. 서버를 시작하고 API 키를 복사한 뒤, `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate`, `/api/openai/generate` 또는 `/api/upscale/generate` 로 작업을 POST하고, `/api/status/<id>` 를 폴링하세요. 이 페이지는 모든 모델과 지원되는 종횡비를 나열합니다. 전체 스키마: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## 파일 위치

| 항목 | macOS | Windows |
|---|---|---|
| 출력 (이미지 / 동영상) | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| 설정, 세션, 계정, 캐릭터 | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

각 페이지는 `output` 안에 자체 하위 폴더를 가지며(실행마다 더 작은 폴더 하나), 페이지마다 저장 폴더를 변경할 수 있습니다. 설정, 프롬프트 목록, 세션, 캐릭터 라이브러리 및 계정 목록은 저장되어 다음에 앱을 열 때 복원됩니다.

---

## 문제 해결

**모든 것이 잠겨 있음 / 구매 화면이 계속 열림** — 요금제가 만료되었거나 계정이 다른 기기에서 로그인되었습니다. 등급 배지(왼쪽 아래)를 확인하고 갱신하세요. Google Vids와 Google Pics는 PLUS/MAX 요금제가, Webhook API는 MAX가 필요합니다.

**Grok 생성이 아무것도 하지 않음** — Grok은 `grok.com` 탭을 통해 실행됩니다. **Auth Helper** 브라우저 확장을 설치/활성화하고(설정 → Grok 계정) grok.com에 로그인되어 있는지 확인하세요.

**Google Pics에 계정이 없다고 표시됨** — Pics는 Google Vids 계정을 사용합니다. 설정 → **Google 계정** 에서 하나를 추가하세요.

**페이지에 "활성: 계정 0개"** — 해당 페이지의 계정 탭(설정)에서 계정을 추가하거나 다시 활성화하세요. 또는 토큰이 만료되었을 수 있으니 **모두 새로고침** 을 누르세요.

**Windows가 "Windows protected your PC" 에서 차단함** — **More info → Run anyway** 를 클릭하세요. 앱이 아직 Microsoft 인증서로 코드 서명되지 않아 표시되는 것이며 — 바이러스가 아닙니다.

**macOS가 앱이 손상되었다 / 열 수 없다고 함** — 아직 Apple 서명이 없어서입니다. 처음에는 마우스 오른쪽 클릭 → **Open** 으로 열거나, `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` 를 실행하세요.

**업데이트가 설치되지 않음** — [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) 에서 최신 빌드를 수동으로 다운로드하세요.
