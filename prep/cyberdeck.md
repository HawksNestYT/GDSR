# Cyberdeck Build Plan — "The Deck"

A rugged, self-powered field station: offline library + local AI + maps + comms + network, in a waterproof, drop-resistant case. Prices are rough (late 2026) and RAM-heavy hardware prices have been volatile, so re-check before buying.

## Design rules
1. **Transport sealed, operate open.** Closed = waterproof and drop-resistant (IP65–67 case). Open = vents and fans running; keep it out of direct rain.
2. **Modular:** every part unplugs and replaces without tools (USB‑C, HDMI, XT60/Anderson, SMA). Nothing soldered on the critical path.
3. **Degrades gracefully:** screen dies → HDMI to anything, or a phone browser over Wi‑Fi. Computer dies → the phones have the core library. Internal battery dies → external power station / solar / car.
4. **Two of every input:** touchscreen + keyboard trackpad. Wired + wireless.
5. **Heat is the enemy.** A sealed box + a 100 W computer = an oven. Design airflow from day one.
6. **Self-documenting:** labeled ports, a quick-start card + Wi‑Fi info in the lid, wiring diagram in this repo.
7. **Printed parts in PETG/ASA, not PLA.** PLA softens around 55–60 °C, which a hot car beats easily.

## Layout (concept)
```
 LID ─────────────────────────────────────────────┐
 │  15.6" matte touchscreen behind polycarbonate  │
 │  pocket: quick-start card, cables, antenna     │
 └────────────────────────────────────────────────┘
 BASE (top deck plate, 3D-printed tiles or cut HDPE/aluminum)
 ┌────────────────────────────────────────────────┐
 │ [keyboard + trackpad, removable]   [I/O panel] │
 │                                    USB-C  HDMI │
 │ [volt/amp meter] [master switch]   RJ45  SMA×2 │
 │                                    XT60 power  │
 ├──── under the plate ───────────────────────────┤
 │ compute │ battery + fuse block │ router │ SDR  │
 │ (fans → vents)                │ Meshtastic     │
 └────────────────────────────────────────────────┘
```

## Subsystems

### 1. Case — pick it LAST (after the parts, measure, then buy)
| Option | Rating | Est. $ | Notes |
|---|---|---|---|
| **Harbor Freight Apache 4800 / 5800** | IP65 | 50–90 | Best value. Fine for rain/drops when closed |
| Nanuk 925 / 935 | IP67 | 180–300 | Tougher latches, lighter |
| Pelican 1495 / 1490 / Air | IP67 | 200–350 | Gold standard; laptop-sized |
- Add **pressure-purge valve** (most good cases have one), **IP67 cable glands** or bulkhead connectors for anything that passes through the wall
- Vents: printed louvered vent + fan with a **screw-on cover** for transport mode

### 2. Compute — "a competent AI model"
The model you can run depends on **memory the AI can use**. In 2025–26, **mixture-of-experts (MoE)** models (e.g. the gpt-oss / Qwen3‑30B‑A3B class) give big-model quality at small-model speed. That favors machines with lots of unified/shared memory.

**Decision:** the 2070 laptop stays whole as the home hub server + dev bench. The deck gets its own mini PC.

Two numbers decide AI ability: **memory size** (which models fit) and **memory bandwidth** (how fast they talk). For offline *vibecoding*, also **prompt processing** (how fast it reads big code files), where NVIDIA is strongest.

| Tier | Machine | Memory | Best models it runs (2025–26 class) | Offline vibecoding | Power (idle / AI) | Power input | Est. $ |
|---|---|---|---|---|---|---|---|
| **1 — Budget** | Ryzen 7 8845HS / Ryzen AI 9 HX 370 mini PC, **64 GB** | 64 GB DDR5 (shared) | gpt-oss-20b, Qwen3‑30B‑A3B / Qwen3‑Coder‑30B‑A3B (MoE) | Small scripts, fixes, explanations | ~8–12 W / 45–65 W | often 19 V barrel or USB‑C | 600–1,200 (RAM prices up — check) |
| **2 — Sweet spot ★** | **Ryzen AI Max+ 395 "Strix Halo", 128 GB** (Framework Desktop, GMKtec EVO‑X2, Beelink, etc.) | 128 GB unified, ~96 GB+ usable for AI | **gpt-oss-120b**, GLM‑4.5‑Air‑class, 70B dense | **Real multi-file projects** with an agent (slower than cloud, but it works) | ~10–15 W / 60–140 W (adjustable TDP) | varies (many have internal AC PSUs — check) | **3,400–4,400** (Nov 2026; launched ~$2k, then the RAM shortage hit) |
| **3 — Max** | **NVIDIA DGX Spark** (GB10), 128 GB | 128 GB unified + CUDA | same size class as Tier 2, **much faster prompt processing** | Best for coding agents with big context | low idle / up to ~240 W | **USB‑C PD** (great for a deck) | ~4,000–4,700 |
| Alt — efficiency | Mac mini M4 Pro 64 GB / Mac Studio M4 Max 128 GB | unified, high bandwidth | Tier 2 class (Studio) | Good | very low idle | **AC only** (needs inverter) | 2,000–4,000+ |

