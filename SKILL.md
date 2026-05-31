---
name: procurement
description: >
  Research any consumer or business product (bicycles, PCs, cameras, audio gear, smart-home,
  appliances, cosmetics, furniture, mobility, IT software, medical devices, and anything
  else — unknown categories auto-derive a new domain pack and save it for future runs) as
  a professional procurement specialist would: formalize requirements, build a candidate
  slate, validate standards compliance and compatibility, run TCO and vendor-risk analysis,
  and deliver a documented decision memo with a post-purchase lifecycle plan. Self-feeds —
  builds up its own domain-pack library as it researches new categories. Supports both B2C
  (personal / household) and B2B (company / procurement) modes. Auto-extracts context from
  working-directory files and asks the user only for what's missing.
  Triggers on: "research [product]", "compare [A] vs [B]", "help me pick a [category]",
  "is X compatible with Y", "what should I upgrade on my [thing]", "should I buy [product]",
  "build me a [PC/bike/setup] for [budget]", "evaluate [product] for [use case]",
  "TCO of [product]", "procurement analysis for [product]", "RFP for [category]",
  "vendor comparison for [SaaS/equipment]".
allowed-tools: Read, Write, Edit, Glob, Grep, WebSearch, WebFetch, AskUserQuestion, Skill
---

# procurement

## Operating mindset

This skill behaves as a **professional procurement specialist**, not a casual shopping assistant. It maps the consumer/prosumer buying problem onto the CIPS 13-stage procurement-and-supply cycle. See `references/procurement-playbook.md` for the full mental model.

Every research request runs the same structured pipeline; depth of each step scales to the Kraljic classification produced in step 1.5.

## When to use

- "research a [product]" / "help me pick a [category]"
- "compare [A] vs [B] vs [C]"
- "is [X] compatible with [Y]"
- "what should I upgrade on my [bike/PC/setup]?"
- "should I buy [product]?" / "build me a [setup] for [budget]"
- "TCO of [product]" / "procurement analysis for [product]"
- Any time the user is weighing a meaningful purchase or upgrade decision.

## When NOT to use

- Pure price lookup ("what does X cost on Amazon?") — just answer directly.
- Pure spec recall ("what's the IP rating of X?") — just answer directly.
- Reviews of products the user already owns and isn't changing.
- Recommendations on consumables the user has already chosen brand/model for.

## Inputs required

The skill needs (or auto-extracts, or asks for):
- Product / category and intent (new-purchase / upgrade / comparison / compat-check)
- **Mode**: B2C (personal/household) or B2B (company/procurement) — see `references/b2b-modifiers.md`
- Region + currency (always asked, no default)
- Budget envelope
- Use-case profile
- Must-haves / nice-to-haves / dealbreakers
- Existing ecosystem (gear the user already owns — for compatibility)
- Audience level: casual or pro (asked once; controls report density)
- TCO horizon (typically 3 or 5 years; B2B often 5+)
- ESG weighting (optional)
- Cooling-off threshold (household-rule for when to enforce a sleep-on-it pause); for B2B replaced by formal approval chain
- **Output format(s)** — Markdown (always), optionally + Executive deck (.pptx) + PDF brief + One-pager + Word .docx; see `references/output-formats.md`

## Workflow — the 11-step procurement process

Run these in order. Step depth scales to the Kraljic class set in step 1.5.

### Pre-purchase

**1. Scope & domain.** Parse the user's message for product noun + brand/model. **Read `references/domain-index.md`** and match keywords. Classify intent (new-purchase / upgrade / comparison / compat-check). If ambiguous, ask one clarifying question via AskUserQuestion. If no domain matches → load `references/domain-unknown.md` to derive + self-feed a new pack (see self-feeding section below).

Also at this step, infer or ask **mode**: B2C (default for personal language) or B2B (triggered by "company", "office", "team", "procurement", "PO", "RFP", "vendor", "fleet" cues). See `references/b2b-modifiers.md`.

**1.5. Kraljic classification** — see `references/kraljic-classification.md`. Place purchase on supply-risk × importance matrix: routine / leverage / bottleneck / strategic. The classification dictates how deep the rest of the steps go.

**2. Load playbooks.** Read `references/procurement-playbook.md` + `references/universal-dimensions.md` + the matched `references/domain-<name>.md` from step 1. If mode = B2B, also read `references/b2b-modifiers.md`. If domain was `unknown`, follow `references/domain-unknown.md` to acquire the criteria-side knowledge:
- **Path A (preferred when available)**: delegate to the `deep-research` skill via the Skill tool with a composite 8-category prompt; parse its cited synthesis into the domain-pack template.
- **Path B (fallback)**: run the inline 8-category deep search (~20–30 web calls) with **parallel-batched WebSearch/WebFetch calls per category** (multiple tool calls per turn).

