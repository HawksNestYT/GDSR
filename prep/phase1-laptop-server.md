# Phase 1 — 2070 Laptop → Main Hub Server

The laptop runs **our own stack** ([stack.md](stack.md)) with the full content set and the biggest models, and serves it to the whole house over Wi‑Fi. It's x86 + an NVIDIA GPU (8 GB VRAM), so llama.cpp gets CUDA acceleration.

## Hardware prep
- [ ] **Screen:** plug an external monitor or TV into HDMI for setup. Long term, run it **headless** (use it from phones/SSH) or replace the panel (~$50–120)
- [ ] **Storage:** upgrade to a **2 TB NVMe SSD** (check the M.2 slot; many 2070 laptops have two)
- [ ] Clean the fans and repaste the CPU/GPU. AI runs push it hard
- [ ] Back up anything on Windows you care about. **The Ubuntu install wipes the drive** (unless you dual-boot)

## OS
1. [ ] Download **Ubuntu 24.04 LTS** (Desktop, or Server if you'll stay headless) from ubuntu.com
2. [ ] Flash it to a USB stick with **balenaEtcher** or **Rufus**
3. [ ] Boot from USB (F12/F2/Esc at power-on) → install, with "third-party software for graphics and Wi‑Fi" enabled
4. [ ] Drivers + basics:
   ```bash
   sudo apt update && sudo apt full-upgrade -y
   sudo ubuntu-drivers install
   sudo apt install -y git build-essential cmake python3-venv openssh-server rsync
   sudo reboot
   nvidia-smi        # should show the RTX 2070
   ```
5. [ ] Install the **CUDA toolkit** (`sudo apt install nvidia-cuda-toolkit`, or NVIDIA's repo if you need a newer version)
6. [ ] Lid closed = keep running: in `/etc/systemd/logind.conf` set `HandleLidSwitch=ignore` and `HandleLidSwitchExternalPower=ignore`
7. [ ] BIOS: enable "power on after AC loss" if available

## The stack
- [ ] Create `~/hub/{zim,maps,models,docs,index,app,bin}`
- [ ] **llama.cpp** built with CUDA:
  ```bash
  git clone https://github.com/ggml-org/llama.cpp && cd llama.cpp
  cmake -B build -DGGML_CUDA=ON && cmake --build build -j --config Release
  ```
- [ ] **kiwix-tools** (x86-64 static build) → `hub/bin/`
- [ ] **go-pmtiles** (linux x86-64) → `hub/bin/`
- [ ] Models: one 7–9B chat model at Q4/Q5 that fits in 8 GB VRAM, a small 1–3B one for quick answers, and a small embedding model
- [ ] Content: see [content-manifest.md](content-manifest.md)
- [ ] Dashboard + `/ask` (milestones M3–M5 in [stack.md](stack.md))
- [ ] **systemd services** so everything starts on boot (M7)

## Networking (the house Wi‑Fi for the hub)
- [ ] **GL.iNet travel router** (Beryl AX class): SSID `HUB` (pick your own) + a password
- [ ] Laptop on Ethernet to the router; **reserved IP** (e.g. `192.168.8.10`)
- [ ] Bookmark `http://192.168.8.10:8080` on every phone/tablet
- [ ] Label the router + laptop with the SSID, password, and IP
- [ ] Day to day: keep it online so the update scripts can refresh content. When the internet dies, nothing changes for clients

## Tests
- [ ] Router unplugged from the internet: library, maps, AI all still work from a phone
- [ ] Wall power unplugged: battery runtime at idle vs. AI → [log.md](log.md)
- [ ] Watt meter: idle vs. AI draw → [power.md](power.md)
- [ ] Tokens/sec for each model → [log.md](log.md)
