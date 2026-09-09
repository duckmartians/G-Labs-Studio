<h1 align="center">G-Labs Studio</h1>

<p align="center"><b>Um único app de desktop para gerar imagens e vídeos em lote em todas as grandes IAs — Google Flow (Veo 3.1, Omni Flash, Nano Banana), Grok Imagine, Meta AI e ChatGPT GPT Image 2.</b></p>

<p align="center">
  <a href="../../README.md">English</a> ·
  <a href="README.vi.md">Tiếng Việt</a> ·
  <a href="README.zh.md">简体中文</a> ·
  <a href="README.es.md">Español</a> ·
  <b>Português</b> ·
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

## Instalação

Baixe a versão mais recente em **[Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest)**:

| Plataforma | Arquivo |
|---|---|
| 🪟 **Windows** | `G-Labs-Studio-win.exe` — execute o instalador (admin/UAC) |
| 🍎 **macOS (Apple Silicon)** | `G-Labs-Studio-mac-arm64.dmg` |
| 🍎 **macOS (Intel)** | `G-Labs-Studio-mac-intel.dmg` |

**Primeira abertura no macOS** — o app não é assinado pela Apple, então o macOS o coloca em quarentena. Abra-o pela primeira vez com **clique com o botão direito → Open**, ou remova a marca pelo Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"
```

**Você precisa de uma conta G-Labs.** Abra o app, entre com o Google e escolha um plano. Os planos (**FREE / PLUS / MAX**) desbloqueiam diferentes ferramentas e modelos; você pode comprar um de dentro do app (QR bancário, PayPal ou USDT). Uma conta roda em **uma máquina por vez** — entrar em outro lugar desconecta a máquina anterior. O selo no canto inferior esquerdo da barra lateral mostra seu nível atual.

O app **se atualiza sozinho**: verifica o GitHub Releases na inicialização e pode baixar e instalar a nova versão de dentro do app.

---

## Primeira execução

1. **Abra o app e entre com o Google.** O selo de nível (canto inferior esquerdo) confirma seu plano.
2. **Conecte as contas das ferramentas que você vai usar** (Settings → a aba de conta correspondente):
   - Contas **Google** → Flow Image / Flow Video
   - Contas **ChatGPT** → GPT Image 2
   - Contas **Meta** → Meta Media
   - **Grok** → funciona pela sua aba `grok.com` com login feito, por meio da extensão de navegador complementar (Auth Helper) — sem pool de contas
   Cada aba de conta mostra **"Active: N accounts"** na barra de título para você saber quantas estão utilizáveis.
3. **Escolha uma página na barra lateral esquerda** e comece a gerar. Toda página de geração segue o mesmo ritmo: digite ou importe prompts à esquerda, eles caem em uma **tabela** à direita, e então pressione **Run**.

Todo cabeçalho de página traz uma **barra de status** ao vivo — *Running · Queued · Done · Failed · Accounts* — para você ver o lote de relance. Clique em **Queued** para abrir o gerenciador de fila e em **Accounts** para ir às configurações de conta.

---

## Recursos

- **Todos os grandes geradores, um app** — Google Flow (imagem + vídeo), Grok Imagine, Meta AI (vibes.ai) e OpenAI GPT Image 2, cada um em sua própria página com os modelos e proporções que aquele provedor suporta.
- **Feito para lotes** — cole uma lista de prompts (um por linha) ou importe um arquivo `.txt`/Excel; cada um vira uma linha. Imagens de referência são combinadas automaticamente pelo nome do arquivo. Execute a lista inteira com a concorrência que você escolher.
- **Adicione primeiro, execute quando estiver pronto** — as linhas vão para uma fila; **Run / Pause / Stop** são separados. Nada começa até você mandar, e um gerenciador de fila permite reordenar e inspecionar.
- **Biblioteca de personagens** — salve um personagem uma vez (imagem de referência + a própria voz + notas) e insira-o em qualquer prompt com `@name`; o vídeo mantém a aparência e a voz daquele personagem.
- **Workflow (grafo de nós)** — conecte nós em um pipeline: prompt → imagem → vídeo → extrair último quadro → próximo vídeo, além de um nó **Merge Video** que une dois clipes com cortes e transições (crossfade, wipe, slide, dissolve…). Nós de lote repetem toda a cadeia por prompt ou por imagem.
- **Webhook API** — um servidor REST local para que scripts e agentes de IA possam enviar tarefas de image/video/Grok/Meta/OpenAI e consultar os resultados.
- **Image Upscaler** e um **Video Editor** (cortar, juntar, apresentação de slides) para a finalização.
- **Resiliente** — os resultados são verificados e salvos automaticamente; as sessões são restauradas; linhas que falham são repetidas.
- **Tema escuro / claro**, interface conforme o nível, e **15 idiomas**.

---

## Páginas

### 🖼 Flow Image — geração de imagens do Google Flow

![Flow Image](../screenshots/01-image.png)

Gere imagens em lote com **Nano Banana Pro / 2 / Lite**. Escolha o modelo, a proporção e a resolução (**1K / 2K / 4K** — 2K/4K usam o upscaler do modelo), defina quantas linhas rodam de uma vez e o atraso entre elas. Cole prompts (ou importe um arquivo), anexe imagens de referência por linha (arraste uma pasta e elas se combinam automaticamente pelo nome do arquivo), e use `@name` para trazer personagens. **Run** envia a lista inteira para a fila.

### 🎬 Flow Video — Veo &amp; Omni Flash

![Flow Video](../screenshots/02-flow-video.png)

Três abas: **Text / Frames → Video** (um prompt de texto, ou um quadro inicial/final), **Image / Video ingredients → Video** (imagens de referência ou um vídeo de referência), e **Scene stitch → Video**. Modelos: **Veo 3.1 Fast / Lite / Quality** e **Omni Flash**. Escolha a proporção, o upscale (720p / 1080p / 4K) e a seed. Passe o cursor sobre o **?** na barra de abas para uma explicação simples sobre frames versus ingredients.

### 🤖 Grok Media — Grok Imagine

![Grok Media](../screenshots/03-grok.png)

Text-to-image, image-to-image, text-to-video e image-to-video pelo Grok Imagine (sua aba `grok.com` com login feito, por meio da extensão Auth Helper). As imagens oferecem **8 proporções** (incl. 4:3, 21:9, 5:2); o vídeo é gerado em **480p / 720p / 1080p**. Image-to-video tem dois modos: **First frame** (a imagem abre o clipe) e **Reference** (até 14 imagens de orientação).

### 🎨 Meta Media — Meta AI (vibes.ai)

![Meta Media](../screenshots/04-meta.png)

Geração de imagem e vídeo pelo Meta AI. Modos: text-to-image, image-to-image (componentes Character / Scene / Style), text-to-video e image-to-video (quadro inicial / final).

### ✨ GPT Image 2 — OpenAI

![GPT Image 2](../screenshots/05-openai.png)

Gere com o OpenAI **GPT Image 2** usando suas contas ChatGPT, com até 5 imagens de referência. Escolha a proporção (10 opções, incluindo 21:9, 4:5 e **custom** — onde você escreve a proporção no prompt), a qualidade, o modo de prompt, o esforço de raciocínio e a busca na web.

### 🔍 Image Upscaler

![Image Upscaler](../screenshots/06-upscaler.png)

Amplie uma pasta de imagens localmente — escolha o alvo e deixe processar a fila, com progresso e status por linha (processing / done / error).

### 👤 Characters

![Characters](../screenshots/07-character.png)

Crie uma biblioteca de personagens reutilizáveis: uma imagem de referência, uma voz personalizada opcional e notas de aparência/personalidade. Marque-os com `@name` em qualquer prompt do Flow e a geração preservará essa identidade.

### 🔗 Workflow

![Workflow](../screenshots/08-workflow.png)

Um canvas visual de nós. Clique com o botão direito no soquete de um nó e o menu oferece apenas os nós que se encaixam — escolha um e ele se conecta automaticamente. Encadeie prompt → generate → video → **Extract Frame** → próximo vídeo, e use **Merge Video** para unir dois clipes (corte cada ponta, escolha uma transição). Salve/carregue o grafo inteiro como um arquivo `.json`; **Run Flow** o executa de ponta a ponta.

### 🌐 Webhook API

![Webhook API](../screenshots/09-webhook.png)

Transforme o app em um servidor de automação local. Inicie-o, copie sua API key, e faça POST de tarefas para `/api/image/generate`, `/api/video/generate`, `/api/grok/generate`, `/api/meta/generate` ou `/api/openai/generate`, e então consulte `/api/status/<id>`. A página lista cada modelo e as proporções que ele suporta. Esquema completo: [`docs/WEBHOOK_INTEGRATION.en.md`](../WEBHOOK_INTEGRATION.en.md).

---

## Onde as coisas ficam

| O quê | macOS | Windows |
|---|---|---|
| Saída (imagens / vídeos) | `~/Documents/G-Labs Studio` | `%USERPROFILE%\Documents\G-Labs Studio` |
| Configurações, sessões, contas | `~/Library/Application Support/G-Labs Studio` | `%APPDATA%\G-Labs Studio` |

Suas configurações, listas de prompts, sessões, biblioteca de personagens e lista de contas são salvas e restauradas na próxima vez que você abrir o app.

---

## Solução de problemas

**Tudo está bloqueado / a tela de compra fica abrindo** — seu plano expirou, ou a conta entrou em outra máquina. Verifique o selo de nível (canto inferior esquerdo) e renove.

**Uma geração do Grok não faz nada** — o Grok funciona pela sua aba `grok.com`. Instale/ative a extensão de navegador **Auth Helper** (Settings → Grok) e certifique-se de estar logado no grok.com.

**"Active: 0 accounts" em uma página** — adicione ou reative uma conta na aba de conta daquela página (Settings), ou o token dela expirou — pressione **Refresh all**.

**O macOS diz que o app está danificado / não pode ser aberto** — ele não é assinado pela Apple. Clique com o botão direito → **Open** na primeira vez, ou execute `xattr -dr com.apple.quarantine "/Applications/G-Labs Studio.app"`.

**Uma atualização não instala** — baixe a versão mais recente manualmente em [Releases](https://github.com/duckmartians/G-Labs-Studio/releases/latest).
