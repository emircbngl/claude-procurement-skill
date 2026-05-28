# B2B / B2C modifiers

The skill serves both end-users (B2C, prosumer) and companies (B2B, procurement teams). The core 11-step procurement pipeline is the same, but several steps shift weight or get additional sub-steps depending on which mode applies.

This file describes the overlays. Domain packs include domain-specific B2B notes where they matter; this file holds the cross-cutting modifiers.

## Determining mode

Ask early in step 4 (requirements) if not obvious from context:

```
Q: "Is this purchase for personal use, or a company / organization?"
Options:
- Personal / household (B2C)
- Small team / freelance / sole proprietor (mixed)
- Company / enterprise procurement (B2B)
```

Defaults:
- If no other signal → assume B2C
- If user mentions "for our team", "for the company", "for the office", "procurement", "PO", "RFP" → B2B
- If user mentions HR / IT / facilities / fleet language → B2B

The mode is captured in the report header and drives the modifiers below.

## Step-by-step modifiers

### Step 1.5 (Kraljic classification)

| Mode | Modifier |
|---|---|
| B2C | Importance scaled by % of monthly household income |
| B2B | Importance scaled by spend authority tier (e.g., < manager limit, < director limit, board-level), business-criticality (revenue impact if unavailable), and category strategy (commodity vs differentiating) |

### Step 3.5 / 3.6 (Option space)

| Mode | Modifier |
|---|---|
| B2C | Make-vs-buy / rent-vs-buy / subscribe — household scope |
| B2B | Adds: lease-vs-buy (capex vs opex implication), outsource / managed service (BPO), insource development (build), open-source self-host vs SaaS |

### Step 4 (Requirements)

Additional B2B requirements always captured:
- **Procurement authority / approval chain** — who signs off; spend tier; legal review needed?
- **Multi-stakeholder** — IT + Finance + end-user + Security + Legal each have requirements
- **Volume / scale** — current seats/units + 12mo growth projection + 36mo projection
- **Integration with existing stack** — must connect to <ERP / CRM / SSO provider / ITSM>
- **Compliance regime** — applicable data-protection law (GDPR for EU, UK GDPR, CCPA / CPRA for California, LGPD for Brazil, PIPEDA for Canada, PDPA for Singapore / Thailand, PIPL for China, APP for Australia, KVKK for Turkey, POPIA for South Africa), industry obligations (HIPAA for US healthcare, SOC 2 attestation, PCI-DSS for payments, FERPA for US education, FedRAMP for US federal, equivalents in other jurisdictions)
- **Audit / reporting** — admin dashboards, audit log retention, export to SIEM
- **SLA targets** — uptime %, response time, recovery time objective
- **Contract structure** — term length, auto-renewal notice, termination for convenience clause, price-lock
- **Vendor onboarding** — security questionnaire required, vendor risk assessment

### Step 5 (Compliance)

Additional B2B compliance checks:
- **Vendor security questionnaire** (SIG / CAIQ standard sets)
- **SOC 2 Type II report** review (most recent, ≤12mo old, no qualified opinion)
- **ISO 27001 / 27017 / 27018 certificates**
- **Penetration test summary** within last 12mo
- **Data Processing Agreement** signed-version available
- **Cyber-insurance** of vendor (in case of breach)
- **Sanctions / OFAC / UN screening** of vendor and ultimate beneficial owner
- **Insurance certificates** (general liability, E&O, cyber)
- **Vendor business continuity / disaster-recovery plan**

### Step 6 (Price discovery — RFP / RFQ)

B2B price discovery is fundamentally different from B2C:
- **Formal RFI → RFP → RFQ** process, not just retailer comparison
- **Volume pricing tiers** (per-seat declines with volume; per-unit declines with order size)
- **Multi-year contract discounts** (often 10–25% off list for 2yr commit, 20–35% for 3yr)
- **End-of-quarter timing** — sales reps incentivized; same vendor will quote 15–25% lower in last 2 weeks of quarter
- **Multi-vendor negotiation** — let vendors know they're in competition (factual not bluff)
- **Reference-customer calls** — ask vendor for 2–3 customers similar in size/industry
- **POC / pilot** — paid 30–60 day pilot with success criteria, before full commit
- **Net price** includes all discounts + rebates + service credits — not just list-minus-discount-percent

For B2B, the "fair-price band" output of step 6 also includes:
- **Floor** (best-in-market for similar customer profile, often via reference-customer benchmarking)
- **Negotiated target** (what your size/segment typically achieves)
- **List anchor** (starting point; never accept list)

