# The Stack — Our Own Offline Hub (no NOMAD)

We use the **same open content** NOMAD uses (Kiwix ZIM files, OpenStreetMap data, PDFs), but we build the interface and the AI layer ourselves. One codebase runs on every device:

| Device | CPU | AI acceleration | Role |
|---|---|---|---|
| Phone (Termux or Linux phone) | ARM64 | CPU (GPU backends experimental) | Pocket hub: small model, core content |
| 2070 laptop (Ubuntu) | x86-64 | NVIDIA CUDA | Main hub: full content, 7–9B models, serves the house |
| MacBook | ARM64 | Apple Metal | Strongest AI, copy #2 |

## Design principles
1. **Plain files, standard tools.** Everything is a file you can copy: `.zim`, `.pmtiles`, `.gguf`, `.pdf`. No databases that only work inside one app.
2. **Each piece runs on its own.** Library, maps, and AI are separate processes. If the AI breaks, the library still works.
3. **Browser is the UI.** One web dashboard on `localhost`, reachable by any device on the hotspot/router. Works the same on every device.
4. **No giant vector database.** We use Kiwix's built-in full-text search to find articles for the AI ("search-then-read"), instead of embedding all of Wikipedia (which is what costs NOMAD 5–10× disk).
5. **Same layout on every device**, so syncing is just copying folders.

## Components
```
                ┌───────────────────────────────────────────┐
  browser  ───► │  hub dashboard  (our code, :8080)         │
 (any device)   │   • search box → library / maps / ask AI  │
                │   • /ask → retrieval + LLM, cites sources │
                └──────┬───────────────┬──────────────┬─────┘
                       │               │              │
               kiwix-serve        pmtiles serve   llama-server
               (:8081)            (:8082)         (:8083)
               ZIM library +      offline vector  llama.cpp, any
               full-text search   map tiles       .gguf model
                       │               │              │
                   /hub/zim       /hub/maps      /hub/models
```

| Piece | Tool | Why |
|---|---|---|
| Library | **kiwix-serve** (kiwix-tools) | Serves every ZIM over HTTP with built-in full-text search. Static ARM64 + x86 builds exist |
| Maps | **PMTiles** file + **MapLibre GL JS** web viewer, served with `pmtiles serve` (or any server that supports HTTP range requests) | A single file per region, cut from the Protomaps planet build. Pure web, no app |
| Turn-by-turn | **Organic Maps / OsmAnd** app (fallback) | Offline routing is hard to build; these apps already do it well |
| AI runtime | **llama.cpp** `llama-server` | Fastest portable runtime: CPU/ARM, CUDA, and Metal from one codebase. OpenAI-compatible API + built-in chat UI |
| AI retrieval | Our code: kiwix full-text search → fetch top articles → pick best passages → LLM answers **with links to the source articles** | No 5–10× index. Answers you can verify |
| Personal docs | Small embedding model (llama.cpp) + **SQLite + sqlite-vec** index for *our own* PDFs only | That's a small set, so a real vector index is cheap here |
| Dashboard | Small Python (FastAPI) or Go app + a single HTML page | Runs in Termux, Ubuntu, and macOS |

## "Ask" flow (search-then-read)
1. User asks: *"how do I make oral rehydration solution"*
2. LLM (or simple keyword extraction) turns the question into 1–3 search queries
3. Query kiwix-serve full-text search across WikiMed, Wikipedia, survival ZIMs
4. Fetch the top ~5 articles, strip the HTML, split them into paragraphs
5. Rank paragraphs (BM25 first; small embedding model later if needed), keep the best ~3–6
6. LLM answers **only from those passages** and lists the sources as clickable links into the local library
7. If nothing relevant is found, say so instead of guessing

This makes a small phone model much more trustworthy: it reads the source instead of answering from memory.

## Folder layout (identical on every device)
```
hub/
  zim/        *.zim             (Wikipedia, WikiMed, WikiHow, iFixit, survival packs)
  maps/       *.pmtiles + style/fonts/sprites (all offline!)
  models/     *.gguf            (chat model(s) + embedding model)
  docs/       *.pdf             (Hesperian, Army manuals, device manuals)
  index/      personal-docs.sqlite
  app/        dashboard code
  bin/        kiwix-serve, pmtiles, llama-server binaries for this platform
```

## Gotchas to remember
- **Map fonts/sprites must be local.** Most MapLibre styles fetch glyphs from the internet, so download them into `maps/` and point the style at them.
- **Android kills background processes** (the "phantom process killer"). Turn off child-process restrictions in Developer Options (Android 14+), or disable it with an ADB command on 12–13. See [phone-linux.md](phone-linux.md).
- **Model memory:** a quantized model needs roughly its file size in RAM, plus ~1–2 GB for context. Phones have to leave room for the OS.

## Build milestones
- [ ] **M1** — `hub/` layout + kiwix-serve running with WikiMed on the laptop and the phone
- [ ] **M2** — llama-server running a model on both; measure tokens/sec
- [ ] **M3** — dashboard v0: one page linking library, maps, chat
- [ ] **M4** — offline map viewer (PMTiles + MapLibre, local fonts)
- [ ] **M5** — `/ask` search-then-read retrieval with source links
- [ ] **M6** — personal-docs index (PDFs → sqlite-vec)
- [ ] **M7** — one-command start script per platform + autostart on boot
- [ ] **M8** — sync script: laptop → phones/drives (rsync or copy)
