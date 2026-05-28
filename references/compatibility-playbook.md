# Compatibility playbook

For any upgrade or existing-ecosystem purchase, the question isn't "is this product good?" — it's "will this product work with what I already own?" A great-on-paper part that doesn't fit is a refund queue, not an upgrade.

Run this **only when** intent = upgrade OR the user has stated existing ecosystem gear. For new-from-scratch purchases, skip this and use the domain pack's internal-compat check instead (e.g., for a new PC build, verify CPU↔mobo↔RAM↔PSU↔case among the candidate parts).

## The compatibility matrix

Build a table that crosses **existing parts** (from step 3 context extraction) against **candidate parts** (from step 5 RFI).

| Existing part | Candidate | Standard / axis | Compatible? | Notes / source |
|---|---|---|---|---|
| Giant Revolt frame, BSA BB, 142×12 thru-axle, flat-mount brakes | Hunt 4-Season Disc wheelset, Centerlock, 142×12 | Hub spacing + rotor mount | ✓ | Matches both axle width and rotor standard |
| 11sp 105 R7000 shifter | SRAM XPLR 1×12 derailleur | Drivetrain speed + shifter/derailleur protocol | ✗ blocker | Shimano 11sp shifters do not pull SRAM 12sp ratio |
| AM4 cooler with original bracket | AM5 CPU | Cooler bracket | ⚠ adapter | Some AM4 coolers reuse with adapter; verify per cooler model |

## Three compatibility verdicts

- **✓ Compatible** — drops in, no adapter, no caveat.
- **⚠ Adapter / partial** — works with an adapter or in a degraded mode. Document the adapter SKU + cost; flag in TCO.
- **✗ Blocker** — physically or electrically incompatible. Candidate gets disqualified.

## Compatibility data sources

Per axis, use this priority:

1. **Manufacturer compatibility chart** — Shimano / SRAM publish tier-by-tier compat tables; ASUS publishes RAM QVLs; etc. Always check brand site first.
2. **Domain pack** — `domain-<name>.md` lists the canonical standards table.
3. **Reputable third-party** — BikeRadar, GamersNexus, GCN, Linus Tech Tips have ongoing compat content.
4. **Forums / Reddit** — useful for edge cases, but require ≥2 corroborating sources before treating as authoritative.
5. **Web search**: `"<existing-part> compatible with <candidate-part>"` — read 2+ sources before deciding.

**Citation rule**: standards/compat claims require **≥2 independent sources** before going in the report.

## Common multi-axis pitfalls

Some candidates pass a single-axis check but fail at the system level:

- **PC**: AM5 CPU + AM4 cooler + AM5 mobo — cooler may fit but airflow patterns differ; check cooler manufacturer's AM5 support list, not just bracket compatibility.
- **Bike**: 142×12 hub + 12sp cassette + 11sp drivetrain — wheel spacing correct, but cassette won't index with the existing shifter.
- **Camera**: lens mount matches, but lens is full-frame and body is APS-C — works but crops; check sensor format compatibility.
- **Audio**: connector matches, but headphone impedance (300Ω) exceeds amp drive capability — physically fits but underperforms.

For each candidate, walk the **full chain** of axes from the domain pack, not just the obvious one.

## Output

The completed matrix goes into the report's "Compliance & validation → Compatibility matrix" section. Every blocker becomes a Do-Not-Buy reason. Every adapter becomes a TCO line item.
