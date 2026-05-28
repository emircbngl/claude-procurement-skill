# Report template

Every research run produces a file at `tasks/research/<slug>.md` using the structure below. Fill in every section; mark `N/A` (with reason) when a section doesn't apply (e.g., compatibility matrix for a new-purchase intent).

If `tasks/research/<slug>.md` already exists, **append a new `## Re-evaluation <YYYY-MM-DD>` section** containing only what changed. Do not overwrite.

---

```markdown
# <Product / Research Question>
> Generated: <date> · Region: <region> · Budget: <range+currency> · Use case: <summary> · Audience: <casual|pro> · Intent: <new-purchase|upgrade|comparison|compat-check> · Kraljic class: <routine|leverage|bottleneck|strategic>

## Executive summary (Casual TL;DR)
- **Verdict**: <one-line recommendation + target price + best channel>
- **Why**: <one sentence>
- **Main caveat**: <one sentence>
- **Estimated all-in cost (TCO over <N>yr)**: <amount>
- **Walk-away price**: <amount> — don't pay above this

## Procurement detail

### 1. Context (auto-extracted)
What was pulled from working-directory files: existing gear, prior quotes, prior research files, must-haves/dealbreakers found in user's notes. List the source file for each.

### 2. Purchase classification (Kraljic)
- Class: <routine|leverage|bottleneck|strategic>
- Rationale: <supply risk + importance assessment>
- Rigor applied: <which steps ran in full vs shortcut>

### 3. Option-space check
- Make-vs-buy verdict: <buy | make | not applicable> + reasoning
- Build-vs-buy-vs-rent-vs-subscribe verdict: <purchase | rent | subscribe | borrow | N/A> + reasoning
- If non-purchase wins → recommendation states this and the rest of the report is abbreviated.

### 4. Requirements
| Type | Item | Weight | Source |
|------|------|--------|--------|
| Must-have | <item> | — | user/inferred |
| Must-have | <item> | — | user/inferred |
| Nice-to-have | <item> | 1–5 | user |
| Dealbreaker | <item> | — | user |

- Budget envelope: <range+currency, tight or stretchable>
- Timeline: <when needed>
- TCO horizon: <N years>
- ESG weighting: <on/off>

### 5. Candidate slate (RFI output)
| # | Name | MSRP | Key specs (3–5) | Source link |
|---|------|------|-----------------|-------------|
| 1 | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... |
| 3 | ... | ... | ... | ... |

### 6. Compliance & validation
**Per candidate**:
- Certifications: CE / FCC / UL / RoHS / CCC / Energy Star / EPREL — pass/fail/missing
- Authorized-dealer verification: ✓ / ⚠ / ✗
- Return policy: window / restocking fee / shipping cost
- IoT cyber & privacy (smart devices only): rating + firmware cadence
- Counterfeit risk: low / medium / high

**Compatibility matrix** (only if upgrade or existing-ecosystem):

| Existing part | Candidate | Standard | Compatible? | Notes |
|---|---|---|---|---|
| ... | ... | ... | ✓ / ⚠ / ✗ | source |

**Disqualified candidates** + reason.

### 7. Price discovery (RFQ output)
Fair-price band per candidate:

| Candidate | MSRP | Current low | 12-mo low | Used median | Aspirational | Target | Walk-away | Best channel | Red flags |
|-----------|------|-------------|-----------|-------------|--------------|--------|-----------|--------------|-----------|
| ... | ... | ... | ... | ... | ... | ... | ... | ... | ... |

**Top-3 sellers per candidate** (with link + listed price + net-of-discount price). **Cross-border note + destination-region landed-cost math** when applicable.

### 8. Decision matrix
Method: **<weighted-score | AHP | Pugh>** (chosen because <Kraljic class + rationale>).

| Dimension | Weight | Candidate A | Candidate B | Candidate C |
|-----------|--------|-------------|-------------|-------------|
| Functional fit | ... | x/5 | x/5 | x/5 |
| Reliability | ... | | | |
| Repairability | ... | | | |
| TCO (lower=better) | ... | | | |
| Vendor risk (lower=better) | ... | | | |
| Upgrade path | ... | | | |
| ESG (optional) | ... | | | |
| **Weighted total** | | | | |

For AHP: include the consistency ratio.

### 9. Landed-cost TCO (over <N>-year horizon)
| Cost line | Cand A | Cand B | Cand C |
|---|---|---|---|
| Purchase (target price) | | | |
| Accessories | | | |
| Consumables | | | |
| Energy | | | |
| Maintenance / service | | | |
| Expected repairs | | | |
| Insurance / extended warranty net of CC | | | |
| Financing cost (0% taksit / BNPL) | | | |
| Rebates / CC bonuses (−) | | | |
| Resale value at horizon (−) | | | |
| **Net TCO** | | | |
| Opportunity cost note | | | |

### 10. Risk assessment
**FMEA-lite (top-3 per candidate)**:

| Candidate | Failure mode | S | O | D | RPN | Mitigation |
|---|---|---|---|---|---|---|
| ... | ... | | | | | |

**Single-source-of-failure / ecosystem lock-in**: <per candidate>

**Vendor risk profile**: warranty regional coverage, parts availability, service network in user's region, EOL signals, recall history, supply-chain notes.

### 11. Negotiation playbook
- **Best channel + price**: <retailer> at <target price> — <URL>
- **Levers to pull**: <price match / bulk / cash discount / bundle / etc.>
- **Discount calendar**: next 2 likely windows + estimated depth
- **Substitutes** (if waiting / over budget): <list with their fair-price targets>

### 12. Recommendation
- **Primary pick**: <name> — buy at <target price> from <channel>. Why: <tied back to decision matrix + TCO + fair-price band>.
- **Runner-up**: <name>. Would beat primary when: <condition>.
- **Do not buy**: <eliminated candidates> — reasons: <compliance fail / over budget / unacceptable risk / overpriced vs fair band>.

### 13. Pre-mortem + devil's advocate
**Top regret scenarios + mitigations**:
1. <scenario> → <mitigation>
2. <scenario> → <mitigation>
3. <scenario> → <mitigation>

**Devil's advocate**: <strongest counter-argument + verdict on whether it survives>

### 14. Cooling-off recommendation
- Applies: <yes / no>
- If yes: **Re-confirm before purchase after <YYYY-MM-DD + 24h/72h>**. Re-read this report; if reasoning still holds, proceed.

### 15. Lifecycle plan
**Day 0 — Receive & inspect**:
- Quantity, damage, spec, function, counterfeit re-check

**Day +1 to +30 — Register & secure**:
- Warranty registration deadline: <date+30d> at <URL>
- Day-1 firmware update + change default credentials (if smart device)
- Insurance rider (if high-value): add to policy
- Documentation archival: store at <suggested path>

**Ongoing — Recall + maintenance**:
- Recall sources: <urls>
- Maintenance calendar:
  - <task> every <interval>
  - ...
- Spare parts to stock: <list with sources + prices>

**End-of-life** (when replacing):
- Resale target: ~<amount> via <channel> at age <N>yr (eBay sold-median)
- Trade-in alternative: <OEM program> at ~<amount>
- Recycle route: <regional e-waste program / OEM take-back URL>
- Data wipe steps (smart devices): <list>

### 16. Open questions — verify before purchase
- <pre-purchase check 1>
- <pre-purchase check 2>
- ...

### 17. Sources
1. <URL> — <one-line note on what this source supports>
2. <URL> — ...

(Standards/compat ≥2 sources; opinions ≥1; price data ≥1 aggregator + ≥1 primary seller.)
```

---

## Audience-density rules

Both `casual` and `audience=pro` produce the same Executive summary (top). The Procurement detail sections compress or expand:

**`audience=casual`**: each subsection is 1–3 sentences, candidate slate of 2–3, TCO single bottom-line per candidate, risk = top-3 bullets only, fewer sources cited.

**`audience=pro`**: full tables, 3–5 candidates, all TCO line items, full FMEA per candidate, longer source list, explicit method matrix.

Either way: the analysis runs in full. Only reporting density changes.

## Slug rules

- `<category>-<keyword>`: kebab-case, lowercase.
- Examples: `bicycle-gravel-upgrade`, `pc-rtx-5070-build`, `headphones-anc-sony-bose`, `espresso-machine-prosumer-home`.
- If file exists: append `## Re-evaluation <YYYY-MM-DD>` section, do NOT overwrite.
- Auto-create `tasks/research/` if missing.
