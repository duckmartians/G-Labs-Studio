<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Eine Desktop-App zur Stapelerzeugung von Bildern &amp; Videos über alle großen KI-Anbieter hinweg — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI und ChatGPT GPT Image 2.</b></p>

<p align="center">
  <a href="../../README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
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

![G-Labs Studio](../screenshots/01-image.png)

---

## Installation

Lade den neuesten Build von **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)** herunter:

| Plattform | Datei |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-v<version>-win.exe` — führe den Installer aus (Admin/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-v<version>-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-v<version>-mac-intel.dmg` |

**Erster Start unter macOS** — die App ist nicht von Apple signiert, deshalb wird sie von macOS in Quarantäne gesetzt. Öffne sie beim ersten Mal mit **Rechtsklick → Öffnen**, oder entferne die Markierung über das Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**Du benötigst ein G-Labs-Konto.** Öffne die App, melde dich mit Google an und wähle einen Plan. Die Pläne (**FREE / PLUS / MAX**) schalten unterschiedliche Werkzeuge und Modelle frei; du kannst einen direkt in der App kaufen (Bank-QR, PayPal oder USDT). Ein Konto läuft auf **jeweils einem Gerät** — meldest du dich woanders an, wird das vorherige Gerät abgemeldet. Das Abzeichen unten links in der Seitenleiste zeigt deine aktuelle Stufe.

Die App **aktualisiert sich selbst**: Sie prüft beim Start die GitHub Releases und kann die neue Version direkt aus der App heraus herunterladen und installieren.

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

Verwandle die App in einen lokalen Automatisierungsserver. Starte ihn, kopiere deinen API-Schlüssel und sende POST-Aufträge an `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` oder `/api/openai/generate`, und frage dann `/api/status/<id>` ab. Die Seite listet jedes Modell und seine unterstützten Seitenverhältnisse auf. Vollständiges Schema: [`docs/WEBHOOK_INTEGRATION.en.md`](../WEBHOOK_INTEGRATION.en.md).

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