### Step 7 (TCO + risk + negotiation)

B2B TCO has additional lines:
- **Implementation / onboarding** — often 1–3× annual license cost for enterprise SaaS; capital investment cost for hardware
- **Training** — per-user, per-admin, certification programs
- **Change management** — internal communication, process redesign, transition support
- **Ongoing admin** — FTE % allocated for tool admin (large SaaS = 0.25–1 FTE typical)
- **Integration cost** — middleware, custom connectors, API limits if exceeded
- **Audit / compliance reporting cost** — many SaaS charge for advanced reporting tiers required for audit
- **Exit cost** — data export, retraining users on replacement, parallel-run period
- **FX exposure** for cross-border vendors (e.g., USD-denominated SaaS billed monthly to a non-USD entity creates exchange-rate risk; negotiate local-currency pricing or annual prepay to lock the rate)

B2B vendor-risk additions:
- **Financial health** of vendor (D&B rating, recent funding round date, layoff news)
- **Acquihire risk** — popular SaaS gets acquired; pricing & roadmap shift
- **Roadmap alignment** — vendor's planned features vs your needs
- **Customer churn** rate (where disclosed)
- **Support tier purchased** — basic vs premium support determines incident response time
- **Escalation path** — named contact / TAM (Technical Account Manager) for enterprise tier

B2B negotiation levers:
- Multi-year commit (3yr = ~20–30% discount)
- Bundling additional products from same vendor
- Volume commitment with growth clause
- Co-marketing / case-study commitment for additional discount
- Annual prepay vs monthly invoice
- Customer reference rights
- Beta / early-access for unreleased features

### Step 8 (Decide & document)

B2B decision framework usually requires more rigor:
- **AHP** standard for strategic vendors (>$50k annual or business-critical)
- **Multi-stakeholder weighted scoring** — different stakeholders weight criteria differently; consolidate
- **Vendor Comparison Matrix** as procurement standard deliverable
- **Decision Brief** for executive approval (1–2 page summary of recommendation + alternatives + financials)

### Step 8.5 (Pre-mortem)

B2B-specific regret scenarios to test:
- Vendor acquired / changes pricing
- Vendor breach / security incident
- Vendor deprecates feature critical to our workflow
- Switching cost trapped us 3yr in
- Integration breaks with our planned ERP/CRM migration
- Compliance audit fails because vendor's controls are insufficient

### Step 8.6 (Cooling-off)

B2B replaces cooling-off with formal **approval chain**:
- Procurement → Legal → InfoSec → Finance → end-user team lead → director sign-off
- Each step is a documented checkpoint; recommendation memo from step 8 is the input

### Steps 9–11 (Lifecycle)

B2B lifecycle is more formalized:
- **Step 9** receive/inspect = vendor onboarding: kickoff call, named TAM assigned, integration plan, security setup, user provisioning
- **Step 10** ongoing = quarterly business review (QBR) with vendor, usage analytics review, mid-contract negotiation if usage diverges from forecast, change-control on integrations
- **Step 11** end-of-contract = renewal-or-exit decision starts 6+ months before contract end; competitive RFP if exit is on the table; data migration plan if changing vendors

## Special B2B categories

Categories that are predominantly B2B (route through this overlay):
- IT software (SaaS, infrastructure, security)
- IT hardware (networking, servers, endpoints at scale)
- Office furniture (contract-grade)
- Industrial / manufacturing equipment
- Commercial vehicles / fleet
- Hospitality equipment
- Medical equipment (clinics, hospitals)
- Construction / professional tools at scale

Categories that are predominantly B2C (default to consumer pipeline):
- Cosmetics
- Personal mobility (e-bike, e-scooter — except fleet)
- Camera (except studio / agency)
- Audio (except commercial AV / studio)
- Mattress / personal furniture
- Personal medical device (CPAP, hearing aid for individual use)

Categories that genuinely span both (read context cues):
- Small appliances (consumer at home / commercial in cafe)
- Smart home (consumer / commercial AV)
- Power tools (DIYer / contractor)
- Bicycle (personal / shop fleet)

## Output

For B2B runs, the report header includes:
> Mode: B2B · Procurement authority: <tier> · Approval chain: <step list>

And the report includes additional sections under "Procurement detail":
- Vendor security & compliance audit summary
- Multi-stakeholder requirements consolidation
- Implementation & integration plan
- Contract terms + negotiation positions
- Approval-chain checklist

For B2C runs, the report uses the standard template as-is (B2B-only sections are omitted with "N/A — B2C purchase" note).
