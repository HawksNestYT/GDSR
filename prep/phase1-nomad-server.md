# Phase 1 — 2070 Laptop → Project NOMAD Server

**Project NOMAD** (by Crosstalk Solutions) bundles Kiwix (Wikipedia etc.), offline maps, Khan Academy, Jellyfin media, and a local AI chat (Ollama + a Qdrant document database) behind one web dashboard. Any device on its Wi‑Fi can open it in a browser.

- Site: https://www.projectnomad.us
- Install guide: https://www.projectnomad.us/install
- Source: https://github.com/Crosstalk-Solutions/project-nomad

**Always copy the install command from the official install page.** Don't copy it from videos or blog posts, since it may have changed.

## Requirements
- x86 (Intel/AMD) machine ✅ (the 2070 laptop)
- Debian-based Linux — **Ubuntu 24.04 LTS** recommended
- Internet during setup (it pulls containers + content). Fully offline after.
- NVIDIA GPU strongly recommended for AI ✅ (RTX 2070, 8 GB VRAM)

## Hardware prep
- [ ] **Screen:** plug an external monitor or TV into HDMI for setup. Long term, either run it **headless** (no screen, use it from phones) or replace the laptop panel (~$50–120, search your laptop model + "LCD replacement")
- [ ] **Storage:** upgrade to a **2 TB NVMe SSD** (check that your laptop has an M.2 NVMe slot; many 2070 laptops have two)
- [ ] Clean the fans and repaste the CPU/GPU if the laptop is old. AI runs push it hard
- [ ] Back up anything on the Windows install you care about. **The Ubuntu install will wipe the drive** unless you dual-boot (you can, but a dedicated box is simpler)

## Install steps
1. [ ] On another computer, download the **Ubuntu 24.04 LTS Desktop** ISO from ubuntu.com
2. [ ] Flash it to a USB stick (8 GB+) with **balenaEtcher** or **Rufus**
3. [ ] Boot the laptop from USB (usually F12/F2/Esc at power-on), choose "Install Ubuntu"
   - Turn on "Install third-party software for graphics and Wi‑Fi hardware"
4. [ ] After first boot, update and install NVIDIA drivers:
   ```bash
   sudo apt update && sudo apt full-upgrade -y
   sudo ubuntu-drivers install
   sudo reboot
   nvidia-smi        # should show the RTX 2070 and driver version
   ```
5. [ ] Install Project NOMAD with the **one-liner from https://www.projectnomad.us/install**
6. [ ] Open the NOMAD dashboard in a browser (the installer tells you the address)
7. [ ] In the **Content Explorer**, pick collections: Medicine, Survival & Preparedness, Agriculture & Food, DIY & Repair, Computing. Add full Wikipedia
8. [ ] In the **Maps** section, download your region (or the full planet if you have the space)
9. [ ] In the **AI** section, pull a model that fits 8 GB VRAM (a 7–9B model at 4-bit, e.g. Llama 3.1 8B / Qwen 8B class / Gemma ~9B class). Try a couple and keep the best
10. [ ] Knowledge base: add your **own** PDFs (the Hesperian books, Army manuals) to the AI's document library, so it can quote them. Budget **5–10× the document size** in disk space for this
11. [ ] Set the laptop to **never sleep** when plugged in; set it to auto-power-on after power loss if the BIOS allows

## Networking (the "NOMAD" Wi‑Fi)
- [ ] Buy a **GL.iNet travel router** (Beryl AX / Slate class)
- [ ] Set SSID `NOMAD` (or whatever you like) + a password
- [ ] Plug the laptop into it with Ethernet if possible (more reliable than Wi‑Fi)
- [ ] In the router admin, give the laptop a **static/reserved IP** (e.g. `192.168.8.10`)
- [ ] Bookmark `http://192.168.8.10` (or your chosen IP) on every phone/tablet
- [ ] Label the router and laptop with the SSID, password, and IP (masking tape works)
- [ ] Keep it online day-to-day so content stays updated; when the internet dies, nothing changes for clients

## Test
- [ ] Unplug the internet from the router. Can phones still browse Wikipedia, maps, and AI chat?
- [ ] Unplug **wall power**. How long does the laptop battery run it? Write it in [log.md](log.md)
- [ ] Measure power draw with a cheap USB-C/AC watt meter: idle vs. AI query (feeds [power.md](power.md))

## Alternative: no wipe
NOMAD has a **WSL2 install path for Windows** (community-supported): https://www.projectnomad.us/install/wsl2. It's fine for trying it out, but bare-metal Ubuntu is the recommended setup for a dedicated survival box.
