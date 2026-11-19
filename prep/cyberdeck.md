# Cyberdeck Build (hobby track)

## Design rules
1. **Modular:** every part can be unplugged and replaced without tools (USB‑C, HDMI, barrel jacks; no soldered-in parts on the critical path)
2. **Degrades gracefully:** if the screen dies, use any HDMI display or a phone browser. If the computer dies, the phones still have the core library. If the battery dies, use wall or solar power
3. **Rugged:** hard case, foam or 3D-printed mounts, strain relief on every cable
4. **Self-documenting:** label every port, and tape the NOMAD Wi‑Fi info + quick-start card inside the lid

## Build path
### Mk I — "Laptop in a box" (cheapest, do this first)
- [ ] Replace or ignore the broken screen; run the 2070 laptop headless
- [ ] Hard case (Harbor Freight Apache 3800/4800 or Pelican) + pick-and-pluck foam
- [ ] Laptop + GL.iNet router + short Ethernet cable + power bricks, all fixed in place
- [ ] Outside the case: one power input and one USB-C/HDMI passthrough (optional)

### Mk II — Integrated deck
- [ ] 13–15" **USB‑C portable monitor** mounted in the lid
- [ ] Compact keyboard (wired + Bluetooth) in a lid pocket
- [ ] Meshtastic node with an external antenna on a bulkhead SMA connector
- [ ] Power station or a built-in LiFePO4 pack + a DC distribution board with a voltage meter
- [ ] Fan and vents for the laptop (AI makes it run hot)

### Mk III — Purpose-built
- [ ] Swap the laptop for an x86 **mini PC** (Ryzen class) + optionally an eGPU, or keep the laptop guts
- [ ] Integrated SDR (RTL-SDR) for listening, and a ham HF/VHF radio with a digital interface (Winlink/JS8Call)
- [ ] Hot-swappable battery packs

## Parts / ideas backlog
- [ ] RTL-SDR v4 (receive-only scanner/weather satellites, ~$40)
- [ ] USB watt meter
- [ ] Spare SSD with a full content mirror
- [ ] Ammo can / metal box for spare drive + spare Meshtastic node + spare radio
