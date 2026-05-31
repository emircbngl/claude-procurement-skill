# Schemas

Canonical, normative shapes for everything the skill writes to disk. This skill runs in a single agent context (no enforced StructuredOutput tool), so "schema" here means a **precise spec the model self-validates against before writing**. Drift between runs is the enemy; this file is the anti-drift contract.

Three artifacts are schema-governed:
1. **Domain pack** (`references/domain-<slug>.md`) — including the per-dimension confidence map
2. **Research report** (`tasks/research/<slug>.md`) — the decision memo
3. **In-run objects** — verification verdict, per-candidate price object, compatibility-matrix row

Before writing any artifact, run the **self-validation checklist** at the bottom of this file.

---

## 1. Domain pack schema

### Frontmatter (YAML)

| Field | Type | Required | Notes |
|---|---|---|---|
| `status` | enum: `auto-generated` \| `human-reviewed` | yes | `auto-generated` until a human reviews and promotes |
| `derived-from-query` | string | auto only | verbatim user query that triggered creation |
| `first-run-date` | date `YYYY-MM-DD` | auto only | |
| `last-updated` | date `YYYY-MM-DD` | yes | bump on every refinement run |
| `run-count` | int ≥ 1 | yes | increment per run touching this pack |
| `confidence` | enum: `low` \| `medium` \| `high` | yes | **aggregate** — computed from `dimension-confidence` per §3 |
| `dimension-confidence` | map<dimension, enum> | yes (auto); optional (hand) | per-dimension scores; see §3. Absent on a hand-authored pack ⇒ treat all dimensions as `high`. |
| `deep-search-completed` | bool | auto only | `true` if all 8 categories ran; `false` if derivation degraded |
| `acquired-via` | enum: `inline` \| `deep-research-delegation` | auto only | which discovery path (Path A/B in `domain-unknown.md`) |
| `verification` | map<claim-or-dimension, verdict> | auto only | adversarial-verify results; see §4 |
| `search-categories-covered` | list<dimension-key> | auto only | which of the 8 ran |
| `sources-used` | list<url> | auto only | 15–25 URLs from deep search |
| `human-reviewed` | bool | yes | `true` only after explicit human promotion |

### Dimension keys (the 8 deep-search categories)

```
buying-guides           # research dimensions / spec axes
standards-regulators     # standards + certification marks
brand-landscape          # brands per region + distribution
pitfalls-failure-modes   # common failures
repairability-eol        # repair + end-of-life
compliance-recall         # safety certs + recall registries
tco-drivers              # consumables, energy, maintenance, lifespan
long-term-reviews        # 2yr+ ownership signals
```

Plus one synthetic high-stakes dimension scored separately:
```
compatibility            # interop rules (subset of standards, but scored on its own — highest stakes)
```

### Body sections (fixed order, all required; mark `N/A — <reason>` when empty)

```markdown
---
<frontmatter per table above>
---

# Domain: <Category Name> (auto-generated, deep search)

> <banner — ℹ for medium/high confidence, ⚠ for low; see self-feeding.md>

## Research dimensions
- functional_specs: [...]
- quality_signals: [...]
- economic: [...]
- usage_fit: [...]

## Required user inputs (overrides universal)
- [...]

## Standards & compatibility axes
| Axis | Values | Compat rule | Verified? |
|------|--------|-------------|-----------|

## Common pitfalls / failure modes
- [...]

## Regional notes
[...]

## B2B variant
[...]

## Trusted sources for web fallback
[...]

## Dimension confidence
| Dimension | Confidence | Basis |
|-----------|-----------|-------|
<one row per dimension key, mirrors frontmatter dimension-confidence>
```

The "Verified?" column on the standards table and the "Dimension confidence" body section are **new in v1.3** — they make the per-dimension scoring and adversarial-verify visible to a human reader, not just machine-readable in frontmatter.

---

## 2. Research report schema

The full 17-section structure lives in `references/report-template.md` — that file is the canonical report schema. This section only adds the **v1.3 typing rules** layered on top:

- Header line MUST include `Pack confidence: <aggregate>` when the run used an auto-generated pack, so the reader knows the criteria-side data's trust level.
- Section 6 (Compliance & validation) MUST carry a **verification status** per high-stakes claim (see §4).
- Section 6 compatibility matrix rows MUST follow the row schema in §6 below.
- Section 7 price rows MUST follow the price-object schema in §5 below.
- A claim whose verification verdict is `refuted` or `unverified` MUST NOT appear as a settled fact — render it with an explicit caveat and surface it in Section 16 (Open questions).

---

## 3. Per-dimension confidence model (quality scoring)

Each dimension gets one of three scores. **One blanket pack confidence hides that, e.g., standards data is rock-solid while long-term-review data is thin.** Per-dimension scoring fixes that.

### Scoring rubric (per dimension)

| Score | Criteria |
|---|---|
| `high` | ≥2 independent authoritative sources **AND** (for high-stakes dimensions) adversarial-verify returned `verified` |
| `medium` | ≥2 sources, OR 1 authoritative source (manufacturer / standards body / regulator), not adversarially refuted |
| `low` | only 1 weak source (forum / single blog), source conflict unresolved, not found, or adversarial-verify returned `refuted`/`unverified` |