Either path saves the result as `references/domain-<slug>.md` with `confidence: medium` + appends to `domain-index.md` (self-feeding — see `references/self-feeding.md`). Note: prices and current availability are intentionally never cached — step 6 always runs live. Cache derived dimensions for this run.

**3. Auto-extract context.** Glob `**/*.md`, `**/*.txt`, `**/notes/**` + loose files in `.`. Grep for product names, model numbers, existing gear, prior quotes, must-haves/dealbreakers, prior research in `tasks/research/`. Build `known_context`. **Never re-ask for anything already found.**

**3.5. Option-space analysis** — see `references/option-space.md`. Test make-vs-buy and build/buy/rent/subscribe before assuming the answer is "purchase".

**4. Formalize requirements** — see `references/requirements-framework.md`. Build the requirements doc (must-have/nice-to-have weighted/dealbreaker). Ask via AskUserQuestion only for what's missing — single batched call. Always ask region+currency, audience level, Kraljic-derived importance, **and output format(s)** (Markdown default; optional .pptx / PDF / one-pager / .docx — see `references/output-formats.md`).

### Sourcing & validation

**5. RFI → shortlist + compliance** — see `references/compliance-checks.md` + `references/compatibility-playbook.md`. Build 2–5 candidate SKUs. Verify: certification marks (CE/FCC/UL/RoHS/CCC/Energy Star/EPREL), authorized-dealer/SKU verification, return policy, IoT cyber/privacy (smart devices), counterfeit risk, compatibility with user's existing gear. Disqualify failures + document reasons.

**6. RFP → RFQ + price discovery** — see `references/price-discovery.md`. For each surviving candidate, run MSRP capture → aggregator scan (region-appropriate: Google Shopping / PriceSpy / Idealo / Geizhals / Newegg / PCPartPicker / Kakaku / regional equivalents — see the table in `price-discovery.md`) → price history (camelcamelcamel / Keepa) → used/refurb floor (eBay sold, manufacturer refurb) → peer-tier benchmark → cross-border landed-cost math if relevant → red-flag pass → synthesize **fair-price band** (aspirational / target / walk-away).

**7. TCO + risk + negotiation** — see `references/tco-and-risk.md` + `references/sourcing-and-negotiation.md`. Compute landed-cost TCO (purchase + accessories + consumables + energy + maintenance + repairs − resale − rebates − CC bonuses + financing + insurance net of CC). Run FMEA-lite + single-source-of-failure + vendor risk. Assemble negotiation playbook.

### Decision & commit

**8. Decide & document** — see `references/decision-frameworks.md`. Method scales with Kraljic class: routine → quick weighted; leverage → full weighted; bottleneck → risk-adjusted; strategic → AHP or Pugh. Render `references/report-template.md` into `tasks/research/<slug>.md`. Slug = kebab-case `<category>-<keyword>`. **If exists**: append `## Re-evaluation <YYYY-MM-DD>`. Auto-create `tasks/research/`.

After the canonical Markdown is written, **chain to additional output formats** if the user requested any in step 4 — see `references/output-formats.md`. The skill calls `anthropic-skills:pptx` for executive decks, `anthropic-skills:pdf` for PDF briefs and PDF one-pagers, and `anthropic-skills:docx` for Word reports. All formats land in `tasks/research/<slug>.<ext>` alongside the Markdown.

**8.5. Pre-mortem + devil's advocate** — see `references/pre-commit-checks.md`. Klein's prospective hindsight: top-3 regret scenarios + mitigations. Inversion check.

**8.6. Cooling-off pause.** Threshold rule: above household threshold, recommend a 24–72h pause. Report flags with "Re-confirm after <date>".

### Post-purchase (lifecycle)

**9. Receive + register + archive** — see `references/lifecycle-management.md`. Incoming inspection, warranty registration deadline, day-1 firmware/secure setup, insurance enrollment, document archival.

**10. Recall + maintenance + spares.** Recall monitoring sources, maintenance calendar, spare-parts stocking.

**11. End-of-life.** Resale target / trade-in / recycle plan + data-wipe for smart devices. Lessons-learned to `tasks/lessons.md` per CLAUDE.md §3.

Steps 9–11 are written into the report as a **Lifecycle plan** — the skill provides a dated checklist, not autonomous execution.

## Domain detection rules

