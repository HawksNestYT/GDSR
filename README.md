# Offline Ops Hub

Planning, prepping, and build log for an offline knowledge and comms setup that keeps working when the internet, cell network, or grid goes down.

> The stump-grinding site files (`index.html`, `styles.css`, `assets/`) are left over from this repo's earlier use. All prep material lives in [`prep/`](prep/).

## Goal
- An offline information hub (Wikipedia, medical, survival, repair, maps, education) that **doesn't stop working when one part breaks**
- Local AI that doesn't need the internet
- Comms with family and nearby people without cell towers
- Power to run it all
- A cyberdeck build as a long-running hobby

## Where we are

| Phase | What | Status |
|---|---|---|
| 0 | Phones and tablets as offline libraries (apps first), printed binder | ⬜ Not started |
| 0b | Phones → debloated + Termux Linux, our stack running on the phone | ⬜ Not started |
| 1 | 2070 laptop → main hub server (our own stack) + travel router | ⬜ Not started |
| 1b | MacBook → offline AI + second library copy | ⬜ Not started |
| 2 | Power (power station + solar) | ⬜ Not started |
| 2 | Comms (Meshtastic, GMRS, NOAA radio, ham later) | ⬜ Not started |
| 3 | Cyberdeck build (rugged case) | ⬜ Not started |

Update the status emoji as you go: ⬜ not started · 🟨 in progress · ✅ done

## Hub index
| File | What's in it |
|---|---|
| [prep/inventory.md](prep/inventory.md) | Devices you own, specs, and the job each one has |
| [prep/phase0-phones.md](prep/phase0-phones.md) | Turn phones and tablets into offline libraries this week |
| [prep/stack.md](prep/stack.md) | **Our own offline stack:** architecture, components, AI design, milestones |
| [prep/phone-linux.md](prep/phone-linux.md) | Linux on the phones: options, Samsung debloat + Termux, OnePlus postmarketOS |
| [prep/dev-workflow.md](prep/dev-workflow.md) | How we vibecode the stack from the phone (cloud agent → GitHub → git pull) |
| [prep/phase1-laptop-server.md](prep/phase1-laptop-server.md) | Step-by-step: 2070 laptop → main hub server |
| [prep/phase1b-mac-ai.md](prep/phase1b-mac-ai.md) | Local AI on the MacBook |
| [prep/content-manifest.md](prep/content-manifest.md) | What to download, approximate sizes, and where each copy lives |
| [prep/print-binder.md](prep/print-binder.md) | What to print. Paper still works with no power at all |
| [prep/power.md](prep/power.md) | Power budget, battery, solar |
| [prep/comms.md](prep/comms.md) | Radio and mesh comms plan, licenses |
| [prep/deck-mk1-bom.md](prep/deck-mk1-bom.md) | **Deck Mk I parts list + total cost** (budget compute) |
| [prep/cyberdeck.md](prep/cyberdeck.md) | The hobby build: design rules and parts |
| [prep/shopping-list.md](prep/shopping-list.md) | Everything to buy, by phase and priority |
| [prep/log.md](prep/log.md) | Build and test log: what you did, what broke, what you learned |

## Ground rules
1. **Three copies of the library on separate devices** (laptop, Mac, phones/drives). Keep one copy in a metal box.
2. **The AI finds answers and the documents confirm them.** Small local models make things up. For medical questions and water safety, always check the source page.
3. **Test offline monthly.** Put everything in airplane mode and use it for an hour. Anything you haven't tested shouldn't count as ready.
4. **Paper beats everything** for the top 20 procedures.
5. **No single point of failure.** If the screen dies, use another screen. If the box dies, the phones still have the core.
