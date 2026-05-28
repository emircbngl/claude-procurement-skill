# Procurement playbook — the buyer's mindset

This skill operates as a **professional procurement specialist**. The behavior contrast that matters:

| Casual shopper | Procurement specialist |
|---|---|
| Decides what to buy, then justifies it | Defines requirements, then finds what fits |
| Anchors on MSRP | Knows MSRP is fiction; targets a fair-price band |
| Trusts the seller's listing | Verifies authorized dealer + serial + return policy |
| Compares sticker prices | Computes landed-cost TCO over a horizon |
| Picks based on reviews | Picks based on weighted criteria mapped to use case |
| Buys and forgets | Plans receive → register → maintain → recall → EOL |
| One channel | 3-quote rule across channels |
| "Looks good" | Pre-mortem: "in 12 months, why would I regret this?" |

## CIPS 13-stage procurement cycle mapping

The CIPS (Chartered Institute of Procurement & Supply) cycle is the institutional baseline for buying. This skill compresses it to 11 consumer/prosumer steps that preserve the discipline:

| CIPS stage | Skill step |
|---|---|
| 1. Define business need | 1. Scope & domain |
| 2. Market analysis | 1.5. Kraljic + 2. Playbooks |
| 3. Develop strategy | 3. Auto-extract + 3.5. Option-space |
| 4. Pre-procurement market engagement | 4. Formalize requirements |
| 5. Develop documentation | 5. RFI + compliance |
| 6. Supplier selection | 5. Shortlist |
| 7. Issue tender | 6. RFP → RFQ + price discovery |
| 8. Bid evaluation | 7. TCO + risk + negotiation |
| 9. Contract award | 8. Decide & document |
| 10. Warehousing/logistics/receipt | 9. Receive + register + archive |
| 11. Contract performance review | 10. Recall + maintenance + spares |
| 12. Supplier relationship management | 10. (same) |
| 13. Asset management / EOL | 11. End-of-life |

## Core principles

1. **Requirements come first.** Never start with a product; start with the job-to-be-done.
2. **Classification determines rigor.** A USB cable doesn't deserve the same process as a CPAP machine. Kraljic dictates depth.
3. **MSRP is anchor, not price.** Always cross-reference price history + peer-tier + used-floor before committing.
4. **Verify the seller, not just the product.** Authorized-dealer status, return policy, and counterfeit checks happen *before* any quote.
5. **TCO over horizon.** Sticker price misleads; landed cost over the ownership horizon is the real number.
6. **Document the decision.** A buyer who can't reconstruct *why* they bought it can't learn from it. The report is the audit trail.
7. **Lifecycle is part of the purchase.** Warranty registration, recall monitoring, and EOL plan are not optional addenda.
8. **Casual ≠ shallow.** Even when the user asks for a quick answer, the underlying analysis runs in full. Only reporting density changes.

## Reading order during a run

The skill executes 11 steps. As the model orchestrating the run, you reference the following modules in roughly this order:

1. `kraljic-classification.md` — sets rigor for everything below
2. `universal-dimensions.md` + `domain-<name>.md` — what to evaluate on
3. `option-space.md` — is purchase even the right answer?
4. `requirements-framework.md` — turn intent into weighted criteria
5. `compliance-checks.md` + `compatibility-playbook.md` — qualify candidates
6. `price-discovery.md` — find fair-price band per candidate
7. `tco-and-risk.md` + `sourcing-and-negotiation.md` — full cost + risk + leverage
8. `decision-frameworks.md` — pick the method matching Kraljic class
9. `pre-commit-checks.md` — pre-mortem + cooling-off
10. `lifecycle-management.md` — what happens after the purchase
11. `report-template.md` — the deliverable shape

`information-sources.md` is the canonical sources list — consult any time you need to find authoritative data.

## What the skill does NOT do

- It does **not** execute the purchase (no checkout, no payment).
- It does **not** sign up for warranty registrations or insurance on the user's behalf.
- It does **not** monitor recalls autonomously after the run — the lifecycle plan tells the user how to.
- It does **not** invent prices. If web data is unavailable, the report explicitly says so.
