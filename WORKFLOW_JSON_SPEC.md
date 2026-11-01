# G-Labs Automation - Workflow JSON Specification

> Audience: developers and AI agents that need to **generate a `.json` workflow file**
> the G-Labs Automation **Workflow** page can load (toolbar → **Open Flow**, or drop the
> file into `.../workflow/sample/`).
> Goal: everything needed to emit a valid, loadable node graph - the file schema, every
> node type with its sockets and settings, how to wire nodes, and a complete example.

A workflow is a **node graph**: nodes (prompt, image/video generators, loaders…) connected
by edges. When the user clicks **RUN FLOW**, nodes execute in topological order (upstream
first); each node passes its output (a prompt string, an image path, or a video path) to the
nodes wired to it.

---

## 1. Top-level file structure

```json
{
  "nodes":  [ <node>, <node>, ... ],
  "edges":  [ <edge>, <edge>, ... ],
  "groups": []
}
```

- `nodes` - array of node objects (see §3). **Order matters**: edges reference nodes by
  their **0-based index in this array**, NOT by `id`.
- `edges` - array of connections (see §4).
- `groups` - visual node grouping. Optional; use `[]`.

---

## 2. Core concepts

- **Sockets.** Each node has input sockets (left) and output sockets (right). Sockets carry
  a **data type**: `string` (a prompt), `image`, `video`, or `any`. An edge is valid only
  when the source output type is compatible with the target input type (`any` matches
  anything).
- **Socket order.** Input socket **index 0 is always the Prompt** for generator nodes;
  indices 1+ are reference-image sockets. Edges target sockets by index, so the number and
  order of a node's `inputs` must match what its settings imply (see per-node tables).
- **Dataflow.** A node reads its inputs from the nodes wired into its sockets:
  - Prompt socket ← a `prompt` node (or `batch_prompt` / `prompt_writer`) output.
  - Reference/image socket ← any node whose output is an image (`reference`, `batch_loader`,
    `frame_extract`, or another generator that outputs an image).
- **Execution.** Only nodes reachable/complete run. A node missing a required input is
  skipped. A cycle aborts the run with an error.

---

## 3. Node object

Every node has these fields:

| Field | Type | Required | Notes |
|-------|------|:--------:|-------|
| `id` | int | ✅ | Unique per node (any distinct integers, e.g. 1, 2, 3…). |
| `type` | string | ✅ | One of the node types in §3.1. |
| `title` | string | ❌ | Display label. Re-translated on load, so any value is fine. |
| `x`, `y` | number | ✅ | Canvas position (top-left). Space nodes out, e.g. 400px apart. |
| `w`, `h` | number | ❌ | Size. Generator nodes use `400`×`400`; prompt `400`×`300`. Defaults are applied if omitted. |
| `disabled` | bool | ❌ | `true` = node is off (skipped at run). Default `false`. |
| `skipped` | bool | ❌ | `true` = skip this node but keep it. Default `false`. |
| `inputs` | string[] | ✅ | Input socket **labels** - the array **length = number of input sockets** (this is what edges target). Text is cosmetic; the count matters. |
| `outputs` | string[] | ✅ | Output socket labels (usually one). |
| `values` | object | ✅ | Widget settings - keys/values per node type (§3.1). Use `{}` if none. |
| `ref_mode` | string | ❌ | Reference nodes only: `"pro"`. |

**`values` combo rule:** for dropdown settings, use the **data value** listed in the tables
below (e.g. `"t2v"`, `"landscape_16_9"`), not the display label. On load the app resolves
it by data first, then by visible text.

### 3.1 Node types

There are **12** node types. Each block below lists the output type (**→ type**), the input
sockets, and a **values** table with every setting key, its accepted values, and how it
serializes. Two labels are used throughout:

- **stable** - the accepted values are fixed and safe to hardcode in a `.json`.
- **server** - the option list is fetched from the account's server config at runtime, so the
  exact value depends on the logged-in tier (see the note after `video_generate`).

Combos serialize their **data value** when one exists, else their visible text; the app
resolves on load by data first, then by text. Where a table says *"index/text"* the combo has
no data value - omit the key to keep its default rather than hardcoding localized text.

---

