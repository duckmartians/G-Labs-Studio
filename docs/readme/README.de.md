<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Eine Desktop-App zur Stapelerzeugung von Bildern &amp; Videos über alle großen KI-Anbieter hinweg — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Google Vids, Google Pics, ChatGPT GPT Image 2, Meta Vibes und Grok — plus Video-Werkzeuge, ein Node-Workflow und eine Webhook-API.</b></p>

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
  <b>Deutsch</b> ·
  <a href="README.id.md">Bahasa Indonesia</a> ·
  <a href="README.ko.md">한국어</a>
</p>

<p align="center">
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe"><img alt="Herunterladen — Windows" src="https://img.shields.io/badge/Herunterladen-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg"><img alt="Herunterladen — macOS (Apple Silicon)" src="https://img.shields.io/badge/Herunterladen-macOS%20Apple%20Silicon-000000?style=for-the-badge&logo=apple&logoColor=white"></a>&nbsp;
  <a href="https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg"><img alt="Herunterladen — macOS (Intel)" src="https://img.shields.io/badge/Herunterladen-macOS%20Intel-555555?style=for-the-badge&logo=apple&logoColor=white"></a>
</p>

---

## Installation

### Schritt 1 — Wähle die richtige Version für deinen Rechner

Lade die neueste Version von **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** herunter und wähle die Datei, die zu deinem Rechner passt:

