# Requirements framework

Convert vague intent ("I want a good bike") into a structured, weighted requirements document. This is the spine the rest of the workflow scores against.

## The three buckets

### Must-haves
Binary, non-negotiable. A candidate that misses a must-have is **disqualified** — no scoring required.

Examples:
- "Must be a gravel bike with 40mm+ tire clearance"
- "Must support DDR5 RAM"
- "Must come with manufacturer warranty valid in user's region"
- "Must arrive within 2 weeks"

### Nice-to-haves
Weighted on a 1–5 scale. A candidate accumulates score from nice-to-haves it hits.

| Weight | Meaning |
|---|---|
| 5 | Strong preference; willing to pay a premium |
| 4 | Clear preference |
| 3 | Moderate preference |
| 2 | Mild preference |
| 1 | Nice if free, not worth paying for |

Examples:
- "Tubeless-ready wheels" (weight 4)
- "Quiet operation under load" (weight 5)
- "Front-facing camera" (weight 2)

### Dealbreakers
Like must-haves but stated in the negative. A candidate with a dealbreaker is **auto-disqualified**.

Examples:
- "No subscription model"
- "No proprietary charger"
- "No fragrance"
- "Not from <brand X>"

## Required inputs (always captured in step 4)

- **Region + currency** (no default — ask each run)
- **Budget envelope** with currency and tightness ("hard cap" vs "willing to stretch 20%")
- **Use case** — primary use, secondary use, exclusion ("not for X")
- **Timeline** — when needed (affects discount-window strategy)
- **TCO horizon** — default 3 years, can be 5 or other
- **Audience level** — casual or pro (controls report density)
- **Kraljic-derived importance** — confirms / overrides step 1.5 classification
- **ESG weighting** — optional; if user signals interest, add ESG as a scoring dimension
- **Cooling-off threshold** — household rule for when to enforce a pause (default: above 10% of monthly income OR above strategic Kraljic class)

## Captured but optional

- Brand preferences / exclusions
- Channel preferences (only authorized retailer? open to refurbished? open to used?)
- Aesthetic constraints (color, size, design language)
- Compatibility constraints from existing gear (auto-extracted in step 3)

## How to ask via AskUserQuestion

Batch into a single call with multi-select where possible:

- Q1: "What's the budget envelope and currency?" (text or option ranges)
- Q2: "Primary use case + must-haves + dealbreakers?" (text)
- Q3: "Audience level?" (casual / pro)
- Q4: "TCO horizon?" (3yr / 5yr / other)

Skip any question where step 3 auto-extraction already captured the answer.

## Output of step 4

A markdown table written into the report's "Requirements" section:

| Type | Item | Weight | Source |
|------|------|--------|--------|
| Must-have | Frame fits 40mm+ tires | — | user |
| Must-have | Warranty valid in user's region | — | inferred from region answer |
| Nice-to-have | Tubeless-ready | 4 | user |
| Nice-to-have | Under 9.5kg | 3 | user |
| Dealbreaker | No press-fit BB | — | user (prior bad experience) |

Plus budget envelope, timeline, use case, TCO horizon, ESG weighting, cooling-off threshold all stored as named fields.
