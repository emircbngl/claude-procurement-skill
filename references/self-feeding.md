# Self-feeding: skill learns its own domain packs over time

The skill starts with a finite set of `domain-<name>.md` packs. Every time it researches a category that doesn't have a pack, it derives the missing dimensions via web search (per `domain-unknown.md`). **Self-feeding** means: those derived dimensions are saved back to disk as a new `domain-<name>.md`, so future runs on that category benefit from the prior work.

This turns the skill into a knowledge base that grows with use — without any human-author intervention required.

## Lifecycle of an auto-generated domain pack

```
1. First run on unknown category X
   → derive dimensions via 3 WebSearches (domain-unknown.md)
   → run the full pipeline on the derived dimensions
   → SAVE derived dimensions to references/domain-<X>.md with auto-generated marker
   → write report to tasks/research/

2. Second run on same category X (could be days/weeks later)
   → SKILL.md domain-detection table now matches → loads references/domain-<X>.md
   → no WebSearch needed for dimensions
   → run full pipeline using saved pack
   → if pipeline surfaces new info worth saving, append/refine the pack

3. Nth run on category X
   → pack now mature, stable; serves as if hand-authored

4. Human review (optional but recommended every ~3 months)
   → user opens references/ folder, reads auto-generated packs
   → corrects / promotes / removes marker
```

## What gets saved (and what doesn't)

**Save**:
- Research dimensions (functional, quality, economic, usage_fit) derived from WebSearch 1
- Standards & compatibility axes derived from WebSearch 2
- Common pitfalls / failure modes derived from WebSearch 3
- Trusted sources actually used in the run (the URLs that paid off)
- Domain detection keywords (slugs / synonyms the skill should match next time)

**Do not save**:
- Specific product candidates (those belong in `tasks/research/`, not the domain pack)
- User-specific context (existing gear, budget — that's per-user, not per-domain)
- Price data (changes constantly; per-run data lives in research reports)

## File format for auto-generated packs

Same skeleton as hand-authored packs (`domain-<name>.md`), but with a frontmatter marker so the skill (and human reviewers) can tell them apart:

```markdown
---
status: auto-generated
derived-from-query: "<user's original query>"
first-run-date: 2026-05-28
last-updated: 2026-05-28
run-count: 1
confidence: low
sources-used:
  - https://...
  - https://...
human-reviewed: false
---

# Domain: <Name> (auto-generated)

> ⚠ **Auto-generated pack** — derived from web search on first encounter with this
> category. Dimensions and standards may have gaps or inaccuracies. Treat as a
> starting point; verify critical claims (compliance, standards, compat rules)
> against authoritative sources before relying on them for purchase decisions.

[rest of file follows the standard domain-pack template — see domain-bicycle.md
or domain-pc.md as the canonical reference]
```

## Confidence levels

Track per pack:
- **`low`** (first 1–2 runs) — derived from a few WebSearches; significant gaps possible
- **`medium`** (3–5 runs OR explicit human review) — refined across multiple uses, edge cases surfaced
- **`high`** (`human-reviewed: true` flag set by user) — verified by a human

The skill should:
- Cite low-confidence packs with a warning in the report ("Note: domain pack for X is auto-generated, low-confidence; verify compatibility claims independently.")
- Stop warning at medium / high confidence

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
6. After 3+ successful runs without contradiction → bump `confidence` from `low` to `medium`.

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
