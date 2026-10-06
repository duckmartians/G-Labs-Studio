<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Una sola app de escritorio para generar por lotes imágenes &amp; videos en todas las grandes IA — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Google Vids, Google Pics, ChatGPT GPT Image 2, Meta Vibes y Grok — además de herramientas de video, un workflow de nodos y una Webhook API.</b></p>

<p align="center">
  <a href="README.en.md">English</a> ·
  <a href="../../README.md">Tiếng Việt</a> ·
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
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Descargar — Windows" src="https://img.shields.io/badge/Descargar-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Descargar — macOS (Apple Silicon)" src="https://img.shields.io/badge/Descargar-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Descargar — macOS (Intel)" src="https://img.shields.io/badge/Descargar-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Instalación

### Paso 1 — Elige la versión correcta para tu equipo

Descarga la última versión desde **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** y elige el archivo que corresponda a tu equipo:

| Tu equipo | Descarga | Google Drive | Notas |
|---|---|---|---|
| 🪟 **Windows 10/11 (64 bits)** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | Para cualquier PC con Windows |
| 🍎 **Mac con chip Apple (M1/M2/M3/M4)** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Mac desde finales de 2020 en adelante |
| 🍎 **Mac con chip Intel** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Mac más antiguos (antes de 2020) |

**¿No sabes qué chip tiene tu Mac?** Haz clic en el menú  (arriba a la izquierda) → **About This Mac**:
- Una línea **Chip** que dice “Apple M1 / M2 / M3…” → descarga la versión **arm64**.
- Una línea **Processor** que dice “Intel…” → descarga la versión **intel**.

> La versión **Intel** funciona igual en un Mac con chip Apple (solo más lenta), pero la versión **arm64** **no se abre** en un Mac Intel — así que elige la correcta.

### Paso 2 — Instalar

<details open>
<summary><b>🪟 En Windows</b></summary>

1. Abre el **`G-Labs-Studio-win.exe`** descargado.
2. Si aparece **“Windows protected your PC”** (SmartScreen): haz clic en **More info** → **Run anyway**. *(La app aún no está firmada con un certificado de Microsoft, por eso se marca — no es un virus.)*
3. Haz clic en **Yes** en el aviso de administrador (UAC) y sigue el instalador hasta el final.
4. Ábrela desde el **Start Menu** o el acceso directo del **Desktop**.

</details>

<details open>
<summary><b>🍎 En macOS</b></summary>

1. Abre el **`.dmg`** descargado y **arrastra G-Labs Studio a la carpeta Applications**.
2. Ve a **Applications**, **clic derecho** (o Control-clic) en **G-Labs Studio** → **Open** → vuelve a hacer clic en **Open** en el diálogo. *(La app no está firmada por Apple, así que debes abrirla así la **primera vez**; después se abre normal.)*
3. Si macOS dice que la app está **“dañada / no se puede abrir”**, o no hay botón Open, abre la **Terminal** y pega:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   Luego abre la app de nuevo.

</details>

### Paso 3 — Inicia sesión y elige un plan

**Necesitas una cuenta de G-Labs.** Abre la app, inicia sesión con Google y elige un plan. Los planes (**BASIC / PLUS / MAX**) desbloquean distintas herramientas y modelos; puedes comprar uno desde dentro de la app (QR bancario, PayPal o USDT). Una cuenta funciona en **una sola máquina a la vez** — iniciar sesión en otro lugar cierra la sesión de la máquina anterior. La insignia en la esquina inferior izquierda de la barra lateral muestra tu nivel actual. ¿Necesitas varios dispositivos a la vez? Puedes comprar un plan **Team** (el precio aumenta según la cantidad de dispositivos adicionales que elijas).

> **¿Acabas de pasar de la versión antigua (G-Labs Automation)?** La nueva versión **no** traslada tus cuentas. Tendrás que **volver a iniciar sesión en todas tus cuentas** (Google/Flow, ChatGPT, Meta…) en la nueva G-Labs Studio.

La app **se actualiza sola**: comprueba GitHub Releases al iniciarse y puede descargar e instalar la nueva versión desde dentro de la app.

---

## Primer uso

