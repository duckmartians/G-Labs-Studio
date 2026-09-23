<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Eine Desktop-App zur Stapelerzeugung von Bildern &amp; Videos über alle großen KI-Anbieter hinweg — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI und ChatGPT GPT Image 2.</b></p>

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

| Dein Rechner | Download | Hinweise |
|---|---|---|
| 🪟 **Windows 10/11 (64-Bit)** | [`G-Labs-Studio-win.exe`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-win.exe) | Für jeden Windows-PC |
| 🍎 **Mac mit Apple-Chip (M1/M2/M3/M4)** | [`G-Labs-Studio-mac-arm64.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-arm64.dmg) | Macs ab etwa Ende 2020 |
| 🍎 **Mac mit Intel-Chip** | [`G-Labs-Studio-mac-intel.dmg`](https://github.com/duckmartians/G-Labs-Studio/releases/latest/download/G-Labs-Studio-mac-intel.dmg) | Ältere Macs (vor 2020) |

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

**Du brauchst ein G-Labs-Konto.** Öffne die App, melde dich mit Google an und wähle einen Tarif. Die Tarife (**FREE / PLUS / MAX**) schalten unterschiedliche Tools und Modelle frei; kaufen kannst du direkt in der App (Bank-QR, PayPal oder USDT). Ein Konto läuft **auf einem Rechner gleichzeitig** — eine Anmeldung woanders meldet den vorherigen Rechner ab. Das Abzeichen unten links in der Seitenleiste zeigt deine aktuelle Stufe. Brauchst du mehrere Geräte gleichzeitig? Du kannst einen **Team**-Tarif kaufen (der Preis steigt mit der Anzahl der zusätzlichen Geräte).

> **Gerade von der alten Version (G-Labs Automation) gewechselt?** Die neue Version **übernimmt deine Konten nicht**. Du musst dich in der neuen G-Labs Studio **bei allen Konten neu anmelden** (Google/Flow, ChatGPT, Meta…).

Die App **aktualisiert sich selbst**: Sie prüft beim Start GitHub Releases und kann die neue Version direkt aus der App herunterladen und installieren.

---

## Erster Start

1. **Öffne die App und melde dich mit Google an.** Das Stufen-Abzeichen (unten links) bestätigt deinen Plan.
2. **Verbinde die Konten für die Werkzeuge, die du nutzen wirst** (Einstellungen → der passende Konto-Tab):
   - **Google**-Konten → Flow Image / Flow Video
   - **ChatGPT**-Konten → GPT Image 2
   - **Meta**-Konten → Meta Media
   - **Grok** → läuft über deinen angemeldeten `grok.com`-Tab per Begleit-Browsererweiterung (Auth Helper) — kein Konto-Pool
   Jeder Konto-Tab zeigt in seiner Titelleiste **„Active: N accounts"**, damit du weißt, wie viele nutzbar sind.
3. **Wähle eine Seite in der linken Seitenleiste** und beginne mit der Generierung. Jede Generierungsseite folgt demselben Rhythmus: Prompts links eintippen oder importieren, sie landen rechts in einer **Tabelle**, dann **Run** drücken.

Jeder Seitenkopf trägt eine Live-**Statusleiste** — *Running · Queued · Done · Failed · Accounts* — damit du den Stapel auf einen Blick siehst. Klicke auf **Queued**, um den Warteschlangen-Manager zu öffnen, auf **Accounts**, um zu den Konto-Einstellungen zu springen.

---

## Funktionen

![G-Labs Studio](../screenshots/01-image.png)

- **Jeder große Generator, eine App** — Google Flow (Bild + Video), Grok Imagine, Meta AI (vibes.ai) und OpenAI GPT Image 2, jeweils auf einer eigenen Seite mit den Modellen und Seitenverhältnissen, die der Anbieter unterstützt.
- **Von Grund auf für Stapel gemacht** — füge eine Liste von Prompts ein (einer pro Zeile) oder importiere eine `.txt`/Excel-Datei; jeder wird zu einer Zeile. Referenzbilder werden anhand des Dateinamens automatisch zugeordnet. Führe die ganze Liste mit einer von dir gewählten Parallelität aus.
- **Erst hinzufügen, dann starten, wenn du bereit bist** — Zeilen wandern in eine Warteschlange; **Run / Pause / Stop** sind getrennt. Nichts startet, bevor du es sagst, und ein Warteschlangen-Manager erlaubt dir, umzusortieren und zu prüfen.
- **Charakterbibliothek** — speichere einen Charakter einmal (Referenzbild + eigene Stimme + Notizen) und füge ihn mit `@name` in jeden Prompt ein; das Video behält das Aussehen und die Stimme dieses Charakters bei.
- **Workflow (Node-Graph)** — verdrahte Knoten zu einer Pipeline: Prompt → Bild → Video → letztes Bild extrahieren → nächstes Video, plus einen **Merge Video**-Knoten, der zwei Clips mit Zuschnitten und Übergängen (Crossfade, Wipe, Slide, Dissolve …) verbindet. Batch-Knoten lassen die ganze Kette pro Prompt oder pro Bild durchlaufen.
- **Webhook API** — ein lokaler REST-Server, damit Skripte und KI-Agenten Bild-/Video-/Grok-/Meta-/OpenAI-Aufträge einreichen und Ergebnisse abfragen können.
- **Image Upscaler** und ein **Video Editor** (schneiden, zusammenfügen, Diashow) für den Feinschliff.
- **Widerstandsfähig** — Ergebnisse werden verifiziert und automatisch gespeichert; Sitzungen werden wiederhergestellt; fehlgeschlagene Zeilen werden erneut versucht.
- **Dunkles / helles Design**, stufenbewusste Oberfläche und **15 Sprachen**.

---

## Seiten

### 🖼 Flow Image — Bildgenerierung mit Google Flow

![Flow Image](../screenshots/01-image.png)

Erzeuge Bilder im Stapel mit **Nano Banana Pro / 2 / Lite**. Wähle das Modell, das Seitenverhältnis und die Auflösung (**1K / 2K / 4K** — 2K/4K nutzen den Upscaler des Modells), lege fest, wie viele Zeilen gleichzeitig laufen und die Verzögerung dazwischen. Füge Prompts ein (oder importiere eine Datei), hänge pro Zeile Referenzbilder an (ziehe einen Ordner hinein, und sie werden anhand des Dateinamens automatisch zugeordnet), und nutze `@name`, um Charaktere einzubinden. **Run** schickt die ganze Liste in die Warteschlange.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Drei Tabs: **Text / Frames → Video** (ein Textprompt oder ein Start-/Endbild), **Image / Video ingredients → Video** (Referenzbilder oder ein Referenzvideo) und **Scene stitch → Video**. Modelle: **Veo 3.1 Fast / Lite / Quality** und **Omni Flash**. Wähle Seitenverhältnis, Upscale (720p / 1080p / 4K) und Seed. Fahre mit der Maus über das **?** in der Tab-Leiste für eine verständliche Erklärung von Frames vs. Ingredients.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Text-zu-Bild, Bild-zu-Bild, Text-zu-Video und Bild-zu-Video über Grok Imagine (dein angemeldeter `grok.com`-Tab per Auth Helper-Erweiterung). Bilder bieten **8 Seitenverhältnisse** (inkl. 4:3, 21:9, 5:2); Video wird in **480p / 720p / 1080p** erzeugt. Bild-zu-Video hat zwei Modi: **First frame** (das Bild eröffnet den Clip) und **Reference** (bis zu 14 leitende Bilder).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Bild- und Videogenerierung über Meta AI. Modi: Text-zu-Bild, Bild-zu-Bild (Komponenten Character / Scene / Style), Text-zu-Video und Bild-zu-Video (Start-/Endbild).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

Generiere mit OpenAI **GPT Image 2** über deine ChatGPT-Konten, mit bis zu 5 Referenzbildern. Wähle das Seitenverhältnis (10 Optionen, darunter 21:9, 4:5 und **custom** — wobei du das Verhältnis in den Prompt schreibst), die Qualität, den Prompt-Modus, den Denkaufwand (reasoning effort) und die Websuche.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Skaliere einen Ordner mit Bildern lokal hoch — wähle das Ziel und lass die Warteschlange abarbeiten, mit Fortschritt und Status pro Zeile (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

Baue eine Bibliothek wiederverwendbarer Charaktere auf: ein Referenzbild, eine optionale eigene Stimme sowie Notizen zu Aussehen/Persönlichkeit. Markiere sie mit `@name` in jedem Flow-Prompt, und die Generierung behält diese Identität bei.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Eine visuelle Node-Leinwand. Klicke mit der rechten Maustaste auf den Anschluss eines Knotens, und das Menü bietet nur die passenden Knoten an — wähle einen aus, und er verdrahtet sich automatisch. Verkette Prompt → generieren → Video → **Extract Frame** → nächstes Video, und nutze **Merge Video**, um zwei Clips zu verbinden (jedes Ende zuschneiden, einen Übergang wählen). Speichere/lade den ganzen Graph als `.json`-Datei; **Run Flow** führt ihn von Anfang bis Ende aus.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Verwandle die App in einen lokalen Automatisierungsserver. Starte ihn, kopiere deinen API-Schlüssel und sende POST-Aufträge an `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` oder `/api/openai/generate`, und frage dann `/api/status/<id>` ab. Die Seite listet jedes Modell und seine unterstützten Seitenverhältnisse auf. Vollständiges Schema: [`WEBHOOK_INTEGRATION.en.md`](../../WEBHOOK_INTEGRATION.en.md).

---

## Wo die Dinge liegen

| Was | macOS | Windows |
|---|---|---|
| Ausgabe (Bilder / Videos) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Einstellungen, Sitzungen, Konten | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Deine Einstellungen, Prompt-Listen, Sitzungen, Charakterbibliothek und Kontoliste werden gespeichert und beim nächsten Öffnen der App wiederhergestellt.

---

## Fehlerbehebung

**Alles ist gesperrt / der Kaufbildschirm öffnet sich immer wieder** — dein Plan ist abgelaufen, oder das Konto wurde auf einem anderen Gerät angemeldet. Prüfe das Stufen-Abzeichen (unten links) und verlängere.

**Eine Grok-Generierung tut nichts** — Grok läuft über deinen `grok.com`-Tab. Installiere/aktiviere die **Auth Helper**-Browsererweiterung (Einstellungen → Grok) und stelle sicher, dass du bei grok.com angemeldet bist.

**„Active: 0 accounts" auf einer Seite** — füge im Konto-Tab dieser Seite (Einstellungen) ein Konto hinzu oder aktiviere es erneut, oder sein Token ist abgelaufen — drücke **Refresh all**.

**macOS sagt, die App sei beschädigt / lasse sich nicht öffnen** — sie ist nicht von Apple signiert. Öffne sie beim ersten Mal mit Rechtsklick → **Öffnen**, oder führe `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"` aus.

**Ein Update lässt sich nicht installieren** — lade den neuesten Build manuell von [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest) herunter.
