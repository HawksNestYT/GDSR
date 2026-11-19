# Linux on the Phones — Options and Plan

Goal: as much Linux-level control as possible, minimal Android bloat and restrictions, without giving up performance.

## The options, honestly
| Option | Real Linux? | Performance | Hardware works? | Difficulty | Notes |
|---|---|---|---|---|---|
| **A. Debloated Android + Termux (native packages)** | Linux userland on Android's kernel | **Full speed** | Everything | Easy | Best balance for the Samsung. Our stack runs here natively |
| **B. A + Debian in proot** | Full Debian userland | Slower for disk-heavy work | Everything | Easy | Use for tools that won't build in Termux. Don't put the heavy stuff here |
| **C. A + Debian chroot (needs root)** | Full Debian | Near-native | Everything | Medium | Needs an unlocked bootloader + root |
| **D. Android 15/16 "Linux Terminal" VM** | Debian VM on the device's hypervisor | Good CPU, limited GPU/RAM | Partial | Easy | Device support varies — Pixels first; check whether your Samsung offers it under Developer Options |
| **E. Custom ROM (LineageOS etc.)** | Android without the bloat | Full | Mostly | Medium–Hard | Good for the OnePlus/Razer if they're supported |
| **F. Native Linux phone OS (postmarketOS, Mobian, Ubuntu Touch)** | **Yes, a real Linux phone** | Full CPU, varying GPU | Depends on the model | Hard | Best supported on a few older phones — **OnePlus 6 / 6T is one of the best**. Modern Samsungs are poorly supported |

### Samsung specifics
- **US Snapdragon Galaxy phones have locked bootloaders.** No root, no custom ROMs, no native Linux. So: **Option A (+B, maybe D)**.
- International Exynos models can usually unlock, but that permanently trips Knox (Samsung Pay/Secure Folder stop working).
- Samsung's old "Linux on DeX" was discontinued.

### Recommended setup
- **Samsung (strongest):** **Option A** — debloat with ADB, Termux, the stack running natively. Your powerful pocket hub.
- **OnePlus:** if it's a **6 or 6T → postmarketOS** (true Linux phone, your "Linux purist" device). Otherwise LineageOS or Option A.
- **Razer Phone:** LineageOS if available for your model, or Option A. Good dedicated backup library or Meshtastic messenger.

## Expected performance on the phone (ballpark, llama.cpp, 4-bit models, CPU)
| Phone class | RAM | Model that's comfortable | Rough speed |
|---|---|---|---|
| Recent Samsung flagship (Snapdragon 8 Gen 2/3 class) | 8–12 GB | 3–4B | ~10–20 tokens/s |
| same | 12 GB+ | 7–8B | ~4–8 tokens/s (usable, warm phone) |
| OnePlus 6/6T (Snapdragon 845) | 6–8 GB | 1–3B | ~4–10 tokens/s |
| Older/mid phones | 4–6 GB | 1–2B | slow but works |

Reading speed is ~5–8 tokens/s, so anything at or above that feels fine. **Measure on your actual phones in M2** and replace this table with real numbers.

What a phone *can't* do well: big models (14B+), long documents in one go, or hours of sustained AI (heat and battery). That's what the laptop and Mac are for.

## Step-by-step: Samsung → Option A
### 1. Debloat (no root, reversible)
- [ ] Enable Developer Options (Settings → About → Software info → tap Build number 7×) → enable **USB debugging**
- [ ] On the laptop/Mac: install `adb` (Android platform-tools)
- [ ] Use **Universal Android Debloater Next Generation (UAD-ng)**, a GUI that lists safe-to-remove packages. Stick to the "Recommended" list at first
- [ ] Turn off: Bixby, Samsung/Google ads and "customization service", the Facebook preinstalls, unused carrier apps
- [ ] Note what you removed in [log.md](log.md) (packages can be restored with `adb shell cmd package install-existing <pkg>`)

### 2. Stop Android from killing our processes
- [ ] Developer Options → **Disable child process restrictions** (Android 14+)
  - On Android 12–13: `adb shell settings put global settings_enable_monitor_phantom_procs false`
- [ ] Settings → Apps → Termux → Battery → **Unrestricted**
- [ ] In Termux, run `termux-wake-lock` while the hub is running

### 3. Termux
- [ ] Install **Termux from F-Droid or its GitHub releases** (the Play Store version is outdated)
- [ ] Also install **Termux:Boot** (autostart) and **Termux:API** (battery/sensors), from the same source
- [ ] Base setup:
  ```bash
  pkg update && pkg upgrade
  pkg install git python openssh rsync proot-distro
  termux-setup-storage          # access to shared storage / SD card
  ```
- [ ] SSH in from the laptop for comfortable typing: run `sshd` in Termux (port 8022)

### 4. The stack
- [ ] `pkg install llama-cpp` (or build llama.cpp from source with `cmake`)
- [ ] kiwix-serve: static **linux-aarch64** build of kiwix-tools from download.kiwix.org
- [ ] pmtiles: the **linux arm64** release of go-pmtiles
- [ ] Our dashboard (see [stack.md](stack.md))

### 5. Optional Debian (for everything else)
```bash
proot-distro install debian
proot-distro login debian
```

## Step-by-step: OnePlus 6/6T → postmarketOS (hobby track)
- [ ] Confirm the exact model (Settings → About phone)
- [ ] Back up anything on it; this **wipes the phone**
- [ ] Unlock the bootloader (`fastboot oem unlock`)
- [ ] Follow the postmarketOS wiki page for your device (codename `enchilada` = OnePlus 6, `fajita` = 6T)
- [ ] Choose a UI: Phosh (simple) or Plasma Mobile
- [ ] Then install the stack as on any ARM64 Linux machine
