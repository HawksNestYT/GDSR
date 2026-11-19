# Comms

Layered, from "works today with no license" up to "hobby-grade long distance."

## Layer 1 — Listen (no license)
- [ ] **NOAA weather radio** with hand crank + solar + AM/FM/shortwave. Emergency broadcasts come through here
- [ ] Note your local NOAA frequency and AM news stations in the binder

## Layer 2 — Meshtastic text mesh (no license, the best value here)
LoRa radios (US 915 MHz band) that pair to a phone over Bluetooth. Messages hop node to node, with no cell towers or internet. Range runs from roughly 1–2 miles in town to 10+ miles line-of-sight with good placement.
- [ ] Buy 2–4 nodes, e.g. **SenseCAP T1000‑E** (card-sized, ready to go), **LilyGo T‑Echo**, **RAK WisBlock**, **Heltec V3** (cheapest, needs a case + battery)
- [ ] Flash/update firmware via the web flasher (flasher.meshtastic.org)
- [ ] Set the region to **US**, make a **private channel** with a key for family, and keep the default public channel to talk with the local mesh
- [ ] One node goes on a **high, fixed point** (attic/roof, solar-powered) as a relay
- [ ] Check local Meshtastic activity (meshmap.net or local groups) — an existing mesh in your area greatly extends range
- [ ] Test: send messages across town with cell data turned off

## Layer 3 — GMRS voice (license: $35, no exam, covers the household, 10 years)
- [ ] Get the license at fcc.gov (ULS)
- [ ] Buy GMRS handhelds (Midland/Wouxun/BTech class). Repeater-capable radios give much more range
- [ ] Look up local GMRS repeaters (mygmrs.com)
- [ ] Assign a family channel + check-in times; write it in the binder

## Layer 4 — Amateur (ham) radio (hobby path)
- [ ] **Technician** license: study (hamstudy.org), take the exam with a local VE team (small fee + $35 FCC fee). Unlocks local VHF/UHF + repeaters
- [ ] **General**: unlocks HF — regional/national/worldwide
- [ ] Later: **Winlink** (radio email), **JS8Call** (keyboard messaging over weak signals), **APRS**. All fit the cyberdeck
- Note: transmitting on ham bands without a license is illegal except in a genuine life-threatening emergency. Get licensed; it's not hard.

## Comms plan (fill in and print)
| What | Value |
|---|---|
| Family Meshtastic channel name | ? |
| GMRS channel / repeater | ? |
| Check-in times | e.g. top of each hour 8am–8pm, then 9pm |
| Out-of-area contact | ? |
| Meet-up points | ? |
