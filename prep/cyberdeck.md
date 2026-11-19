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

| Tier | Machine | AI memory | What it runs | Power | Est. $ |
|---|---|---|---|---|---|
| **Mk I (free)** | The 2070 laptop (guts or whole) | 8 GB VRAM + system RAM | 7–9B well; ~20–30B MoE slowly | 60–180 W | $0 |
| Budget | Ryzen 7/9 mini PC (8845HS/AI 9 class), 64 GB RAM | shared, 64 GB | 20–30B MoE at usable speed | 35–80 W | 500–900 |
| **Best balance (recommended)** | **AMD Ryzen AI Max+ 395 "Strix Halo" mini PC, 64–128 GB** (Framework Desktop, GMKtec, Beelink, etc.) | up to ~96 GB+ for AI | 70B dense, ~100B+ MoE (gpt-oss-120b class) | 50–140 W (adjustable) | 1,500–2,800 |
| Most efficient | Mac mini M4 Pro, 48–64 GB | unified | 30–70B | very low idle; ~40–80 W load | 1,400–2,200 |

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

### 7. Power
- **Simple and safe (Mk I/II):** the deck has **one XT60 or Anderson input**; feed it from an external LiFePO4 power station + solar. Small internal LiFePO4 pack as a UPS (bridge power while you swap sources)
- **Integrated (Mk II/III):** **12 V LiFePO4 pack** (20–50 Ah ≈ 256–640 Wh) with BMS → **fused distribution block** → buck converters (12 V → 5 V/USB‑C PD for screen, router, radios) + 12 V → 19/20 V for the computer
- **Master switch, inline fuse per circuit, volt/amp/Wh meter** on the panel
- LiFePO4 only (much safer chemistry inside a sealed box)
- Budget: library + router + screen ~20–40 W; AI bursts add 50–140 W. Run the AI in bursts

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
| **Mk II** | + Strix Halo 64–128 GB (or Mac mini), internal LiFePO4 + distribution, better screen | **$2,000–4,000** |
| Printer + filament | | $400–1,000 |
