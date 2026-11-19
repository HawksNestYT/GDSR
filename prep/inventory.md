# Device Inventory

Fill in the `?` fields. Specs decide which AI models and how much content each device can hold.

| Device | Model | Chip | RAM | Storage | SD slot? | Role | Status |
|---|---|---|---|---|---|---|---|
| Windows laptop (busted screen) | ? | ? (Intel/AMD) | ? | ? | n/a | **Main hub server** (our stack, CUDA) | ⬜ |
| MacBook | ? | ? (M1/M2/M3/M4?) | ? | ? | n/a | **Best offline AI** + library copy #2 | ⬜ |
| Samsung phone | ? | ? | ? | ? | ? | Pocket hub (Termux + our stack) + client | ⬜ |
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
- We build our own stack ([stack.md](stack.md)) on llama.cpp + kiwix-serve + PMTiles, which run on x86 **and** ARM, so every device runs the same thing at its own scale.
- Phones: debloated Android + Termux runs the stack at full speed. See [phone-linux.md](phone-linux.md) for the options, including a true Linux phone (postmarketOS) on a supported OnePlus.
