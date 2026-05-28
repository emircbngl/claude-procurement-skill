# Self-feeding: skill learns its own domain packs over time

The skill starts with a finite set of `domain-<name>.md` packs. Every time it researches a category that doesn't have a pack, it runs an **8-category deep search** (~20–30 web calls) and saves the result as a new `domain-<name>.md`. **Self-feeding** means future runs on that category reuse the saved pack and skip dimension research entirely.

This turns the skill into a knowledge base that grows with use — without any human-author intervention required.

## What we cache vs what stays live

This is the most important distinction:

- **Cached (saved to pack, ~zero web cost per future run)**: research dimensions, standards & compatibility axes, certification marks, brand landscape per region, common pitfalls, regulatory bodies, repairability norms, trusted source URLs. **This is the criteria-side knowledge — the stable "how do you evaluate this category" content.**
- **Live (re-fetched every query)**: current prices, stock, active promos, fair-price band, recent recalls, vendor news, FX rates. **This is the dynamic data — caching it would be a feature anti-pattern because stale prices mislead buyers.**

The skill never goes back to the internet to **re-derive criteria** for a known domain. It always goes back to the internet for **current pricing and availability**, every query. Both are intentional.

## Lifecycle of an auto-generated domain pack

```
1. First run on unknown category X
   → trigger 8-category DEEP SEARCH (~20–30 web calls; criteria-side only)
   → SAVE derived criteria/standards/brands/pitfalls to references/domain-<X>.md
     with confidence: medium + deep-search-completed: true
   → also run live price discovery (step 6) for this query
   → write report to tasks/research/

2. Second run on same category X (could be days/weeks/months later)
   → domain-index.md matches → loads references/domain-<X>.md
   → ZERO web calls for dimensions/standards/brands/pitfalls
   → live price discovery + availability runs as normal
   → if pipeline surfaces new criteria-side info, append to pack

3. Nth run on category X
   → pack mature; serves as if hand-authored

4. Human review (optional)
   → user reads pack, makes corrections, removes the auto-generated banner,
     sets confidence: high + human-reviewed: true
```

## What gets saved (and what doesn't)

**Save (cached forever, refreshed only every ~18 months)**:
- Research dimensions (functional_specs, quality_signals, economic, usage_fit)
- Standards & compatibility axes
- Common pitfalls / failure modes
- Brand landscape per region
- Trusted sources for future verification + future price discovery
- Domain detection keywords (synonyms the skill should match)
- Regulatory bodies + certification marks for the category
- Repairability + EOL norms

**Do not save (intentionally re-fetched every query)**:
- Current prices, stock, promo discounts
- Fair-price band (calculated per query from live data)
- Recent recalls or vendor news
- Specific product candidates (those live in `tasks/research/`, not the pack)
- User-specific context (existing gear, budget — per-user, not per-domain)
- FX rates

## File format for auto-generated packs

Same skeleton as hand-authored packs (`domain-<name>.md`), but with a frontmatter marker so the skill (and human reviewers) can tell them apart:

```markdown
---
status: auto-generated
derived-from-query: "<user's original query>"
first-run-date: 2026-05-28
last-updated: 2026-05-28
run-count: 1
confidence: medium
deep-search-completed: true
search-categories-covered: [buying-guides, standards-regulators, brand-landscape, pitfalls-failure-modes, repairability-eol, compliance-recall-registries, tco-drivers, long-term-reviews]
sources-used:
  - https://...
  - https://...
  - <~15–25 URLs from the 8 deep-search categories>
human-reviewed: false
---

# Domain: <Name> (auto-generated, deep search)

> ℹ **Auto-generated pack** — derived from a comprehensive 8-category deep search
> on first encounter with this category. Treat as a working reference;
> human review can promote to `confidence: high` and remove this banner.
> For purchase decisions involving regulatory or safety claims, verify against
> the sources listed at the bottom of this file.

[rest of file follows the standard domain-pack template — see domain-bicycle.md
or domain-pc.md as the canonical reference]
```

## Confidence levels

