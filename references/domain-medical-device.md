# Domain: Medical Device (CPAP, hearing aid, glucose monitor, BP cuff, mobility aid)

Lowest-research-but-highest-stakes category for consumers. Health outcomes depend on correct choice. Regulatory compliance, prescription requirements, reimbursement (national public-insurance scheme or private insurance — varies by country), and ongoing service all matter more than spec sheets.

## CRITICAL DISCLAIMERS

- **Not medical advice.** This skill helps with procurement research; clinical fit must be confirmed by a qualified healthcare provider.
- **Prescription may be required.** Many medical devices (CPAP, prescription hearing aids, insulin pumps, certain mobility aids) require physician prescription. Verify before proceeding.
- **Reimbursement / insurance eligibility** depends on diagnosis, doctor's report, device class, authorized supplier, and the user's specific public-insurance scheme or private insurer. Don't assume what's not been confirmed in writing by the insurer.

## Research dimensions
- **functional_specs**: clinical efficacy (peer-reviewed evidence + device-specific studies), accuracy (meters: ISO 15197 compliance; BP: validation per AAMI/ESH/ISO standards), comfort / wearability for chronic-use devices, alarms + alerts, data export + clinician access, battery / power redundancy, cleaning / hygiene protocol
- **quality_signals**: clinical-trial registration, FDA / CE-MDR / TÜRGİV registrations, sleep-medicine community recommendations (CPAP forums), professional society guidelines (AASM for sleep, ADA for diabetes, ATS for respiratory), device-specific failure-mode databases (FDA MAUDE for US, RAPEX for EU)
- **economic**: device + supplies (CPAP masks 3–6mo, filters monthly, hose annual; CGM sensors 7–14 days; hearing aid batteries weekly or rechargeable) + service + cleaning gear; public-insurance / private-insurance reimbursement; out-of-pocket residual; horizon: device 5–10yr depending on class
- **usage_fit**: diagnosed condition severity (mild OSA vs severe; T1 vs T2 diabetes; mild vs profound hearing loss), patient mobility / dexterity, lifestyle (travel? hospital-grade portability needed?), at-home vs clinic, family support