#### `prompt` - a text prompt  → `string`
- **inputs:** `[]` (none).  **outputs:** `["Prompt"]`.

| key | values | notes |
|-----|--------|-------|
| `prompt` | any string | the prompt text |

---

#### `batch_prompt` - many prompts; loops the whole downstream chain once per line  → `string`
- **inputs:** `[]`.  **outputs:** `["Prompt"]`.

| key | values | notes |
|-----|--------|-------|
| `prompt_list` | multi-line string | one prompt per line |
| `mode` | index/text: Sequential \| Random | **stable**; omit ⇒ Sequential |
| `limit_mode`, `limit_val` | index/text + number | optional cap; omit ⇒ use all lines |

---

#### `prompt_writer` - an LLM writes a finished prompt from a short idea (+ reference images)  → `string`
- **inputs:** `["Prompt", "Ref 1"]`: socket 0 = optional context text (from `prompt` / `batch_prompt` /
  another `prompt_writer`); sockets 1+ = reference images the LLM looks at (up to **4**; the node adds one
  empty image socket each time the last one is connected, so list one more label per extra image wired).
  **outputs:** `["Prompt"]`. Default size `400`×`550`.
- Output = the finished prompt text only (no title / notes), ready for the Prompt socket of `generate`,
  `video_generate`, `grok`, `meta` or `openai`. `@tags` written in the idea / context are kept inline.
- Needs a **PLUS** (or higher) license and an LLM source set up in the app's **Settings › LLM Assistant**
  (Claude CLI, Antigravity CLI, Codex CLI, 9Router or a direct API key). Runs once per batch iteration.

| key | values | notes |
|-----|--------|-------|
| `model` | `""` or a model selector | `""` = use the model chosen in Settings › LLM Assistant (recommended in shared files). Otherwise e.g. `"claude-cli:claude-haiku-4-5"`, `"agy"`, `"codex"`, `"gemini:<model>"`, or a 9Router model id; machine-dependent (must be installed / signed in there) |
| `target` | `"image"` \| `"video"` | **stable**; kind of prompt to write |
| `category` | image: `default`, `photo_portrait`, `product_commercial`, `cinematic_still`, `illustration_anime`, `render_3d`, `infographic_text`, `logo_minimal`, `architecture_interior`, `food_drink`, `fashion_editorial`, `character_sheet`, `nature_wildlife` · video: `default`, `cinematic_narrative`, `documentary_nature`, `product_commercial_video`, `dialogue_scene`, `action_sequence`, `establishing_timelapse`, `music_video`, `animation_style`, `ugc_vlog`, `asmr_closeup`, `horror_suspense` | **stable**; must belong to `target`; omit ⇒ `default` |
| `lang` | `"en"` \| `"same"` | **stable**; `en` = English prompt (spoken dialogue and on-image text keep their own language), `same` = same language as the idea |
| `idea` | multi-line string | the short idea / instructions; may be empty when socket 0 or images are wired |
| `result` | string | last prompt written (display only, ignored at run; use `""`) |

---

#### `reference` - one image file from disk  → `image`
- **inputs:** `[]`.  **outputs:** `["Image"]`.  Add top-level `"ref_mode": "pro"`.

| key | values | notes |
|-----|--------|-------|
| `file_path` | absolute path | the file must exist on the machine running the app |

---

#### `batch_loader` - a folder of images; loops once per image  → `image`
- **inputs:** `[]`.  **outputs:** `["Image"]`.

| key | values | notes |
|-----|--------|-------|
| `file_path` | absolute folder path | folder must exist on the machine |
| `sort_mode` | index/text | **stable**; optional, omit ⇒ default order |
| `limit_mode`, `limit_val` | index/text + number | optional cap; omit ⇒ use all |

---

#### `frame_extract` - pull the last frame of a video as an image  → `image`
- **inputs:** `["Video"]` (wire a video-producing node here).  **outputs:** `["Image"]`.
- **values:** `{}` (no settings).

---

#### `render` - merge two videos into one (local ffmpeg)  → `video`
- **inputs:** `["Video A", "Video B"]` (index 0 = first clip, index 1 = second clip; wire a video-producing node into each).  **outputs:** `["Video"]`.
- Runs ffmpeg **locally** (no account). Video B is auto-normalized to A's size/fps. Optional trim of each clip's head/tail, plus a transition between them.

