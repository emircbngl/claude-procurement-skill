# Domain: Unknown (fallback + self-feeding workflow)

When the user asks about a product category that doesn't match any pack in `references/domain-index.md`, this file guides the skill to **derive** the missing domain pack on-the-fly via web search, **save** it to disk as a new `domain-<name>.md`, and run the standard procurement pipeline.

This is the self-feeding mechanism — see `self-feeding.md` for the full design.

## When to use

Step 1 maps the product to a domain by consulting `domain-index.md`. If no matching row, load this file instead.

Examples that hit this path on first encounter: drones, 3D printers, espresso machines (dedicated tier beyond small-appliance), watches, baby products, supplements, solar panels, niche professional gear.

## Discovery routing

Two paths to acquire the criteria-side knowledge. Choose Path A when available; fall back to Path B otherwise.

### Path A — Delegate to `deep-research` skill (preferred when available)

If the `deep-research` skill is registered in the current Claude Code setup (check the available-skills list for an entry named exactly `deep-research`), delegate the criteria-side research to it via the Skill tool. Rationale: `deep-research` already implements proper fan-out + adversarial verification + cited synthesis — reusing it beats re-implementing it.

**Invocation**:

```
Skill(skill="deep-research", args="<composite-prompt below>")
```

**Composite prompt template** (substitute `<category>` and the user's region):

```
Research <category> for procurement purposes. Cover ALL 8 of the following dimensions,
with cited sources for each. Do NOT cover prices, current stock, or current promos —
those will be re-fetched live elsewhere and would go stale.

1. Buying-guide spec dimensions — 4–8 functional specs experts use to differentiate
   products in this category; common use-case profiles (beginner / enthusiast / pro);
   tier breakpoints (entry / mid / premium / flagship) with anchored price ranges.

2. Standards + regulatory bodies — ISO / IEC / IEEE / EN standards; physical interfaces,
   connectors, protocols; required certification marks per major region
   (CE, FCC, UL, RoHS, CCC, PSE, KC, RCM, BIS, INMETRO, regional national marks).

3. Brand landscape across regions — 5–10 dominant brands globally; per-region distinction
   (which brands strong in US / EU / UK / CA / AU / JP / IN / BR / MENA / other);
   authorized-distribution patterns (DTC vs dealer network).

4. Common pitfalls + failure modes — 8–12 known failure patterns from long-term-ownership
   reviews and repair-shop sources; brand-reliability signals; industry-wide design flaws.

5. Repairability + EOL — iFixit-style scores if available; modular-vs-sealed norms;
   manufacturer right-to-repair posture; standard EOL routes (resale, trade-in, recycle).

6. Compliance / safety / recall registries — per-region recall-monitoring URLs
   (CPSC SaferProducts.gov, EU RAPEX, MHRA, TGA, Health Canada, national equivalents);
   recent high-profile recalls in the category; category-specific safety-cert hierarchy.

7. TCO drivers — consumables with replacement cadence; energy spec range
   (watts, kWh/yr); typical maintenance schedule; expected lifespan in years.

8. Long-term ownership signals — which brands hold up at 2+ years; sub-categories with
   reliability problems; aesthetic / ergonomic regret patterns.

Output format: 8 numbered sections, each with bulleted findings and cited URLs.
User region context: <region>
```

When `deep-research` returns its synthesis, parse it into the auto-generated domain-pack template (see "Save the derived pack to disk" below). Frontmatter: `confidence: medium`, `deep-search-completed: true`, `delegated-to: deep-research`, `sources-used:` populated from the synthesis's citations.

### Path B — Inline 8-category deep search (fallback)

When `deep-research` is not registered, run the 8-category deep search inline (~20–30 WebSearch + WebFetch calls total). **Use parallel-batched tool calls per category** — Claude supports multiple tool calls per turn, so issue 3–5 WebSearch / WebFetch calls in one message rather than sequential one-per-turn. Per category, identify the best 3–5 sources via WebSearch then WebFetch them in parallel for full content extraction.

**Critical scope clarification (applies to both paths)**: this deep search captures **criteria-side knowledge** only — what the category is, what specs matter, what standards apply, what brands exist, what fails. It does **NOT** capture prices, current stock, or current promos. Those are dynamic and would go stale immediately; step 6 (price discovery) re-runs live every query and is intentionally not cached.

The 8 categories of Path B follow:

### Category 1: Buying guides + spec dimensions (3–5 sources)

Queries: `"<category> buying guide key specifications"`, `"how to choose <category>"`, `"<category> spec comparison expert review"`.

Target sources: Wirecutter, Consumer Reports, RTINGS, expert-domain sites (e.g., DPReview for cameras, Whole Latte Love for espresso), manufacturer "how to choose" pages, top-of-rank YouTube channels in the category.

Extract: 4–8 key functional specs experts use to differentiate products; common use-case profiles (beginner / enthusiast / pro); tier breakpoints (entry / mid / premium / flagship) with typical price ranges (anchored, not current).

### Category 2: Standards + regulatory bodies (2–4 sources)

Queries: `"<category> compatibility standards"`, `"<category> connector types"`, `"<category> ISO IEC standard"`, `"<category> certification mark"`.

Target sources: ISO Online Browsing Platform, IEC, IEEE, EN/DIN standards, manufacturer compatibility charts, industry-body publications.

Extract: physical interfaces (mounts, connectors, cutouts); electrical / protocol standards; ecosystem dependencies (proprietary vs open); required adapters; mandatory certification marks per major region.

If a category has no notable compatibility axes (standalone product), explicitly note "no compatibility axes — skip step 5 compat matrix" in the saved pack.

### Category 3: Brand landscape across regions (3–5 sources)

Queries: `"<category> best brands 2026"`, `"<category> top manufacturers"`, `"<category> brands US EU UK"`, `"<category> authorized dealer"`.

Target sources: market-share reports, retailer brand-category landing pages, professional society recommendations, region-specific best-of lists.

Extract: 5–10 dominant brands globally; per-region distinction (which brands strong where); authorized-distribution patterns (direct-to-consumer vs dealer network); B2C vs B2B brand split if applicable.

### Category 4: Common pitfalls + failure modes (2–3 sources)

Queries: `"<category> common problems"`, `"<category> worst mistakes buying"`, `"<category> what to avoid"`, `"<category> reliability comparison"`.

Target sources: forum threads (Reddit, specialist forums), long-term-ownership reviews, repair-shop YouTube content, consumer-protection databases.

Extract: top 8–12 failure modes / pitfalls (input to FMEA-lite in step 7); brand-reliability signals; known industry-wide design flaws or recall patterns.

### Category 5: Repairability + EOL (1–2 sources)

Queries: `"<category> repairability"`, `"<category> right to repair"`, `"<category> end of life recycling"`.

Target sources: iFixit, EU repairability index documentation, manufacturer take-back / recycling programs.

Extract: typical repairability stance (modular vs sealed); iFixit-style scores if published for the category; manufacturer right-to-repair posture; standard EOL routes (resale, trade-in, recycle).

### Category 6: Compliance / safety / recall registries (1–2 sources)

Queries: `"<category> recall registry"`, `"<category> safety certification"`, `"<category> regulatory authority"`.

Target sources: CPSC SaferProducts.gov, EU RAPEX Safety Gate, MHRA / TGA / Health Canada / regional regulators, brand-specific recall pages.

Extract: per-region recall-monitoring URLs; any high-profile recent recalls in the category; safety-cert hierarchy specific to the category (e.g., IEC 60601 for medical electrical).

### Category 7: TCO drivers — consumables, energy, service (1–2 sources)

Queries: `"<category> consumables cost"`, `"<category> energy consumption running cost"`, `"<category> maintenance schedule"`, `"<category> service intervals"`.

Target sources: manufacturer service manuals, energy-database entries (Energy Star, EPREL), specialist sites that publish TCO breakdowns.

Extract: consumable list with typical replacement cadence; energy spec range (watts, kWh/yr); maintenance schedule template; expected lifespan in years.

### Category 8: Reviews + long-term ownership signals (2–3 sources)

Queries: `"<category> long term review"`, `"<category> after 2 years"`, `"<category> buyitforlife"`, `"<category> reliability long term"`.

Target sources: r/BuyItForLife, multi-year YouTube revisit videos, professional reviewers' long-term updates, specialist forums.

Extract: which brands hold up at 2+ years; which sub-categories have reliability problems; aesthetic / ergonomic regret patterns reported by long-term owners.

---

After all 8 categories complete (~20–30 calls), run adversarial verification (next), then score and save.

## Adversarial verification of high-stakes dimensions

Before saving, **verify the high-stakes dimensions** — `compatibility`, `standards-regulators`, `compliance-recall` — per `references/adversarial-verify.md`. These are the dimensions where a wrong claim causes a "won't fit" or "isn't legal" failure, and they must survive an independent attempt to refute them before the pack trusts them.

- Extract the 3–8 highest-stakes claims from those dimensions (e.g., "X mount fits Y", "CE + <national mark> required for sale", "no active recall on the current model line").
- Run the refutation pass (Route A: delegate to `deep-research` with the refutation prompt; Route B: inline skeptic pass with independent sources).
- Each claim gets a verdict (`verified` / `partially-verified` / `refuted` / `unverified`) per `schemas.md` §4.
- `refuted` claims are corrected or removed; `unverified` high-stakes claims are flagged and cap their dimension at `low`.

## Score per-dimension confidence

Assign each of the 9 dimensions a confidence (`low`/`medium`/`high`) using the rubric in `schemas.md` §3:
- High-stakes dimensions: scored partly by the verification verdicts above.
- Other dimensions: scored by source count + authority (≥2 authoritative → high; 1 authoritative → medium; weak/single → low).
- Compute the **aggregate** `confidence` from the per-dimension map using the weighted-floor rule (`schemas.md` §3) — do not hand-pick it. Any high-stakes dimension at `low` forces aggregate `low`.

## Save the derived pack to disk (self-feeding)

After verification + scoring:

1. Compute a slug from the category: `<category>` → kebab-case (e.g., "espresso machine" → `espresso-machine`).
2. Check `domain-index.md` for keyword overlap with existing packs (avoid duplicates).
3. Write the new pack to `references/domain-<slug>.md` using the auto-generated template (below) — including the `dimension-confidence` map, the `verification` map, the standards-table "Verified?" column, and the closing "## Dimension confidence" section. Run the `schemas.md` self-validation checklist before writing.
4. Append a row to `references/domain-index.md` with the new pack's keywords + `status: auto-gen` + the computed aggregate `confidence`.
5. Note in the research report: "Created new domain pack: `references/domain-<slug>.md` (auto-generated via deep search; aggregate confidence: `<computed>`; high-stakes dimensions adversarially verified). Subsequent runs on this category will skip dimension research and reuse the saved pack."

### Auto-generated pack template

Full schema in `references/schemas.md` §1. The shape:

```markdown
---
status: auto-generated
derived-from-query: "<verbatim user query that triggered this>"
first-run-date: <YYYY-MM-DD>
last-updated: <YYYY-MM-DD>
run-count: 1
confidence: <aggregate computed from dimension-confidence per schemas.md §3>
dimension-confidence:
  buying-guides: <low|medium|high>
  standards-regulators: <low|medium|high>
  brand-landscape: <low|medium|high>
  pitfalls-failure-modes: <low|medium|high>
  repairability-eol: <low|medium|high>
  compliance-recall: <low|medium|high>
  tco-drivers: <low|medium|high>
  long-term-reviews: <low|medium|high>
  compatibility: <low|medium|high>
deep-search-completed: true
acquired-via: <inline | deep-research-delegation>
search-categories-covered:
  - buying-guides
  - standards-regulators
  - brand-landscape
  - pitfalls-failure-modes
  - repairability-eol
  - compliance-recall
  - tco-drivers
  - long-term-reviews
verification:
  "<high-stakes claim>": { verdict: <verified|partially-verified|refuted|unverified>, confidence: <low|medium|high>, sources: [<url>, <url>] }
sources-used:
  - <url 1>
  - <~15–25 URLs across the 8 categories>
human-reviewed: false
---

# Domain: <Category Name> (auto-generated, deep search)

> ℹ **Auto-generated pack** — derived from a comprehensive 8-category deep search
> on first encounter with this category. High-stakes dimensions were adversarially
> verified. Treat as a working reference; human review can promote to confidence: high
> and remove this banner. (If aggregate confidence is `low`, use ⚠ and name the weak dimension.)

## Research dimensions
- functional_specs: [from category 1]
- quality_signals: [reviews / MTBF / owner-satisfaction]
- economic: [price tiers, consumables, typical lifespan]
- usage_fit: [profiles from category 1]

## Required user inputs (overrides universal)
- [category-specific inputs derived from buying guides]

## Standards & compatibility axes

| Axis | Values | Compat rule | Verified? |
|------|--------|-------------|-----------|
| [from category 2; may be empty if standalone product] | | | <verified/unverified/refuted> |

## Common pitfalls / failure modes
[from category 4]

## Regional notes
[region-specific brands, distribution, regulatory variation. Otherwise: "Not derived — refine on next run with user's region context."]

## B2B variant
[if category has a B2B dimension; otherwise: "B2C-dominant category" or "B2B-dominant category"]

## Trusted sources for web fallback
[the actual URLs surfaced across the 8 categories — typically 15–25 URLs]

## Dimension confidence
| Dimension | Confidence | Basis |
|-----------|-----------|-------|
| buying-guides | <score> | <n authoritative sources / notes> |
| standards-regulators | <score> | <verification verdict + sources> |
| compatibility | <score> | <verification verdict + sources> |
| compliance-recall | <score> | <verification verdict + sources> |
| brand-landscape | <score> | <basis> |
| pitfalls-failure-modes | <score> | <basis> |
| repairability-eol | <score> | <basis> |
| tco-drivers | <score> | <basis> |
| long-term-reviews | <score> | <basis> |
```

## Standard pipeline still runs

Once dimensions are derived AND saved, the rest of the workflow proceeds normally:
- Step 4 (requirements) uses the derived dimensions to ask the right questions.
- Step 5 (RFI + compliance) uses the derived standards for compliance checks.
- **Step 6 (price discovery) runs live — uses the derived `sources-used` list for which aggregators to scan, but pulls actual prices fresh from those sources every query.** Prices are intentionally never cached.
- Step 7 (TCO) uses derived consumables data + live price discovery.
- Steps 8–11 proceed standard.

The research report is written to `tasks/research/<slug>.md` as usual. The new domain pack lives at `references/domain-<slug>.md`.

## Refinement on subsequent runs

If the skill runs on the same category **again**:

1. `domain-index.md` now matches (added on first run).
2. Load `references/domain-<slug>.md` instead of `domain-unknown.md`.
3. Run the standard pipeline.
4. If the run surfaces new info worth saving:
   - A standard / axis the pack missed → **append** to the pack's standards table.
   - A new failure mode → **append** to pitfalls.
   - A new authoritative source → **append** to sources list.
   - A correction to an existing entry → **flag for review** (don't auto-overwrite; ambiguous).
5. Increment `run-count` in the pack's frontmatter; update `last-updated`.
6. Confidence stays at **medium** after deep search; human review promotes it to **high** + sets `human-reviewed: true`.
7. If `last-updated` is > 18 months old, recommend re-running the deep search — standards and brand landscape drift over time.

## Failure mode

If the 8-category deep search doesn't yield clear results (e.g., extremely niche category, no authoritative sources online):
- Surface the partial findings to the user.
- Ask via AskUserQuestion: "I couldn't auto-derive complete information for `<category>`. Can you tell me the 3–5 specs that matter most to you for this product?"
- Treat user's answer as supplementary dimensions.
- Still **save** the pack with `confidence: low` (not medium — deep search did not complete) and `deep-search-completed: false` in frontmatter; future runs benefit and may trigger re-derivation.
- Continue the pipeline.

## Avoiding duplicate / near-duplicate packs

Before creating a new pack, scan `domain-index.md` for keyword overlap:

- If the user asked about "espresso machine" and `domain-small-appliance.md` already covers it broadly → ask the user via AskUserQuestion: "Should I create a dedicated `espresso machine` pack or use the existing `small-appliance` pack?"
- If the user asked about "noise-cancelling headphones" and `domain-audio.md` covers it → use existing, don't duplicate.

The heuristic: if a query matches an existing pack with confidence ≥ medium, use existing. Create a new pack only when the existing pack would noticeably under-serve the query (different standards, different sourcing, different failure modes).

## Opt-out

User can pass `--no-save-pack` in their query to skip the save step. Default is save. Knowledge accumulation is the goal.
