# TCO + risk

Run for every candidate that survived steps 5–6. Outputs feed the decision matrix in step 8.

## Landed-cost TCO

Compute over the user's stated horizon (default 3 years). All numbers in user's currency.

### Cost lines

| Line | What goes in |
|---|---|
| **Purchase** | Target price from step 6 fair-price band (not MSRP, not list) |
| **Accessories** | Required accessories the product doesn't come with (cables, mounts, software) |
| **Consumables** | Per-year cost × horizon: ink, filters, beans, chains, batteries, tires |
| **Energy** | Operating wattage × hours used per year × kWh price for user's region × horizon |
| **Maintenance / service** | Scheduled service per year × horizon (oil changes, descaling, bike tune-ups) |
| **Expected repairs** | Estimated probability × cost of one major repair over horizon (use reliability data + brand reputation) |
| **Insurance / extended warranty** | Cost of extended warranty NET of credit-card-provided coverage |
| **Financing cost** | 0% installment plans / BNPL (Klarna, Affirm, Afterpay, Tabby, Tamara, taksit, etc.) — usually free at face value but check late-fee terms and whether unpaid balance accrues interest |
| **Rebates / CC bonuses** | Negative line — manufacturer rebates submitted, CC sign-up bonus pro-rated |
| **Resale value at horizon end** | Negative line — use eBay sold-median for the SKU at age N |

### Net TCO formula

```
Net TCO = Purchase + Accessories + Consumables + Energy + Maintenance
        + Expected_Repairs + Insurance_net + Financing
        − Rebates − Resale_at_horizon
```

### Opportunity cost note

For strategic-class purchases, also note: if instead of spending the purchase amount now the user invested it (high-yield savings, index fund, debt payoff), what would it return over the horizon? This isn't subtracted from TCO but is flagged as context.

## Insurance / extended warranty net of credit-card

Many premium credit cards (Amex Platinum globally, Chase Sapphire / Capital One in US, certain bank-tier cards in EU/UK/MENA/APAC) provide free extended warranty doubling the manufacturer's warranty by 1 year. Before quoting an extended-warranty cost in TCO, check:

1. What does the user's primary card already cover?
2. What's the manufacturer warranty length?
3. What's the extended-warranty product offering?

Net cost = Extended warranty price − (value of overlap with CC coverage). If the CC already covers the extension period, the extended warranty is wasted money.

## FMEA-lite (Failure Mode and Effects Analysis)

For each candidate, list the top 3–5 failure modes. Score each on:

- **Severity** (1–10): how bad if it fails?
- **Occurrence** (1–10): how likely to happen?
- **Detection** (1–10, inverted): how hard to detect before it harms?

**Risk Priority Number (RPN)** = Severity × Occurrence × Detection.

Address the top-3 RPN modes with mitigations: spare parts on hand, monitoring approach, alternate vendor identified.

Example (e-bike battery):
| Failure mode | S | O | D | RPN | Mitigation |
|---|---|---|---|---|---|
| Battery cells degrade below 70% at 18mo | 7 | 8 | 4 | 224 | Battery replacement budgeted in TCO; vendor stocks replacements |
| Controller failure | 9 | 3 | 7 | 189 | Verify controller is replaceable, not soldered |
| Frame crack at battery mount | 10 | 2 | 8 | 160 | Annual visual inspection; warranty covers frame |

## Single-source-of-failure

Identify per candidate:
- **Proprietary battery / charger** — what happens when the brand stops producing it?
- **Cloud-dependent operation** — does the product brick if the vendor's servers go down?
- **Ecosystem lock-in** — HomeKit-only vs Matter, proprietary mounting standard, single-source consumable.
- **Niche connector** — anything that isn't USB-C / standard 3.5mm / etc. is a long-term risk.
- **Sole-source vendor for the category** — only one company makes this; if they pull out, no replacement.

## Vendor / supplier risk profile

Per candidate brand, capture:

| Field | What to check |
|---|---|
| Brand reliability | Consumer Reports, JD Power, owner-satisfaction surveys, recall history |
| Warranty terms | Length, transferable?, regional coverage |
| **In-country warranty coverage** | Does the brand have an official distributor in the user's region? Will gray-market units be honored locally? International / global warranty exists for some brands; many are region-locked. |
| Parts availability | Official channel + third-party; lead time |
| Service network | Authorized service centers in user's region; turnaround time |
| EOL signals | Model just refreshed? Brand pulling out of category? Stocks being cleared? |
| Recall history | Search CPSC SaferProducts.gov, EU RAPEX, brand's own recall page |
| Supply chain stability | Recent shortages, single-region manufacturing dependence, geopolitical risk |
| IoT cyber & privacy | Vendor data practices, firmware cadence, security disclosure process (smart devices only) |

## Output to report

Three sub-sections in the final report:

1. **Landed-cost TCO** — full table with all cost lines per candidate, Net TCO bottom row, opportunity-cost note for strategic class.
2. **Risk assessment** — FMEA-lite top-3 per candidate + single-source-of-failure analysis + vendor risk profile.
3. Combined with `sourcing-and-negotiation.md` output for the **Negotiation playbook** section.