Authoritative source = manufacturer datasheet, standards body (ISO/IEC/IEEE/EN), regulator (CPSC/RAPEX/MHRA/etc.), or a top-tier independent lab (RTINGS, Consumer Reports, iFixit). Forums/Reddit/single blogs are corroborating, not authoritative on their own.

### Aggregate confidence (computed, not guessed)

The frontmatter `confidence` field is **derived** from the per-dimension map using a weighted floor rule that protects against high-stakes weakness:

```
HIGH_STAKES = {compatibility, compliance-recall, standards-regulators}

aggregate =
  if any HIGH_STAKES dimension is `low`          -> low
  elif ≥3 dimensions are `low`                    -> low
  elif all HIGH_STAKES dimensions are `high`
       and ≥6 of 9 dimensions are `high`          -> high
  else                                            -> medium
```

Rationale: a pack can't be "high" overall if any of its safety/interop dimensions is weak — that's exactly where a wrong call causes a "won't fit" or "isn't legal" failure. And one thin review dimension shouldn't drag an otherwise-solid pack to `low`.

Hand-authored packs with no `dimension-confidence` map are treated as `high` across all dimensions (human-curated). They don't need retrofitting.

---

## 4. Verification verdict schema

Produced by `references/adversarial-verify.md`. One verdict per verified claim or dimension.

| Field | Type | Notes |
|---|---|---|
| `claim` | string | the specific assertion under test (e.g., "Shimano 11sp shifter cannot pull SRAM 12sp ratio") |
| `dimension` | dimension-key | which dimension this claim belongs to |
| `stakes` | enum: `high` \| `medium` \| `low` | compat + compliance + safety = high |
| `verdict` | enum: `verified` \| `partially-verified` \| `refuted` \| `unverified` | |
| `confidence` | enum: `low` \| `medium` \| `high` | verifier's confidence in its own verdict |
| `sources` | list<url> | the **independent** sources the verifier used (not the ones the original claim used) |
| `note` | string | what the refutation attempt found |

### Verdict → dimension-confidence interaction

- `verified` (high confidence) → dimension may be `high`
- `partially-verified` → dimension capped at `medium`
- `refuted` → the specific claim is removed or corrected; dimension dropped to `low`; correction logged
- `unverified` (couldn't find independent sources) → dimension capped at `low` for high-stakes, `medium` otherwise

---

## 5. Per-candidate price object schema

Emitted by step 6 (price discovery). One per surviving candidate. Already sketched in `price-discovery.md`; formalized here:

| Field | Type | Required | Notes |
|---|---|---|---|
| `sku` | string | yes | |
| `region` | string | yes | |
| `currency` | ISO 4217 code | yes | |
| `msrp` | number | yes | |
| `current_low` | number + source | yes | live, never cached |
| `12mo_low` | number \| `null` | no | from price-history tool if available |
| `used_median` | number \| `null` | no | eBay sold etc. |
| `fair_band` | `{aspirational, target, walk_away}` | yes | all three numbers |
| `red_flags` | list<string> | yes | empty list if none |
| `best_channel` | string | yes | retailer + authorized status |
| `return_policy` | string | yes | window + restocking + shipping |
| `authorized_dealer` | bool | yes | |

**Freshness rule**: every numeric field here is live per query — none of it is ever written to a domain pack.

---

## 6. Compatibility-matrix row schema

| Field | Type | Notes |
|---|---|---|
| `existing_part` | string | from step 3 context |
| `candidate` | string | from step 5 |
| `standard_axis` | string | the interop axis being tested |
| `verdict` | enum: `compatible` \| `adapter` \| `blocker` | ✓ / ⚠ / ✗ |
| `verified` | enum: `verified` \| `unverified` \| `refuted` | for strategic-class, adversarial-verify each row |
| `sources` | list<url> | ≥2 for any compat claim |
| `note` | string | adapter SKU+cost if `adapter`; reason if `blocker` |

---

## Self-validation checklist (run before writing each artifact)

**Domain pack**:
- [ ] All frontmatter required fields present and correctly typed
- [ ] `dimension-confidence` map has all 9 dimension keys
- [ ] `confidence` aggregate matches the computed value from §3 (don't hand-pick it)
- [ ] Every high-stakes claim has a `verification` entry
- [ ] Standards table has the "Verified?" column populated
- [ ] "Dimension confidence" body section mirrors the frontmatter map
- [ ] `sources-used` has ≥2 URLs per high-stakes dimension

**Research report**:
- [ ] Header carries `Pack confidence` when an auto-generated pack was used
- [ ] No `refuted`/`unverified` high-stakes claim is stated as settled fact
- [ ] Compatibility rows follow §6; price rows follow §5
- [ ] Sources section satisfies the citation-discipline rule (≥2 standards/compat, ≥1 opinion, ≥1 aggregator + ≥1 seller for price)

**On any mismatch**: fix before writing. The schema is a contract, not a suggestion.
