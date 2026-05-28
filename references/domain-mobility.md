# Domain: Personal Mobility (e-bike, e-scooter, e-skateboard, e-moped, EUC)

Battery-dominated TCO, regulatory grey-area in many regions, safety-critical, fast-evolving market.

## Research dimensions
- **functional_specs**: motor (W rated + W peak), battery (Wh = V × Ah), range (claimed vs real, often 50–70% of claim), top speed (legal vs unlocked), payload kg, weight kg, frame/deck size, suspension, brake type (drum / disc / regen), waterproofing (IPX rating), connectivity (app required?)
- **quality_signals**: brand reliability (Specialized / Trek / Giant for e-bike; Apollo / Segway / Ninebot for e-scooter; Onewheel / Future Motion / Backfire for e-skate), independent crash testing (rare), owner forums for common failures (controller, throttle, battery cell groups)
- **economic**: purchase + replacement battery (30–50% of vehicle cost every 3–5yr) + tires (e-scooter tires last 1500–3000km) + service + insurance + helmet/gear + parking/charging infrastructure
- **usage_fit**: commute (range + carry weight) / recreation (range + comfort) / last-mile (portability + folding) / sport (performance)

## Required user inputs (overrides universal)
- **Commute distance** + **terrain** (flat vs hilly significantly affects motor + battery sizing)
- **Storage** (theft risk requires lock-budget; apartment without elevator + heavy = won't be ridden)
- **Carry / fold** required (subway, bus, train, car-trunk fit)
- **Legal classification** in user's region (TR speed limits, EU L1e-A / L1e-B class, US Class 1/2/3 for e-bikes)
- **Rider weight + ride frequency** (battery degrades faster with deep cycles + heavy load)
- **Existing helmet / gear** (gear is required investment ~10–20% of vehicle cost)

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **E-bike class (EU/TR)** | L1e-A (low-power moped 25 km/h 1 kW), L1e-B (moped 45 km/h 4 kW), conventional pedelec (250W 25 km/h, no plate needed in EU/TR), S-Pedelec (250W+ 45 km/h, requires plate/insurance) | Regulatory class dictates licensing, insurance, helmet, where it can be ridden |
| **E-bike class (US)** | Class 1 (pedal assist 20 mph), Class 2 (throttle 20 mph), Class 3 (pedal assist 28 mph) | Each city/state varies on bike-path eligibility |
| **Battery chemistry** | Li-ion NMC (most), LiFePO4 (longer cycle life, heavier, used in some e-scooter/EUC) | LiFePO4 safer, 2000+ cycle vs NMC 500–1000; not always available |
| **Battery cells brand** | LG, Samsung, Panasonic, BAK, "no-name" | Branded cells = better life + safety; no-name = fire risk |
| **Charger** | brand-proprietary connector, voltage matched to pack | Wrong charger = fire / brick; verify V + connector |
| **E-bike motor type** | mid-drive (Bosch / Shimano EP / Brose / Yamaha / Bafang) vs hub-drive | Mid-drive: better hill climb, replaceable wheel, more expensive; Hub: cheaper, easier service for the wheel, worse on hills |
| **Tire (e-scooter)** | air-filled / honeycomb solid / sealed-foam | Air = best ride, puncture risk; solid = puncture-proof, rougher; some scooters proprietary tire requiring brand source |
| **Charging time** | hours (4–8 typical) | Fast charging available on some models; reduces battery life if used always |
| **Folding mechanism** | latch, lever; locking quality varies | Bad folding mechanism = ride hazard; check reviews + return-rate |
| **Display / app** | proprietary integrated, BLE app, none | App-required scooters become bricks if vendor discontinues app |
| **Replacement parts** | OEM ecosystem, third-party (Bafang, generic), DIY | Some brands lock down with proprietary controllers; serviceability varies hugely |

## Common pitfalls

- **Range claim 70% of reality** — vendor claims always under ideal conditions (single rider, flat, 25 km/h, 20°C). Real range often 50–70% of claim, less in cold.
- **Battery degradation** — typical 70–80% capacity at 500 cycles. After 3–4yr daily use, range drops by 25–35%. Replacement battery expensive.
- **Counterfeit cells / fire risk** — cheap unbranded battery packs cause fires in apartments. Stick to brand-cell vendors.
- **Charger left plugged in unattended** — multiple residential fires from cheap chargers. Buy from authorized; charge in fire-resistant area.
- **TR / EU legal speed limits** — pedelec 25 km/h is the legal cap without registration. Many e-bikes ship unlocked / can be unlocked → fines + insurance issues.
- **E-scooter on bike path / pavement** — depending on city, may be illegal. TR Istanbul/Ankara have shifting regulations.
- **Helmet not worn** — most serious injuries on PEVs are head; helmet should be in TCO budget.
- **Theft** — high-value e-bikes are #1 target for organized theft in cities; locks + insurance + GPS tracker mandatory.
- **App-locked vehicle** — Segway / Ninebot won't run without app pairing on some models. App outage = no ride.
- **Folding fatigue** — folding mechanism is the failure point; cracked welds at hinge area common at 1–2yr daily folding.
- **EUC / Onewheel skill barrier** — high injury rate without practice; not impulse-buy products.

## Regional notes

- **Local PEV regulations**: e-scooter / e-bike rules vary widely and change often (speed caps, license plate requirements, bike-path eligibility, mandatory insurance, age limits). Check user's national + city-level transport authority before purchase.
- **Helmet law**: required in some regions, voluntary in others; always recommended regardless of law.
- **Battery import restrictions**: lithium battery shipments restricted internationally (UN 3480 / 3481); pre-built e-vehicle is preferred over importing a replacement battery cross-border.
- **Shared / micromobility availability**: many cities have shared e-scooter/e-bike services (Lime, Bird, Voi, Marti, Tier, etc.) — viable alternative to ownership for occasional use; see `option-space.md`.
- **Insurance**: in many regions e-bike / e-scooter requires liability insurance over a speed threshold; verify before assuming ownership cost is just purchase.

## B2B variant (fleet / delivery)
- Commercial-grade reliability + service uptime requirements
- Fleet management software, GPS tracking, individual rider/serial accountability
- Insurance + corporate liability
- Charging infrastructure (cargo bikes need overnight 220V; sharing fleets need fast-charge swap-batteries)
- Maintenance contracts with replacement vehicle during downtime

## Trusted sources for web fallback

- [Electrek](https://electrek.co) — e-bike + EV reviews and news
- [ElectricBikeReview](https://electricbikereview.com) — e-bike specialty
- [BicyclingDoctor / Bike Rumor](https://bikerumor.com) — e-bike + e-MTB
- [The Verge mobility](https://www.theverge.com/transportation)
- [r/ebikes](https://reddit.com/r/ebikes), [r/ElectricScooters](https://reddit.com/r/ElectricScooters), [r/onewheel](https://reddit.com/r/onewheel), [r/ElectricUnicycle](https://reddit.com/r/ElectricUnicycle)
- [Endless Sphere](https://endless-sphere.com) — DIY e-mobility deep technical
- Regional: country-specific cycling / e-mobility forums + complaint aggregators reveal failure-mode patterns by climate and use-case — search `"<brand> <model> issues <country>"` to surface them.
