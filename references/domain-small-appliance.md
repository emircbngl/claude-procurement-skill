# Domain: Small Appliance (countertop / handheld)

Coffee makers, espresso machines, blenders, food processors, air fryers, electric kettles, toasters, stand mixers, vacuum cleaners (cordless), robot vacuums, hair dryers, irons.

## Research dimensions
- **functional_specs**: power (W), capacity (L / g / cups), noise (dB), specific functional metric (espresso: bar pressure + boiler size + PID; vacuum: suction Pa + battery min; blender: motor W + jar material; air fryer: capacity L + temperature range), control type (mechanical / electronic / app)
- **quality_signals**: brand reputation in category (Vitamix/Blendtec for blenders; Breville/Rancilio/Lelit for espresso; Dyson/Tineco/Roborock for vacuums; KitchenAid for stand mixers), independent testing (RTINGS for vacuums, Project Farm, Specialty Coffee shops for espresso)
- **economic**: purchase + consumables (filters, descaler, blades, jars), expected lifespan (espresso 5–15yr depending on tier, blender 5–10yr, air fryer 3–5yr), repair vs replace economics
- **usage_fit**: usage frequency (daily commute coffee vs weekend host), skill level (espresso: beginner needs auto vs prosumer wants manual), kitchen counter footprint, storage between uses

## Required user inputs (overrides universal)
- **Counter footprint** (W × D) — small kitchens can't fit large machines
- **Power circuit** (some espresso/induction kettles want 16A circuit, not shared with high-draw)
- **Water hardness** — affects descaling cadence + boiler longevity for water-using devices
- **Cabinet height** for storage (stand mixer 30–40cm tall, may not fit upper cabinet)
- For espresso: bean type (whole vs pre-ground), grind freshness preference (grinder = mandatory companion)

## Standards & compatibility axes (per category)

### Espresso machine

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Group head** | 58mm (commercial / prosumer), proprietary (most home) | 58mm uses standard portafilter + tampers (huge accessory ecosystem); proprietary locks user in |
| **Boiler type** | Single boiler (slow steam), heat exchanger (HX), dual boiler, thermoblock (cheap) | Dual boiler best; HX good compromise; single boiler annoying for milk + espresso back-to-back |
| **Pressure** | 9 bar spec for proper espresso; 15-bar pumps are commonly oversold | Look for pressure profiling, not max-bar marketing |
| **PID** | Yes / No | PID = temperature stability; non-PID drifts during use |
| **Grinder mandatory** | Yes for any "real" espresso | Pre-ground = stale; budget for grinder as part of TCO |

### Blender

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Motor** | W rating (1000W+ for ice/frozen), peak vs continuous | Continuous spec matters; peak is marketing |
| **Jar material** | BPA-free plastic (Tritan), glass, stainless | Stainless = no taste/smell retention; glass heavy + can shatter |
| **Container size** | Personal (single-serve), family (1.5–2L) | Mismatched sizes = food doesn't blend |
| **Tamper / accessory** | Vitamix tamper, Blendtec gentle pulse | Affects what you can blend (nut butters need tamper) |

### Robot vacuum

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Navigation** | Random / camera-based / LiDAR | LiDAR best for multi-room mapping; random = budget tier |
| **Suction** | Pa rating (2000+ for pet hair, 5000+ premium) | Higher = better but louder |
| **Mop integration** | None / pad / sonic mop / self-cleaning station | Self-cleaning station = much higher purchase but lower ongoing maintenance |
| **App platform** | Brand app, Matter, Apple Home, Google Home, Alexa | Matter best for cross-platform; brand-only is lock-in |
| **Battery type** | proprietary | Replacement batteries from third party often work but void warranty |

### Cordless stick vacuum

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Battery** | proprietary per brand (Dyson V series, Tineco, Roborock) | Replacement battery part of long-term TCO; verify part availability before buying |
| **Brush head ecosystem** | Brand-specific attachments | Buying into a brand = also buying its accessory ecosystem |

## Common pitfalls

- **Espresso without grinder** — pre-ground stales in 15min after grinding; serious espresso requires concurrent grinder budget (often 50–100% of machine cost).
- **Blender motor burnout from continuous frozen blending** — undersized motor + ice = early failure. Vitamix/Blendtec for ice.
- **Robot vacuum on dark/black flooring** — many models can't navigate or detect edges (cliff sensors fail on dark surface) → stair falls.
- **Hard water in espresso machine without descale routine** — scale builds up in 6mo, can crack boiler. Monthly descale or use bottled filtered water.
- **Counterfeit Dyson / Vitamix / Roborock** on third-party marketplace sellers (Amazon Marketplace, eBay, regional marketplaces) — gray-market or counterfeit with no warranty. Stick to first-party retailer or authorized brand store.
- **Air fryer capacity vs marketing claim** — "5L" might fit only 2 chicken breasts; check actual basket dimensions, not L spec.
- **Smart appliance vendor app discontinued** — IoT vacuums lose mapping data when brand app shuts down. Choose brands with proven long support OR open-protocol (Matter).
- **Replacement parts EOL** — small appliance brands phase out parts at 5–7yr; check parts availability before buying.

## Regional notes

- **Local-brand budget tier**: most regions have inexpensive local brands with acceptable quality + accessible service. Premium imports usually carry significant markup vs origin-market pricing.
- **Premium import warranty**: brands like Vitamix, Breville, Dyson, Roborock, Tineco enforce regional warranty — verify authorized distributor in user's country; gray-market voids warranty.
- **Voltage / plug compatibility**: cross-border import (e.g., 110V US appliance to a 220V market) requires step-up transformer or won't work; verify voltage compatibility before import.

## B2B variant (cafe / office / hospitality)
- Commercial-grade builds (cast brass groups, larger boilers, 220V single-phase or 380V three-phase depending on region)
- Service contracts and parts availability take precedence over consumer features
- Health-code / food-safety compliance for food-prep appliances in commercial use — verify user-region's specific requirements (US: NSF / ServSafe; EU: HACCP-aligned; other regions: national food-safety authority)
- Volume / multi-unit discount applies

## Trusted sources for web fallback

- [Whole Latte Love](https://www.wholelattelove.com), [Seattle Coffee Gear](https://www.seattlecoffeegear.com) — espresso
- [Home-Barista forum](https://www.home-barista.com) — espresso community deep-dives
- [RTINGS vacuums](https://www.rtings.com/vacuum) — robot + cordless vacuums, raw data
- [Wirecutter](https://www.nytimes.com/wirecutter/) — countertop appliances
- [America's Test Kitchen / Cook's Illustrated](https://www.cooksillustrated.com) (paywalled) — gold-standard cooking-tool testing
- [Project Farm](https://www.youtube.com/@ProjectFarm) — durability comparisons
- [r/espresso](https://reddit.com/r/espresso), [r/Coffee](https://reddit.com/r/Coffee), [r/Vacuums](https://reddit.com/r/Vacuums)
