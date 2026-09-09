<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Una sola app de escritorio para generar por lotes imágenes y videos en todas las grandes IA — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI y ChatGPT GPT Image 2.</b></p>

<p align="center">
  <a href="../../README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.zh.md">简体中文</a> ·
  <b>Español</b> ·
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

![G-Labs Studio](../screenshots/01-image.png)

---

## Instalación

Descarga la última versión desde **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**:

| Plataforma | Archivo |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-win.exe` — ejecuta el instalador (admin/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-mac-intel.dmg` |

**Primer inicio en macOS** — la app no está firmada por Apple, así que macOS la pone en cuarentena. Ábrela la primera vez con **clic derecho → Open**, o elimina la marca desde la Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**Necesitas una cuenta de G-Labs.** Abre la app, inicia sesión con Google y elige un plan. Los planes (**FREE / PLUS / MAX**) desbloquean distintas herramientas y modelos; puedes comprar uno desde dentro de la app (QR bancario, PayPal o USDT). Una cuenta funciona en **una sola máquina a la vez** — iniciar sesión en otro lugar cierra la sesión de la máquina anterior. La insignia en la esquina inferior izquierda de la barra lateral muestra tu nivel actual.

La app **se actualiza sola**: comprueba GitHub Releases al iniciarse y puede descargar e instalar la nueva versión desde dentro de la app.

---

## Primer uso

1. **Abre la app e inicia sesión con Google.** La insignia de nivel (abajo a la izquierda) confirma tu plan.
2. **Conecta las cuentas de las herramientas que vayas a usar** (Settings → la pestaña de cuenta correspondiente):
   - Cuentas de **Google** → Flow Image / Flow Video
   - Cuentas de **ChatGPT** → GPT Image 2
   - Cuentas de **Meta** → Meta Media
   - **Grok** → funciona a través de tu pestaña de `grok.com` con sesión iniciada mediante la extensión de navegador complementaria (Auth Helper) — sin grupo de cuentas
   Cada pestaña de cuenta muestra **"Active: N accounts"** en su barra de título para que sepas cuántas están disponibles.
3. **Elige una página en la barra lateral izquierda** y empieza a generar. Todas las páginas de generación comparten el mismo ritmo: escribe o importa prompts a la izquierda, aparecen en una **tabla** a la derecha, y luego pulsa **Run**.

Cada encabezado de página lleva una **barra de estado** en vivo — *Running · Queued · Done · Failed · Accounts* — para ver el lote de un vistazo. Haz clic en **Queued** para abrir el gestor de cola, y en **Accounts** para ir a la configuración de cuentas.

---

## Características

- **Todos los grandes generadores, una app** — Google Flow (imagen + video), Grok Imagine, Meta AI (vibes.ai) y OpenAI GPT Image 2, cada uno en su propia página con los modelos y proporciones que ese proveedor admite.
- **Diseñado para lotes** — pega una lista de prompts (uno por línea) o importa un archivo `.txt`/Excel; cada uno se convierte en una fila. Las imágenes de referencia se emparejan automáticamente por nombre de archivo. Ejecuta toda la lista con la concurrencia que elijas.
- **Añade primero, ejecuta cuando estés listo** — las filas van a una cola; **Run / Pause / Stop** son independientes. Nada arranca hasta que tú lo digas, y un gestor de cola te permite reordenar e inspeccionar.
- **Biblioteca de personajes** — guarda un personaje una vez (imagen de referencia + su propia voz + notas) y colócalo en cualquier prompt con `@name`; el video mantiene el aspecto y la voz de ese personaje.
- **Workflow (grafo de nodos)** — conecta nodos en una tubería: prompt → imagen → video → extraer último fotograma → siguiente video, además de un nodo **Merge Video** que une dos clips con recortes y transiciones (crossfade, wipe, slide, dissolve…). Los nodos de lote repiten toda la cadena por cada prompt o por cada imagen.
- **Webhook API** — un servidor REST local para que scripts y agentes de IA envíen trabajos de image/video/Grok/Meta/OpenAI y consulten los resultados.
- **Image Upscaler** y un **Video Editor** (cortar, unir, presentación de diapositivas) para dar los últimos toques.
- **Resiliente** — los resultados se verifican y guardan automáticamente; las sesiones se restauran; las filas fallidas se reintentan.
- **Tema oscuro / claro**, interfaz según el nivel, y **15 idiomas**.

---

## Páginas

