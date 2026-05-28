# Domain: PC (desktop build / upgrade)

## Research dimensions
- **functional_specs**: CPU (cores/threads/base+boost clock/TDP/cache/iGPU), GPU (memory size/bus/TDP/length/connectors/required PSU wattage), RAM (DDR4/DDR5, speed MT/s, latency CL, capacity, kit configuration), storage (NVMe/SATA/HDD, PCIe gen, capacity, endurance TBW), PSU (wattage, efficiency rating, modular/non-modular, connector set), case (form factor, GPU clearance, cooler clearance, radiator support, drive bays), cooler (air vs AIO, TDP rating, height), motherboard (chipset, VRM phases, PCIe gen, M.2 slots, IO panel)
- **quality_signals**: brand reliability (NewMaxx SSD tier list, JonnyGuru PSU tier list, GamersNexus reviews, Hardware Unboxed long-term), Amazon/Newegg review patterns, RMA experience reports
- **economic**: street price tracking via PCPartPicker/Newegg, used GPU market (eBay sold), expected lifespan (CPU 5–8 yrs, GPU 4–6 yrs, PSU 7–10 yrs, NVMe ~5 yrs heavy use)
- **usage_fit**: office / general / 1080p gaming / 1440p gaming / 4K gaming / esports high-refresh / streaming / content creation (Premiere/DaVinci/Blender) / 3D rendering / AI workloads / NAS / HTPC / HomeLab