1. **Abre la app e inicia sesión con Google.** La insignia de nivel (abajo a la izquierda: **BASIC / PLUS / MAX**) confirma tu plan.
2. **Conecta las cuentas de las herramientas que vayas a usar** (**Configuración** → la pestaña de cuentas correspondiente):
   - **Cuentas de Flow** → Flow Imagen / Flow Vídeo
   - **Cuentas de Google** → **Google Vids** y **Google Pics** (ambas páginas comparten estas cuentas de Google; cada cuenta se activa por separado para los videos de Vids y para las imágenes de Pics)
   - **Cuenta ChatGPT** → GPT Image 2
   - **Cuenta de Vibes** → Meta Vibes
   - **Cuenta de Grok** → sin almacén de cuentas: esta pestaña te guía para instalar la extensión de navegador **Auth Helper**, y luego Grok funciona a través de tu pestaña de `grok.com` con sesión iniciada en Chrome

   Cada pestaña de cuentas muestra **"Activas: N cuentas"** en su barra de título para que sepas cuántas están disponibles.
3. **Elige una página en la barra lateral izquierda** y empieza a generar. Todas las páginas de generación siguen el mismo ritmo: escribe o importa prompts a la izquierda, aparecen en una **tabla** a la derecha, y luego pulsa **Run**.

Cada encabezado de página lleva una **barra de estado** en vivo — *En curso · En cola · Hecho · Error · Cuentas* — para ver todo el lote de un vistazo. Haz clic en **En cola** para abrir el gestor de cola, y en **Cuentas** para ir a la configuración de cuentas.

---

## Características

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **Todos los grandes generadores, una app** — Google Flow (imagen + video), Google Vids, Google Pics, GPT Image 2, Meta Vibes y Grok, cada uno en su propia página con los modelos y proporciones que ese proveedor admite.
- **Diseñado para lotes** — pega una lista de prompts (uno por línea) o importa `.txt`/Excel; cada prompt se convierte en una fila. Las imágenes de referencia se emparejan automáticamente por nombre de archivo. Ejecuta toda la lista con el número de hilos en paralelo que elijas.
- **Añade primero, ejecuta cuando estés listo** — las filas van a una cola; **Run / Pause / Stop** son independientes. Nada arranca hasta que tú lo digas, y el gestor de cola te permite reordenar e inspeccionar.
- **Eliminación automática del logo Gemini ✦** — las imágenes de Google Pics y los videos de Google Vids se limpian justo después de descargarse (activa **Mostrar logo de Gemini** para conservarlo). Los archivos sin logo no se tocan.
- **Biblioteca de personajes** — guarda un personaje una vez (imagen de referencia + voz + notas) y llámalo con `@name` en los prompts de Flow Imagen, Flow Vídeo y Google Vids para mantener las escenas coherentes.
- **Flujo de trabajo (grafo de nodos)** — conecta nodos en una tubería: prompt → imagen → video → extraer el último fotograma → siguiente video, además de un nodo **Unir vídeo** que une dos clips con una transición.
- **Herramientas de Video** — edición de video en línea de tiempo, presentaciones de imágenes sincronizadas con subtítulos, división de video, extracción de fotogramas y eliminación del logo de video, dentro de la propia app.
- **Ampliador de imágenes** en tu propio equipo y una **API de Webhook** para automatización.
- **Resiliente** — los resultados se verifican y guardan automáticamente; las sesiones se restauran; las filas fallidas se reintentan.
- **Tema claro / oscuro**, interfaz según el nivel, y **15 idiomas**.

---

## Páginas

### 🖼 Flow Imagen — generación de imágenes de Google Flow

![Flow Imagen](../screenshots/en/flow-image.webp)

Genera imágenes por lotes con **Nano Banana Pro / 2 / 2 Lite**. Elige el modelo, la proporción y la resolución (**1K / 2K / 4K** — 2K/4K usan el escalador del modelo), define cuántas filas se ejecutan a la vez y el retardo entre ellas. Pega prompts (o importa un archivo), adjunta imágenes de referencia por fila (suelta una carpeta y se emparejan automáticamente por nombre de archivo), y usa `@name` para incorporar un personaje. El interruptor **Mostrar logo de Veo / Gemini** (desactivado por defecto) se comparte con la página Flow Vídeo. **Run** envía toda la lista a la cola.

### 🎬 Flow Vídeo — Veo &amp; Omni Flash

![Flow Vídeo](../screenshots/en/flow-video.webp)

