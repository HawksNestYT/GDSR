# Power

## Power budget (fill in with real measurements from a watt meter)
| Device | Idle (W) | Working (W) | Hours/day | Wh/day |
|---|---|---|---|---|
| NOMAD laptop (browsing) | ? | ? (~35–60 est.) | ? | ? |
| NOMAD laptop (AI query bursts) | — | ? (~60–150 est.) | ? | ? |
| Travel router | ~3–6 | ~5 | 24 | ~120 |
| Phones (each) | — | ~5–10 while charging | ~2 | ~15 |
| Meshtastic node | <1 | ~1 | 24 | ~5–15 |
| MacBook (AI) | ? | ? | ? | ? |
| **Total** | | | | **?** |

Wh/day ÷ battery Wh = days of runtime. Solar watts × ~4 sun-hours × ~0.7 losses ≈ Wh/day of solar recharge.

## Plan
- **Tier 1 (cheap):** a couple of 20,000 mAh USB‑C PD power banks (keep phones and Meshtastic going for days)
- **Tier 2:** **LiFePO4 power station, 500 Wh–1 kWh** (Bluetti/EcoFlow/Anker/Jackery class). LiFePO4 = thousands of cycles, safer chemistry
- **Tier 3:** **100–200 W folding solar panel** compatible with the station's input (check the voltage/connector)
- **Car as a generator:** a 12 V car outlet or a small inverter can top up power banks while you drive

## Rules
- Run the AI in **bursts**, not all day. Library browsing is cheap, AI is expensive.
- **Charge from USB‑C directly** when possible. DC→AC→DC (going through the inverter) wastes 10–20%.
- Store power stations at 50–80% charge and **top them up every 3 months**.
- [ ] Measure the real draw of each device and fill in the table
- [ ] Do a 24-hour "grid down" test on the power station, log results in [log.md](log.md)
