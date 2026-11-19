# Device Inventory

Fill in the `?` fields. Specs decide which AI models and how much content each device can hold.

| Device | Model | Chip | RAM | Storage | SD slot? | Role | Status |
|---|---|---|---|---|---|---|---|
| Windows laptop (busted screen) | ? | ? (Intel/AMD) | ? | ? | n/a | **NOMAD server** (main hub) | ⬜ |
| MacBook | ? | ? (M1/M2/M3/M4?) | ? | ? | n/a | **Best offline AI** + library copy #2 | ⬜ |
| Samsung phone | ? | ? | ? | ? | ? | Pocket library + maps + NOMAD client | ⬜ |
| Samsung tablet(s) | ? | ? | ? | ? | ? | Big-screen library, reading, maps | ⬜ |
| OnePlus | ? | ? | ? | ? | ? | Backup library (drawer / metal box) | ⬜ |
| Razer phone | ? | ? | ? | ? | ? | Backup library / Meshtastic messenger | ⬜ |

## How to find specs
- **Windows laptop:** `Win+R` → `msinfo32`. Or after Ubuntu is installed: `lscpu`, `free -h`, `lsblk`, `nvidia-smi`
- **MacBook:** Apple menu → About This Mac
- **Android:** Settings → About phone. For free space: Settings → Storage

## What specs mean for local AI (rough guide)
| Available memory for the model | Model size that runs well | Quality |
|---|---|---|
| 4–6 GB (phones) | 1–4B | OK for simple Q&A, makes things up often |
| 8 GB VRAM (RTX 2070 laptop) | 7–9B (4-bit quantized) | Good everyday helper |
| 16 GB Mac | 7–14B | Good |
| 24–36 GB Mac | 14–32B | Very good |
| 48 GB+ Mac | 32–70B | Excellent |

## Why each device has the role it has
- **Project NOMAD only runs on x86 (Intel/AMD)**, so the Windows laptop is the only device here that can run it. The Mac and the phones are ARM.
- Phones are worth more as **independent working devices** than as hacked Linux boxes. You *can* run Debian on Android (Termux + `proot-distro`), but it's slow, and nothing it offers here is better than the native apps. Keep it as a hobby side quest.
