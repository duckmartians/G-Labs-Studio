<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Одно настольное приложение для пакетной генерации изображений и видео во всех крупных ИИ — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI и ChatGPT GPT Image 2.</b></p>

<p align="center">
  <a href="README.en.md">English</a> ·
  <a href="../../README.md">Tiếng Việt</a> ·
  <a href="README.zh.md">简体中文</a> ·
  <a href="README.es.md">Español</a> ·
  <a href="README.pt.md">Português</a> ·
  <b>Русский</b> ·
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
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Скачать — Windows" src="https://img.shields.io/badge/%D0%A1%D0%BA%D0%B0%D1%87%D0%B0%D1%82%D1%8C-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Скачать — macOS (Apple Silicon)" src="https://img.shields.io/badge/%D0%A1%D0%BA%D0%B0%D1%87%D0%B0%D1%82%D1%8C-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Скачать — macOS (Intel)" src="https://img.shields.io/badge/%D0%A1%D0%BA%D0%B0%D1%87%D0%B0%D1%82%D1%8C-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Установка

### Шаг 1 — Выберите правильную сборку для вашего компьютера

Скачайте последнюю версию из **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** и выберите файл, подходящий вашему компьютеру:

| Ваш компьютер | Скачать | Google Drive | Примечания |
|---|---|---|---|
| 🪟 **Windows 10/11 (64-бит)** | [`G-Labs-Studio-win.exe`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | Для любого ПК с Windows |
| 🍎 **Mac с чипом Apple (M1/M2/M3/M4)** | [`G-Labs-Studio-mac-arm64.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Mac примерно с конца 2020 года |
| 🍎 **Mac с чипом Intel** | [`G-Labs-Studio-mac-intel.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Более старые Mac (до 2020 года) |

**Не знаете, какой чип у вашего Mac?** Нажмите меню  (вверху слева) → **About This Mac**:
- Строка **Chip** со значением «Apple M1 / M2 / M3…» → скачивайте сборку **arm64**.
- Строка **Processor** со значением «Intel…» → скачивайте сборку **intel**.

> Сборка **Intel** всё равно запустится на Mac с чипом Apple (только медленнее), но сборка **arm64** **не откроется** на Intel Mac — поэтому выбирайте правильную.

### Шаг 2 — Установка

<details open>
<summary><b>🪟 На Windows</b></summary>

1. Откройте скачанный **`G-Labs-Studio-win.exe`**.
2. Если появится **«Windows protected your PC»** (SmartScreen): нажмите **More info** → **Run anyway**. *(Приложение пока не подписано сертификатом Microsoft, поэтому появляется предупреждение — это не вирус.)*
3. Нажмите **Yes** в запросе администратора (UAC) и пройдите установщик до конца.
4. Запустите его из **Start Menu** или ярлыком на **Desktop**.

</details>

<details open>
<summary><b>🍎 На macOS</b></summary>

1. Откройте скачанный **`.dmg`** и **перетащите G-Labs Studio в папку Applications**.
2. Откройте **Applications**, **щёлкните правой кнопкой** (или Control-клик) по **G-Labs Studio** → **Open** → ещё раз нажмите **Open** в диалоге. *(Приложение не подписано Apple, поэтому в **первый раз** его нужно открыть так; далее оно открывается обычно.)*
3. Если macOS пишет, что приложение **«повреждено / не может быть открыто»**, или нет кнопки Open, откройте **Terminal** и вставьте:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   Затем откройте приложение снова.

</details>

### Шаг 3 — Войдите и выберите план

**Вам нужен аккаунт G-Labs.** Откройте приложение, войдите через Google и выберите план. Планы (**FREE / PLUS / MAX**) открывают разные инструменты и модели; купить можно прямо в приложении (банковский QR, PayPal или USDT). Один аккаунт работает **на одной машине одновременно** — вход в другом месте выходит из предыдущей машины. Значок в левом нижнем углу боковой панели показывает ваш текущий уровень. Нужно несколько устройств одновременно? Можно купить план **Team** (цена растёт с числом добавленных устройств).

> **Только что перешли со старой версии (G-Labs Automation)?** Новая версия **не** переносит ваши аккаунты. Нужно **заново войти во все аккаунты** (Google/Flow, ChatGPT, Meta…) в новой G-Labs Studio.

Приложение **обновляется само**: при запуске проверяет GitHub Releases и может скачать и установить новую версию прямо из приложения.

---

## Первый запуск

1. **Откройте приложение и войдите через Google.** Значок уровня (внизу слева) подтверждает ваш план.
2. **Подключите учётные записи для инструментов, которыми будете пользоваться** (Настройки → соответствующая вкладка учётной записи):
   - Учётные записи **Google** → Flow Image / Flow Video
   - Учётные записи **ChatGPT** → GPT Image 2
   - Учётные записи **Meta** → Meta Media
   - **Grok** → работает через вашу авторизованную вкладку `grok.com` с помощью браузерного расширения-компаньона (Auth Helper) — без пула учётных записей
   Каждая вкладка учётной записи показывает **«Active: N accounts»** в заголовке, чтобы вы знали, сколько из них пригодны к использованию.
3. **Выберите страницу на левой боковой панели** и начните генерацию. У каждой страницы генерации один и тот же ритм: слева вводите или импортируете промпты, они попадают в **таблицу** справа, затем нажимаете **Run**.

В заголовке каждой страницы есть живая **строка состояния** — *Running · Queued · Done · Failed · Accounts* — чтобы вы могли увидеть пакет одним взглядом. Нажмите **Queued**, чтобы открыть менеджер очереди, **Accounts** — чтобы перейти к настройкам учётных записей.

---

## Возможности

![G-Labs Studio](../screenshots/01-image.png)

- **Все крупные генераторы в одном приложении** — Google Flow (изображения + видео), Grok Imagine, Meta AI (vibes.ai) и OpenAI GPT Image 2, каждый на своей странице с моделями и соотношениями сторон, которые поддерживает провайдер.
- **Пакетная работа по замыслу** — вставьте список промптов (по одному на строку) или импортируйте файл `.txt`/Excel; каждый становится строкой. Референсные изображения автоматически сопоставляются по имени файла. Запускайте весь список с выбранной вами параллельностью.
- **Сначала добавьте, запустите когда готовы** — строки уходят в очередь; **Run / Pause / Stop** разделены. Ничего не запускается, пока вы не скажете, а менеджер очереди позволяет переупорядочивать и просматривать.
- **Библиотека персонажей** — сохраните персонажа один раз (референсное изображение + собственный голос + заметки) и добавляйте его в любой промпт через `@name`; видео сохраняет внешность и голос этого персонажа.
- **Workflow (граф узлов)** — соедините узлы в конвейер: промпт → изображение → видео → извлечь последний кадр → следующее видео, плюс узел **Merge Video**, который объединяет два клипа с обрезкой и переходами (crossfade, wipe, slide, dissolve…). Пакетные узлы прогоняют всю цепочку для каждого промпта или каждого изображения.
- **Webhook API** — локальный REST-сервер, чтобы скрипты и ИИ-агенты могли отправлять задачи image/video/Grok/Meta/OpenAI и опрашивать результаты.
- **Image Upscaler** и **Video Editor** (нарезка, склейка, слайд-шоу) для финальной обработки.
- **Устойчивость** — результаты проверяются и автоматически сохраняются; сеансы восстанавливаются; неудавшиеся строки повторяются.
- **Тёмная / светлая тема**, интерфейс с учётом уровня и **15 языков**.

---

## Страницы

### 🖼 Flow Image — генерация изображений Google Flow

![Flow Image](../screenshots/01-image.png)

Пакетная генерация изображений с **Nano Banana Pro / 2 / Lite**. Выберите модель, соотношение сторон и разрешение (**1K / 2K / 4K** — 2K/4K используют апскейлер модели), задайте, сколько строк выполняется одновременно, и задержку между ними. Вставьте промпты (или импортируйте файл), прикрепите референсные изображения к строкам (перетащите папку — они автоматически сопоставятся по имени файла) и используйте `@name`, чтобы подтянуть персонажей. **Run** отправляет весь список в очередь.

### 🎬 Flow Video — Veo и Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Три вкладки: **Text / Frames → Video** (текстовый промпт или начальный/конечный кадр), **Image / Video ingredients → Video** (референсные изображения или референсное видео) и **Scene stitch → Video**. Модели: **Veo 3.1 Fast / Lite / Quality** и **Omni Flash**. Выберите соотношение сторон, апскейл (720p / 1080p / 4K) и seed. Наведите курсор на **?** на панели вкладок для понятного объяснения различия кадров и ингредиентов.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Текст-в-изображение, изображение-в-изображение, текст-в-видео и изображение-в-видео через Grok Imagine (ваша авторизованная вкладка `grok.com` через расширение Auth Helper). Для изображений доступно **8 соотношений сторон** (в т. ч. 4:3, 21:9, 5:2); видео генерируется в **480p / 720p / 1080p**. Изображение-в-видео имеет два режима: **First frame** (изображение открывает клип) и **Reference** (до 14 направляющих изображений).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Генерация изображений и видео через Meta AI. Режимы: текст-в-изображение, изображение-в-изображение (компоненты Character / Scene / Style), текст-в-видео и изображение-в-видео (начальный / конечный кадр).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

Генерируйте с OpenAI **GPT Image 2**, используя ваши учётные записи ChatGPT, с до 5 референсными изображениями. Выберите соотношение сторон (10 вариантов, включая 21:9, 4:5 и **custom** — где вы пишете соотношение прямо в промпте), качество, режим промпта, усилие рассуждения и веб-поиск.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Апскейл папки с изображениями локально — выберите цель и дайте обработать очередь, с прогрессом и статусом по каждой строке (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

Соберите библиотеку многоразовых персонажей: референсное изображение, необязательный пользовательский голос и заметки о внешности/характере. Отметьте их через `@name` в любом промпте Flow, и генерация сохранит эту идентичность.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Визуальный холст узлов. Кликните правой кнопкой по сокету узла — меню предложит только подходящие узлы; выберите один, и он соединится автоматически. Соедините промпт → генерация → видео → **Extract Frame** → следующее видео и используйте **Merge Video**, чтобы объединить два клипа (обрежьте каждый конец, выберите переход). Сохраняйте/загружайте весь граф как файл `.json`; **Run Flow** выполняет его от начала до конца.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Превратите приложение в локальный сервер автоматизации. Запустите его, скопируйте свой API-ключ и отправляйте задачи POST на `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` или `/api/openai/generate`, затем опрашивайте `/api/status/<id>`. На странице перечислены все модели и поддерживаемые ими соотношения сторон. Полная схема: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Где что хранится

| Что | macOS | Windows |
|---|---|---|
| Вывод (изображения / видео) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Настройки, сеансы, учётные записи | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Ваши настройки, списки промптов, сеансы, библиотека персонажей и список учётных записей сохраняются и восстанавливаются при следующем открытии приложения.

---

## Устранение неполадок

**Всё заблокировано / постоянно открывается экран покупки** — ваш план истёк, или учётная запись вошла на другой машине. Проверьте значок уровня (внизу слева) и продлите.

**Генерация Grok ничего не делает** — Grok работает через вашу вкладку `grok.com`. Установите/включите браузерное расширение **Auth Helper** (Настройки → Grok) и убедитесь, что вы вошли на grok.com.

**«Active: 0 accounts» на странице** — добавьте или снова включите учётную запись во вкладке учётных записей этой страницы (Настройки), либо истёк её токен — нажмите **Refresh all**.

**macOS сообщает, что приложение повреждено / не может быть открыто** — оно не подписано Apple. Откройте через правый клик → **Open** в первый раз или выполните `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Обновление не устанавливается** — скачайте последнюю сборку вручную из раздела [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
