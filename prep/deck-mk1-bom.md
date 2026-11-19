# Deck Mk I — Bill of Materials (budget compute)

Prices are **estimates as of Nov 2026** (the RAM/SSD shortage has pushed prices up and they move weekly). Verify before buying. Buy the **case last**, after measuring the parts.

## Compute choice
| Option | Machine | Est. $ | What it runs | Why |
|---|---|---|---|---|
| **★ Recommended** | **Ryzen 7 8845HS mini PC, 32 GB, 1 TB** (Beelink SER8 / GMKtec K8 Plus class) | ~750–900 | gpt-oss-20b, Qwen3‑30B‑A3B‑class MoE models at roughly 15–25 tokens/s; plus all library/maps | **RAM is socketed (SODIMM)**: buy 32 GB now and upgrade to 64–96 GB when RAM prices drop |
| Step up | same, **64 GB** (e.g. SER8 64 GB, ~$1,250 at Best Buy) | ~1,250 | same models, longer context, a small + big model loaded together | If you'd rather not upgrade later |
| Ultra-budget | Raspberry Pi 5 16 GB + NVMe | ~200–300 | library, maps, 1–4B AI | Lowest power; weak AI |

Power setup for the mini PC: **cap its power to ~35–45 W** in BIOS (barely slower for AI, much better battery life and heat).

## Parts list (recommended build)
| # | Part | Example | Est. $ |
|---|---|---|---|
| **Enclosure** | | | |
| 1 | Hard case IP65 | Harbor Freight Apache 5800 (confirm interior depth fits the power station) | 90 |
| 2 | Polycarbonate sheet 2–3 mm (screen cover) | hardware store | 20 |
| 3 | Fan + vent (USB 5 V, low noise) ×2 | Noctua/AC Infinity USB fans | 30 |
| 4 | Mounting: 3M Dual Lock, Velcro, standoffs, zip ties, foam | | 50 |
| **Compute & storage** | | | |
| 5 | Mini PC, 32 GB, 1 TB | Ryzen 7 8845HS class | 800 |
| 6 | 2 TB NVMe (second slot: library + models) | WD/Samsung/Crucial | 150 |
| **Screen & input** | | | |
| 7 | 15.6" portable **touchscreen**, 1080p, USB‑C | UPERFECT/ARZOPA class | 150 |
| 8 | Wireless keyboard with touchpad | Logitech K400 Plus | 30 |
| 9 | Trackball (no flat surface needed) | Elecom/Kensington | 40 |
| **Power** | | | |
| 10 | LiFePO4 power station ~250–300 Wh, XT60 solar input | EcoFlow River 3 / 3 Plus or current equivalent (same XT60 as your big EcoFlow panel) | 270 |
| 11 | USB‑C PD → 20 V barrel cable for the mini PC (check plug size + wattage) | 100 W PD trigger cable | 15 |
| 12 | XT60 panel-mount bulkhead + MC4→XT60 cable (your panel may already include one) | | 25 |
| **Network** | | | |
| 13 | Travel router (USB‑C powered) | GL.iNet Beryl AX | 90 |
| 14 | Panel-mount pass-throughs: USB‑C, HDMI, RJ45 | | 40 |
| **Radio & sensors** | | | |
| 15 | Meshtastic deck node + SMA bulkhead + 915 MHz antenna | Heltec V3 or XIAO ESP32S3 + Wio‑SX1262 | 45 |
| 16 | RTL‑SDR receiver kit (NOAA weather, scanner, AM/FM/SW, weather sats) | RTL‑SDR Blog V4 + dipole kit | 55 |
| 17 | USB GPS (map position + time with no internet) | VK‑162 class | 20 |
| **Misc** | | | |
| 18 | Small USB hub | | 20 |
| 19 | USB LED strip (lid light) | | 10 |
| | **Total** | | **≈ $1,950** |

## Ways to cut it
| Cut | Saves | New total |
|---|---|---|
| Use the mini PC's included 1 TB for now (skip #6) | 150 | ~1,800 |
| Run the deck off your **big EcoFlow by cable** for now; add the internal battery later (skip #10) | 270 | ~1,530 |
| Non-touch monitor | ~50 | ~1,480 |
| **Lean build (all three)** | ~470 | **≈ $1,480** |
| **Pi 5 build** instead of the mini PC (+ lean cuts) | ~600 more | **≈ $850–950** |

## Add-ons (not in the deck total)
| Item | Est. $ |
|---|---|
| 2× pocket Meshtastic nodes for family (SenseCAP T1000‑E) | 80 |
| GMRS license + 2 handhelds | 35 + 80–150 |
| Pinecil soldering iron + mini multimeter | 60 |
| 3D printer (Bambu A1 → P1S/P2S class) + filament | 350–950 |
| Later: RAM upgrade to 64–96 GB | ~150–400 (depends on the RAM market) |

## Power math (rough, 286 Wh battery)
| Mode | Draw | Runtime |
|---|---|---|
| Library + maps + router, screen dim | ~20–30 W | ~9–12 h |
| + occasional AI questions | ~35–50 W | ~6–7 h |
| Continuous AI / coding (PC capped at 45 W) | ~60–75 W | ~3.5–4.5 h |
Recharge from your big EcoFlow or the solar panel straight into the deck's XT60.

## Build order
1. Mini PC + monitor + keyboard on a desk → install Ubuntu → our stack (same as the laptop)
2. Add router, Meshtastic, SDR, GPS → test everything on the desk ("breadboard deck")
3. Measure everything → buy the case → layout + printed mounts → install
4. Field tests (see [cyberdeck.md](cyberdeck.md) phase E)