| key | values | notes |
|-----|--------|-------|
| `trim_a_head` / `trim_a_tail` | seconds (string, e.g. `"0"`, `"1.5"`) | cut from the start / end of Video A; omit ⇒ `0` |
| `trim_b_head` / `trim_b_tail` | seconds (string) | cut from the start / end of Video B; omit ⇒ `0` |
| `transition` | `"cut"` \| `"fade"` \| `"dissolve"` \| `"wipeleft"` \| `"wiperight"` \| `"slideup"` \| `"slidedown"` \| `"circleopen"` \| `"radial"` \| `"fadeblack"` | **stable**; `"cut"` = hard concat (no crossfade) |
| `xfade_dur` | seconds (string, e.g. `"0.5"`) | transition length; ignored when `transition` = `"cut"` |

---

#### `generate` - Flow image generator (Google)  → `image`
- **inputs:** `["Prompt", "Ref 1"]` - index 0 prompt; 1+ optional image refs (auto-grow).  **outputs:** `["Image"]`.

| key | values | notes |
|-----|--------|-------|
| `model` | `"GEM_PIX_2"` (Nano Banana Pro) \| `"NARWHAL"` (Nano Banana 2) \| `"HARBOR_SEAL"` (Nano Banana 2 Lite) | **server default** - all three support upscale |
| `ratio` | `"IMAGE_ASPECT_RATIO_LANDSCAPE"` (16:9) \| `"IMAGE_ASPECT_RATIO_LANDSCAPE_FOUR_THREE"` (4:3) \| `"IMAGE_ASPECT_RATIO_PORTRAIT_THREE_FOUR"` (3:4) \| `"IMAGE_ASPECT_RATIO_PORTRAIT"` (9:16) \| `"IMAGE_ASPECT_RATIO_SQUARE"` (1:1) | **server default**; store the API constant, not the UI key |
| `res_group` | `"1K"` \| `"2K"` \| `"4K"` | **stable** (button text); 2K/4K need an upscale-capable model (all current models qualify) |
| `seed_mode` | index/text: Random \| Fixed | omit ⇒ Random |
| `seed` | number string | only when `seed_mode` = Fixed |

---

#### `video_generate` - Veo / Omni Flash video generator (Google)  → `video`
- **inputs (by `mode`):**
  - `image` → `["Prompt", "Start Image", "End Image (optional)"]` (fixed 3 sockets)
  - `components` → `["Prompt", "Ref 1", ...]` (auto-grow refs)
- **outputs:** `["Video"]`.

| key | values | notes |
|-----|--------|-------|
| `mode` | `"image"` \| `"components"` | **stable** |
| `model` | `"fast"` (Veo Fast) \| `"fast_lite"` (Veo Lite) \| `"lite_relaxed"` (Veo Lower) \| `"quality"` (Veo Quality) \| `"omni_flash"` (Omni Flash) | **server default**; default `"fast"` |
| `ratio` | `"VIDEO_ASPECT_RATIO_LANDSCAPE"` (16:9) \| `"VIDEO_ASPECT_RATIO_PORTRAIT"` (9:16) | **stable** |
| `resolution` | `"720p"` \| `"1080p"` \| `"4K"` | **stable** |
| `seed_mode` | index/text: Random \| Fixed | omit ⇒ Random |
| `seed` | number string | only when `seed_mode` = Fixed |

> **`model` values are server-configured.** The `generate` `model`/`ratio` and `video_generate`
> `model` lists above are the **current server defaults** (from `RUNTIME_CONFIG`); an admin can
> add/rename models, so if a value is rejected on load, rebuild the node in the UI and **Save
> Flow** to read the live key. Every other value in both nodes is **stable**.

---

#### `grok` - Grok image/video generator  → `any` (image in t2i/i2i, video in t2v/i2v)
- **inputs (by `mode`):** `t2i`/`t2v` → `["Prompt"]`; `i2i`/`i2v` → `["Prompt", "Ref 1"]`.
- **outputs:** `["Output"]`.