Track per pack:
- **`low`** — derivation failed (deep search didn't complete cleanly); pack saved with user-supplied dimensions as a fallback. Report should warn user.
- **`medium`** — deep search completed (default for auto-generated packs); or hand-authored without explicit review. Refined across uses.
- **`high`** — `human-reviewed: true` flag set by user after review.

The skill should:
- Cite low-confidence packs with a warning in the report ("Note: domain pack for X is auto-generated and the deep search did not complete cleanly; verify critical claims independently.")
- Treat medium and high confidence as equivalent for runtime decisions — no warning needed in reports.

## Update / refinement on subsequent runs

When the skill runs on an existing auto-generated pack:

1. Read the pack as the starting point.
2. Run the normal pipeline.
3. If the run surfaces:
   - A standard / axis the pack missed → **append** to the pack's standards table
   - A new failure mode → **append** to pitfalls
   - A new authoritative source → **append** to sources list
   - A correction to an existing entry → **flag for review** (don't auto-overwrite; ambiguous)
4. Increment `run-count`.
5. Update `last-updated` date.
6. Deep-search-completed packs start at `medium`; they don't auto-bump to `high` (that requires human review).
7. If `last-updated` is > 18 months old, recommend re-running the deep search — standards and brand landscape drift over time.

## Promotion to hand-authored

When a user reviews an auto-generated pack and is satisfied:
- Remove the warning banner from the top of the file.
- Set `status: human-reviewed`, `human-reviewed: true`, `confidence: high`.
- Optionally remove or compress the frontmatter (it's no longer auto-managed).

Promotion is a manual user action, not automatic.

## Domain detection table — keep it growing

After saving a new pack, SKILL.md's domain-detection table needs to know about it. The skill should:

1. On first save, write the new entry into SKILL.md's domain detection table (or, alternately, **maintain a separate `references/domain-index.md`** that's the authoritative list).

For v1, use option two: keep a lightweight `domain-index.md` that the skill consults FIRST on every run. SKILL.md's hard-coded table acts as fallback documentation; the index is the dynamic source of truth.

### `references/domain-index.md` format

```markdown
# Domain Pack Index

Authoritative list of available domain packs. The skill consults this on step 1
to map user query keywords to a pack.

| Domain | Pack file | Keywords | Status |
|---|---|---|---|
| Bicycle | domain-bicycle.md | bicycle, bike, MTB, gravel, road, drivetrain, cassette, hub | hand |
| PC | domain-pc.md | PC, build, motherboard, CPU, GPU, RAM, PSU | hand |
| Cosmetics | domain-cosmetics.md | skincare, makeup, serum, sunscreen, retinol, niacinamide | hand |
| ... | ... | ... | ... |
| Espresso | domain-espresso.md | espresso, coffee machine, portafilter, group head | auto-gen |
```

The skill maintains this file. On each save of a new pack, append a row.

## Failure modes of self-feeding

- **Pack quality drift** — if early runs derive incorrect dimensions, later runs propagate the error. Mitigation: low-confidence warning + human review cadence.
- **Duplicate / near-duplicate packs** — "domain-headphones" and "domain-audio" overlap. Mitigation: before creating a new pack, check the index for keyword overlap; merge instead of duplicating.
- **Auto-generated pack vs reality** — manufacturer standards change; auto-gen packs go stale. Mitigation: `last-updated` field + recommend re-derivation if > 18mo old.
- **Hostile / wrong-information source** — if the skill's WebSearch lands on a low-quality blog spam page, derived dimensions could be wrong. Mitigation: require ≥2 sources for any standard saved to a pack.

## Workflow change for `domain-unknown.md`

The current `domain-unknown.md` ends with "If the user runs the skill on the same unknown category multiple times, consider this a signal to promote the category to its own pack (out-of-scope for v1)." With self-feeding, this changes: **promotion happens on the first run**, not after N runs. See updated `domain-unknown.md`.

## User opt-out

A user who wants to disable self-feeding (e.g., for a one-off research session) can:
- Pass `--no-save-pack` (skill respects this if encoded as a query modifier)
- Or simply delete the auto-generated pack after the run

Default behavior: save the pack. Knowledge accumulation is the goal.
