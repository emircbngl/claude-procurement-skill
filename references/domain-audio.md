# Domain: Audio (headphones, IEMs, speakers, amps, DACs)

## Research dimensions
- **functional_specs**: driver type (dynamic / planar magnetic / electrostatic / BA + DD hybrid for IEMs), impedance Ω, sensitivity dB/mW, frequency response, ANC / passive isolation, codec support (SBC / AAC / aptX / aptX Adaptive / LDAC / LC3), battery life, microphone quality
- **quality_signals**: measurements (Crinacle IEM database, Resolve / The HEADPHONE Show, Audio Science Review SINAD), targeted-curve match (Harman target for headphones), professional reviews, industry rec (Innerfidelity legacy, Stereophile)
- **economic**: cost-vs-perceived-quality flattens above $300–500; chain cost (DAC + amp + cable + source); replacement pads / cables / drivers (modular = repairable)
- **usage_fit**: commute (need ANC + portability) / home critical listening / studio reference / mixing / gaming / sport / sleep / general

## Required user inputs (overrides universal)
- **Use environment** (loud commute requires ANC; home quiet allows open-back)
- **Source device** + its output (phone DAC vs dedicated DAC vs interface) — drives amp need
- **Music genre** influences sound-signature preference (V-shape for EDM / bass-heavy; neutral for vocal/jazz)
- **Wired tolerance** (closed-back wired vs wireless; many "premium" Bluetooth still has codec bottleneck)
- **Existing chain** (headphones to drive impedance-match amp; speakers to room-match)
- For speakers: room dimensions + treated/untreated

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Headphone connector** | 3.5mm TRS, 2.5mm balanced, 4.4mm balanced, XLR, USB-C, Lightning, proprietary (Apple) | Source output must match; balanced needs balanced source |
| **Headphone impedance** | low (16–32Ω) drives off phone; mid (32–80Ω) needs amp for high SPL; high (80–600Ω) requires dedicated amp | Underpowered amp = low SPL ceiling + flabby bass |
| **Sensitivity** | dB/mW or dB/V | Lower = needs more power; pair with high-output amp |
| **Bluetooth codec** | SBC (baseline) → AAC → aptX → aptX HD → aptX Adaptive → LDAC → LC3 | Both source AND sink must support same codec; SBC is the fallback floor |
| **Wireless protocol** | Bluetooth (universal-ish), proprietary 2.4GHz (low latency for gaming), DECT, UWB | Proprietary = transmitter + receiver brand-locked |
| **Multipoint Bluetooth** | yes / no / number of devices | Connect to multiple sources simultaneously; not all premium offers it |
| **DAC chip / format support** | PCM up to 32/384, DSD64/128/256/512 | High-res streaming sources require DAC supporting the format |
| **Amp impedance matching** | Output impedance ÷ headphone impedance ≤ 1/8 rule | Higher output impedance = colored sound + damping issues |
| **Speaker impedance** | 4Ω, 6Ω, 8Ω | Amp must support speaker impedance; under-spec amp may distort |
| **Speaker placement / room** | nearfield (1–2m), midfield (2–4m), far-field (4m+) | Room treatment + placement dominate result over speaker quality |
| **Subwoofer crossover** | 80Hz standard | Speaker low-end roll-off + sub high-end crossover should overlap |
| **Multi-channel** | 2.0 / 2.1 / 5.1 / 7.1.4 (Atmos) | Source + receiver + speaker count must all align |
| **HDMI 2.1 eARC** | for Atmos lossless TV→soundbar / receiver | Need HDMI 2.1 capable TV + ARC/eARC support |

## Common pitfalls

- **Underpowered high-impedance headphones** — DT 770 250Ω on phone = quiet, lifeless. Need amp.
- **High-output-impedance amp + low-impedance IEMs** — over-bassy, distorted. Output impedance must be ≤ Z_headphone / 8.
- **Bluetooth LDAC marketing vs actual** — LDAC bitrate adapts; "true LDAC" 990kbps only at strong signal. Drop to 660 or 330 routinely.
- **Codec mismatch** — Sony WH-1000XM5 + iPhone = AAC only, not LDAC. Brand-codec capability ≠ practical use.
- **Counterfeit AirPods / Bose / Apple cables** — pervasive on marketplaces. Buy from Apple / Bose / authorized only.
- **Room ignored for speakers** — $5000 speakers in untreated bedroom < $1500 speakers properly placed and treated.
- **DAC overspend** — for 99% of users, $100–200 DAC is sonically indistinguishable from $1000+ DAC in blind testing. ASR measurements support this.
- **Cable upgrades for digital** — USB / optical / coax / HDMI cables don't audibly differ above basic spec compliance.
- **Multipoint glitches** — devices may switch unexpectedly; some premium models still flaky in 2026.
- **Hi-res via wireless** — Bluetooth LDAC ≠ wired lossless. For true hi-res, use wired or proprietary 2.4GHz with capable source.

## Regional notes

- **Authorized distribution**: verify the brand's authorized distributor in the user's region; major audio brands (Sennheiser, Sony, Bose, Audeze, Focal, etc.) have regional distributors and gray-market units typically void manufacturer warranty in-country.
- **Cross-border savings**: audiophile-tier headphones (Sennheiser HD6xx, Beyerdynamic DT 770/880/990, planar magnetics) are sometimes 20–50% cheaper via direct-from-DE/US shipping but check landed cost (see `price-discovery.md` cross-border section) and warranty trade-off.
- **Used market**: audio gear holds value well (especially planars and tube gear); region-specific second-hand channels (Audiogon, Head-Fi classifieds, regional Facebook audiophile groups) often beat retail by 30–50%.

## B2B variant (studio / broadcast / commercial AV)
- Industry-standard reference (Yamaha NS10, Genelec, Adam Audio for studio monitors)
- Conference / commercial: XLR-only systems, redundant power, IT-managed (Dante/AVB)
- Hearing-protection / pro IEM (Shure SE846, Westone, custom-molded JH Audio)
- Service contracts; multi-unit rental for production work

## Trusted sources for web fallback

- [Crinacle IEM database](https://crinacle.com/rankings/iems/) — IEM measurement + ranking
- [Audio Science Review](https://www.audiosciencereview.com) — objective measurement focus (SINAD-led)
- [The HEADPHONE Show YouTube](https://www.youtube.com/@TheHEADPHONEShow) — Resolve + Andrew
- [Headphones.com reviews](https://headphones.com)
- [Innerfidelity archive](https://www.stereophile.com/category/innerfidelity-tyll-hertsens-archive) — Tyll Hertsens legacy
- [DARKO Audio](https://darko.audio) — hi-fi reviews
- [What Hi-Fi?](https://www.whathifi.com) — generalist audio
- [Stereophile](https://www.stereophile.com) — high-end / classical bent
- [r/headphones](https://reddit.com/r/headphones), [r/audiophile](https://reddit.com/r/audiophile), [r/budgetaudiophile](https://reddit.com/r/budgetaudiophile)
- [Head-Fi](https://www.head-fi.org) — community forum (treat threads as opinion not measurement)