Tres pestañas: **Texto / Fotograma → Vídeo** (un prompt de texto, o fotogramas inicial/final), **Ingredientes de imagen / vídeo → Vídeo** (imágenes de referencia o un video de referencia) y **Cadena de escenas → Vídeo**. Modelos: **Veo 3.1 Fast / Lite / Quality** y **Omni Flash**. Elige la proporción, el escalado (720p / 1080p / 4K) y la seed. Pasa el cursor sobre el **?** en la barra de pestañas para una explicación sencilla de fotogramas frente a ingredientes.

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

Crea videos con tu cuenta de Google en tres pestañas: **Texto → Vídeo**, **Imagen → Vídeo** (una imagen de apertura) y **Componentes → Vídeo** (hasta 3 imágenes de componentes). Elige horizontal/vertical, 720p / 1080p y una duración de 3–10 segundos — o pon una etiqueta como `[4s]` en el prompt para dar a cada fila su propia duración. Los videos terminados se pueden escalar a 1080p directamente desde la tabla. Cada cuenta tiene una cuota medida en segundos de video; añade más cuentas para ir más rápido. El logo Gemini ✦ de los videos descargados (720p / 1080p) se elimina automáticamente a menos que actives **Mostrar logo de Gemini**.

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

Dos pestañas: **Texto → Imagen** e **Imagen → Imagen** con **hasta 14 imágenes de referencia** (personajes, objetos, escenas, estilo). En cada ejecución Google devuelve 3–9 imágenes; **Imágenes a conservar por ejecución** decide cuántas conservar (1–4 o todas). 10 proporciones, incluidas 21:9, 3:2 y 5:4. Cada ejecución cuesta 1 ejecución de Google Pics sin importar el número de imágenes; un prompt rechazado por la política de contenido no cuesta nada. Pics comparte las **Cuentas de Google** con Google Vids.

**Eliminación automática del logo Gemini ✦:** a las imágenes de Pics descargadas se les quita la marca ✦ de la esquina inferior derecha justo después de la descarga, usando un mapa del logo medido específicamente para Google Pics — la mezcla del logo se invierte, de modo que la textura original bajo él se restaura en lugar de difuminarse. Las imágenes en las que no se detecta logo se dejan como están. Para conservar el logo, activa **Mostrar logo de Gemini**.

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

Genera con OpenAI **GPT Image 2** usando tu cuenta de ChatGPT, con hasta 5 imágenes de referencia. Elige la proporción (10 opciones, incluidas 21:9, 4:5 y **custom** — donde escribes la proporción en el prompt), la calidad, el modo de prompt, el nivel de razonamiento y la búsqueda web.

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

Crea imágenes y videos en Meta Vibes en cuatro pestañas: **Texto → Imagen**, **Texto → Video**, **Imagen → Imagen** (imágenes de personaje / escena / estilo) e **Imagen → Video** (fotograma inicial / final). Se ponen en cola y se descargan automáticamente.

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

Texto → Imagen, Imagen → Imagen, Texto → Vídeo e Imagen → Vídeo a través de Grok Imagine (tu pestaña de `grok.com` con sesión iniciada, mediante la extensión Auth Helper). Las imágenes vienen en **8 proporciones** (incl. 4:3, 21:9, 5:2); los videos se renderizan en **480p / 720p / 1080p**. Imagen → Vídeo tiene dos modos: **Primer fotograma** (la imagen abre el clip) e **Imágenes ref.** (hasta 14 imágenes guía).

### 👤 Personajes

![Personajes](../screenshots/en/characters.webp)

Crea un reparto reutilizable: una imagen de referencia, una voz (una de las voces predefinidas de Flow, con una descripción opcional de la forma de hablar) y notas de aspecto/personalidad. Etiquétalos con `@name` en los prompts de Flow Imagen, Flow Vídeo y Google Vids y la generación conservará esa identidad (la voz solo la usa Flow Vídeo; Google Vids usa la imagen).

### 🔗 Flujo de trabajo

![Flujo de trabajo](../screenshots/en/workflow.webp)