| key | values | notes |
|-----|--------|-------|
| `mode` | `"t2i"` \| `"i2i"` \| `"t2v"` \| `"i2v"` | **stable** |
| `ratio` | image (`t2i`/`i2i`): `"9:16"` \| `"16:9"` \| `"1:1"` \| `"2:3"` \| `"3:2"` \| `"4:3"` \| `"21:9"` \| `"5:2"`; video (`t2v`/`i2v`): `"9:16"` \| `"16:9"` \| `"1:1"` \| `"2:3"` \| `"3:2"` | **stable** |
| `video_length` | `6` \| `10` \| `15` | video modes only |
| `resolution` | `"480p"` \| `"720p"` \| `"1080p"` | video modes only |

---

#### `meta` - Meta AI (vibes.ai) image/video generator  → `any` (image in t2i/i2i, video in t2v/i2v)
- **inputs (by `mode`):**
  - `t2i` / `t2v` → `["Prompt"]`
  - `i2i` → `["Prompt", "Character", "Scene", "Style"]` (named component sockets)
  - `i2v` → `["Prompt", "Start Image", "End Image (optional)"]`
- **outputs:** `["Output"]`.

| key | values | notes |
|-----|--------|-------|
| `mode` | `"t2i"` \| `"i2i"` \| `"t2v"` \| `"i2v"` | **stable** |
| `ratio` | `"9:16"` \| `"16:9"` \| `"1:1"` | **stable** |
| `resolution` | `"480p"` \| `"720p"` | video modes only |
| `count` | `1` \| `2` \| `3` \| `4` | images per run |

---

#### `openai` - OpenAI GPT Image 2  → `image`
- **inputs:** `["Prompt", "Ref 1"]` - index 0 prompt; 1+ optional image refs, **up to 5** (auto-grow).  **outputs:** `["Image"]`.

| key | values | notes |
|-----|--------|-------|
| `ratio` | `"square"` \| `"landscape_3_2"` \| `"landscape_4_3"` \| `"landscape_16_9"` \| `"landscape_21_9"` \| `"portrait_2_3"` \| `"portrait_3_4"` \| `"portrait_4_5"` \| `"portrait_9_16"` \| `"custom"` (ratio written in the prompt) | **stable** |
| `quality` | `"low"` \| `"medium"` \| `"high"` | **stable** |
| `prompt_mode` | `"auto"` \| `"direct"` | **stable** |
| `reasoning` | `"none"` \| `"low"` \| `"medium"` \| `"high"` \| `"xhigh"` \| `"max"` | **stable** |
| `web_search` | `true` \| `false` | boolean |

---

## 4. Connection rules - what connects to what

