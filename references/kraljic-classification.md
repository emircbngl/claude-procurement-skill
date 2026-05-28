# Kraljic classification

The Kraljic matrix places a purchase on two axes:

- **Supply risk** (low ↔ high) — how hard is it to replace this if the supplier or product disappears? Single-source, niche, EOL, region-locked, proprietary all raise supply risk.
- **Importance to the user** (low ↔ high) — does failure of this purchase materially affect the user's life, work, or finances?

|  | Low importance | High importance |
|---|---|---|
| **Low supply risk** | Routine | Leverage |
| **High supply risk** | Bottleneck | Strategic |

## Classifying the purchase

Ask (or infer) these to place the purchase:

1. **Spend size relative to user's income** — under 1% of monthly income = low importance signal; over 25% of monthly income = high importance signal.
2. **Substitutability** — many vendors / commodity standard = low supply risk; sole vendor / proprietary = high supply risk.
3. **Operational dependence** — daily-use job-critical = high importance; nice-to-have = low importance.
4. **Reversibility** — can the user return/resell with little loss = lower importance; locked in / consumable / installed = higher importance.

## The four classes and what rigor each gets

### Routine (low risk, low importance)
**Examples**: USB cable, generic SD card, cleaning supplies, replacement chain on a casual bike.

**Skill behavior**:
- Single-channel price scan (no 3-quote rule)
- Skip deep TCO; sticker price + 1-line consumables note
- Skip option-space (purchase is fine)
- Skip pre-mortem
- Skip cooling-off pause
- Minimal lifecycle plan (warranty registration only if explicitly offered)
- Report length: short Executive summary + brief Procurement detail

### Leverage (low risk, high importance)
**Examples**: 4K monitor, camera lens (mass-market mount), midrange headphones, GPU.

**Skill behavior**:
- Full 3-quote rule across channels
- Full price-history + peer-tier benchmark
- Full TCO over 3-year horizon
- Standard weighted-scoring decision matrix
- Standard pre-mortem
- Cooling-off only if over absolute-spend threshold (default ≥ ~10% monthly income)
- Standard lifecycle plan

### Bottleneck (high risk, low importance)
**Examples**: proprietary battery for an aging device, niche spare part, specialty consumable for an obscure product.

**Skill behavior**:
- Supply-stability focus: alternative sources, parts-availability research, EOL signals
- Recommend **stocking spares** before stock runs out
- Lighter TCO (since importance is low)
- Lifecycle plan emphasizes spare-parts cache

### Strategic (high risk, high importance)
**Examples**: e-bike, custom PC build, CPAP machine, professional camera, high-end appliance, mobility scooter.

**Skill behavior**:
- Full 11-step pipeline, no shortcuts
- AHP pairwise comparison **or** Pugh matrix (depending on whether there's an incumbent)
- Full FMEA-lite + single-source-of-failure analysis
- Pre-mortem mandatory with ≥3 regret scenarios
- Cooling-off pause mandatory (24–72h) regardless of spend
- Full lifecycle plan including dated recall-monitoring, maintenance calendar, spare-parts list, EOL resale target

## Edge cases

- **Borderline classification**: when uncertain, climb one quadrant up (more rigor is cheap; insufficient rigor is expensive on strategic purchases).
- **User overrides classification**: respect it. If user says "just give me a quick answer" on a strategic purchase, downgrade to leverage but flag it: "Note: this is a strategic-class purchase; consider running the full process before committing."
- **Compatibility-check intent**: skip classification entirely — that's a different intent, not a procurement run.

## Output of step 1.5

Set internal state: `kraljic_class ∈ {routine, leverage, bottleneck, strategic}` + one-paragraph rationale. Print to report under "Purchase classification" section.
