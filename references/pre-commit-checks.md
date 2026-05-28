# Pre-commit checks

Even a well-scored candidate should survive two stress tests before the user commits: a **pre-mortem** (imagined-failure analysis) and a **cooling-off pause** (forced wait window above a threshold).

## Pre-mortem (Klein's prospective hindsight)

After the decision matrix yields a primary pick, run this thought experiment:

> "Imagine it's 12 months from now. You bought this. You regret it. List the top reasons."

Research shows prospective hindsight improves failure-mode identification by ~30% over forward-only analysis.

### Process

1. **Take the primary pick** as decided.
2. **Imagine the regret state** vividly — what specifically happened?
3. **List ≥3 regret scenarios** drawn from:
   - Compliance failures that slipped through
   - TCO blowouts (consumables, energy, repairs exceeded estimate)
   - Vendor risk realized (warranty refused, brand discontinued, parts unobtainable)
   - Use-case mismatch (it does what's advertised but the user's use case shifted)
   - Compatibility break-downs (an ecosystem change broke interop)
   - Better alternative emerged (model refresh days after purchase)
   - Counterfeit / gray-market consequence
   - Ergonomic / aesthetic / weight regret (especially for daily-use items)
4. **For each scenario, write a mitigation** — what could the user do now to prevent or contain it?

### Output format

| Scenario | Why it would matter | Mitigation |
|---|---|---|
| Brand pulled out of user's region within 2 yrs, warranty became a paperweight | High since this is a strategic purchase | Verify regional distributor contract length; budget for self-repair fund |
| Battery cells degraded faster than spec | Costly replacement | Stock replacement cells now while still available |
| Better tier emerged 6mo later for similar price | Buyer's regret, lost optionality | Pick a model with strong resale value; eBay-sold-median check |

## Devil's advocate / inversion

A second-pass check distinct from pre-mortem:

> "What would a smart skeptic say about this pick? What weakness are we glossing over?"

Look for:
- Confirmation bias in candidate selection (did we filter to the answer we wanted?)
- Source quality bias (are we leaning on one review site disproportionately?)
- Recency bias (favoring a brand because of recent positive reviews while ignoring long-term reliability data)
- Sunk-cost from prior research (committing because we've already done the work)

Document the strongest counter-argument and whether it survives.

## Cooling-off pause

For meaningful purchases, force a sleep-on-it window before the recommendation becomes a "buy now". Threshold rule:

| Condition | Pause |
|---|---|
| Kraljic = strategic | 72h mandatory |
| Spend > 25% of monthly income | 72h mandatory |
| Spend > 10% of monthly income | 24h recommended |
| Kraljic = leverage AND spend ≤ 10% monthly income | None |
| Kraljic = routine | None |

(Monthly income is ideally captured in step 4 setup as part of "cooling-off threshold"; if not captured, default to an absolute currency threshold from the requirements doc or skip.)

### Why

FTC's 3-business-day cooling-off rule applies to specific door-to-door and home contracts but exists for a reason — large-purchase regret is real and predictable. A 24–72h pause costs nothing and prevents purchase regret on a meaningful fraction of strategic-class buys.

### How

The report **does not** auto-execute the purchase (the skill never does). It produces an explicit instruction:

> **Re-confirm before purchase**: Pause until <YYYY-MM-DD + 72h>. Re-read this report after the pause. If your thinking has changed, re-run the skill or update requirements. Otherwise, proceed to the channel link above.

## Output

A "Pre-mortem + devil's advocate" section in the report containing:
- ≥3 regret scenarios + mitigations
- One devil's-advocate counter-argument + verdict
- Cooling-off recommendation with explicit date (if applicable)