Wiring is governed by **socket data types**. An edge is valid only when the source's output
type matches the target input socket's type. There are four types: `string`, `image`,
`video`, and `any`. `any` matches everything (it's the mode-dependent output of `grok`/`meta`).

### 4.1 Output type of each node (what it PRODUCES)

| Node | Output type | Meaning |
|------|-------------|---------|
| `prompt` | `string` | a text prompt |
| `batch_prompt` | `string` | a text prompt (loops per line) |
| `prompt_writer` | `string` | a prompt written by the LLM |
| `reference` | `image` | an image file |
| `batch_loader` | `image` | an image (loops per file) |
| `frame_extract` | `image` | a still frame |
| `generate` | `image` | a generated image |
| `openai` | `image` | a generated image |
| `video_generate` | `video` | a generated video |
| `render` | `video` | two videos merged into one |
| `grok` | `any` | **image** in `t2i`/`i2i`, **video** in `t2v`/`i2v` |
| `meta` | `any` | **image** in `t2i`/`i2i`, **video** in `t2v`/`i2v` |

### 4.2 Input sockets of each node (what each socket ACCEPTS)

Socket **index** is the value you put in an edge's `end_socket`.

| Node | idx | Socket | Accepts (type) | Wire a… |
|------|:---:|--------|----------------|---------|
| `prompt` | - | (no inputs) | - | - |
| `batch_prompt` | - | (no inputs) | - | - |
| `reference` | - | (no inputs) | - | - |
| `batch_loader` | - | (no inputs) | - | - |
| `prompt_writer` | 0 | Prompt / context (opt.) | `string` | `prompt` / `batch_prompt` / `prompt_writer` |
| `prompt_writer` | 1+ | Ref image (≤4) | `image` | image producer |
| `generate` | 0 | Prompt | `string` | `prompt` / `batch_prompt` / `prompt_writer` |
| `generate` | 1+ | Ref image | `image` | `reference` / `batch_loader` / `frame_extract` / image generator |
| `openai` | 0 | Prompt | `string` | `prompt` / `batch_prompt` / `prompt_writer` |
| `openai` | 1+ | Ref image (≤5) | `image` | image producer (above) |
| `video_generate` | 0 | Prompt | `string` | `prompt` / `batch_prompt` / `prompt_writer` |
| `video_generate` | 1 | Start Image | `image` | image producer |
| `video_generate` | 2 | End Image (opt.) | `image` | image producer |
| `grok` | 0 | Prompt | `string` | `prompt` / `batch_prompt` / `prompt_writer` |
| `grok` | 1 | Ref image (`i2i`/`i2v`) | `image` | image producer |
| `meta` | 0 | Prompt | `string` | `prompt` / `batch_prompt` / `prompt_writer` |
| `meta` | 1 | Character (`i2i`) / Start (`i2v`) | `image` | image producer |
| `meta` | 2 | Scene (`i2i`) / End (`i2v`, opt.) | `image` | image producer |
| `meta` | 3 | Style (`i2i`) | `image` | image producer |
| `frame_extract` | 0 | Video | `video` | `video_generate` / `grok`(video) / `meta`(video) / `render` |
| `render` | 0 | Video A | `video` | any video producer |
| `render` | 1 | Video B | `video` | any video producer |

### 4.3 Compatibility summary (source output → target socket)

- **`string`** (prompt / batch_prompt / prompt_writer) → **only the Prompt socket** (index 0) of
  `generate` / `video_generate` / `grok` / `meta` / `openai` / `prompt_writer`.
  Never wire a string into a Ref/image socket, and never wire an image/video into a Prompt
  socket. (The prompt socket accepts **one** connection.)
- **`image`** (reference / batch_loader / frame_extract / generate / openai / grok-image /
  meta-image) → any **Ref / Start / End / Character / Scene / Style** image socket. An image
  never feeds a Prompt socket or a Video socket.
- **`video`** (video_generate / grok-video / meta-video / render) → the `Video` socket of
  `frame_extract`, or the `Video A` / `Video B` sockets of `render`.
- **`any`** output (`grok` / `meta`): choose the target by the node's **mode** - in an image
  mode wire it like an `image`; in a video mode wire it like a `video`. (The type check
  permits `any`↔anything, so the app won't stop a wrong wiring at edit time - it just fails
  at run. Follow the mode.)

### 4.4 Edge object

```json
{ "start_node": 0, "start_socket": 0, "end_node": 1, "end_socket": 0 }
```

- `start_node` / `end_node` - **0-based INDEX into the `nodes` array** (position, NOT `id`).
- `start_socket` - index into the source node's **output** sockets (almost always `0`).
- `end_socket` - index into the target node's **input** sockets (see §4.2).

**A wiring is correct only when all three hold:** (1) the source output type is compatible
with the target socket type (§4.3), (2) `end_socket` exists for that node's current `mode`
(the `inputs` array is long enough - §5 rule 2), and (3) the Prompt socket (index 0) has at
most one incoming edge.

---

## 5. Authoring rules & gotchas

1. **Edges use array index, not `id`.** `start_node`/`end_node` are positions in `nodes`.
2. **Socket count must fit the mode.** For `meta`/`grok`/`video_generate`, set `mode` in
   `values` AND make `inputs` list the sockets that mode uses (e.g. `meta` `i2i` needs 4
   input sockets so `end_socket` 1/2/3 are valid for Character/Scene/Style).
3. **Combo values = data value**, not display text (except the index-based batch combos).
4. **`id` must be unique**; `title` is cosmetic (re-translated on load).
5. **Every generation chain needs a prompt source** feeding socket 0 (a `prompt`,
   `batch_prompt` or `prompt_writer` node), and image/video modes need their reference image(s) wired.
6. **Files must exist** on the machine running the app (`reference.file_path`,
   `batch_loader.file_path`).
7. Running requires a **PLUS/MAX** license and the relevant logged-in accounts (Google for
   generate/video, Grok session, Meta account, ChatGPT account for openai). `prompt_writer` also
   needs an LLM source in Settings › LLM Assistant.
8. **Blocked prompts are auto-fixed.** With *Settings › LLM Assistant › Auto-fix prompts when blocked* on
   (PLUS+), a `generate` / `video_generate` node whose prompt Google blocks for content (celebrity,
   sensitive content, minors, copyright...) is rewritten by the LLM and run again, at most 2 times.
   Blocked reference / input images are not rewritten.

---

## 6. Complete example

Prompt → **GPT Image 2** (16:9, high) and the same prompt → **Grok** text-to-video (720p) →
**Extract Frame**. This file loads as-is.

```json
{
  "nodes": [
    {
      "id": 1,
      "type": "prompt",
      "title": "Prompt",
      "x": -360, "y": 0, "w": 400, "h": 300,
      "inputs": [],
      "outputs": ["Prompt"],
      "values": { "prompt": "a red apple on a wooden table, soft daylight" }
    },
    {
      "id": 2,
      "type": "openai",
      "title": "GPT Image 2",
      "x": 80, "y": -140, "w": 400, "h": 400,
      "inputs": ["Prompt", "Ref 1"],
      "outputs": ["Image"],
      "values": {
        "ratio": "landscape_16_9",
        "quality": "high",
        "prompt_mode": "auto",
        "reasoning": "none",
        "web_search": false
      }
    },
    {
      "id": 3,
      "type": "grok",
      "title": "Grok - Text to Video",
      "x": 80, "y": 180, "w": 400, "h": 400,
      "inputs": ["Prompt"],
      "outputs": ["Output"],
      "values": {
        "mode": "t2v",
        "ratio": "9:16",
        "video_length": 6,
        "resolution": "720p"
      }
    },
    {
      "id": 4,
      "type": "frame_extract",
      "title": "Extract Frame",
      "x": 520, "y": 180, "w": 400, "h": 100,
      "inputs": ["Video"],
      "outputs": ["Image"],
      "values": {}
    }
  ],
  "edges": [
    { "start_node": 0, "start_socket": 0, "end_node": 1, "end_socket": 0 },
    { "start_node": 0, "start_socket": 0, "end_node": 2, "end_socket": 0 },
    { "start_node": 2, "start_socket": 0, "end_node": 3, "end_socket": 0 }
  ],
  "groups": []
}
```

Reading the edges: node index `0` (the prompt) feeds node index `1` (openai) socket 0 and
node index `2` (grok) socket 0; node index `2` (grok, video output) feeds node index `3`
(frame_extract) socket 0.

### 6.1 Meta AI image-to-image (named components)

A `reference` image wired into the **Character** socket (input index 1) of a `meta` node in
`i2i` mode:

```json
{
  "nodes": [
    { "id": 1, "type": "prompt", "title": "Prompt", "x": -360, "y": 0, "w": 400, "h": 300,
      "inputs": [], "outputs": ["Prompt"],
      "values": { "prompt": "the same character in a snowy forest" } },
    { "id": 2, "type": "reference", "title": "Character", "x": -360, "y": 260, "w": 400, "h": 320,
      "inputs": [], "outputs": ["Image"], "ref_mode": "pro",
      "values": { "file_path": "C:/images/hero.png" } },
    { "id": 3, "type": "meta", "title": "Meta AI", "x": 120, "y": 0, "w": 400, "h": 400,
      "inputs": ["Prompt", "Character", "Scene", "Style"], "outputs": ["Output"],
      "values": { "mode": "i2i", "ratio": "1:1", "resolution": "720p", "count": 1 } }
  ],
  "edges": [
    { "start_node": 0, "start_socket": 0, "end_node": 2, "end_socket": 0 },
    { "start_node": 1, "start_socket": 0, "end_node": 2, "end_socket": 1 }
  ],
  "groups": []
}
```

Here node index `1` (the reference) connects to `end_socket: 1` - the **Character** input of
the `meta` node. Use `end_socket` 2 for Scene, 3 for Style.

### 6.2 Batch + video-to-frame chain (all-stable nodes)

Exercises the nodes not shown above: `batch_prompt` (loops the chain per line) → `meta`
text-to-video → `frame_extract` (last frame) → `openai` image-to-image using that frame as a
reference. Every value here is **stable**, so the file loads and runs as-is.

```json
{
  "nodes": [
    { "id": 1, "type": "batch_prompt", "title": "Prompts", "x": -400, "y": 0, "w": 400, "h": 300,
      "inputs": [], "outputs": ["Prompt"],
      "values": { "prompt_list": "a paper boat on a puddle\na paper plane over a desk" } },
    { "id": 2, "type": "meta", "title": "Meta - Text to Video", "x": 60, "y": -160, "w": 400, "h": 400,
      "inputs": ["Prompt"], "outputs": ["Output"],
      "values": { "mode": "t2v", "ratio": "16:9", "resolution": "720p", "count": 1 } },
    { "id": 3, "type": "frame_extract", "title": "Last Frame", "x": 520, "y": -160, "w": 400, "h": 100,
      "inputs": ["Video"], "outputs": ["Image"], "values": {} },
    { "id": 4, "type": "openai", "title": "GPT Image 2", "x": 520, "y": 120, "w": 400, "h": 400,
      "inputs": ["Prompt", "Ref 1"], "outputs": ["Image"],
      "values": { "ratio": "landscape_16_9", "quality": "medium",
                  "prompt_mode": "auto", "reasoning": "none", "web_search": false } }
  ],
  "edges": [
    { "start_node": 0, "start_socket": 0, "end_node": 1, "end_socket": 0 },
    { "start_node": 0, "start_socket": 0, "end_node": 3, "end_socket": 0 },
    { "start_node": 1, "start_socket": 0, "end_node": 2, "end_socket": 0 },
    { "start_node": 2, "start_socket": 0, "end_node": 3, "end_socket": 1 }
  ],
  "groups": []
}
```

Edges: the `batch_prompt` (index 0) feeds both `meta` (index 1, socket 0) and `openai`
(index 3, socket 0); `meta`'s video output (index 1) feeds `frame_extract` (index 2); and the
extracted frame (index 2) feeds `openai`'s **Ref 1** socket (index 3, `end_socket: 1`).


### 6.3 Prompt Writer → GPT Image (LLM writes the prompt from an idea + a reference photo)

`prompt_writer` reads the idea and the wired photo, writes an image prompt in the
`product_commercial` category, and feeds it to `openai`, which also gets the same photo as a
reference. `model: ""` uses the model chosen in Settings › LLM Assistant.

```json
{
  "nodes": [
    { "id": 1, "type": "reference", "title": "Product photo", "x": -460, "y": 0, "w": 400, "h": 320,
      "ref_mode": "pro", "inputs": [], "outputs": ["Image"],
      "values": { "file_path": "C:/images/bottle.png" } },
    { "id": 2, "type": "prompt_writer", "title": "Prompt Writer", "x": 0, "y": 0, "w": 400, "h": 550,
      "inputs": ["Prompt", "Ref 1", "Ref 2"], "outputs": ["Prompt"],
      "values": { "model": "", "target": "image", "category": "product_commercial", "lang": "en",
                  "idea": "summer ad for this bottle on a sunny beach, headline FRESH", "result": "" } },
    { "id": 3, "type": "openai", "title": "GPT Image 2", "x": 460, "y": 0, "w": 400, "h": 400,
      "inputs": ["Prompt", "Ref 1"], "outputs": ["Image"],
      "values": { "ratio": "landscape_16_9", "quality": "medium",
                  "prompt_mode": "auto", "reasoning": "none", "web_search": false } }
  ],
  "edges": [
    { "start_node": 0, "start_socket": 0, "end_node": 1, "end_socket": 1 },
    { "start_node": 1, "start_socket": 0, "end_node": 2, "end_socket": 0 },
    { "start_node": 0, "start_socket": 0, "end_node": 2, "end_socket": 1 }
  ],
  "groups": []
}
```

Edges: the photo (index 0) feeds the writer's **Ref 1** (`end_socket: 1`; the writer lists
`"Ref 2"` too because it always keeps one empty image socket after the last connected one) and
`openai`'s **Ref 1**; the writer's prompt (index 1) feeds `openai`'s Prompt socket (index 2,
`end_socket: 0`).
