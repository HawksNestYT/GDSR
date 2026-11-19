# Phase 1b — MacBook: Offline AI + Library Copy #2

The Mac runs the same stack ([stack.md](stack.md)) with llama.cpp on Apple Metal, which is fast and power-efficient. LM Studio / Ollama are handy extras for trying out models.

## AI (pick one or both)
- [ ] **LM Studio** (lmstudio.ai) — easiest, a GUI with a built-in model browser
- [ ] **Ollama** (ollama.com) — can also serve AI to other devices on your network
  ```bash
  # after installing the Ollama app
  ollama pull llama3.1:8b
  ollama pull qwen3:8b
  ollama run qwen3:8b
  ```
- [ ] Optional chat UI with document upload: **Open WebUI** or **AnythingLLM** (AnythingLLM has a simple desktop app)

## Model size by Mac RAM (rough)
| RAM | Try |
|---|---|
| 8 GB | 3–4B models (Gemma/Qwen/Llama 3.2 3B) |
| 16 GB | 7–9B, maybe 12–14B |
| 24–36 GB | 14–32B — this is where quality jumps |
| 48 GB+ | 32B–70B |

Download 2–3 models of different sizes: a small fast one, and the largest that runs smoothly.

## Library copy #2
- [ ] **Kiwix desktop** for Mac + the same ZIMs as the laptop hub (or at least WikiMed, Wikipedia, survival packs)
- [ ] **Offline maps:** Organic Maps on the Mac (via the iPad app on Apple Silicon) or keep the map files on the phones
- [ ] Keep the PDF folder synced (copy, don't rely on iCloud)

## Checklist
- [ ] Record Mac chip/RAM in [inventory.md](inventory.md)
- [ ] Install LM Studio or Ollama, download models
- [ ] Load your survival PDFs into a document-chat tool; test 5 questions
- [ ] Airplane-mode test: everything works with Wi‑Fi off
- [ ] Note battery life during heavy AI use in [log.md](log.md)
