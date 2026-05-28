# Price discovery

A single "price" is a fiction. A procurement-grade workflow tracks at minimum **eight price tiers** and synthesizes them into a **fair-price band** (aspirational / target / walk-away) before the recommendation step.

## The eight price tiers

| Tier | What it is | Where to find |
|---|---|---|
| **MSRP / RRP / List** | Manufacturer's suggested retail. Anchor, not binding. Often inflated to make discounts look bigger. | Manufacturer product page |
| **Street price** | Actual transaction price across authorized retail. Always below MSRP for mature SKUs. | Regional aggregators (Google Shopping, PriceSpy, Idealo, Kakaku, regional equivalents — see step 2 table) |
| **Net price** | Out-of-pocket after coupons, cashback, loyalty, bundled rebates. **The decision anchor.** | Seller page after applying discounts |
| **Refurbished / open-box / B-stock** | Manufacturer- or retailer-restored. Open-box ~10–30% off new; refurb usually ≥90-day warranty; B-stock cosmetic-grade. | Manufacturer outlet, Best Buy Outlet, Amazon Renewed, retailer refurb |
| **Used market** | eBay **sold** listings, specialist resellers. Truth-tier for resale value. | eBay sold (`&LH_Sold=1&LH_Complete=1`), MPB/KEH (cameras), specialist forums |
| **Gray market / parallel import** | Genuine product, unauthorized channel. 10–25% cheaper but voids warranty in most regions; region-locked firmware risk. | Cross-border marketplaces |
| **Bundle price** | SKU sold with accessories/extended warranty. Standalone price often matched, bundle "discounted". | Retailer listing |
| **Trade-in residual** | OEM credit for old unit. Anchors TCO and replacement cycle. | OEM trade-in program |

## The 3-quote rule

Institutional procurement minimum: **3 independent suppliers/channels per SKU** before committing. For consumer buying, 3–7 is the practical range before admin burden exceeds informational gain. Always run at least 3 channels.

## Price-discovery sub-process

For each surviving candidate from step 5, run in parallel where possible:

### 1. MSRP capture
WebFetch the manufacturer product page. Record list price + any active OEM promo.

### 2. Aggregator scan
Use the user's region (from step 4) to pick the right aggregators. Pull top 3 lowest sellers from each.

| Region | Primary aggregators | Major first-party marketplaces |
|---|---|---|
| US | Google Shopping, PCPartPicker (for PC), Amazon, Newegg | Amazon, B&H, Adorama, Newegg, Best Buy |
| UK | PriceSpy, PriceHippo, Google Shopping | Amazon UK, Currys, John Lewis, Argos |
| EU (general) | Idealo (DE/AT/IT/FR/ES), Geizhals (DE/AT), PriceSpy (Nordics) | Amazon DE/FR/IT/ES, MediaMarkt, Saturn, Otto, Fnac |
| Canada | PCPartPicker, Newegg.ca, Google Shopping | Amazon.ca, Best Buy, Canada Computers |
| Australia | StaticICE, PCPartPicker AU, Shopbot | Amazon.au, JB Hi-Fi, Officeworks |
| Japan | Kakaku.com, Price.com | Amazon.co.jp, Rakuten, Yodobashi |
| India | Compare India, Mysmartprice, PriceDekho | Amazon.in, Flipkart, Croma |
| Turkey | Akakce, Cimri | Amazon.com.tr, Hepsiburada, Trendyol, N11 |
| Other / unlisted region | WebSearch `"<category> price comparison <region>"` to identify local aggregators | Local marketplaces + Amazon if available |

**General caveat**: aggregators surface listing price, not transacted price, and may not strip coupons / loyalty discounts. Manual spot-check at the seller page is mandatory in every region.

### 3. Price history
- Amazon SKUs: `camelcamelcamel.com/product/<ASIN>` (free, full history) or `keepa.com` (11 marketplaces, deeper data).
- Capture: lowest-ever, 90-day low, 12-month median.
- Use to detect fake "was/now" discounts — the FTC bans inflating "was" prices under 16 CFR 233.1. If price-history shows the "was" never held for >2 weeks in 6 months, the discount is fictional.

