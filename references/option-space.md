# Option-space analysis

Before assuming the answer is "buy this product", explicitly test whether **purchase** is even the right path. Run this step at depth proportional to Kraljic class — a one-line check for routine, a documented decision for strategic.

## Make-vs-buy

For products where the user has the skills, tools, and time to build:

| Buy when | Make when |
|---|---|
| Skill gap or risk of injury (electrical, plumbing) | User has the skills and tools already |
| Time-to-need is tight | Project is also a goal in itself |
| Total DIY cost (materials + tools + time) > buying price | Significant savings + reusable knowledge |
| Warranty / certification matters (safety, code compliance) | Certification doesn't matter |
| Sourcing parts is hard | Parts are readily available |

**Examples**:
- Bicycle wheel build: experienced cyclist + truing stand + 4h time = cheaper than pre-built equivalent. Beginner = buy.
- PC: building from parts is almost always cheaper than pre-built at the same tier, IF the user is comfortable doing it. Otherwise, buy pre-built.
- Furniture: IKEA-tier assembly = buy. Custom dimensions / matched wood = make.

## Build-vs-buy-vs-rent-vs-subscribe

For tools, equipment, software, and increasingly even physical goods:

| Option | Best when |
|---|---|
| **Build** (DIY, custom) | Frequent use, specific needs not met by market |
| **Buy** | Daily/weekly use over multi-year horizon |
| **Rent** | One-time or seasonal use; storage/disposal would be a hassle |
| **Subscribe** | Recurring need with versioning, support, or content updates (SaaS, cloud storage, streaming) |
| **Borrow / library / shared** | One-off + community has it (tool library, makerspace) |

### Rent-vs-buy decision rule

```
buy if:  use_freq × ownership_horizon × per-use-value  >  buy_cost + storage + maintenance + disposal − resale
rent if: rent_cost × use_freq × ownership_horizon  <  buy_cost − resale
```

### Examples by category

**Tools**:
- Tile cutter for one bathroom job → **rent** from a hardware-store rental program or tool library
- Drill used monthly → **buy** (cheap, frequent)
- Specialty plumbing tool → **rent or borrow**

**Software / digital**:
- Photoshop used quarterly → **subscribe** (Creative Cloud monthly)
- 3D modeling software for daily work → **buy perpetual license** if available
- Cloud backup → **subscribe** (recurring infrastructure)

**Physical equipment**:
- Camera for a single trip → **rent** (lensrentals.com, local equivalents)
- Camera for ongoing hobby → **buy used** (depreciation already absorbed)
- Wedding suit → **rent** (one-off)
- Daily work jacket → **buy**

**Vehicles**:
- City weekend errands → **subscribe / share** (Zipcar, getaround, local car-share or ride-hail)
- Commute and family use → **buy**
- Ski trip → **rent**

## When to skip option-space

- Compatibility-check intent (user already has the product, just checking interop).
- Routine class where purchase is obvious (USB cable, batteries, consumables).
- User explicitly stated "I want to buy X" — don't second-guess unless rent/borrow is dramatically better.

## Output of step 3.5

One paragraph per applicable framework:
- Make-vs-buy verdict + reasoning
- Build/buy/rent/subscribe verdict + reasoning

If a non-purchase option wins → write the report with `Recommendation = "purchase not recommended; <alternative> recommended instead"` and skip the rest of the pipeline. If purchase wins → proceed to step 4.
