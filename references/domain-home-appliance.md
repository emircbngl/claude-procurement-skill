# Domain: Home Appliance (major / white goods)

Washer, dryer, dishwasher, refrigerator, freezer, oven, cooktop, range hood, water heater, HVAC. High-spend, multi-year horizon, installation constraints critical, energy efficiency dominates TCO.

## Research dimensions
- **functional_specs**: capacity (kg load, L volume), efficiency class (EU energy label A–G, scaled 2021), noise level dB, water consumption L/cycle, cycle programs, smart features, install type (freestanding/built-in/integrated), connection standard (gas/electric/dual-fuel for cooking)
- **quality_signals**: brand reliability index (Consumer Reports brand surveys, Stiftung Warentest, Yandex.Market user ratings), MTBF / mean time to first repair, recall history, owner forums for common failures (e.g., AEG dishwasher pumps, certain LG compressors)
- **economic**: purchase + delivery + installation + parts/service over 8–12yr lifespan, energy cost / year (kWh × hours × kWh price), water cost / year, consumables (filters, salt for dishwasher, descaler)
- **usage_fit**: household size, dietary patterns (large oven for hosting vs single-person), hard-water region (calcium handling), apartment-noise tolerance, kitchen layout constraints

## Required user inputs (overrides universal)
- **Cutout dimensions** for built-in/integrated (W × H × D in mm); plus door swing clearance
- **Plumbing connections** (washer/dishwasher water inlet + drain height + position)
- **Gas vs electric** preference for ovens/cooktops; gas requires existing connection or installation
- **Electrical** — single-phase 16A standard household vs 3-phase for high-power ovens/induction
- **Water hardness** in user's region (affects dishwasher salt, descaling cadence, washer detergent dosing)
- **Energy tariff** kWh price (varies hugely by region/contract)

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **EU energy label** | A–G (re-scaled 2021), measured under EU 2017/1369 | Use EPREL.ec.europa.eu QR-lookup; ratings comparable within product category only |
| **EU repairability index** | A–E (mandatory for smartphones/tablets since 6/2025; expanding to appliances) | Higher = easier/cheaper repair; affects TCO |
| **Voltage / frequency** | 220–240V 50Hz EU/TR; 110–120V 60Hz US/JP | Cross-border buy needs converter or different SKU |
| **Plug type** | Type F (EU/TR Schuko), Type G (UK), Type A/B (US) | Adapters work for low-power; high-power appliances need direct compatible plug |
| **Built-in cutout** | Standardized 600mm/900mm widths for ovens/dishwashers; brand-specific depths | Cabinet cutout must match appliance spec exactly; even 2mm matters |
| **Hood ducting** | duct-out (best) vs recirculating (filter-only) | Recirculation cheaper to install but lower performance; duct-out needs external wall path |
| **Refrigerant** | R600a (isobutane, EU/TR standard), R134a (older), R290 (propane, commercial) | Service requires refrigerant-matched technician; future-proof = R600a/R290 |
| **Smart-home protocol** | Wi-Fi, Matter, Brand-app-only, Zigbee (rare) | Matter best for cross-brand interop; brand-app risks vendor lock-in / EOL |
| **Drainage** | gravity drain vs pump | Dishwasher/washer drain hose max-height spec (typically 1–1.2m) — kitchen design constraint |

## Common pitfalls

- **Cutout mismatch** — ordering a 60cm appliance for a 59cm cabinet means it won't slide in. Verify TR-spec cutouts match the EU dimension on the spec sheet.
- **Door swing clearance** — fridges and dishwashers need clearance for door at 90°+; corner installations get stuck.
- **Water inlet pressure** — some Bosch/Siemens dishwashers require min 1 bar; rural / top-floor with low pressure = pump issue.
- **Hard-water effect** — uncalibrated water-softener salt level in dishwasher → spotting + scale. Must set hardness on first use.
- **High-power induction on 16A circuit** — full-power double-burner can trip standard breaker; check kW draw vs panel capacity.
- **Gas conversion fees** — LPG-to-natural-gas conversion kits cost ~500–1500 TRY + technician fee. Factor into TCO.
- **Energy class mislead** — "A" today is much higher bar than "A" pre-2021 rescaling; "A+++" no longer exists.
- **Counterfeit refrigerant** — service market sometimes uses non-spec refrigerant; demand R600a fill on R600a units.
- **Smart-features EOL risk** — brand pulls app support 5 yrs in; appliance still works but smart features die.
- **Recall checks** — Beko/Indesit/Whirlpool have had fire-risk recalls in EU; verify model isn't on recall list before buying used or even new old stock.

## Regional notes

- **Local vs imported brands**: most regions have strong local brands (Bosch/Siemens in DE-influenced markets, Whirlpool/GE/Maytag in NA, Haier/Hisense in CN, LG/Samsung globally, regional brands elsewhere) with longer parts availability and easier service. Imported brands may offer features at higher cost + longer parts lead time.
- **Service network in-country**: verify the brand has authorized service in user's region (call a service center to confirm parts in stock for the specific model). 10+ year parts availability is a strong reliability signal.
- **Trade-in programs**: many appliance brands run trade-in promos (usually 10–20% off new with old unit handover); ask the dealer.
- **Energy-tariff variability**: kWh prices vary 10× across regions and tariff plans — TCO energy line is highly region-sensitive.

## B2B variant (rental property / dorm / commercial)
- Heavy-duty / professional series (Miele Professional, Whirlpool Commercial, Electrolux Professional)
- Coin-op / token / app-controlled where applicable
- Compliance: commercial certification often required for hospitality use (regulations vary by region — check local hotel/short-term-rental rules)
- Service contract included with purchase (4–8yr extended), critical for downtime cost
- Multi-unit volume discount applies

## Trusted sources for web fallback

- [EPREL EU energy database](https://energy-efficient-products.ec.europa.eu/eprel_en) — authoritative energy label lookup
- [Consumer Reports](https://www.consumerreports.org) — paywalled brand reliability surveys
- [Stiftung Warentest](https://www.test.de) (German, paywalled) — gold-standard EU appliance testing
- [Wirecutter](https://www.nytimes.com/wirecutter/) — top-pick reviews
- [Reviewed.com](https://www.reviewed.com)
- [r/appliances](https://reddit.com/r/appliances), brand-specific subreddits
- Regional complaint / review databases — most countries have an owner-complaint aggregator that reveals real-world failure modes (e.g., consumer-protection databases, country-specific complaint sites). Search `"<brand> <model> complaints <country>"` to surface them.
- Brand's region-specific site (country TLD) — pricing, parts availability, service-center finder, current promotions vary by region.