### 4. Used / refurb floor
- eBay sold listings: append `&LH_Sold=1&LH_Complete=1` to any search URL. Use median of 5–10 sales. Ignore Best Offer strikethroughs — actual sale price is hidden.
- Manufacturer certified-refurb outlet (Apple, Sony, DJI, Best Buy Outlet) — usually 10–25% off new with ≥90-day warranty.
- Domain-specific: KEH / MPB for cameras; Bicycle Bluebook for bikes; eBay for everything else.

### 5. Peer-tier benchmark
Repeat steps 2–3 at lower depth for 2–3 peer SKUs from the candidate slate. Output: peer-tier median price. Used to anchor whether the SKU itself is overpriced for its tier, independent of any one retailer's markup.

### 6. Cross-border check (optional)
Only if user signaled openness to importing.

- WebFetch the listing on a major cross-border retailer (Amazon US/DE/UK, B&H, etc.) priced in the source currency.
- Apply **landed-cost math** for the user's region: `CIF (cost + insurance + freight) + customs duty + VAT/sales tax + any excise / luxury tax + shipping`.
- Use the user-region's official customs calculator (search `"<country> import duty calculator"` and prefer the government source). Examples:
  - US: USITC Tariff Database; for personal imports the de minimis threshold varies per country of origin.
  - EU (any member state): TARIC database (`ec.europa.eu/taxation_customs/dds2/taric`).
  - UK: gov.uk Trade Tariff tool.
  - Turkey: ticaret.gov.tr.
  - Other regions: search for the equivalent national customs authority tool.
- **Verify de minimis rules** in user's region — many countries have removed or lowered the low-value customs exemption in 2024–2026; assume full duty + VAT applies unless verified otherwise.
- **Rule of thumb**: an item must be roughly **≥30–40% cheaper abroad** before import math breaks even for personal-volume buying. Exact break-even depends on the destination's duty + VAT stack.

### 7. Red-flag pass
For each top-3 seller in step 2, scan for:
- Third-party marketplace seller (vs. seller-fulfilled-by-marketplace vs. first-party retailer)
- Listing age < 30 days (new sellers = unknown reputation)
- "Was/now" discount where price-history shows the "was" never held
- Refurb listing with no warranty term or < 90-day warranty
- FX-margin manipulation on local listings of imported goods (cross-check against the user-region central bank's effective rate)
- Generic stock images instead of actual product photos
- Seller rating < 95% or < 100 reviews on first-tier marketplaces

### 8. Synthesize fair-price band
Three numbers per candidate:
- **Aspirational** = `min(12-month low, eBay sold median × 1.15)` — best plausible deal seen recently
- **Target** = `peer-tier median − 5%` — the "happy buy" price
- **Walk-away** = `min(peer-tier median + 10%, MSRP)` — ceiling; above this, kill the deal

### 9. Deliverable
Per candidate, a structured object:

```
{
  sku: "Sony WH-1000XM5",
  region: "<user region>",
  currency: "<user currency>",
  msrp: <amount>,
  current_low: <amount> (<aggregator>, <seller>),
  12mo_low: <amount> (camelcamelcamel or Keepa, FX-converted to user currency),
  used_median: <amount> (eBay sold, age <N>-months-old units),
  fair_band: { aspirational: <amount>, target: <amount>, walk_away: <amount> },
  red_flags: ["<list of any red flags from step 7>"],
  best_channel: "<retailer name + authorized status>",
  return_policy: "<window + restocking fee + shipping>",
  authorized_dealer: <true/false>
}
```

This object feeds into the TCO computation (step 7) using `target` as the assumed purchase price, and into the report's Price Discovery table.

## Key sources

Cross-region:
- **camelcamelcamel** — Amazon price history (US/UK/DE/FR/IT/ES/CA/JP/AU/MX), free, full
- **Keepa** — 11 Amazon marketplaces, paid for deep history
- **PCPartPicker** — PC components with native price history (US/UK/DE/CA/AU/FR/IT/ES + others)
- **eBay sold listings** — used-market truth in any region; append `&LH_Sold=1&LH_Complete=1`
- **MPB**, **KEH** — used camera gear with public price indices (US/EU/UK ship globally)
- **Manufacturer direct** — sometimes cheaper than authorized retailer; always check first

Regional aggregators (see step 2 table for full list per region). For any region not pre-mapped, derive via `WebSearch "<category> price comparison site <country>"`.

## Citation rule

Price data in the report: ≥1 aggregator link + ≥1 primary seller link, per candidate.
