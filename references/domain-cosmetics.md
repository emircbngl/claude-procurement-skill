# Domain: Cosmetics (skincare, makeup, fragrance, haircare)

Highly counterfeit-prone, ingredient-driven, allergy/skin-type-sensitive. Authorized-channel verification is non-negotiable.

## Research dimensions
- **functional_specs**: active ingredients (concentration % matters: retinol 0.3% vs 1%, vitamin C 10–20%, niacinamide 5–10%, SPF 30/50+), formulation type (serum/cream/oil/gel), pH (for actives), packaging (airless pump prevents oxidation of vitamin C/retinol), volume, fragrance-free
- **quality_signals**: independent lab analysis (PAULA'S Choice ingredient analyzer, INCIDecoder, Skincarisma), dermatologist endorsements, peer-reviewed efficacy studies, owner-reported reactions
- **economic**: cost per ml/g (not per bottle), shelf life after opening (PAO symbol — 6M/12M/24M), repurchase cadence, sample-vs-full-size strategy
- **usage_fit**: skin type (dry/oily/combo/sensitive/mature), specific concerns (acne/pigmentation/aging/dehydration), routine position (cleanse → tone → treat → moisturize → SPF), morning vs evening, seasonal

## Required user inputs (overrides universal)
- Skin type + sensitivities + known allergies
- Existing routine (so new product slots in, doesn't conflict — e.g., retinol + vitamin C timing)
- Pregnancy / breastfeeding status (excludes retinoids, hydroquinone, salicylic acid >2%)
- Region (formulations differ — EU bans many UV filters US allows; Asian SPF often higher)
- Pro tier (dermatologist-grade / Rx) or OTC?

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Ingredient layering** | water-based → oil-based; thinnest → thickest | Layer in increasing viscosity; pH-sensitive actives need pH-matched skin (vitamin C at pH<3.5) |
| **Actives that don't mix** | retinol + AHA/BHA/vitamin C (irritation); benzoyl peroxide + retinol (deactivation) | Stagger AM/PM or alternate nights |
| **SPF system** | chemical (avobenzone, octinoxate, octocrylene) vs mineral (zinc oxide, titanium dioxide) | Mineral safer for sensitive; chemical lighter texture; check reef-safe restrictions |
| **Packaging** | airless pump / opaque tube / open jar / dropper | Vitamin C and retinol degrade in light/air → require opaque + sealed |
| **EU vs US/JP/KR regulation** | EU bans 1300+ ingredients vs US ~30 | Region-specific reformulation; same brand can have different formula per region |
| **Halal / vegan / cruelty-free** | Halal-certified, Vegan Society, Leaping Bunny | Affects ingredient sources (no animal-derived, e.g., carmine, lanolin, beeswax) |
| **Allergen disclosure** | EU 26 mandatory allergens (limonene, linalool, etc.) | Surface for sensitive users |

## Common pitfalls

- **Counterfeit on marketplaces** — luxury brands (La Mer, SK-II, Dior, Lancôme, etc.) are heavily counterfeited on most third-party marketplaces globally (Amazon Marketplace, regional marketplace third-party sellers). Stick to brand boutique, official brand website, Sephora, or country-specific authorized drugstore chains.
- **Gray market with no batch code** — original formulation may differ; warranty/return policy varies.
- **Expired / past-PAO product** — opened jars have 6/12/24-month shelf life shown by PAO symbol. Check production date (batch code lookup at checkcosmetic.net).
- **pH-incompatible actives** — vitamin C in alkaline serum is inert; check formulator's pH claim.
- **Active overload** — combining 3+ actives causes barrier damage and rebound issues. Less is more.
- **Patch-test skipped** — any new active should be patch-tested 48h on inner forearm before face application.
- **Sun exposure with retinoids/AHAs without SPF** — photosensitizing; SPF mandatory.

## Sourcing standards (region-agnostic)

| Tier | Authorized channels |
|------|---------------------|
| Premium / luxury | Brand boutique, Sephora (or regional equivalent), official brand website (country TLD) |
| Mid-tier / drugstore | Country-specific authorized drugstore chains (CVS / Walgreens / Boots / dm / Watsons / Gratis / Müller, etc.), pharmacy chains, department-store cosmetics counters |
| Korean / Asian | YesStyle, Stylevana, OliveYoung Global, regional importer of Asian-beauty brands; verify the brand has a regional distributor for warranty / batch traceability |
| Niche / indie | Brand's own webstore preferred over marketplaces |

Verify authenticity: most premium brands have a batch-code or QR-verification page on their official site (search `"<brand> verify authenticity"` or `"<brand> batch code"`).

## B2B variant (spa / salon / clinic)
- Professional-grade formulations (higher actives, larger volumes)
- Sourcing through medical/aesthetic distributors (not retail)
- Sterility + bulk packaging
- Regulatory: cosmetic vs cosmeceutical vs medical device classification (different paths)
- Liability insurance considerations

## Trusted sources for web fallback

- [INCIDecoder](https://incidecoder.com), [Skincarisma](https://www.skincarisma.com) — ingredient analysis
- [Paula's Choice ingredient dictionary](https://www.paulaschoice.com/ingredient-dictionary)
- [Beautypedia](https://www.beautypedia.com) — reviews + ingredient assessments
- [r/SkincareAddiction](https://reddit.com/r/SkincareAddiction), [r/AsianBeauty](https://reddit.com/r/AsianBeauty) — community reviews
- [CheckCosmetic.net](https://checkcosmetic.net) — batch code → manufacture date lookup
- [SCCS opinions](https://health.ec.europa.eu/scientific-committees/scientific-committee-consumer-safety-sccs_en) — EU scientific safety opinions
- Brand's own publication record (PubMed for serious actives)