| Dein Rechner | Download | Google Drive | Hinweise |
|---|---|---|---|
| 🪟 **Windows 10/11 (64-Bit)** | [Windows](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | [Windows](https://drive.google.com/drive/u/0/folders/1ovx97E2UJ4qeIoiHg-_0dinDQC1rjR46) | Für jeden Windows-PC |
| 🍎 **Mac mit Apple-Chip (M1/M2/M3/M4)** | [macOS ARM](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | [macOS ARM](https://drive.google.com/drive/u/0/folders/1kfENU5CPWq_Djo641XvWiZERdKNun26Q) | Macs ab etwa Ende 2020 |
| 🍎 **Mac mit Intel-Chip** | [macOS Intel](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | [macOS Intel](https://drive.google.com/drive/u/0/folders/1qvFV8P5k6FpHfGfnwbL8CccrwXgGoYg0) | Ältere Macs (vor 2020) |

**Nicht sicher, welchen Chip dein Mac hat?** Klick auf das -Menü (oben links) → **About This Mac**:
- Eine Zeile **Chip** mit „Apple M1 / M2 / M3…“ → lade die **arm64**-Version.
- Eine Zeile **Processor** mit „Intel…“ → lade die **intel**-Version.

> Die **Intel**-Version läuft auch auf einem Mac mit Apple-Chip (nur langsamer), aber die **arm64**-Version lässt sich auf einem Intel-Mac **nicht öffnen** — wähle also die richtige.

### Schritt 2 — Installieren

<details open>
<summary><b>🪟 Unter Windows</b></summary>

1. Öffne die heruntergeladene **`G-Labs-Studio-win.exe`**.
2. Falls **„Windows protected your PC“** (SmartScreen) erscheint: klick **More info** → **Run anyway**. *(Die App ist noch nicht mit einem Microsoft-Zertifikat signiert, daher die Warnung — es ist kein Virus.)*
3. Klick **Yes** bei der Administrator-Abfrage (UAC) und folge dem Installer bis zum Ende.
4. Starte sie über das **Start Menu** oder die **Desktop**-Verknüpfung.

</details>

<details open>
<summary><b>🍎 Unter macOS</b></summary>

1. Öffne die heruntergeladene **`.dmg`** und **zieh G-Labs Studio in den Applications-Ordner**.
2. Geh zu **Applications**, **Rechtsklick** (oder Control-Klick) auf **G-Labs Studio** → **Open** → klick im Dialog noch einmal **Open**. *(Die App ist nicht von Apple signiert, daher musst du sie beim **ersten Mal** so öffnen; danach öffnet sie normal.)*
3. Wenn macOS sagt, die App sei **„beschädigt / kann nicht geöffnet werden“**, oder es keinen Open-Button gibt, öffne das **Terminal** und füge ein:
   ```bash
   xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
   ```
   Dann öffne die App erneut.

</details>

### Schritt 3 — Anmelden und Tarif wählen

**Du brauchst ein G-Labs-Konto.** Öffne die App, melde dich mit Google an und wähle einen Tarif. Die Tarife (**BASIC / PLUS / MAX**) schalten unterschiedliche Tools und Modelle frei; kaufen kannst du direkt in der App (Bank-QR, PayPal oder USDT). Ein Konto läuft **auf einem Rechner gleichzeitig** — eine Anmeldung woanders meldet den vorherigen Rechner ab. Das Abzeichen unten links in der Seitenleiste zeigt deine aktuelle Stufe. Brauchst du mehrere Geräte gleichzeitig? Du kannst einen **Team**-Tarif kaufen (der Preis steigt mit der Anzahl der zusätzlichen Geräte).

> **Gerade von der alten Version (G-Labs Automation) gewechselt?** Die neue Version **übernimmt deine Konten nicht**. Du musst dich in der neuen G-Labs Studio **bei allen Konten neu anmelden** (Google/Flow, ChatGPT, Meta…).

Die App **aktualisiert sich selbst**: Sie prüft beim Start GitHub Releases und kann die neue Version direkt aus der App herunterladen und installieren.

---

## Erster Start

1. **Öffne die App und melde dich mit Google an.** Das Stufen-Abzeichen (unten links: **BASIC / PLUS / MAX**) bestätigt deinen Plan.
2. **Verbinde Konten für die Werkzeuge, die du nutzen wirst** (**Einstellungen** → der passende Konten-Tab):
   - **Flow-Konten** → Flow Image / Flow Video
   - **Google-Konten** → **Google Vids** und **Google Pics** (beide Seiten teilen sich diese Google-Konten; jedes Konto wird für Vids-Videos und für Pics-Bilder separat eingeschaltet)
   - **ChatGPT-Konto** → GPT Image 2
   - **Vibes-Konto** → Meta Vibes
   - **Grok-Konto** → kein Kontospeicher: Dieser Tab führt dich durch die Installation der Browsererweiterung **Auth Helper**, danach läuft Grok über deinen angemeldeten `grok.com`-Tab in Chrome

   Jeder Konten-Tab zeigt in seiner Titelleiste **„Aktiv: N Konten“**, damit du weißt, wie viele nutzbar sind.
3. **Wähle eine Seite in der linken Seitenleiste** und beginne mit der Generierung. Jede Generierungsseite folgt demselben Rhythmus: Prompts links eintippen oder importieren, sie landen rechts in einer **Tabelle**, dann **Run** drücken.

Jeder Seitenkopf trägt eine Live-**Statusleiste** — *Läuft · Warteschlange · Fertig · Fehler · Konten* — damit du den ganzen Stapel auf einen Blick siehst. Klicke auf **Warteschlange**, um den Warteschlangen-Manager zu öffnen, auf **Konten**, um zu den Konto-Einstellungen zu springen.

---

## Funktionen

![G-Labs Studio](../screenshots/en/flow-image.webp)

- **Jeder große Generator, eine App** — Google Flow (Bild + Video), Google Vids, Google Pics, GPT Image 2, Meta Vibes und Grok, jeweils auf einer eigenen Seite mit den Modellen und Seitenverhältnissen, die der Anbieter unterstützt.
- **Für Stapel gebaut** — füge eine Prompt-Liste ein (einer pro Zeile) oder importiere `.txt`/Excel; jeder Prompt wird zu einer Zeile. Referenzbilder werden anhand des Dateinamens automatisch zugeordnet. Führe die ganze Liste mit der von dir gewählten Anzahl paralleler Threads aus.
- **Erst hinzufügen, dann starten, wenn du bereit bist** — Zeilen wandern in eine Warteschlange; **Run / Pause / Stop** sind getrennt. Nichts startet, bevor du es sagst, und der Warteschlangen-Manager erlaubt dir, umzusortieren und zu prüfen.
- **Automatische Entfernung des Gemini ✦-Logos** — Google-Pics-Bilder und Google-Vids-Videos werden direkt nach dem Download bereinigt (schalte **Gemini-Logo anzeigen** ein, um es zu behalten). Dateien ohne Logo bleiben unverändert.
- **Charakterbibliothek** — speichere einen Charakter einmal (Referenzbild + Stimme + Notizen) und rufe ihn mit `@name` in Prompts von Flow Image, Flow Video und Google Vids auf, um Szenen konsistent zu halten.
- **Workflow (Node-Graph)** — verdrahte Knoten zu einer Pipeline: Prompt → Bild → Video → letztes Bild extrahieren → nächstes Video, plus einen **Video zusammenfügen**-Knoten, der zwei Clips mit einem Übergang verbindet.
- **Video-Tools** — Videobearbeitung auf der Timeline, untertitelsynchrone Bild-Diashows, Video-Aufteilung, Frame-Extraktion und Video-Logo-Entfernung, direkt in der App.
- **Bild-Hochskalierer** auf deinem eigenen Rechner und eine **Webhook-API** für Automatisierung.
- **Widerstandsfähig** — Ergebnisse werden verifiziert und automatisch gespeichert; Sitzungen werden wiederhergestellt; fehlgeschlagene Zeilen werden erneut versucht.
- **Helles / dunkles Design**, stufenbewusste Oberfläche und **15 Sprachen**.

---

## Seiten

### 🖼 Flow Image — Bildgenerierung mit Google Flow

![Flow Image](../screenshots/en/flow-image.webp)

Erzeuge Bilder im Stapel mit **Nano Banana Pro / 2 / 2 Lite**. Wähle das Modell, das Seitenverhältnis und die Auflösung (**1K / 2K / 4K** — 2K/4K nutzen den Upscaler des Modells), lege fest, wie viele Zeilen gleichzeitig laufen und die Verzögerung dazwischen. Füge Prompts ein (oder importiere eine Datei), hänge pro Zeile Referenzbilder an (lege einen Ordner ab, und sie werden anhand des Dateinamens automatisch zugeordnet), und nutze `@name`, um einen Charakter einzubinden. Der Schalter **Veo / Gemini-Logo anzeigen** (standardmäßig aus) wird mit der Seite Flow Video geteilt. **Run** schickt die ganze Liste in die Warteschlange.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/en/flow-video.webp)

Drei Tabs: **Text / Frame → Video** (ein Textprompt oder Start-/Endbilder), **Bild- / Video-Zutaten → Video** (Referenzbilder oder ein Referenzvideo) und **Szenenkette → Video**. Modelle: **Veo 3.1 Fast / Lite / Quality** und **Omni Flash**. Wähle Seitenverhältnis, Upscale (720p / 1080p / 4K) und Seed. Fahre mit der Maus über das **?** in der Tab-Leiste für eine verständliche Erklärung von Frames vs. Zutaten.

### 📽 Google Vids

![Google Vids](../screenshots/en/vids.webp)

Erstelle Videos mit deinem Google-Konto in drei Tabs: **Text → Video**, **Bild → Video** (ein Eröffnungsbild) und **Komponenten → Video** (bis zu 3 Komponentenbilder). Wähle Quer-/Hochformat, 720p / 1080p und eine Dauer von 3–10 Sekunden — oder setze ein Tag wie `[4s]` in den Prompt, um jeder Zeile ihre eigene Länge zu geben. Fertige Videos lassen sich direkt aus der Tabelle auf 1080p hochskalieren. Jedes Konto hat ein Kontingent, gemessen in Videosekunden; füge mehr Konten hinzu, um schneller zu arbeiten. Das Gemini ✦-Logo auf heruntergeladenen Videos (720p / 1080p) wird automatisch entfernt, außer du schaltest **Gemini-Logo anzeigen** ein.

### 🖼 Google Pics

![Google Pics](../screenshots/en/pics.webp)

Zwei Tabs: **Text → Bild** und **Bild → Bild** mit **bis zu 14 Referenzbildern** (Charaktere, Objekte, Szenen, Stil). Bei jedem Durchlauf liefert Google 3–9 Bilder; **Bilder pro Durchlauf behalten** legt fest, wie viele behalten werden (1–4 oder alle). 10 Seitenverhältnisse, darunter 21:9, 3:2 und 5:4. Jeder Durchlauf kostet 1 Google-Pics-Durchlauf, egal wie viele Bilder; ein von der Inhaltsrichtlinie abgelehnter Prompt kostet nichts. Pics teilt sich die **Google-Konten** mit Google Vids.

**Automatische Entfernung des Gemini ✦-Logos:** Bei heruntergeladenen Pics-Bildern wird das ✦-Zeichen in der unteren rechten Ecke direkt nach dem Download entfernt, mithilfe einer speziell für Google Pics vermessenen Logo-Map — die Logo-Überblendung wird umgekehrt, sodass die ursprüngliche Textur darunter wiederhergestellt statt verwischt wird. Bilder, in denen kein Logo erkannt wird, bleiben unverändert. Um das Logo zu behalten, schalte **Gemini-Logo anzeigen** ein.

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/en/gpt-image.webp)

Generiere mit OpenAI **GPT Image 2** über dein ChatGPT-Konto, mit bis zu 5 Referenzbildern. Wähle das Seitenverhältnis (10 Optionen, darunter 21:9, 4:5 und **custom** — wobei du das Verhältnis in den Prompt schreibst), die Qualität, den Prompt-Modus, die Denkstufe (reasoning) und die Websuche.

### 🎨 Meta Vibes

![Meta Vibes](../screenshots/en/vibes.webp)

Erstelle Bilder und Videos auf Meta Vibes in vier Tabs: **Text → Bild**, **Text → Video**, **Bild → Bild** (Charakter- / Szenen- / Stilbilder) und **Bild → Video** (Start-/Endbild). Automatisch eingereiht und heruntergeladen.

### 🤖 Grok Imagen

![Grok Imagen](../screenshots/en/grok.webp)

Text → Bild, Bild → Bild, Text → Video und Bild → Video über Grok Imagine (dein angemeldeter `grok.com`-Tab, per Auth Helper-Erweiterung). Bilder gibt es in **8 Seitenverhältnissen** (inkl. 4:3, 21:9, 5:2); Videos werden in **480p / 720p / 1080p** gerendert. Bild → Video hat zwei Modi: **Erstes Bild** (das Bild eröffnet den Clip) und **Referenzbilder** (bis zu 14 leitende Bilder).

### 👤 Charaktere

![Charaktere](../screenshots/en/characters.webp)

Baue eine wiederverwendbare Besetzung auf: ein Referenzbild, eine Stimme (eine der voreingestellten Flow-Stimmen, mit optionaler Beschreibung der Sprechweise) sowie Notizen zu Aussehen/Persönlichkeit. Markiere sie mit `@name` in Prompts von Flow Image, Flow Video und Google Vids, und die Generierung behält diese Identität bei (die Stimme nutzt nur Flow Video; Google Vids nutzt das Bild).

### 🔗 Workflow

![Workflow](../screenshots/en/workflow.webp)

Eine visuelle Node-Leinwand. Klicke mit der rechten Maustaste auf den Anschluss eines Knotens, und das Menü bietet nur die passenden Knoten an — wähle einen aus, und er verdrahtet sich selbst. Es gibt Knoten für Flow Image, Flow Video, Grok, Meta und GPT Image 2. Verkette Prompt → Bild → Video → **Frame extrahieren** → nächstes Video, und nutze **Video zusammenfügen**, um zwei Clips zu verbinden (jedes Ende zuschneiden, einen Übergang wählen). Speichere/lade den ganzen Graph als `.json`-Datei (Format: [`WORKFLOW_JSON_SPEC.md`](../../WORKFLOW_JSON_SPEC.md)); **Run Flow** führt ihn von Anfang bis Ende aus.

### 🎞 Video-Tools

Fünf Tabs auf einer Seite:

**Videobearbeitung** — eine Timeline für Video, SRT-Untertitel und Audio: schneiden, teilen, umsortieren, automatisch anpassen, dann ein fertiges Video exportieren.

![Videobearbeitung](../screenshots/en/vt-video.webp)

**Bild-Diashow passend zur Untertiteldatei** — lade Bilder und eine `.srt`-Datei; jedes Bild wird automatisch einer Untertitelzeile zugeordnet, mit Bewegungseffekten, Overlays und Untertitel-Styling.

![Bild-Diashow passend zur Untertiteldatei](../screenshots/en/vt-slideshow.webp)

**Video in Segmente teilen** — nach Anzahl der Teile, fester oder zufälliger Länge, einer Liste von Zeitstempeln oder einer Liste von A–B-Bereichen; eine Datei oder ein ganzer Stapel, GPU-beschleunigt, wenn verfügbar.

![Video in Segmente teilen](../screenshots/en/vt-slicer.webp)

**Frames aus Video extrahieren** — nach Gesamtanzahl, Zeitintervall, Frame-Intervall oder Bewegung; eine Datei oder ein ganzer Ordner.

![Frames aus Video extrahieren](../screenshots/en/vt-extractor.webp)

**Video-Logo entfernen** — entfernt das ✦-Logo aus Google-Vids-Videos in 720p und 1080p (Quer- oder Hochformat), mit einer Vorher/Nachher-Vorschau in der App. Videos ohne Logo werden übersprungen; Originale bleiben erhalten und Ergebnisse werden als `<name>_nologo.mp4` gespeichert.

![Video-Logo entfernen](../screenshots/en/vt-logo.webp)

### 🔍 Bild-Hochskalierer

![Bild-Hochskalierer](../screenshots/en/upscaler.webp)

Vergrößere und schärfe Bilder direkt auf deinem Computer — füge einzelne Bilder oder einen ganzen Ordner hinzu, wähle ein KI-Modell (Real-ESRGAN, UltraSharp, Remacri…) und einen Faktor von 2x–8x, verfolge den Fortschritt pro Zeile und vergleiche vorher/nachher.

### 🌐 Webhook-API

![Webhook-API](../screenshots/en/webhook.webp)

Verwandle die App in einen lokalen Automatisierungsserver (MAX-Plan), damit n8n, Make, Zapier, Skripte oder KI-Agenten Aufträge in die Warteschlange der App schieben können. Starte ihn, kopiere deinen API-Schlüssel und sende POST-Aufträge an `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate`, `/api/openai/generate` oder `/api/upscale/generate`, und frage dann `/api/status/<id>` ab. Die Seite listet jedes Modell und seine unterstützten Seitenverhältnisse auf. Vollständiges Schema: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Wo die Dinge liegen

| Was | macOS | Windows |
|---|---|---|
| Ausgaben (Bilder / Videos) | `~/Documents/G-Labs Studio/output` | `%USERPROFILE%\Documents\G-Labs Studio\output` |
| Einstellungen, Sitzungen, Konten, Charaktere | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Jede Seite hat einen eigenen Unterordner in `output` (ein kleinerer Ordner pro Durchlauf); den Speicherordner kannst du auf jeder Seite ändern. Deine Einstellungen, Prompt-Listen, Sitzungen, Charakterbibliothek und Kontoliste werden gespeichert und beim nächsten Öffnen der App wiederhergestellt.

---

## Fehlerbehebung

**Alles ist gesperrt / der Kaufbildschirm öffnet sich immer wieder** — dein Plan ist abgelaufen, oder das Konto wurde auf einem anderen Gerät angemeldet. Prüfe das Stufen-Abzeichen (unten links) und verlängere. Google Vids und Google Pics benötigen einen PLUS/MAX-Plan; die Webhook-API benötigt MAX.

**Eine Grok-Generierung tut nichts** — Grok läuft über deinen `grok.com`-Tab. Installiere/aktiviere die **Auth Helper**-Browsererweiterung (Einstellungen → Grok-Konto) und stelle sicher, dass du bei grok.com angemeldet bist.

**Google Pics meldet, dass es kein Konto gibt** — Pics nutzt die Google-Vids-Konten. Füge eines unter Einstellungen → **Google-Konten** hinzu.

**„Aktiv: 0 Konten“ auf einer Seite** — füge im Konten-Tab dieser Seite (Einstellungen) ein Konto hinzu oder aktiviere es erneut, oder sein Token ist abgelaufen — drücke **Alle aktualisieren**.

**Windows blockiert sie mit „Windows protected your PC“** — klicke auf **More info → Run anyway**. Die App ist noch nicht mit einem Microsoft-Zertifikat signiert, daher die Warnung — es ist kein Virus.

**macOS sagt, die App sei beschädigt / lasse sich nicht öffnen** — sie ist noch nicht von Apple signiert. Beim ersten Mal Rechtsklick → **Open**, oder führe `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` aus.

**Ein Update wurde nicht installiert** — lade den neuesten Build manuell von [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) herunter.
