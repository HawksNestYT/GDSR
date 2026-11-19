# Dev Workflow — Vibecoding the Hub from the Phone

## The loop (works today)
```
 Claude app on phone ──► Claude Code (cloud) writes + tests code ──► pushes to GitHub
                                                                          │
 phone (Termux) ◄──────────────── git pull ◄─────────────────────────────┘
   run it, test on real hardware, report back in the chat
```
- The heavy lifting (writing code, running tests on x86 Linux) happens in the cloud session
- The phone only needs `git pull` + run, so its compute goes to the hub itself, not to development
- The same code goes to the laptop and the Mac with the same `git pull`

## Phone setup (Samsung, Termux)
- [ ] Termux from F-Droid/GitHub (see [phone-linux.md](phone-linux.md))
- [ ] `pkg install git python nodejs openssh`
- [ ] GitHub access: make an SSH key (`ssh-keygen -t ed25519`) and add the public key to GitHub → Settings → SSH keys
- [ ] `git clone git@github.com:HawksNestYT/GDSR.git ~/GDSR`
- [ ] Each update: `cd ~/GDSR && git pull`

## Optional: run the coding agent ON the phone
Claude Code is a Node.js CLI and needs internet (the model runs in the cloud). Running it in Termux, or in a proot Debian inside Termux, lets the agent run and test code directly on the phone's hardware. Expect some rough edges on Android. It's good for testing things that only exist on the phone (battery, sensors, ARM builds).

## Offline fallback (no internet = no cloud AI)
- Local coding model (a 7–14B "coder" model) via llama.cpp on the **laptop or Mac**, driven by an open-source terminal agent (e.g. aider, opencode)
- Much weaker than cloud AI but enough for small fixes
- On a phone: possible with a tiny model, not really practical

## True Linux phone (postmarketOS) vs. Termux, for development
| | Termux on Samsung | postmarketOS (e.g. OnePlus 6/6T) |
|---|---|---|
| Speed | Full flagship speed | ~2018 flagship speed |
| Packages | Termux repo (big) + Debian in proot | Full Alpine/Debian repos, native |
| Background processes | Android may kill them (fixable) | Normal Linux, nothing kills them |
| Hardware | Everything works | Calls/camera/battery life vary |
| Local LLM | Best (newer CPU, more RAM) | Small models only |
| Best for | Daily driver + pocket hub + dev | Dedicated Linux handheld / cyberdeck brain |