Un lienzo de nodos visual. Haz clic derecho en el conector de un nodo y el menú solo ofrece los nodos que encajan — elige uno y se conecta solo. Hay nodos para Flow Imagen, Flow Vídeo, Grok, Meta y GPT Image 2. Encadena prompt → imagen → video → **Extraer Fotograma** → siguiente video, y usa **Unir vídeo** para unir dos clips (recorta cada extremo, elige una transición). Guarda/carga todo el grafo como archivo `.json` (formato: [`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)); **Run Flow** lo ejecuta de principio a fin.

### 🎞 Herramientas de Video

Cinco pestañas en una página:

**Edición de vídeo** — una línea de tiempo para video, subtítulos SRT y audio: corta, divide, reordena, ajusta automáticamente y luego exporta un único video terminado.

![Edición de vídeo](../screenshots/en/vt-video.webp)

**Presentación de imágenes según el archivo de subtítulos** — carga imágenes y un archivo `.srt`; cada imagen se empareja automáticamente con una línea de subtítulo, con efectos de movimiento, superposiciones y estilo de subtítulos.

![Presentación de imágenes según el archivo de subtítulos](../screenshots/en/vt-slideshow.webp)

**Dividir vídeo en segmentos** — por número de partes, duración fija o aleatoria, una lista de marcas de tiempo o una lista de rangos A–B; un archivo o un lote entero, con aceleración por GPU cuando está disponible.

![Dividir vídeo en segmentos](../screenshots/en/vt-slicer.webp)

**Extraer fotogramas del vídeo** — por número total, intervalo de tiempo, intervalo de fotogramas o movimiento; un archivo o una carpeta entera.

![Extraer fotogramas del vídeo](../screenshots/en/vt-extractor.webp)

**Quitar logo del vídeo** — elimina el logo ✦ de los videos de Google Vids en 720p y 1080p (horizontal o vertical), con una vista previa antes/después en la app. Los videos sin logo se omiten; los originales se conservan y los resultados se guardan como `<nombre>_nologo.mp4`.

![Quitar logo del vídeo](../screenshots/en/vt-logo.webp)

### 🔍 Ampliador de imágenes

![Ampliador de imágenes](../screenshots/en/upscaler.webp)

Amplía y da nitidez a imágenes directamente en tu computadora — añade imágenes sueltas o una carpeta entera, elige un modelo de IA (Real-ESRGAN, UltraSharp, Remacri…) y una escala de 2x–8x, sigue el progreso por fila y compara antes/después.

### 🌐 API de Webhook

![API de Webhook](../screenshots/en/webhook.webp)

Convierte la app en un servidor de automatización local (plan MAX) para que n8n, Make, Zapier, scripts o agentes de IA puedan enviar trabajos a la cola de la app. Inícialo, copia tu API key, y haz POST de trabajos a `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate`, `/api/openai/generate` o `/api/upscale/generate`, y luego consulta `/api/status/<id>`. La página lista cada modelo y sus proporciones admitidas. Esquema completo: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Dónde se guardan las cosas

| Qué | macOS | Windows |
|---|---|---|
| Salidas (imágenes / videos) | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| Ajustes, sesiones, cuentas, personajes | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Cada página tiene su propia subcarpeta dentro de `output` (una carpeta más pequeña por ejecución); puedes cambiar la carpeta de guardado en cada página. Tus ajustes, listas de prompts, sesiones, biblioteca de personajes y lista de cuentas se guardan y se restauran la próxima vez que abras la app.

---

## Solución de problemas

**Todo está bloqueado / la pantalla de compra no deja de abrirse** — tu plan caducó, o la cuenta inició sesión en otra máquina. Comprueba la insignia de nivel (abajo a la izquierda) y renueva. Google Vids y Google Pics requieren un plan PLUS/MAX; la API de Webhook requiere MAX.

**Una generación de Grok no hace nada** — Grok funciona a través de tu pestaña de `grok.com`. Instala/activa la extensión de navegador **Auth Helper** (Configuración → Cuenta de Grok) y asegúrate de haber iniciado sesión en grok.com.

**Google Pics dice que no hay ninguna cuenta** — Pics usa las cuentas de Google Vids. Añade una en Configuración → **Cuentas de Google**.

**"Activas: 0 cuentas" en una página** — añade o vuelve a activar una cuenta en la pestaña de cuentas de esa página (Configuración), o su token caducó — pulsa **Actualizar todo**.

**Windows lo bloquea con "Windows protected your PC"** — haz clic en **More info → Run anyway**. La app aún no está firmada con un certificado de Microsoft, por eso se marca — no es un virus.

**macOS dice que la app está dañada / no se puede abrir** — aún no está firmada por Apple. Haz clic derecho → **Open** la primera vez, o ejecuta `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Una actualización no se instaló** — descarga la última versión manualmente desde [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