### 🖼 Flow Image — generación de imágenes de Google Flow

![Flow Image](../screenshots/01-image.png)

Genera imágenes por lotes con **Nano Banana Pro / 2 / Lite**. Elige el modelo, la proporción y la resolución (**1K / 2K / 4K** — 2K/4K usan el escalador del modelo), define cuántas filas se ejecutan a la vez y el retardo entre ellas. Pega prompts (o importa un archivo), adjunta imágenes de referencia por fila (arrastra una carpeta y se emparejan automáticamente por nombre de archivo), y usa `@name` para incorporar personajes. **Run** envía toda la lista a la cola.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Tres pestañas: **Text / Frames → Video** (un prompt de texto, o un fotograma inicial/final), **Image / Video ingredients → Video** (imágenes de referencia o un video de referencia), y **Scene stitch → Video**. Modelos: **Veo 3.1 Fast / Lite / Quality** y **Omni Flash**. Elige la proporción, el escalado (720p / 1080p / 4K) y la seed. Pasa el cursor sobre el **?** en la barra de pestañas para una explicación sencilla de frames frente a ingredients.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Text-to-image, image-to-image, text-to-video e image-to-video a través de Grok Imagine (tu pestaña de `grok.com` con sesión iniciada mediante la extensión Auth Helper). Las imágenes ofrecen **8 proporciones** (incl. 4:3, 21:9, 5:2); el video se genera en **480p / 720p / 1080p**. Image-to-video tiene dos modos: **First frame** (la imagen abre el clip) y **Reference** (hasta 14 imágenes guía).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Generación de imagen y video a través de Meta AI. Modos: text-to-image, image-to-image (componentes Character / Scene / Style), text-to-video e image-to-video (fotograma inicial / final).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

Genera con OpenAI **GPT Image 2** usando tus cuentas de ChatGPT, con hasta 5 imágenes de referencia. Elige la proporción (10 opciones, incluidas 21:9, 4:5 y **custom** — donde escribes la proporción en el prompt), la calidad, el modo de prompt, el esfuerzo de razonamiento y la búsqueda web.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Escala una carpeta de imágenes localmente — elige el objetivo y deja que procese la cola, con progreso y estado por fila (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

Crea una biblioteca de personajes reutilizables: una imagen de referencia, una voz personalizada opcional y notas de aspecto/personalidad. Etiquétalos con `@name` en cualquier prompt de Flow y la generación conservará esa identidad.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Un lienzo de nodos visual. Haz clic derecho en el conector de un nodo y el menú solo ofrece los nodos que encajan — elige uno y se conecta automáticamente. Encadena prompt → generate → video → **Extract Frame** → siguiente video, y usa **Merge Video** para unir dos clips (recorta cada extremo, elige una transición). Guarda/carga todo el grafo como archivo `.json`; **Run Flow** lo ejecuta de principio a fin.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Convierte la app en un servidor de automatización local. Inícialo, copia tu API key, y haz POST de trabajos a `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` o `/api/openai/generate`, y luego consulta `/api/status/<id>`. La página lista cada modelo y sus proporciones admitidas. Esquema completo: [`docs/WEBHOOK_INTEGRATION.en.md`](../WEBHOOK_INTEGRATION.en.md).

---

## Dónde se guardan las cosas

| Qué | macOS | Windows |
|---|---|---|
| Salida (imágenes / videos) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Ajustes, sesiones, cuentas | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Tus ajustes, listas de prompts, sesiones, biblioteca de personajes y lista de cuentas se guardan y se restauran la próxima vez que abras la app.

---

## Solución de problemas

**Todo está bloqueado / la pantalla de compra no deja de abrirse** — tu plan caducó, o la cuenta inició sesión en otra máquina. Comprueba la insignia de nivel (abajo a la izquierda) y renueva.

**Una generación de Grok no hace nada** — Grok funciona a través de tu pestaña de `grok.com`. Instala/activa la extensión de navegador **Auth Helper** (Settings → Grok) y asegúrate de haber iniciado sesión en grok.com.

**"Active: 0 accounts" en una página** — añade o vuelve a activar una cuenta en la pestaña de cuenta de esa página (Settings), o su token caducó — pulsa **Refresh all**.

**macOS dice que la app está dañada / no se puede abrir** — no está firmada por Apple. Haz clic derecho → **Open** la primera vez, o ejecuta `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Una actualización no se instala** — descarga la última versión manualmente desde [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
