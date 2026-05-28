# Compliance checks

Run these against every candidate in step 5. A candidate that fails a hard compliance check is **disqualified**; failures get logged with the reason.

## 1. Certification marks

Verify visible on packaging, product, or manufacturer datasheet. Missing required certifications = compliance fail.

| Mark | Region / scope | Required for |
|---|---|---|
| **CE** | EEA | Electronics, toys, PPE, medical devices |
| **UKCA** | UK | UK conformity assessment (post-Brexit; CE still accepted for some categories during transition) |
| **FCC** | US | Any RF-emitting device |
| **UL** / **ETL** | US/Canada | Electrical safety |
| **RoHS** | EU + most markets that follow EU | Electronics — restriction of hazardous substances |
| **CCC** | China | Wide range of consumer goods |
| **PSE** | Japan | Electrical product safety |
| **KC** | South Korea | Korea Certification mark |
| **RCM** | Australia / New Zealand | Regulatory Compliance Mark |
| **BIS** | India | Bureau of Indian Standards |
| **INMETRO** | Brazil | National Institute of Metrology |
| **Energy Star** | US + global (voluntary outside US) | Energy-using devices |
| **EPREL** | EU | Mandatory EU energy-label database; QR on label resolves to entry at `energy-efficient-products.ec.europa.eu/eprel_en` |
| **TÜV / GS** | DE/EU (recognized globally) | Voluntary safety mark |
| **MIL-STD-810** | Mil/industrial | Ruggedness claims |
| **IP rating** (IP67 etc.) | Global (IEC 60529) | Water/dust ingress |

Many countries require additional national marks for sale in-country (e.g., Turkey: TSE, Russia: EAC, Saudi Arabia: SASO, UAE: ECAS, Mexico: NOM). Verify the user-region's mandatory marks for the category.

For any region: an item imported via parallel/gray channel may have a globally-recognized mark (CE/FCC) but lack the local national mark required for in-country sale or warranty — surface as a risk.

## 2. Authorized-dealer / SKU verification

Especially important in any market where parallel imports are common and void manufacturer warranty. Manufacturer warranty is typically honored only by the authorized regional distributor's customers.

Checklist per candidate:
- **Authorized dealer list** — most brands publish this on their official website. Search `"<brand> authorized dealer <country>"` or check `<brand>.<country-TLD>/dealers`.
- **Hologram / GS1 QR / serial sticker** — major brands ship with verifiable hologram or QR. WebSearch `"<brand> verify authenticity"` for the brand's verification page.
- **Manufacturer warranty registration** — if the brand offers warranty registration online with serial number, the dealer must be able to provide a valid serial.
- **Box-content list** — gray-market items often miss accessories, region-specific charger/plug, or printed manual in the local language.
- **Region-locked features** — some firmware locks (Wi-Fi channels, broadcast bands, video frame rates, mobile carrier compatibility) make gray-market units underperform or fail locally.

Red flags:
- Seller listing significantly below authorized-dealer price
- Marketplace listing with no return option or 7-day-only return
- Refurbished without explicit "manufacturer refurbished" + warranty term
- Listing uses generic stock images, not actual product photos

## 3. Return-policy review

Before accepting any quote, verify per channel:
- **Return window** — varies by region by law and by seller policy. Examples of legal-minimum windows for online/distance sales: EU 14 days (Consumer Rights Directive), UK 14 days (Consumer Contracts Regulations / CRA 2015), Turkey 14 days, Australia depends on fault (ACL), US — no federal requirement (seller policy only; many offer 30 days). Confirm the user-region's consumer-protection minimum and the seller's actual policy.
- **Restocking fee** — common 10–20% on electronics in many markets; some regions disallow it for distance sales.
- **Return shipping cost** — who pays? Often the buyer pays return unless item is faulty.
- **Condition requirements** — sealed/unopened/used acceptable?
- **Exclusions** — consumables, software downloads, personalized items.

For any region: search `"<country> consumer rights return policy <year>"` to confirm minimum legal protections, and verify the seller's published policy matches or exceeds.

## 4. IoT cybersecurity / privacy (smart devices only)

For any internet-connected device, evaluate:
- **Vendor data practices** — what does the device collect, where is it stored, sold to whom (review privacy policy or external audit). Apply user-region's data-protection law (GDPR / UK GDPR / KVKK / CCPA-CPRA / LGPD / PDPA / PIPL).
- **Firmware update cadence** — last firmware update date, support lifecycle (devices that stopped getting updates are security liabilities).
- **IoT certifications** — UK PSTI compliance, US Cyber Trust Mark, EU Cyber Resilience Act (CRA) conformance, Singapore Cybersecurity Labelling Scheme, Mozilla Privacy Not Included rating.
- **Local-control fallback** — does the device still work if vendor's cloud goes away? Matter / HomeKit-only vs proprietary cloud-only matters.
- **Default credentials** — does it ship with unique credentials or shared default (default-credential devices are flagged).

Red flag: any smart device whose vendor was previously breached or that lacks a published security disclosure process.

## 5. Counterfeit risk

Categories with high counterfeit prevalence:
- Apple accessories (cables, chargers, AirPods)
- Camera batteries
- Memory cards (SD / microSD — capacity counterfeiting is common; tools: H2testw, F3)
- Bike components (Shimano XTR, SRAM AXS — high-end groupset parts)
- Optics (Zeiss, Leica)
- Cosmetics, supplements, pharmaceuticals

Mitigations:
- Buy only from authorized dealer (#2 above).
- For memory cards specifically: run a capacity test on arrival (H2testw on Windows, F3 on Linux/macOS) before relying on it.
- For batteries: check for OEM markings, weight, and verify serial on manufacturer site.

## 6. Compatibility (if upgrade or existing-ecosystem)

See `compatibility-playbook.md` for the matrix methodology. Compatibility failures are disqualifying blockers — flag in step 5, do not silently drop them.

## Output of compliance checks

For each candidate, record verdict per check:

| Candidate | Certifications | Authorized dealer | Return policy | IoT cyber | Counterfeit risk | Compatibility | Verdict |
|---|---|---|---|---|---|---|---|
| ... | ✓ CE/FCC + regional mark | ✓ Authorized regional distributor | ✓ 30d, no fee | ✓ Updates Q1 2026 | Low | ✓ matches user's gear | PASS |
| ... | ✗ no regional mark | ⚠ marketplace 3P | ✗ 7d, 15% restock | n/a | High | ✓ | **DISQUALIFY** |

Disqualified candidates go to the "Do not buy" section of the final report with the failure reason.