**Recommendation: Tier 2, 128 GB.** Best intelligence per watt per dollar, x86 (runs anything, including Windows if ever needed), adjustable power limit for battery mode. Get **128 GB, not 64**: memory is the ceiling, and you can't upgrade it later (it's soldered). Tier 3 is worth it only if offline coding is a top priority and the budget allows.

**Run two models:** a small fast one (e.g. 20–30B MoE) always loaded for quick questions at low power, and the big one loaded on demand for hard problems and coding.

Offline coding agents to pair with the local model: open-source terminal agents (aider, opencode, etc.) pointed at llama.cpp's OpenAI-compatible server. Expect quality roughly like cloud AI from a generation or two back: genuinely useful, but it needs more hand-holding.

Notes:
- **Mac mini has an internal AC power supply** — needs AC (inverter or power station), which wastes power in a 12 V deck. Strix Halo boxes vary (some AC, some DC brick), so **check the power input before buying**.
- Everything in our stack (llama.cpp, kiwix-serve, PMTiles) runs on all of these.
- Storage: **2–4 TB NVMe** inside + a spare mirrored SSD in the metal box.

### 3. Screen
- **15.6" portable USB‑C monitor, 1080p, matte, touchscreen**, as bright as you can find (≥400 nits helps outdoors; many portables are ~300)
- Mount in the lid with printed brackets + **foam backing**; cover with **2–3 mm polycarbonate** (not acrylic, which cracks)
- One USB‑C cable for video + power + touch; HDMI as backup
- Alternative: salvage the 2070 laptop's panel + a cheap controller board (budget hobby option)

### 4. Input
- **Primary:** wired compact keyboard with built-in trackpad, or a silicone washable keyboard (spill-proof). A Logitech K400‑class wireless with touchpad is a cheap backup
- **Mouse alternative:** **trackball** (no flat surface needed) + the touchscreen
- Keyboard sits in a recess on the deck plate, held by magnets or printed clips, and removable so you can use it on your lap

### 5. Network
- **GL.iNet travel router** (Beryl AX class), USB‑C powered: the deck's Wi‑Fi. Phones/laptops in range use the library and AI
- **Bulkhead RJ45** for wired connections
- Optional: **4G/5G router** (GL.iNet cellular models) for when cell service exists
- Optional: external Wi‑Fi antenna on an SMA bulkhead for range

### 6. Radio
| Item | License | Est. $ | Role |
|---|---|---|---|
| **Meshtastic node** (RAK WisBlock / Heltec V3 / Station G2) + SMA bulkhead antenna | none | 30–100 | Off-grid text mesh; USB to the computer → messages show in our dashboard |
| **RTL‑SDR Blog V4** + telescoping antenna | none (receive only) | 40–60 | NOAA weather radio, scanner, AM/FM/shortwave, weather-satellite images, aircraft tracking |
| GMRS handheld (in a foam slot) | GMRS $35 | 40–150 | Family voice comms |
| **Mk III:** ham radio + **Digirig** interface | Technician/General | 150–700 | Winlink radio email, APRS, JS8Call long-distance text |
| Roll-up J‑pole antenna (2 m/70 cm) | — | 20–40 | Hang it high, huge range boost |

### 7. Power — deck has its own battery, takes solar directly
**System:** the big EcoFlow + solar panel = base station (stays out of the box). The deck has its **own LiFePO4 battery** and **one rugged DC input** that accepts **either** the solar panel **or** the EcoFlow.

```
 solar panel (MC4) ──► MC4→XT60 adapter ─┐
                                         ├─► [DECK DC INPUT, XT60 bulkhead]
 EcoFlow DC out (12 V car port / USB‑C) ─┘            │
                                              charger/MPPT (built in or Victron)
                                                      │
                                              LiFePO4 battery (BMS)
                                                      │
                                   master switch → fuse block → loads
                                   (USB‑C PD: screen, router, compute if USB‑C)
                                   (12 V: radios, fans  ·  19–20 V boost: compute if barrel)
```

**Option A — small LiFePO4 power station inside the case (recommended first)**
- 250–300 Wh LiFePO4 unit with a solar (XT60) input + strong USB‑C PD outputs (EcoFlow River 3‑class, Anker SOLIX C300 DC‑class). Built-in MPPT, BMS, and protections: plug-and-play and safe
- Wire its solar input to the deck's XT60 bulkhead, its outputs to the internal loads
- Trade-offs: bulkier, fixed outputs, its own fan/heat