## Required user inputs (overrides universal)
- Use case + target resolution + refresh-rate target (gaming)
- Peripherals already owned (monitor, keyboard, mouse, GPU, OS license)
- Existing parts to reuse (especially case, PSU, storage, OS)
- Quietness preference (silent / quiet / acceptable / don't care)
- Aesthetic constraints (RGB on/off, color scheme, window/no-window)
- Linux compatibility required?
- Overclocking interest?

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **CPU socket** | Intel LGA1200 (10/11th gen), LGA1700 (12/13/14th gen), LGA1851 (Core Ultra Series 2 / Arrow Lake) · AMD AM4 (Ryzen 1000–5000), AM5 (Ryzen 7000+) · sTRX4 (Threadripper), TR5/SP6 (Threadripper Pro 7000+) | Motherboard socket must match CPU; verify BIOS supports specific CPU |
| **Chipset** | Intel: B660/B760/H670/Z690/Z790/B860/Z890 · AMD: B650/B650E/X670/X670E/B850/X870/X870E | Determines features (PCIe lanes, OC support, USB4); not socket-compatibility but feature gating |
| **RAM** | DDR4 (older) vs DDR5 (newer) — board + CPU generation determines support, not interchangeable. ECC vs non-ECC depending on platform | RAM type must match board's supported type; check QVL for tested kits at target speed |
| **RAM channels** | Dual / quad (HEDT/server) | Populate matched pair (slots 2+4 typical) for dual-channel; quad needs 4-stick set on supporting platforms |
| **PCIe** | Gen 3 / Gen 4 / Gen 5 + ×1/×4/×8/×16 lane counts | GPU bandwidth runs at min(GPU spec, slot spec); also affects NVMe drive speed |
| **PSU 12V connectors** | 24-pin ATX, 4+4-pin EPS (CPU), 6+2-pin PCIe (GPU), 12VHPWR / 12V-2×6 (RTX 40/50 series) | GPU power must match PSU; old PSU may need 12VHPWR adapter (fire-risk on early adapters) |
| **PSU wattage** | 450W / 550W / 650W / 750W / 850W / 1000W / 1200W+ | Sum component max draw + 30% headroom; check GPU manufacturer's PSU recommendation |
| **PSU efficiency** | 80+ White / Bronze / Silver / Gold / Platinum / Titanium | Higher = lower waste heat + lower bill; significant only at sustained high load |
| **Case form factor** | E-ATX / ATX / mATX / mini-ITX / SSI-EEB | Motherboard must fit case; case spec lists supported form factors |
| **Case GPU clearance** | mm length spec | Modern GPUs 300–360 mm common; case spec must support card length |
| **Case CPU cooler clearance** | mm height spec | Tower air coolers 150–170 mm common; case spec must support cooler height |
| **Case radiator support** | mm × position (top/front/side) | AIO 240/280/360/420 mm needs matching case mount |
| **CPU cooler bracket** | AM4 / AM5 / LGA1700 / LGA1851 / LGA1200 etc. | Many AM4 coolers cross to AM5 with same/free bracket (Noctua does this well); LGA1700 needs taller bracket than LGA1200 |
| **M.2 slot** | M-key vs B-key, SATA vs PCIe, Gen3/4/5 ×4 | Drive interface must match slot type; some slots share lanes with PCIe/SATA |
| **Storage SATA** | SATA 6 Gb/s standard | Universally compatible across modern boards |
| **Display output** | HDMI 2.0/2.1, DisplayPort 1.4/2.0, USB-C DP-alt | Monitor max refresh/resolution gated by output spec |
| **OS license** | Windows OEM/Retail, Linux free | Reusing existing Windows OEM is fine; OEM tied to original board for license validation |

## Common upgrade pitfalls

- **DDR4 mobo + DDR5 RAM** = won't boot. DDR4 and DDR5 sticks are physically keyed differently but the platform must match.
- **12VHPWR-only GPU on older PSU needs adapter** = early 12VHPWR adapters caused melting connector failures on RTX 4090s; use ATX 3.0 / 3.1 PSU with native 12V-2×6 when possible.
- **AM4 cooler may or may not fit AM5** = depending on bracket. Noctua / many premium brands ship free upgrade brackets. Cheap towers often don't.
- **AM5 needs DDR5** — no DDR4 path (unlike Intel 12/13/14th gen which supported both).
- **PCIe Gen 5 NVMe + Gen 4 slot** = drive runs at Gen 4 speed, no benefit from Gen 5 controller.
- **iGPU absent (F-suffix Intel, X-suffix AMD pre-7000)** = needs discrete GPU to display anything.
- **High-TDP CPU with weak cooler** = throttles under load; check Cinebench R23 sustained perf vs spec.
- **Mini-ITX case + long GPU** = won't fit; ITX builds need careful clearance check.
- **PSU sleeved cables from one brand to another** = often incompatible pinout; can fry components. Only use cables matched to specific PSU.
- **BIOS too old for new CPU** = LGA1700 boards need BIOS update for 13/14th gen on B660/H670 boards bought at launch.
- **AM5 BIOS too old for Zen 5** = older X670/B650 may need BIOS update to boot Ryzen 9000.

## Trusted sources for web fallback

- [PCPartPicker](https://pcpartpicker.com) — first stop for compatibility + pricing (US/UK/DE/etc.)
- [GamersNexus](https://gamersnexus.net) and [Hardware Unboxed YouTube](https://www.youtube.com/@HardwareUnboxed) — review depth
- [NewMaxx Google Doc](https://docs.google.com/spreadsheets/d/) — SSD tier list (community-maintained)
- [PSU Tier List (Cultists Network)](https://cultists.network/140/psu-tier-list/) — PSU reliability ranking
- [TechPowerUp](https://www.techpowerup.com) — GPU/CPU databases + reviews
- [Logical Increments](https://www.logicalincrements.com) — build tier reference
- [r/buildapc](https://reddit.com/r/buildapc), [r/buildapcsales](https://reddit.com/r/buildapcsales), [r/hardwareswap](https://reddit.com/r/hardwareswap)
- PCPartPicker indexes most major Western markets (US/UK/DE/CA/AU/FR/IT/ES + more). For regions PCPartPicker doesn't cover, search `"PC components price comparison <country>"` to find local PC-component retailer aggregators; pricing must be manually compiled in those regions.
- Manufacturer QVL (qualified vendor list) for RAM compatibility — ASUS / MSI / Gigabyte / ASRock each publish for their boards
