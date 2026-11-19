# Build & Test Log

Newest entries at the top. Record what you did, what broke, measurements, and lessons.

## Template
```
### YYYY-MM-DD — <short title>
- Did:
- Result / measurements:
- Problems:
- Next:
```

---

### 2026-11-19 — Deck compute + power direction
- Decided: 2070 laptop stays whole = home hub server + dev bench. Deck gets its own mini PC (leaning Tier 2: Strix Halo 128 GB)
- Power: EcoFlow + solar = base station outside the box; deck gets its own LiFePO4 battery with an XT60 input that takes solar OR EcoFlow
- Next: Samsung details, laptop model, EcoFlow model + panel wattage/Voc

### 2026-11-19 — Direction change: build our own stack
- Decided: skip Project NOMAD as a product; use the same open content (ZIMs, OSM maps, PDFs) and build the interface + AI ourselves. See [stack.md](stack.md)
- Phones: Linux-first via debloated Android + Termux (Samsung), postmarketOS on the OnePlus if supported. See [phone-linux.md](phone-linux.md)
- Next: phone/laptop model numbers → pick the Linux route per device; milestone M1 (kiwix-serve + WikiMed on laptop and phone)

### 2026-11-19 — Hub created
- Did: set up this repo as the planning hub; mapped device roles (2070 laptop = main hub server, MacBook = best AI, phones = pocket libraries + clients)
- Next: fill in [inventory.md](inventory.md) specs; start [Phase 0](phase0-phones.md)
