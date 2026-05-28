# Token efficiency

One of the strongest reasons to use this skill instead of asking Claude directly is **token efficiency over time**. Naive "ask Claude to research X" sessions cost more tokens and more web calls than necessary because they re-derive the same context every time. This skill avoids that.

## The four mechanisms

### 1. Progressive disclosure

`SKILL.md` is ~150 lines. It loads at the start of every run. The detailed playbooks (`references/*.md`) are 2,000+ lines combined but **only load when relevant**. A run on a known domain pulls in ~3 reference files; a strategic-class run pulls in ~6.

Without progressive disclosure, every run would have to load the entire procurement framework into context. With it, the model loads just what it needs.

### 2. Self-feeding (criteria-side caching)

The skill ships with 13 hand-authored domain packs. For categories outside those, the first encounter runs a **deep search** — 20–30 WebSearch + WebFetch calls across 8 categories (buying guides, standards, brands, pitfalls, repairability, compliance, TCO drivers, reviews). The results are saved to `references/domain-<slug>.md`.

**Subsequent runs on the same domain do zero criteria research.** The pack is loaded from disk. Future encounters with "Anycubic vs Elegoo 3D printer" don't re-derive what a 3D printer's compatibility axes are — those are already saved.

### 3. Auto-extraction

The skill scans the working directory for files containing relevant context (existing gear lists, prior quotes, prior research notes) before asking the user anything. Anything found there is **never re-asked**. Users who research multiple related products over time benefit cumulatively — context accumulates in their working directory.

### 4. Compressed report template

The output `tasks/research/<slug>.md` is dense but not bloated. Tables compress what would otherwise be paragraphs of prose. Sections are numbered and scannable. Casual-audience mode condenses sections further.

## What we cache vs what stays live

This is the most important distinction, and it's intentional:

| Cached (saved to domain pack, ~0 web cost per future run) | Live (re-fetched every query) |
|---|---|
| Research dimensions (which specs matter) | **Current prices** |
| Standards & compatibility axes (e.g., bike BB shells, PC CPU sockets) | **Stock / availability** |
| Certification marks per region | **Active promos / discounts** |
| Brand landscape per region | **Fair-price band** (calculated per query) |
| Common pitfalls / failure modes | **Recent recalls / news** |
| Trusted source URLs | **FX rates** |
| Regulatory bodies | **Reference-customer references (B2B)** |
| Repairability norms | **Vendor financial health updates** |
| EOL / lifecycle patterns for the category | **Current model lineup vs EOL** |

**Why this split**: caching prices would be a feature anti-pattern. Stale prices mislead buyers. The skill explicitly re-runs **price discovery (step 6)** every query — that's the right design. Caching the **stable knowledge about how to buy a category** is the right cache. Caching what something costs today is the wrong cache.

## Rough numerical comparison

> Illustrative only — actual token counts depend on prompt complexity, model version, and the specific category researched.

| Scenario | Input tokens (est.) | Web calls (est.) |
|---|---|---|
| Naive "Claude, research X for me" — no skill | 40–60k | 20–60 (varies wildly; no structure) |
| This skill, **first encounter** with unknown domain | 25–35k | 20–30 (deep search on criteria) + 5–10 (live price discovery) |
| This skill, **subsequent encounter** with same domain (saved pack reused) | 8–15k | 3–8 (price + availability only) |
| This skill, **known hand-authored domain** (e.g., bicycle) from day 1 | 8–15k | 3–10 |

**Across 10 runs on the same category**, the skill saves roughly **70–80% of tokens and web calls** vs naive use — the first-run deep-search investment amortizes quickly.

## Verification

If you want to measure the actual savings on your own usage:

1. Before installing the skill, run a research session naively: ask Claude "research the best X for my needs". Note the number of web tool calls and the final token usage.
2. After installing, run the same query through the skill. Note the same.
3. Re-run a similar query in the same category a week later. The savings compound.

Most users see the skill pay for its install effort within the first 2–3 research sessions, especially if they research multiple products in the same domain.

## Limitations

- **Stale domain packs**: if a pack is > 18 months old, standards and brand landscape may have drifted (e.g., new compliance regulation, brand acquisitions, EOL of previously-prevalent standards). The skill flags packs at this age for re-derivation. The 18-month threshold is a heuristic — adjust based on category volatility (e.g., consumer electronics ~12 months, mature appliance categories ~36 months).
- **First encounter is expensive**: the 20–30 web call deep search is a one-time cost. If you only ever research one product in a category, the savings don't materialize — the skill is optimized for repeated use of the same skill, not single-shot queries.
- **Price discovery is intentionally not cached**: every query re-runs step 6. If you want price snapshots cached, that's a different feature (and arguably a misfeature, see "What we cache vs what stays live" above).

## Comparison vs other research approaches

| Approach | Tokens per session | Web calls per session | Repeat efficiency |
|---|---|---|---|
| Direct Claude prompt ("research X") | High | Variable, often high | None — same cost every time |
| Manual research with web search | n/a (human time) | Variable | None — same human time every time |
| Generic AI research agent (no skill) | High | Variable | None |
| **This skill, repeated use on same category** | **Low (8–15k)** | **Low (3–10)** | **Compounding** — criteria-side knowledge accumulates per category |

The skill's efficiency is structural, not marginal. It comes from the architecture — progressive disclosure + self-feeding + auto-extraction + compressed output — not from prompt tuning.

## When NOT to use this skill (efficiency lens)

The skill is **less efficient** than naive Claude for:
- A single one-shot lookup ("what does X cost on Amazon right now?") — no need for the full pipeline
- Pure spec recall ("what's the IP rating of model Y?") — no structured procurement needed
- Categories the user will only ever research once and never revisit — the deep-search cost doesn't amortize

For these cases, just ask Claude directly. The skill is optimized for **research sessions that produce a decision memo** AND for **repeated use within a category over time**.
