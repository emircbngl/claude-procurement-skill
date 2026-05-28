# Lifecycle management

The purchase decision is not the end — it's a milestone in a multi-year ownership lifecycle. Steps 9–11 produce a **dated checklist** the user can act on. The skill does not execute these autonomously; it writes them into the report so the user has a single document covering the entire ownership arc.

## Step 9 — Receive + register + archive (day 0 to day 30)

### 9.1 Incoming inspection
Within 24h of receipt:
- **Quantity** — does the shipment include everything in the listing?
- **Damage** — physical inspection, photograph any cosmetic issue immediately (return-claim evidence).
- **Spec match** — model number / SKU on the unit matches what was ordered.
- **Function test** — basic operational test (powers on, makes the sound it should make, scans, prints, rides, etc.).
- **Counterfeit re-check** — hologram / GS1 QR / serial-lookup on manufacturer site for high-counterfeit categories.

Reject and return immediately if any fail — the return window starts ticking from delivery, not from when the user noticed.

### 9.2 Warranty registration
Many brands extend coverage by 30–60 days IF the buyer registers within 30 days of purchase. Surface in the report:

> **Warranty registration deadline**: <date+30d>. Register at <manufacturer URL>.

### 9.3 Day-1 firmware / secure setup (smart devices)
- Change all default passwords / IoT credentials.
- Run firmware update before connecting to home network long-term.
- Disable telemetry/cloud features the user doesn't need.
- Enable automatic security updates if available.
- Add device to home-network inventory; segregate IoT VLAN if user has one.

### 9.4 Insurance enrollment
For high-value items (≥ X% of household belongings value, typically anything over a few thousand TRY):
- Add as a homeowner / renter rider with serial number and proof-of-purchase.
- Verify replacement-cost vs depreciated-value coverage.

### 9.5 Documentation archival
One folder per purchase (physical or digital):
- Receipt with itemized line-by-line cost
- Serial number(s)
- Warranty card and registration confirmation
- Original manual / quick-start guide
- Photos of the unit on day 0 (condition baseline)
- Channel link (for any future repurchase or recommendation)

Output to user: a folder path or naming convention to use.

## Step 10 — Recall + maintenance + spares (ongoing)

### 10.1 Recall monitoring
Set up monitoring sources:

| Region | Source |
|---|---|
| US | [CPSC.gov](https://www.cpsc.gov/Recalls), [SaferProducts.gov](https://www.saferproducts.gov/) |
| EU | [Safety Gate (RAPEX)](https://ec.europa.eu/safety-gate-alerts/) |
| UK | [Product Safety Database](https://www.gov.uk/guidance/product-recalls-and-alerts) |
| Canada | [Canada.ca recalls](https://recalls-rappels.canada.ca/en) |
| Australia | [Product Safety Australia](https://www.productsafety.gov.au/recalls) |
| Other countries | Search `"<country> product recalls"` — most national consumer-protection authorities publish a recall registry; brand's own recall page is also a key source |
| Auto | NHTSA (US), DVSA (UK), KBA (DE), TC (CA), ANCAP (AU), brand site for any country |

Plus the manufacturer's recall mailing list (subscribe on the warranty-registration page).

The report should give the user the exact URLs and a calendar reminder ("Check for recalls quarterly").

### 10.2 Maintenance schedule
Generate a calendar (the user adds to their preferred system):

| Item | Frequency | Source |
|---|---|---|
| Replace filter | Every 6 months | Manufacturer manual |
| Lubricate chain | Every 200 km | Domain pack |
| Update firmware | Quarterly | Manufacturer's update cadence |
| Descale | Every 3 months (hard water region) | Manufacturer |
| Battery health check | Annual | User initiative |

Surface domain-specific maintenance in the appropriate `domain-<name>.md` file.

### 10.3 Spare-parts stocking
For bottleneck-class items and any product with proprietary/scarce parts:
- Identify the 2–3 parts most likely to fail or go EOL first.
- Buy and store while stocks are available (often 30–50% cheaper than emergency post-EOL prices).
- Note: only stock what makes sense; over-stocking is waste.

## Step 11 — End-of-life

When the product approaches retirement (replacement decision triggered by failure, obsolescence, or user-driven upgrade):

### 11.1 Resale plan
- Check eBay sold-median for the SKU at current age — that's the realistic resale value.
- Choose channel: eBay (global) / specialist marketplaces (KEH or MPB for cameras, Pinkbike for bikes, Reverb for music gear, etc.) / regional general marketplaces (Craigslist / Facebook Marketplace in NA, Gumtree in UK/AU, LeBonCoin in FR, Kleinanzeigen in DE, OLX in many emerging markets, Mercari in US/JP).
- Photograph well, list with original receipt + box if kept, include serial.

### 11.2 Trade-in
Some OEMs run trade-in programs (Apple, Sony, Samsung, Specialized). Compare against open-market resale; trade-in is often less but more convenient.

### 11.3 Recycle / dispose
For products that have no resale value or are damaged:
- E-waste route — use the user-region's licensed e-waste recycler or municipal collection program (most countries have national WEEE-equivalent regulations and authorized collection points).
- Manufacturer take-back programs (Apple, HP, Dell, many large brands).
- Donation to schools / community projects where the device still has use.

### 11.4 Data wipe (smart devices only)
**Before any disposal/resale**:
- Factory reset
- Disconnect from cloud accounts
- Verify on the cloud-side that the device is removed
- For storage devices: secure erase (not just delete)

### 11.5 Lessons learned
Append a `tasks/lessons.md` entry per CLAUDE.md §3 — what worked, what to do differently next purchase in this category. This is how the skill compounds value over multiple buys.

## Output to report

A single "Lifecycle plan" section near the end of the report:

```markdown
### 15. Lifecycle plan

**Day 0 — Receive & inspect** (checklist of 5 items above)
**Day +1 to +30 — Register & secure**:
- Warranty registration deadline: <date+30d> at <URL>
- Day-1 firmware update + change default credentials
- Insurance rider: add to policy (if high-value)
- Documentation archival: <folder path>

**Ongoing — Recall + maintenance**:
- Recall sources: <urls>
- Maintenance calendar:
  - <task> every <interval>
  - ...
- Spare parts to stock: <list with sources>

**End-of-life** (when replacing):
- Resale target: <eBay sold-median at age N> via <channel>
- Trade-in alternative: <OEM program> at <price>
- Recycle route: <regional e-waste / OEM take-back program>
- Data wipe steps (if smart device)
```

This section is dated and actionable — the user can paste calendar reminders directly from it.