## Required user inputs (overrides universal)
- **Diagnosis + severity** (from physician — AHI for OSA, A1C + insulin regimen for diabetes, audiogram for hearing)
- **Prescription** (exists? what device class is prescribed? generic class or specific brand?)
- **Reimbursement path** (national public-insurance scheme / private insurance; what's covered; preferred supplier list)
- **Physician / clinic recommendation** (often the most important input; respect it)
- **Travel needs** (international power, airline-approved battery, smaller form factor)
- **Other devices** worn / used (interactions matter — pacemaker affects MRI / certain stim devices)
- **Allergies** (mask silicone, adhesive on CGM, hearing aid mold material)

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Regulatory class** | FDA Class I/II/III, EU MDR Class I/IIa/IIb/III, TR Tıbbi Cihaz Yönetmeliği | Higher class = stricter clinical evidence and post-market surveillance; verify registered in user's region |
| **CPAP mask interface** | Nasal pillow / nasal mask / full-face / hybrid; brand-specific or industry-standard connector | Mask brand often interchangeable across CPAP machines (most use 22mm hose); cushion + frame brand-specific |
| **CPAP hose** | 22mm standard, 15mm slim, heated hose with proprietary connector | Heated hose typically requires matching CPAP machine model |
| **CPAP machine data export** | SD card / Bluetooth / cellular | SD card + OSCAR open-source software is power-user standard; some machines lock data to brand cloud |
| **CGM sensor / transmitter** | Dexcom G6/G7, Abbott Libre 2/3, Medtronic Guardian | Sensor / transmitter / receiver / phone app all brand-locked; not cross-compatible |
| **Insulin pump tubing / infusion set** | Brand-specific connectors (Medtronic, Tandem, Omnipod tubeless) | Tubing brand-locked; infusion set type matters for skin tolerance |
| **Hearing aid form factor** | BTE (behind-ear) / RIC (receiver-in-canal) / ITE / ITC / CIC / IIC (invisible-in-canal) | Form factor matched to hearing loss severity + dexterity + cosmetic preference |
| **Hearing aid Bluetooth** | MFi (Apple), ASHA (Android, Google), Auracast (LE Audio next-gen) | Phone OS determines streaming compatibility; older phones may lack MFi/ASHA |
| **Hearing aid battery** | rechargeable (Li-ion) / disposable (size 10, 13, 312, 675) | Disposable battery weekly cost adds up; rechargeable adds upfront cost |
| **BP cuff size** | Small (17–22cm arm), Medium (22–32cm), Large (32–42cm), XL | Wrong cuff size = wrong reading (often 10–20 mmHg off) |
| **Mobility aid** | Cane / walker / rollator / wheelchair manual / power wheelchair / scooter | Match to patient mobility level; physical-therapy assessment is the gold standard |
| **Pulse oximeter** | medical-grade vs consumer (FDA-cleared vs not) | Apple Watch / Fitbit consumer-grade may not be accurate enough for clinical decisions |

## Common pitfalls

- **Buy CPAP / hearing aid without titration / audiogram** — you'll get suboptimal therapy. Don't skip the medical step.
- **Mask doesn't fit / leaks** — single most common CPAP failure mode; trial period + mask fitter critical.
- **CGM under skin / adhesive allergy** — switch sensor brand if adhesive reactions persist.
- **Gray-market CPAP without warranty / parts** — Philips DreamStation recall (2021–2024) affected millions; only authorized service can handle recall/replacement.
- **OTC hearing aid for severe loss** — OTC class (US FDA, since 2022) is for mild-moderate only; severe loss needs prescription / audiologist programming.
- **Reimbursement paperwork insufficient** — public-insurance denials are common when forms are missing or wrong. Use a supplier experienced with the user's specific insurer / scheme.
- **Counterfeit / refurbished as new** — common in hearing aid and CGM marketplace channels; only authorized.
- **Glucose meter accuracy** — non-ISO-15197-compliant meters may be off by 15–20%; clinical decisions on bad data is dangerous.
- **BP cuff wrong size** — even brand-name cuffs ship with one size; user's arm circumference dictates whether to order alternate.
- **Pulse-ox dark-skin bias** — published research shows commercial pulse oximeters less accurate on darker skin tones; clinical follow-up if numbers suggest hypoxia.
- **Sleep apnea diagnosis without sleep study** — at-home rings / watches CAN flag risk but proper polysomnography needed for prescription path.

## Reimbursement & regional sourcing notes

Medical-device reimbursement varies hugely by country and insurance system. Confirm in the user's region:

- **Public health-insurance / social-security coverage** — most countries with public insurance cover qualifying medical devices (CPAP, insulin pumps, hearing aids, mobility aids) with prescription + medical-board report. Examples: Medicare/Medicaid (US), NHS (UK), CPAM/Sécu (FR), GKV (DE), Medicare (AU), SGK (TR), CSST/Régimes (CA), etc. Eligibility criteria, reimbursement %, and required paperwork differ substantially.
- **Authorized-supplier list** — public-insurance reimbursement usually requires purchase from a list of approved suppliers; using an off-list supplier voids reimbursement. The supplier list is published by the insurer.
- **Private insurance** — varies by carrier and plan; pre-authorization often required for higher-cost devices.
- **Private hospitals / clinics** — often have preferred suppliers; ask before committing if going self-pay.
- **Major global brands per category** (verify regional distributor):
  - **CPAP**: ResMed, Philips Respironics (subject to ongoing recall — verify model affected), Löwenstein, Fisher & Paykel, BMC
  - **Hearing aid**: Sonova (Phonak / Unitron), WS Audiology (Widex / Signia), GN (ReSound / Beltone), Starkey, Demant (Oticon)
  - **Glucose monitor / CGM**: Dexcom, Abbott (FreeStyle Libre), Medtronic, Senseonics
  - **Insulin pump**: Medtronic, Tandem (t:slim), Insulet (Omnipod), Ypsomed
  - **BP monitor**: Omron, A&D, Withings, iHealth
- **Audiology / fitting service**: hearing aids especially require professional fitting + ongoing adjustment; choose a clinic / audiologist as much as a device brand.

## B2B variant (clinic / hospital / care home)
- Hospital-grade certification (IEC 60601 for medical electrical equipment)
- Sterilization compatibility (autoclave, ETO, chemical) for reusable items
- Service contracts with response-time SLA (4hr / 24hr / next-day)
- Bulk supplies pricing
- Compliance: ISO 13485 supplier certification, FDA 510(k) registration verification, EU MDR UDI tracking
- Medical-device vigilance reporting requirements

## Trusted sources for web fallback

- [FDA Recalls](https://www.fda.gov/safety/recalls-market-withdrawals-safety-alerts) + [MAUDE database](https://www.accessdata.fda.gov/scripts/cdrh/cfdocs/cfMAUDE/search.cfm) — US adverse event data
- [EU Safety Gate (RAPEX)](https://ec.europa.eu/safety-gate-alerts/), [EUDAMED medical device database](https://ec.europa.eu/tools/eudamed) — EU
- [MHRA](https://www.gov.uk/government/organisations/medicines-and-healthcare-products-regulatory-agency) — UK regulator
- [TGA](https://www.tga.gov.au) — Australia regulator
- [Health Canada — Medical Devices](https://www.canada.ca/en/health-canada/services/drugs-health-products/medical-devices.html)
- For other regions: search `"<country> medical device regulator"` — every country has a national authority (e.g., PMDA Japan, NMPA China, ANVISA Brazil, CDSCO India, TITCK Turkey)
- [AASM Sleep](https://aasm.org) — sleep medicine professional society
- [ADA / diabetes.org](https://diabetes.org) — diabetes professional resources
- [HearingTracker](https://www.hearingtracker.com) — hearing aid reviews + clinician network
- [CPAPtalk.com](https://www.cpaptalk.com), [Apnea Board](https://www.apneaboard.com) — CPAP user community + OSCAR data analysis
- [r/CPAP](https://reddit.com/r/CPAP), [r/diabetes](https://reddit.com/r/diabetes), [r/HearingAids](https://reddit.com/r/HearingAids)
- ClinicalTrials.gov for device-specific evidence; PubMed for peer-reviewed efficacy
- **Most important**: the user's treating physician / audiologist / endocrinologist / sleep specialist

## When to escalate

If at any point the user's question reveals:
- Undiagnosed condition being self-treated
- Choice between medical device and medication being made without physician
- Reimbursement / insurance fraud risk
- Use of device outside its intended population (pediatric vs adult, etc.)

→ **The skill should explicitly recommend consulting a healthcare provider before completing the procurement decision.** Health outcomes outweigh procurement efficiency.
