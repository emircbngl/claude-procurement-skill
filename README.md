# claude-procurement-skill

> A **Claude Code skill** that turns any buying decision — from a USB cable to an enterprise SaaS contract — into a professional procurement workflow: formalized requirements, fair-price discovery, total cost of ownership, vendor risk, a documented decision, and a post-purchase lifecycle plan.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-orange)](https://docs.claude.com/en/docs/claude-code)
[![Region-neutral](https://img.shields.io/badge/region-neutral-green)](#)
[![Self-feeding](https://img.shields.io/badge/self--feeding-domain%20packs-purple)](#self-feeding-knowledge-base)

---

## What it does

- **Researches any product** — bicycle, PC build, camera, headphones, smart-home device, appliance, cosmetics, furniture, e-mobility, SaaS tool, medical device, or anything else.
- **Runs a procurement-grade pipeline** modeled on the **CIPS 13-stage procurement cycle**, condensed to 11 LLM-driven steps.
- **Classifies every purchase** using the **Kraljic matrix** (routine / leverage / bottleneck / strategic) so depth scales to importance — no over-engineering a USB cable, no under-engineering a CPAP machine.
- **Validates compliance and compatibility** before pricing: certification marks (CE, FCC, UL, RoHS, etc.), authorized-dealer verification, return-policy review, IoT cyber/privacy checks, and physical/electrical compatibility with the user's existing ecosystem.
- **Discovers fair prices**, not just MSRP — eight price tiers tracked (MSRP, street, net, refurb, used, gray market, bundle, trade-in), 3-quote rule, 6–12 month price history via camelcamelcamel / Keepa, peer-tier benchmarks, regional aggregators (Google Shopping, PriceSpy, Idealo, Kakaku, PCPartPicker, and equivalents per region).
- **Computes landed-cost TCO** over a horizon — consumables, energy, maintenance, expected repairs, insurance net of credit-card coverage, financing, rebates, resale, opportunity cost.
- **Surfaces vendor risk** — FMEA-lite, single-source-of-failure, ecosystem lock-in, EOL signals, recall history.
- **Chooses a decision method** that matches the purchase: quick weighted scoring for routine, full weighted matrix for leverage, **AHP** or **Pugh matrix** for strategic purchases.
- **Stress-tests the decision** with a Klein-style **pre-mortem** and a threshold-based **cooling-off pause**.
- **Plans the lifecycle** post-purchase: receive + inspect, warranty registration deadline, day-1 firmware/secure setup, recall monitoring, maintenance schedule, spare-parts stocking, end-of-life resale / recycle.
- **Outputs a structured decision memo** with full audit trail of sources at `tasks/research/<slug>.md`. Optionally also emits **presentation-ready formats** — executive deck (.pptx), polished PDF brief, stakeholder one-pager, or Word .docx — by chaining to the Anthropic `anthropic-skills:pptx / pdf / docx` skills.
- **Token-efficient by design** — progressive disclosure + criteria-side caching (self-feeding) + no-re-ask auto-extraction. Saves ~70–80% of tokens and web calls vs naive research, especially across repeat sessions in the same category. See [docs/TOKEN_EFFICIENCY.md](docs/TOKEN_EFFICIENCY.md).

## Why use this instead of "asking Claude"

| Asking Claude directly | This skill |
|---|---|
| One-shot answer | Multi-step, structured pipeline |
| MSRP anchor | 8-tier price discovery + fair-price band (aspirational / target / walk-away) |
| Sticker price | Landed-cost TCO over horizon, net of CC bonuses + rebates + resale |
| Generic recommendation | Weighted scoring or AHP / Pugh decision matrix tied to your requirements |
| No compatibility check | Standards matrix vs. your existing gear |
| No risk framework | FMEA-lite, vendor risk, single-source-of-failure |
| No audit trail | Cited sources for every claim, written to disk |
| No follow-through | Lifecycle plan with dated warranty / recall / maintenance / EOL checklist |
| One-size-fits-all | **Kraljic-driven depth**: routine gets a shortcut, strategic gets the full memo |
| Anglo-centric | Region-neutral; works for US, EU, UK, CA, AU, JP, IN, BR, MENA, and any country |
| Personal use only | **B2C and B2B modes** — RFI/RFP/RFQ flow for company procurement |
| Static knowledge | **Self-feeding**: derives + saves a new domain pack on first encounter with a category |
| High token cost per query | **Token-efficient by design**: progressive disclosure + self-feeding cache (criteria only, never prices) + no-re-ask auto-extraction → ~70–80% fewer tokens and web calls vs naive use across repeat sessions ([details](docs/TOKEN_EFFICIENCY.md)) |
| Markdown report only | **Multi-format output**: Markdown (default) + executive deck (.pptx) + PDF brief + one-pager + Word .docx, all chained via `anthropic-skills:pptx/pdf/docx` |

## Quickstart

1. **Clone or download into your Claude Code skills directory**:
   ```bash
   cd ~/.claude/skills/   # or wherever Claude Code looks for skills on your system
   git clone https://github.com/<your-handle>/claude-procurement-skill.git
   ```
2. **Open Claude Code** in any working directory (the skill writes outputs to `tasks/research/<slug>.md` relative to the current dir).
3. **Trigger the skill** with a natural-language prompt such as:
   - *"Research a gravel bike upgrade — I have a Giant Revolt with BSA BB, 142×12 thru-axle, flat-mount brakes, 11sp 105."*
   - *"Build me a 1440p gaming PC under $1500."*
   - *"Compare HubSpot vs Pipedrive vs Close for a 25-seat B2B sales team."*
   - *"Is a SRAM XPLR 12sp rear derailleur compatible with my Shimano 11sp shifter?"*
   - *"Should I buy a CPAP machine — newly diagnosed with sleep apnea, budget $2000."*
   - *"Research espresso machines under $1500 for home use."*
4. **Answer the (single batched) follow-up questions** about region, budget, audience level, etc. The skill only asks for what it couldn't auto-extract from your working-directory files.
5. **Read the report** at `tasks/research/<slug>.md`. The Executive summary at the top is the headline; the Procurement detail below is the full decision memo.

See [examples/](examples/) for three fully worked outputs.

## How it works — the 11-step procurement workflow

The skill walks every research request through the same pipeline, with step depth scaling to the Kraljic classification from step 1.5:

### Pre-purchase
1. **Scope & domain** — identify product category and intent (new-purchase / upgrade / comparison / compat-check). See [references/domain-index.md](references/domain-index.md).
2. **Kraljic classification** — routine / leverage / bottleneck / strategic. See [references/kraljic-classification.md](references/kraljic-classification.md).
3. **Load playbooks** — [procurement-playbook.md](references/procurement-playbook.md), [universal-dimensions.md](references/universal-dimensions.md), domain-specific pack.
4. **Auto-extract context** from working-directory files (gear lists, prior research, notes) — never re-ask for known data.
5. **Option-space analysis** — make-vs-buy, build-vs-buy-vs-rent-vs-subscribe. See [references/option-space.md](references/option-space.md).
6. **Formalize requirements** — must-have / nice-to-have (weighted) / dealbreaker. See [references/requirements-framework.md](references/requirements-framework.md).

### Sourcing & validation
7. **RFI → shortlist + compliance checks** — certifications, authorized-dealer verification, return policy, IoT privacy, counterfeit risk, compatibility matrix. See [references/compliance-checks.md](references/compliance-checks.md) and [references/compatibility-playbook.md](references/compatibility-playbook.md).
8. **RFP → RFQ + price discovery** — MSRP capture, regional aggregator scan, price history, used / refurb floor, peer-tier benchmark, cross-border landed-cost math, red-flag pass, **fair-price band**. See [references/price-discovery.md](references/price-discovery.md).
9. **TCO + risk + negotiation** — landed-cost TCO, FMEA-lite, vendor risk, negotiation tactic playbook. See [references/tco-and-risk.md](references/tco-and-risk.md) and [references/sourcing-and-negotiation.md](references/sourcing-and-negotiation.md).

### Decision & commit
10. **Decide & document** — weighted scoring / AHP / Pugh, chosen by Kraljic class. See [references/decision-frameworks.md](references/decision-frameworks.md).
11. **Pre-commit checks** — pre-mortem (Klein), devil's advocate, threshold-based cooling-off pause. See [references/pre-commit-checks.md](references/pre-commit-checks.md).

### Post-purchase (lifecycle)
The report includes a dated checklist for: receive + inspect, warranty registration deadline, day-1 firmware / secure setup, insurance enrollment, recall monitoring, maintenance schedule, spare-parts stocking, end-of-life resale / recycle. See [references/lifecycle-management.md](references/lifecycle-management.md).

The exact report shape lives in [references/report-template.md](references/report-template.md).

## Domain packs

Pre-built domain knowledge for common categories. Each pack contains the research dimensions, compatibility/standards table, common pitfalls, and trusted sources for that domain.

| Domain | Pack | Mode bias |
|---|---|---|
| Bicycle | [domain-bicycle.md](references/domain-bicycle.md) | B2C |
| PC build | [domain-pc.md](references/domain-pc.md) | B2C / prosumer |
| Cosmetics (skincare, makeup) | [domain-cosmetics.md](references/domain-cosmetics.md) | B2C |
| Home appliance (major / white goods) | [domain-home-appliance.md](references/domain-home-appliance.md) | B2C |
| Small appliance (coffee, blender, vacuum) | [domain-small-appliance.md](references/domain-small-appliance.md) | B2C |
| Camera (mirrorless, lenses, gear) | [domain-camera.md](references/domain-camera.md) | B2C / prosumer |
| Audio (headphones, speakers, amps) | [domain-audio.md](references/domain-audio.md) | B2C / prosumer |
| Smart home (IoT, Matter, Zigbee) | [domain-smart-home.md](references/domain-smart-home.md) | B2C |
| Furniture (incl. mattress) | [domain-furniture.md](references/domain-furniture.md) | B2C + B2B |
| Personal mobility (e-bike, e-scooter, EUC) | [domain-mobility.md](references/domain-mobility.md) | B2C |
| IT software (SaaS, business software) | [domain-it-software.md](references/domain-it-software.md) | B2B |
| Medical device (CPAP, hearing aid, CGM) | [domain-medical-device.md](references/domain-medical-device.md) | B2C + B2B (clinic) |
| **Anything else** | [domain-unknown.md](references/domain-unknown.md) — self-feeding fallback | — |

### Self-feeding knowledge base

When you research a category that doesn't have a pack yet, the skill **derives the missing dimensions via web search and saves a new domain pack to disk** for next time. See [references/self-feeding.md](references/self-feeding.md).

Auto-generated packs start at `confidence: low` with an explicit warning banner. After 3+ runs without contradiction, the skill bumps them to `medium`. When you review a pack and approve it, it gets promoted to `human-reviewed / high`.

The skill's domain library grows with use, no manual authoring required.

## B2C vs B2B modes

The same pipeline serves both personal buyers and corporate procurement. See [references/b2b-modifiers.md](references/b2b-modifiers.md) for the full overlay. Key differences:

- **B2C**: cooling-off pause based on income threshold; consumer-protection law for returns; personal warranty + insurance considerations.
- **B2B**: formal **RFI → RFP → RFQ** process; multi-stakeholder requirements (IT + Finance + Security + Legal + end-user); SOC 2 / ISO 27001 / DPA / BAA validation; AHP for strategic vendor selection; implementation + change-management costs in TCO; approval-chain checklist replacing cooling-off.

## Token efficiency

One of the strongest reasons to use this skill over asking Claude directly: **structural token efficiency that compounds across sessions**.

- **Progressive disclosure** — `SKILL.md` is ~180 lines; the 30+ reference modules load only when relevant. A routine-class run pulls 3 files into context; a strategic-class run pulls 6.
- **Self-feeding (criteria-side caching)** — first encounter with an unknown category runs a one-time deep search across 8 dimensions; result saved as a domain pack with `confidence: medium`. Two acquisition paths: (a) delegate to the `deep-research` skill if registered in your Claude Code setup (preferred — fan-out + adversarial verify), or (b) inline 8-category search with parallel-batched WebSearch/WebFetch calls (~20–30 calls) as fallback. Subsequent runs on the same category cost **zero web calls for criteria research** — only live price discovery + availability is re-fetched.
- **Auto-extraction** — the skill scans the working directory for existing context (gear lists, prior quotes, prior research) before asking the user anything. Repeated research in the same domain compounds.
- **Compressed report template** — tables instead of paragraphs; casual mode condenses sections; the canonical Markdown is dense but scannable.

**What we cache vs what stays live** (this distinction is intentional):

| Cached forever (~0 web cost / future run) | Re-fetched every query (always live) |
|---|---|
| Research dimensions + standards + compatibility axes | Current prices |
| Certification marks + regulatory bodies per region | Stock / availability |
| Brand landscape + authorized-distribution patterns | Active promos / discounts |
| Common pitfalls + failure modes | Fair-price band (calculated per query) |
| Repairability + EOL norms | Recent recalls / vendor news / FX rates |

Caching prices would be a feature anti-pattern — stale prices mislead buyers. The cache is for **how to evaluate this category** (stable). Live re-fetch is for **what it costs today** (dynamic).

**Rough numbers** (illustrative, varies by category):

| Scenario | Input tokens | Web calls |
|---|---|---|
| Naive "Claude, research X" | 40–60k | 20–60 |
| This skill, first encounter unknown domain | 25–35k | 20–30 (deep search) + 5–10 (live prices) |
| This skill, subsequent encounter same domain | 8–15k | 3–8 (prices only) |

Across 10 runs on the same category, the skill saves ~70–80% of tokens and web calls vs naive use. Full details + verification recipe in [docs/TOKEN_EFFICIENCY.md](docs/TOKEN_EFFICIENCY.md).

## Example outputs

Three fully worked sample reports demonstrate the skill across modes and Kraljic classes:

- [examples/bicycle-gravel-upgrade.md](examples/bicycle-gravel-upgrade.md) — **B2C, leverage class, upgrade intent.** Demonstrates compatibility matrix flagging Boost wheels + 12-speed cassettes against an existing 11-speed Shimano 105 + 142×12 thru-axle frame.
- [examples/pc-1440p-gaming-build.md](examples/pc-1440p-gaming-build.md) — **B2C, leverage class, new-build intent.** Internal compatibility across CPU ↔ motherboard ↔ RAM ↔ PSU ↔ case; energy line in TCO; weighted scoring across three builds.
- [examples/saas-crm-comparison.md](examples/saas-crm-comparison.md) — **B2B, strategic class, vendor-comparison intent.** RFI → RFP → RFQ, SOC 2 / DPA compliance, AHP decision method, multi-year contract negotiation, approval-chain checklist.

## Customization

### Add a new domain pack

1. Copy the template from any existing `references/domain-<name>.md`.
2. Fill in: research dimensions, required user inputs, standards & compatibility axes, common pitfalls, trusted sources.
3. Add a row to [references/domain-index.md](references/domain-index.md) with keywords + `status: hand` + mode bias.
4. (Optional) Submit a PR — see *Contributing* below.

### Promote an auto-generated pack

When the skill encounters a category for the first time, it writes `references/domain-<slug>.md` with `status: auto-generated, confidence: low` and a warning banner.

To promote:
1. Open the file, review accuracy, fill in gaps.
2. Remove the warning banner.
3. Update the frontmatter: `status: human-reviewed, confidence: high, human-reviewed: true`.
4. Update the corresponding row in `references/domain-index.md`.

### Tune procurement behavior

- **Requirements weighting**: edit your requirements doc at runtime via the AskUserQuestion prompts; weights live in the report itself.
- **TCO horizon**: pass `3 years` / `5 years` / other when the skill asks.
- **Cooling-off threshold**: ask the skill to use a custom rule (default: 24h pause above 10% of monthly income; 72h pause for strategic-class purchases regardless of spend).
- **Source citation strictness**: defaults to ≥2 sources for standards/compat claims, ≥1 for opinions, ≥1 aggregator + ≥1 primary seller for price data. Edit [SKILL.md](SKILL.md) "Source citation discipline" section to adjust.

## Repository structure

```
claude-procurement-skill/
├── README.md                          # This file
├── LICENSE                            # MIT
├── SKILL.md                           # Skill entry point + 11-step workflow + routing
├── references/
│   ├── procurement-playbook.md        # Professional-buyer mindset + CIPS mapping
│   ├── kraljic-classification.md      # Routine / leverage / bottleneck / strategic
│   ├── option-space.md                # Make-vs-buy + build/buy/rent/subscribe
│   ├── universal-dimensions.md        # Domain-agnostic evaluation criteria
│   ├── requirements-framework.md      # Must-have / nice-to-have / dealbreaker
│   ├── compliance-checks.md           # Cert marks, authorized dealer, IoT, counterfeit
│   ├── compatibility-playbook.md      # Standards matrix methodology
│   ├── price-discovery.md             # 8 price tiers, fair-price band, RFI/RFP/RFQ
│   ├── tco-and-risk.md                # Landed-cost TCO + FMEA-lite + vendor risk
│   ├── sourcing-and-negotiation.md    # Negotiation tactic playbook
│   ├── decision-frameworks.md         # Weighted / AHP / Pugh
│   ├── pre-commit-checks.md           # Pre-mortem + devil's advocate + cooling-off
│   ├── lifecycle-management.md        # Receive / register / monitor / maintain / EOL
│   ├── information-sources.md         # Cross-region source catalog
│   ├── self-feeding.md                # How auto-generated packs work
│   ├── b2b-modifiers.md               # B2C / B2B overlay
│   ├── domain-index.md                # Registry of all domain packs
│   ├── ask-user-patterns.md           # AskUserQuestion question banks
│   ├── report-template.md             # Markdown skeleton for outputs
│   ├── domain-unknown.md              # Fallback + self-feeding workflow
│   └── domain-<13 packs>.md           # Bicycle, PC, cosmetics, appliances, ... medical-device
└── examples/                          # Three fully worked sample reports
    ├── bicycle-gravel-upgrade.md
    ├── pc-1440p-gaming-build.md
    └── saas-crm-comparison.md
```

## Contributing

PRs welcome, especially for new domain packs.

- **New domain pack**: follow the template structure of an existing pack (e.g., [domain-bicycle.md](references/domain-bicycle.md)). Include citations for any standards / compatibility claims (≥2 independent sources). Add an entry to [domain-index.md](references/domain-index.md).
- **Improvements to a process module**: keep [SKILL.md](SKILL.md) short — push detail into the relevant `references/` file. Maintain region-neutrality (no single-country bias; multi-region examples preferred).
- **Bug reports**: open an issue with the user query, expected behavior, actual behavior, and which `references/` file is implicated.
- **Auto-generated pack review**: open a PR that promotes an existing auto-generated pack to `human-reviewed`, with any corrections or additions surfaced from real-world use.

## Star history

<a href="https://star-history.com/#emircbngl/claude-procurement-skill&Date">
  <img src="https://api.star-history.com/svg?repos=emircbngl/claude-procurement-skill&type=Date" alt="Star history chart for emircbngl/claude-procurement-skill" width="640">
</a>

## License

MIT — see [LICENSE](LICENSE).

## Acknowledgments

The methodology draws on established procurement and decision-science literature:

- **CIPS (Chartered Institute of Procurement & Supply)** — 13-stage procurement and supply cycle ([cips.org](https://www.cips.org/intelligence-hub/procurement/procurement-supply-cycle)).
- **Peter Kraljic** — *Purchasing Must Become Supply Management*, Harvard Business Review, 1983 — the supply-risk × importance matrix.
- **Thomas L. Saaty** — *The Analytic Hierarchy Process*, 1980 — pairwise-comparison decision method.
- **Stuart Pugh** — *Total Design*, 1991 — concept selection matrix.
- **Gary Klein** — *Performing a Project Premortem*, Harvard Business Review, 2007.
- **FTC 16 CFR Part 233** — Guides Against Deceptive Pricing.
- **EU regulations** — General Product Safety Regulation, Energy Labelling, EPREL database, Cyber Resilience Act, Right-to-Repair Index.
- **Independent testing labs** — Wirecutter, RTINGS, Consumer Reports, GamersNexus, iFixit, MPB, KEH, and many more, cited in [references/information-sources.md](references/information-sources.md).

Built with [Claude Code](https://claude.com/claude-code) and the [Claude Agent SDK](https://docs.claude.com/en/docs/claude-code) — a skill that researches procurement, built by following procurement-grade research practice.