**Option B — DIY 12 V system (Mk III / hobby)**
- 12 V LiFePO4 pack, 20–50 Ah (≈256–640 Wh), with BMS
- **Victron SmartSolar 75/15 MPPT** (handles panels up to 75 V open-circuit; **check your panel's Voc label**)
- Fused distribution block, master switch, shunt meter (Wh in/out), buck converters (USB‑C PD) + a boost converter for 19–20 V compute
- Most customizable and repairable, more to build

**Runtime math (300 Wh deck battery, rough):**
| Use | Draw | Runtime |
|---|---|---|
| Library + maps server, router, screen dimmed | ~25–35 W | ~8–10 h |
| + occasional AI questions | ~40–60 W avg | ~5–6 h |
| Heavy AI / vibecoding session | ~100–150 W | ~2–3 h |
The EcoFlow then refills the deck; solar refills the EcoFlow (or the deck directly).

- LiFePO4 only (much safer chemistry inside a sealed box)
- **Prefer a compute box with USB‑C PD or 19–20 V DC input.** AC-only machines need an inverter: ~10–20% wasted

### 8. Other critical tools (onboard)
- [ ] **USB GPS receiver**: your position on offline maps, **and accurate time with no internet**
- [ ] **Environment sensor** (temp/humidity/**barometric pressure**): a falling barometer = weather coming. Can hang off the Meshtastic node
- [ ] Small speaker + headphone jack (SDR audio, alerts)
- [ ] **Pinecil** USB‑C soldering iron + solder + mini multimeter (field repairs)
- [ ] Spare cables (USB‑C, HDMI), spare fuses, zip ties, electrical tape
- [ ] microSD/SD reader + a USB stick with OS installers + APKs
- [ ] Headlamp / small LED strip in the lid (work at night)
- [ ] Optional: **Geiger counter / radiation detector** (Radiacode‑class, Bluetooth/USB) given current tensions
- [ ] Pouch: printed quick-start + emergency binder subset

### 9. Software integration (our stack)
Dashboard tiles: Library · Maps (GPS position) · Ask the Librarian (AI) · **Mesh messages** · **NOAA weather (SDR)** · **Barometer trend** · **Battery/power status** · Notes/log

## 3D printer
| Printer | Est. $ | Enclosed? | Why |
|---|---|---|---|
| **Bambu Lab A1** (256 mm bed) | 300–450 | No | Easiest entry, great quality, prints PETG + TPU fine |
| **Bambu Lab P1S / P2S** | 600–900 | Yes | Enclosure → **ASA/ABS** (heat + UV resistant). Best fit for deck parts |
| Prusa Core One / MK4S | 900–1,300 | Core One yes | Most open/repairable; no cloud dependency |

- **Recommendation:** an enclosed printer with a ~256 mm bed (P1S/P2S class) if the budget allows. Otherwise an A1, sticking to PETG + TPU.
- Offline note: Bambu printers can run in **LAN-only mode**. Prusa is the most cloud-independent.
- **Filaments:** PETG (general), ASA (heat/sun), **TPU** (shock-absorbing corner bumpers, gaskets, screen bezel, feet)
- **CAD:** **OpenSCAD** (code-based, so **we can vibecode parametric parts in this repo**), FreeCAD (offline, open source), Fusion (free personal license, cloud-tied)
- Big panels won't fit on one bed: split them into **dovetailed tiles**, or cut the deck plate from HDPE/aluminum and print only the brackets

### First print projects (learn on small stuff)
- [ ] Meshtastic node case with an SMA mount
- [ ] Cable clips + labels
- [ ] Phone/tablet stand
- [ ] TPU corner bumpers for a power bank
- [ ] Louvered vent + fan cover
- [ ] Monitor lid brackets (once the screen + case are chosen)

## Build phases
- [ ] **A. Decide:** compute tier + budget → screen → then measure → case
- [ ] **B. Printer:** buy, calibrate, print the learning projects
- [ ] **C. Bench prototype ("breadboard deck"):** wire everything together on a desk *before* casing it. Run the stack, measure power + heat
- [ ] **D. Case integration:** deck plate, lid mount, power distribution, I/O panel, airflow
- [ ] **E. Field tests:** 24 h battery run, heat test (lid open, AI loop, 30 min), rain/hose test (closed), padded drop test, a full night of off-grid use → log in [log.md](log.md)
- [ ] **F. Mk III upgrades:** ham radio + Digirig, integrated battery, hot-swap packs

## Rough budget
| Build | Contents | Est. total |
|---|---|---|
| **Mk I** | 2070 laptop guts, Apache case, portable touchscreen, keyboard, router, Meshtastic, RTL‑SDR, GPS, wiring | **$350–600** |
| **Mk II** | + Strix Halo 128 GB (or equivalent), internal battery + distribution, better screen | **$4,000–5,500** (at Nov 2026 prices) |
| Printer + filament | | $400–1,000 |
