# Adversarial verification

The cheapest way to be wrong in procurement is to state a plausible-but-false compatibility or compliance claim with confidence. "This wheel fits your frame" / "This is legal to sell in your region" / "This SaaS is SOC 2 compliant" — each, if wrong, costs the user real money or a failed audit. Adversarial verification exists to kill those before they reach the report.

The principle: **a claim hasn't earned its place until an independent skeptic has tried to refute it and failed.** This is the "have specialized reviewers re-examine the findings" idea, implemented in a single-agent skill via two routes (same A/B philosophy as deep search).

## What gets verified (not everything — that's too expensive)

Verification budget is spent on **high-stakes claims only**:

| Stakes | What | Verified? |
|---|---|---|
| **High** | Compatibility / interop rules; mandatory certification marks per region; safety-critical claims; recall status; B2B compliance attestations (SOC 2 / DPA / ISO) | **Always** |
| Medium | Spec-dimension definitions; brand-reliability signals; TCO driver magnitudes | Strategic-class only |
| Low | Review opinions; aesthetic notes; nice-to-have feature presence | Never (not worth the budget) |

So: a routine USB-cable purchase gets little/no verification. A strategic CPAP or a B2B SaaS contract gets every high-stakes claim refuted-tested.

## When it runs

1. **Pack creation** (in `domain-unknown.md`, after the 8-category deep search): verify the high-stakes dimensions — `compatibility`, `standards-regulators`, `compliance-recall` — before saving the pack. Their verdicts set those dimensions' confidence (per `schemas.md` §3–4).
2. **Step 5 compatibility matrix** (strategic-class only): verify each matrix row — both `blocker` and `compatible` verdicts. A wrong `compatible` makes the user buy something that doesn't fit; a wrong `blocker` makes them skip a valid option. Both directions matter.
3. **Step 6 / B2B compliance** (strategic-class B2B): verify vendor compliance attestations against primary sources (the vendor's actual SOC 2 report date, the actual DPA, the regulator's actual registry) — not the vendor's marketing page.
4. **On demand**: user says "double-check the compatibility" / "verify this is legal here" → run a targeted verification regardless of class.

## How it runs — two routes

### Route A — Delegate to `deep-research` (preferred when available)

If the `deep-research` skill is registered, delegate verification to it with an explicitly **refutation-framed** prompt. A fresh delegation means fresh sources and no anchoring on the original claim's evidence.

```
Skill(skill="deep-research", args="<refutation prompt below>")
```

Refutation prompt template:

```
Try to REFUTE each of the following claims. For each, search for independent
evidence that the claim is FALSE or conditional. Do not look for confirming
evidence first — actively seek disconfirmation. Use sources independent of
those the claim was originally based on.

Claims:
1. <claim 1>
2. <claim 2>
...

For each claim return: verdict (verified / partially-verified / refuted /
unverified), your confidence (low/medium/high), the independent sources you
used, and a one-line note on what you found. Default to "unverified" if you
cannot find independent corroboration — do NOT default to "verified".
```

### Route B — Inline skeptic pass (fallback)

When `deep-research` is not available, run the skeptic pass inline. For each high-stakes claim:

1. **Reframe as a refutation question**: not "is the Shimano 11sp shifter incompatible with SRAM 12sp?" but "find evidence that a Shimano 11sp shifter CAN drive a SRAM 12sp cassette." Searching for the opposite of the claim surfaces edge cases and exceptions a confirming search hides.
2. **Require independent sources**: ≥2 sources that are NOT the ones the original claim cited. If the claim came from a forum, the verification needs a manufacturer chart or standards doc.
3. **Issue the searches parallel-batched** (multiple WebSearch/WebFetch per turn).
4. **Score the verdict** per `schemas.md` §4.

Bias rule for both routes: **default to `unverified`, not `verified`.** A claim that can't be independently corroborated is not "probably true" — it's unverified, and it's flagged as such. Optimism here is how false claims survive.

## Multi-lens verification (strategic-class, highest stakes)

For the highest-stakes claims on strategic purchases (e.g., "this medical device is the right class and reimbursable", "this frame standard fits"), use **diverse lenses** rather than one repeated check — each lens catches a different failure mode:

- **Correctness lens**: is the claim factually true per primary sources?
- **Conditionality lens**: is it true *always*, or only under conditions the user may not meet? (e.g., "compatible — but only with a firmware update", "legal — but only with a prescription")
- **Recency lens**: was it true but recently changed? (standard superseded, regulation updated, model revised)
- **Region lens**: true in the source's region but not the user's?

A claim survives only if it passes all relevant lenses. The conditionality and region lenses catch the most expensive procurement mistakes — the "technically true but not for you" trap.

## Output

Verification produces a set of verdict objects (per `schemas.md` §4). These:

1. **Feed dimension-confidence** at pack creation (verified→high eligible; refuted/unverified→low).
2. **Annotate the compatibility matrix** in step 5 (the `verified` column per `schemas.md` §6).
3. **Surface in the report**: any `refuted` or `unverified` high-stakes claim appears in Section 16 (Open questions — verify before purchase) with the explicit caveat. Never bury a failed verification.
4. **Get logged in the pack**: the `verification` frontmatter map records what was tested and the result, so a future run (or human reviewer) sees the verification history.

## Cost discipline

- Verification is **not** a second full research pass. It targets the high-stakes subset only.
- Pack-creation verification: ~3–8 extra calls (the 3 high-stakes dimensions).
- Strategic compat-matrix verification: ~2 calls per matrix row.
- Routine/leverage purchases: little to none.
- If web is unreachable, verification verdicts are all `unverified` and the report says so plainly — better an honest "couldn't verify" than a fake "verified".

## Why this matters (the failure it prevents)

Without adversarial verification, the skill's confidence is only as good as its first source. A single authoritative-looking blog that's subtly wrong about a BB standard, a lens mount, a DDR generation, or a SOC 2 status propagates into the pack, then into every future run on that domain, then into a purchase. Adversarial verification is the circuit breaker: high-stakes claims must survive an independent attempt to prove them false before they're trusted.
