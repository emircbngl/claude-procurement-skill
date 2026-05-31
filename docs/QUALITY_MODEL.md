# Quality model — how the skill knows what it knows

A research skill is only as trustworthy as its weakest unstated assumption. This skill makes its trust model **explicit and machine-checkable** through three mechanisms that work together:

1. **Structured schemas** — every artifact has a defined shape, self-validated before writing
2. **Adversarial verification** — high-stakes claims must survive an independent attempt to refute them
3. **Per-dimension confidence scoring** — trust is tracked per dimension, not as a blanket label

Together they answer the question *"how much should I trust this part of the report?"* — precisely, per claim, rather than with a single vague hand-wave.

---

## 1. Structured schemas

Canonical shapes live in [`references/schemas.md`](../references/schemas.md). Three artifacts are schema-governed:

- **Domain packs** — frontmatter fields (typed), body sections (fixed order), the per-dimension confidence map, and the verification map.
- **Research reports** — the 17-section decision memo, with typing rules layered on (e.g., header must carry pack confidence; no refuted claim stated as fact).
- **In-run objects** — verification verdicts, per-candidate price objects, compatibility-matrix rows.

Because this is a single-agent skill (no enforced StructuredOutput tool), the schema is enforced by a **self-validation checklist** the model runs before writing each artifact. The point is anti-drift: the 50th auto-generated pack should have the same shape as the 1st, so a human (or a future run) always knows where to look.

## 2. Adversarial verification

Methodology in [`references/adversarial-verify.md`](../references/adversarial-verify.md). The principle:

> A claim hasn't earned its place until an independent skeptic has tried to refute it and failed.

This is the cheapest insurance against the most expensive procurement mistakes — a plausible-but-false compatibility or compliance claim. "This wheel fits your frame" / "this is legal to sell here" / "this vendor is SOC 2 compliant", if wrong, cost real money.

**What gets verified** (budget is spent only where stakes are high):

| Stakes | Examples | Verified? |
|---|---|---|
| High | compatibility/interop rules, mandatory certifications, recall status, B2B compliance attestations | always |
| Medium | spec-dimension definitions, reliability signals, TCO magnitudes | strategic-class only |
| Low | review opinions, aesthetics, nice-to-have features | never (not worth it) |

**How** — same two-route philosophy as deep search: prefer delegating a refutation-framed prompt to the `deep-research` skill (fresh sources, no anchoring); fall back to an inline skeptic pass with independent sources. Either way the bias rule is **default to `unverified`, never `verified`** — optimism is how false claims survive.

**Multi-lens** — for the highest-stakes claims, four lenses each catch a different failure mode: correctness, conditionality ("true, but only with a firmware update"), recency ("was true, standard changed"), and region ("true elsewhere, not for you"). The conditionality and region lenses catch the "technically true but not for you" trap that single-pass checks miss.

**When** — at pack creation (verify the high-stakes dimensions before saving), at the step-5 compatibility matrix for strategic purchases (verify every row, both directions), at B2B compliance checks, and on demand.

## 3. Per-dimension confidence scoring

Model in [`references/schemas.md`](../references/schemas.md) §3. Instead of one blanket `confidence: medium` for a whole pack, each of **9 dimensions** is scored independently:

```
buying-guides · standards-regulators · brand-landscape · pitfalls-failure-modes
repairability-eol · compliance-recall · tco-drivers · long-term-reviews · compatibility
```

### Scoring rubric

| Score | Criteria |
|---|---|
| `high` | ≥2 independent authoritative sources AND (high-stakes) adversarial-verify returned `verified` |
| `medium` | ≥2 sources, or 1 authoritative source, not refuted |
| `low` | 1 weak source, unresolved conflict, not found, or adversarial-verify returned `refuted`/`unverified` |

Authoritative = manufacturer datasheet, standards body, regulator, or top-tier independent lab. Forums corroborate; they don't authorize on their own.

### Aggregate is computed, not guessed

```
HIGH_STAKES = {compatibility, compliance-recall, standards-regulators}

aggregate =
  if any HIGH_STAKES dimension is low   -> low
  elif ≥3 dimensions are low            -> low
  elif all HIGH_STAKES are high
       and ≥6 of 9 are high             -> high
  else                                  -> medium
```

The floor rule means a pack can't be "high" overall while any safety/interop dimension is weak — exactly where being wrong hurts. And one thin review dimension can't drag an otherwise-solid pack to `low`.

### Why per-dimension beats blanket

A pack for, say, "resin 3D printers" might have:
- `standards-regulators: high` (well-documented resin/exposure standards)
- `compatibility: high` (verified — vat/FEP/build-plate standards confirmed)
- `long-term-reviews: low` (category too new for 2-year data)

A blanket "medium" hides both the strength and the gap. Per-dimension lets the report say precisely: *"Compatibility and standards are well-verified; long-term reliability data is thin — treat durability claims cautiously."* That's an honest, actionable statement of what's known and what isn't.

---

## How a reader sees it

In the report:
- The header carries `Pack confidence: <aggregate>` when an auto-generated pack was used.
- If any high-stakes dimension is `low`, the report names it specifically rather than warning blandly.
- `refuted`/`unverified` high-stakes claims appear in **Section 16 (Open questions — verify before purchase)** — never buried, never stated as settled fact.

In the pack:
- Frontmatter `dimension-confidence` map + `verification` map (machine-readable).
- A closing `## Dimension confidence` table (human-readable) mirroring the map.
- The standards table carries a `Verified?` column.

## Promotion path

Auto-generated packs are `confidence: <aggregate>`, `human-reviewed: false`. A human can review a pack, correct it, remove the banner, and set `human-reviewed: true` + `confidence: high`. This is the only path to `high` aggregate beyond what the computed rule allows — human judgment is the final authority.

## What this is NOT

- It's not a guarantee of correctness — it's a calibrated, honest statement of confidence with an audit trail.
- It's not a substitute for the user verifying safety/regulatory claims themselves on high-stakes purchases — the report says so explicitly.
- It doesn't verify low-stakes claims — that would waste budget on things that don't cause failures.

The goal is **calibration**: when the skill says `high`, it should be right; when it says `low`, it should be flagging genuine uncertainty. Per-dimension scoring + adversarial verification + schemas are how it earns that calibration.
