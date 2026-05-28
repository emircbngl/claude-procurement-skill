# Decision frameworks

The decision-method choice scales with Kraljic class. Use the lightest framework that does the job — over-engineering routine purchases is wasted effort; under-engineering strategic purchases is wasted money.

## Method by class

| Kraljic class | Method |
|---|---|
| Routine | Quick weighted score |
| Leverage | Full weighted scoring matrix |
| Bottleneck | Risk-adjusted weighted score |
| Strategic | AHP **or** Pugh matrix |

## 1. Weighted scoring matrix (leverage / routine)

The default. Score each candidate 0–5 per dimension; multiply by dimension weight; sum.

| Dimension | Weight | Cand A | Cand B | Cand C |
|---|---|---|---|---|
| Functional fit | 5 | 4 | 5 | 3 |
| Reliability | 4 | 5 | 3 | 4 |
| Repairability | 3 | 3 | 4 | 5 |
| TCO (lower = better) | 5 | 4 | 5 | 2 |
| Vendor risk (lower = better) | 4 | 5 | 4 | 3 |
| Upgrade path | 3 | 3 | 4 | 2 |
| ESG (optional) | 2 | 3 | 3 | 4 |
| **Weighted total** | | 95 | 97 | 71 |

Weights come from step 4 requirements doc (must-haves are already gating; weights apply to nice-to-haves and universal dimensions). Surface ties or sub-5%-margin results to the user — these are not high-confidence winners.

**Routine variant**: 3 dimensions max (price, functional fit, vendor reliability), no documentation overhead.

## 2. Risk-adjusted weighted score (bottleneck)

Same matrix as above, but multiply each total by a **risk factor** = `1 − supply_risk_score / 10`. Penalizes high-supply-risk candidates explicitly.

Additionally: surface "spare-parts plan" prominently in the report — bottleneck candidates always need a stocking plan.

## 3. AHP — Analytic Hierarchy Process (strategic)

Saaty's pairwise-comparison method. More rigorous than flat weights; consistency-checks the user's judgments.

### Steps

1. **List criteria** — typically 4–7 dimensions matter (don't try to compare 11).
2. **Pairwise compare criteria** — for each pair (A vs B), ask user / infer: "is A more important than B, by how much (1–9)?". Build the comparison matrix.
3. **Compute weights** — derive each criterion's normalized weight from the matrix's principal eigenvector. (Approximation: row geometric mean, then normalize.)
4. **Pairwise compare candidates per criterion** — for each criterion, compare each pair of candidates.
5. **Compute scores** — multiply criterion weights × candidate scores per criterion → final ranking.
6. **Consistency ratio** — compute CR; if > 0.10, judgments are inconsistent and need revisiting. Report the CR.

Use AHP when the user is making a strategic-class purchase AND has time for a few rounds of pairwise judgment. Skip if user wants speed — Pugh is faster.

### When to choose AHP

- User explicitly requests rigor
- ≥4 viable candidates
- Criteria importance is itself contested (e.g., user oscillating between "cheap" and "reliable" priorities)

## 4. Pugh matrix (strategic, upgrading from incumbent)

Concept-vs-datum scoring. Pick the user's current product as the **datum**; every candidate is scored relative to it: +, 0, or − on each criterion.

| Criterion | Datum (current) | Cand A | Cand B | Cand C |
|---|---|---|---|---|
| Power | 0 | + | + | 0 |
| Quietness | 0 | + | − | + |
| Price | 0 | − | − | 0 |
| Reliability | 0 | 0 | + | + |
| Sum of + | — | 2 | 2 | 2 |
| Sum of − | — | 1 | 2 | 0 |
| Net | — | +1 | 0 | +2 |

### When to choose Pugh

- Upgrading from a specific existing product (user has a clear "current" to compare against)
- Need a quick visual comparison without numeric weights
- User reasoning in qualitative terms ("better camera, worse battery")

## Choosing the method

If user is strategic and upgrading → Pugh.
If user is strategic and new purchase → AHP.
If user is leverage → weighted scoring matrix.
If user is bottleneck → risk-adjusted weighted.
If user is routine → quick weighted (top 3 dimensions only).

If user explicitly requests a method, use that.

## Output

The chosen method's matrix goes into the report's "Decision matrix" section. Always name the method used. For AHP, include the consistency ratio. For all methods, surface ties or close calls (< 5% margin) explicitly.

## Pre-mortem and devil's advocate

These are handled in step 8.5 — see `pre-commit-checks.md`. They are not decision methods; they stress-test the chosen decision.