**Authoritative source: `references/domain-index.md`** — always consult this first; it is updated as the skill self-feeds new packs.

Current hand-authored packs (snapshot — full list in the index):

| Domain | Pack | Mode bias |
|---|---|---|
| Bicycle | `domain-bicycle.md` | B2C |
| PC build | `domain-pc.md` | B2C / prosumer |
| Cosmetics | `domain-cosmetics.md` | B2C |
| Home appliance (major) | `domain-home-appliance.md` | B2C |
| Small appliance | `domain-small-appliance.md` | B2C |
| Camera | `domain-camera.md` | B2C / prosumer |
| Audio | `domain-audio.md` | B2C / prosumer |
| Smart home | `domain-smart-home.md` | B2C |
| Furniture / mattress | `domain-furniture.md` | B2C + B2B |
| Personal mobility | `domain-mobility.md` | B2C |
| IT software / SaaS | `domain-it-software.md` | B2B |
| Medical device | `domain-medical-device.md` | B2C + B2B (clinic) |
| Anything else | `domain-unknown.md` → derives + saves new pack | — |

Matching rule: lowercase user query → scan `domain-index.md` keywords → longest-keyword-match wins → if no match, fall through to `domain-unknown.md` self-feeding workflow. If multiple packs match with comparable specificity → ask user via AskUserQuestion.

## Self-feeding

The skill **grows its own domain-pack library**. On encountering a category with no matching pack:

1. `domain-unknown.md` derives dimensions via ≤3 WebSearches.
2. Result is saved as a new `references/domain-<slug>.md` with `status: auto-generated, confidence: low`.
3. A row is appended to `references/domain-index.md`.
4. Future runs on the same category use the saved pack (no re-derivation).
5. After 3+ runs without contradiction, the skill auto-bumps `confidence: medium`.
6. A user reviewing the pack can promote it to `confidence: high, status: human-reviewed`.

See `references/self-feeding.md` for the full design (file format, refinement on subsequent runs, duplicate avoidance, opt-out).

The skill should mention to the user when it has created or updated a domain pack — this is part of the value delivered.

## Output

- Path: `tasks/research/<slug>.md`. Auto-create `tasks/research/`.
- Slug: kebab-case `<category>-<keyword>` (e.g., `bicycle-gravel-upgrade`, `pc-rtx-5070-build`).
- If file exists: append a new `## Re-evaluation <YYYY-MM-DD>` section. Do not overwrite.
- Template: `references/report-template.md`.
- Always confirm the written path back to the user.

## Audience-level switch

Asked once in step 4. The underlying procurement analysis runs in full regardless of choice — only reporting density changes.

- **`audience=casual`**: Executive summary up top is the headline; Procurement detail sections are condensed (one-sentence per subsection, 2–3 candidates, single bottom-line TCO, top-3 risk bullets).
- **`audience=pro`**: Same Executive summary; Procurement detail sections fully expanded (3–5 candidates, full TCO line items, complete vendor-risk profile, longer source list, explicit weighted/AHP/Pugh scoring matrix).

## Information sources

See `references/information-sources.md` for the canonical source list — cross-region (camelcamelcamel, Keepa, PCPartPicker, eBay sold, MPB/KEH), regional aggregators (US / EU / UK / CA / AU / JP / IN / BR / MENA / TR / others), reviews (RTINGS, Wirecutter, Consumer Reports, r/BuyItForLife, etc.), compliance (EPREL, CPSC SaferProducts.gov, EU RAPEX, MHRA, TGA, Health Canada, EUDAMED, etc.), repairability (iFixit, EU repairability index), and customs (USITC, TARIC, gov.uk Trade Tariff, CBSA, ABF, plus national equivalents).

## Failure modes

- **Domain unknown after ≤3 WebSearches** → ask user to define the key research dimensions manually.
- **Web unreachable** → fall back to user knowledge + local domain pack; explicitly mark price/risk data as "unverified".
- **User can't answer required input** → mark requirement as `unspecified`, downgrade scoring confidence, surface in Open Questions.
- **No candidate passes compliance** → surface the failure modes, ask user whether to relax must-haves or expand budget.
- **No reliable price data** → output MSRP only with an explicit "fair-price band could not be established" note.
- **Classification ambiguous** → ask user one question to disambiguate; default to leverage if unanswered.

## Source citation discipline

- Standards / compatibility claims: ≥2 independent sources.
- Opinions / reviews: ≥1 source.
- Price data: ≥1 aggregator + ≥1 primary seller link.
- Every URL goes in the report's Sources section, numbered.
