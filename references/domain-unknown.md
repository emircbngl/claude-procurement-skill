# Domain: Unknown (fallback + self-feeding workflow)

When the user asks about a product category that doesn't match any pack in `references/domain-index.md`, this file guides the skill to **derive** the missing domain pack on-the-fly via web search, **save** it to disk as a new `domain-<name>.md`, and run the standard procurement pipeline.

This is the self-feeding mechanism — see `self-feeding.md` for the full design.

## When to use

Step 1 maps the product to a domain by consulting `domain-index.md`. If no matching row, load this file instead.

Examples that hit this path on first encounter: drones, 3D printers, espresso machines (dedicated tier beyond small-appliance), watches, baby products, supplements, solar panels, niche professional gear.

## Discovery workflow

Run up to **3 WebSearch calls** to derive the category's dimensions, then save and proceed:

### WebSearch 1: Buying guide

Query: `"<category> buying guide key specifications"` OR `"how to choose <category>"` OR `"<category> spec comparison"`.

Goal: identify the **canonical research dimensions** for the category. Look for sources like Wirecutter, Consumer Reports, RTINGS, manufacturer "how to choose" pages, expert-domain sites.

Extract:
- 4–8 key functional specs experts use to differentiate products
- Common use-case profiles (beginner / enthusiast / pro)
- Tier breakpoints (entry / mid / premium / flagship) with typical price ranges

### WebSearch 2: Compatibility / standards

Query: `"<category> compatibility standards"` OR `"<category> connector types"` OR `"<category> interoperability"`.

Goal: identify what **standards / interop axes** matter. Look for:
- Physical interfaces (mounts, connectors, cutouts)
- Electrical / protocol standards (voltage, data, RF)
- Ecosystem dependencies (proprietary platform vs open standard)
- Required adapters / accessories

If a category has no notable compatibility axes (standalone product), note that and skip step 5's compatibility check.

### WebSearch 3: Reliability + common failure modes

Query: `"<category> common problems"` OR `"<category> reliability comparison brands"` OR `"<category> long-term review"`.

Goal: identify common failure modes (input to FMEA-lite in step 7) and brand-reliability signals.

## Save the derived pack to disk (self-feeding)

**This is the new step.** After WebSearches 1–3 yield enough information:

1. Compute a slug from the category: `<category>` → kebab-case (e.g., "espresso machine" → `espresso-machine`).
2. Check `domain-index.md` for keyword overlap with existing packs (avoid duplicates).
3. Write the new pack to `references/domain-<slug>.md` using the auto-generated template (below).
4. Append a row to `references/domain-index.md` with the new pack's keywords + `status: auto-gen, confidence: low`.
5. Note in the research report: "Created new domain pack: `references/domain-<slug>.md` (auto-generated, low-confidence). Review before treating as authoritative."

### Auto-generated pack template

```markdown
---
status: auto-generated
derived-from-query: "<verbatim user query that triggered this>"
first-run-date: <YYYY-MM-DD>
last-updated: <YYYY-MM-DD>
run-count: 1
confidence: low
sources-used:
  - <url 1>
  - <url 2>
  - ...
human-reviewed: false
---

# Domain: <Category Name> (auto-generated)

> ⚠ **Auto-generated pack** — derived from web search on first encounter with this
> category. Dimensions and standards may have gaps or inaccuracies. Treat as a
> starting point; verify critical claims (compliance, standards, compat rules)
> against authoritative sources before relying on them for purchase decisions.

## Research dimensions
- functional_specs: [list extracted from WebSearch 1]
- quality_signals: [extracted reviews / MTBF / owner-satisfaction signals]
- economic: [price tiers, consumables, typical lifespan]
- usage_fit: [profiles extracted from WebSearch 1]

## Required user inputs (overrides universal)
- [category-specific inputs derived from buying guides]

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| [from WebSearch 2; may be empty if standalone product] | | |

## Common pitfalls / failure modes
[from WebSearch 3]

## Regional notes
[anything region-specific surfaced during derivation — major regional brands, distribution differences, regulatory variation. Otherwise: "Not derived — refine on next run with user's region context."]

## B2B variant
[if category has a B2B dimension; otherwise: "B2C-dominant category" or "B2B-dominant category"]

## Trusted sources for web fallback

[the actual URLs surfaced in WebSearches 1–3 that gave useful info]
```

## Standard pipeline still runs

Once dimensions are derived AND saved, the rest of the workflow proceeds normally:
- Step 4 (requirements) uses the derived dimensions to ask the right questions.
- Step 5 (RFI + compliance) uses the derived standards for compliance checks.
- Step 6 (price discovery) uses category-appropriate sources.
- Step 7 (TCO) uses derived consumables data.
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
6. After 3+ successful runs without contradiction → bump `confidence` from `low` to `medium`.

## Failure mode

If 3 WebSearches don't yield clear dimensions:
- Surface the partial findings to the user.
- Ask via AskUserQuestion: "I couldn't auto-derive the key research dimensions for `<category>`. Can you tell me the 3–5 specs that matter most to you for this product?"
- Treat user's answer as the dimensions.
- Still **save** the pack (with `confidence: low` + user-provided dimensions marked); future runs benefit.
- Continue the pipeline.

## Avoiding duplicate / near-duplicate packs

Before creating a new pack, scan `domain-index.md` for keyword overlap:

- If the user asked about "espresso machine" and `domain-small-appliance.md` already covers it broadly → ask the user via AskUserQuestion: "Should I create a dedicated `espresso machine` pack or use the existing `small-appliance` pack?"
- If the user asked about "noise-cancelling headphones" and `domain-audio.md` covers it → use existing, don't duplicate.

The heuristic: if a query matches an existing pack with confidence ≥ medium, use existing. Create a new pack only when the existing pack would noticeably under-serve the query (different standards, different sourcing, different failure modes).

## Opt-out

User can pass `--no-save-pack` in their query to skip the save step. Default is save. Knowledge accumulation is the goal.
