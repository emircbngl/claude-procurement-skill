# AskUserQuestion patterns

Batched question banks for AskUserQuestion. The rule: **only ask for what step 3 auto-extraction didn't capture**. Never re-ask data that's already in user files.

Use AskUserQuestion in single batched calls — never one-question-at-a-time.

## Step 1 — Domain clarification (only if ambiguous)

Use when the product noun is genuinely ambiguous (e.g., "drive" → SSD vs. golf club vs. car).

```
Q: "What kind of <product> are you researching?"
Options: <2–4 distinct domain options>
```

## Step 1.5 — Kraljic classification confirmation

Skip if the skill confidently inferred class. Ask only when borderline.

```
Q: "How important is this purchase to you, and how easy would it be to replace?"
Options:
- Routine — small spend, easy to replace if needed
- Leverage — meaningful spend, but plenty of vendors
- Bottleneck — limited vendors or scarce parts
- Strategic — important spend AND limited alternatives
```

## Step 4 — Requirements (most common batched call)

This is where most asking happens. Skip any question already answered by auto-extracted context.

```
Q1 — "What's your budget envelope?"
Options:
- <range option 1>
- <range option 2>
- <range option 3>
- Other (text input)

Q2 — "Primary use case?"
Options:
- <domain-specific use case 1>
- <domain-specific use case 2>
- <domain-specific use case 3>
- Other (text input)

Q3 — "What's your region / currency?"
Options:
- US (USD)
- EU (EUR)
- UK (GBP)
- Other (free text — specify country + currency code)

Q4 — "Audience level for the report?"
Options:
- Casual — short answer, key bullets
- Pro — full procurement detail with TCO + risk + decision matrix

Q5 — "TCO horizon?"
Options:
- 3 years (default)
- 5 years
- Other (text)

Q6 — "Must-haves and dealbreakers? (free text, can be 'none')"

Q7 — "Output format(s)? (multi-select; Markdown is always generated)"
Options:
- Markdown report only (default — fastest)
- + Executive deck (.pptx, 8–12 slides for stakeholder presentation)
- + Polished PDF brief (single-file printable report)
- + Stakeholder one-pager (1-page condensed, PDF or .md)
- + Word .docx report (editable for procurement / legal review)
```

Batch Q1–Q7 into a single AskUserQuestion call where possible. Each questions array entry corresponds to one question.

**Format chaining**: when the user selects formats beyond Markdown, step 8 calls the appropriate downstream skill — `anthropic-skills:pptx` for deck, `anthropic-skills:pdf` for PDF, `anthropic-skills:docx` for Word. See `references/output-formats.md` for the exact chain.

## Step 5 — Compliance follow-up (only if needed)

```
Q: "Open to refurbished / gray-market / used, or new-from-authorized-only?"
Options:
- New only, authorized dealer
- Manufacturer refurbished OK
- Any refurbished with ≥90-day warranty
- Used also fine
```

## Step 6 — Cross-border openness

```
Q: "Open to importing from abroad if 35–40%+ cheaper after customs?"
Options:
- Yes, include cross-border options
- Local / in-country only
- Depends on the difference — show me the math
```

## Step 8.6 — Cooling-off threshold confirmation

```
Q: "Your cooling-off threshold for purchases?"
Options:
- Any purchase over ~10% of monthly income → 24h pause
- Strategic purchases only → 72h pause
- No pause needed
- Use my household rule (text input)
```

## Step 11 — Lessons (optional, post-purchase)

After the user reports back from a purchase made via this skill, optionally:

```
Q: "How did the purchase go? Anything to capture as a lesson?"
Options:
- Went great, lessons file unchanged
- Some issues — describe
- Major regret — describe
```

## Design principles

1. **Batched** — combine related questions into one AskUserQuestion call.
2. **Multi-select where natural** — e.g., compliance flexibility, multiple use cases.
3. **Skip the obvious** — never ask "do you want a good product" or similar; that's universal.
4. **Concrete options** — avoid "Other" as the only entry. Always give 2–4 concrete options + Other.
5. **Stop after step 4** — once requirements are formalized, the skill should not need further input unless a step explicitly says so. Pull from web / domain pack instead of re-asking.
