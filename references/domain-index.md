# Domain pack index

Authoritative list of available domain packs. The skill consults this on **step 1** to map user query keywords to a pack file. Maintained by the skill (new entries appended on every auto-save of a new pack via the self-feeding mechanism — see `self-feeding.md`).

When adding a domain pack: append a row. When the skill writes a new auto-generated pack, it must also append the entry here.

| Domain | Pack file | Keywords (lowercase, partial-match) | Status | Mode bias |
|---|---|---|---|---|
| Bicycle | `domain-bicycle.md` | bicycle, bike, mtb, gravel, road bike, drivetrain, derailleur, bb, cassette, hub, e-bike (bicycle context), saddle, frame, fork, chainring | hand | B2C |
| PC | `domain-pc.md` | pc, build, motherboard, cpu, gpu, ram, psu, case, nvme, ssd, processor, ryzen, intel, gaming pc, workstation | hand | B2C / prosumer |
| Cosmetics | `domain-cosmetics.md` | skincare, makeup, serum, sunscreen, spf, retinol, niacinamide, vitamin c (skincare), moisturizer, fragrance, foundation, lipstick, cosmetics, beauty | hand | B2C |
| Home appliance (major) | `domain-home-appliance.md` | washer, dryer, dishwasher, refrigerator, fridge, freezer, oven, cooktop, range, range hood, water heater, hvac, washing machine, beyaz eşya | hand | B2C |
| Small appliance | `domain-small-appliance.md` | coffee machine, espresso, blender, food processor, air fryer, kettle, toaster, stand mixer, vacuum, robot vacuum, hair dryer, iron, küçük ev aletleri | hand | B2C |
| Camera | `domain-camera.md` | camera, lens, mirrorless, dslr, sensor, mount, full-frame, aps-c, micro four thirds, photography, fotoğraf makinesi | hand | B2C / prosumer |
| Audio | `domain-audio.md` | headphone, iem, earbuds, speaker, amp, amplifier, dac, soundbar, anc, audiophile, hi-fi, kulaklık, hoparlör | hand | B2C / prosumer |
| Smart home | `domain-smart-home.md` | smart home, iot, matter, zigbee, z-wave, thread, hub, sensor, smart switch, smart bulb, smart lock, security camera, alarm, home assistant, akıllı ev | hand | B2C |
| Furniture (incl. mattress) | `domain-furniture.md` | furniture, sofa, chair, desk, bed, mattress, table, bookshelf, ergonomic chair, standing desk, koltuk, masa, yatak, ofis koltuğu | hand | B2C + B2B |
| Personal mobility | `domain-mobility.md` | e-bike (transport context), e-scooter, electric scooter, electric skateboard, eus, euc, electric unicycle, e-moped, e-board, segway | hand | B2C |
| IT software (SaaS) | `domain-it-software.md` | saas, business software, crm, erp, hrms, itsm, helpdesk, project management, communication, slack, salesforce, jira, devtool, infrastructure software, security software | hand | B2B |
| Medical device | `domain-medical-device.md` | cpap, hearing aid, glucose monitor, cgm, insulin pump, blood pressure, mobility aid, wheelchair, walker, oxygen, pulse oximeter, tıbbi cihaz | hand | B2C + B2B (clinic) |

## Future-pack candidates

These are categories the skill is likely to encounter and auto-generate packs for. Once a pack is auto-generated, it appears here.

- IT hardware (networking, server, endpoint) — B2B
- Office furniture (contract grade) — B2B
- Printer / multi-function (consumer + office) — B2C + B2B
- Power tools — B2C + B2B (contractor)
- 3D printer — B2C / prosumer
- Drone — B2C / prosumer / B2B (industrial)
- Espresso machine (dedicated, beyond small-appliance) — B2C / prosumer
- Watches (mechanical / smart) — B2C
- Eyewear / sunglasses — B2C
- Baby products (stroller, car seat) — B2C (critical safety)
- Pet products — B2C
- Outdoor / camping — B2C
- Musical instrument — B2C / prosumer
- Footwear (running / hiking / cycling) — B2C
- Apparel (outdoor / technical) — B2C
- Tires (auto) — B2C
- Battery / portable power — B2C + B2B
- Solar panels (residential) — B2C + B2B
- HVAC (residential AC / heat pump) — B2C + B2B
- Tools (kitchen knives, hand tools) — B2C
- Supplements / vitamins — B2C (verification critical)
- Pharmacy OTC — B2C (verification critical)

## How matching works

1. Skill takes user's first message, lowercases it.
2. For each row in the table, check if any of its keywords appear in the user's message.
3. If exactly one match → load that pack.
4. If multiple matches → use the one with the **most specific** keyword match (longer keyword wins); if tied, ask user via AskUserQuestion.
5. If no match → fall back to `domain-unknown.md` workflow, which derives dimensions and **adds a new row to this index** at the end of the run.

## Promotion lifecycle

Auto-generated packs start `status: auto-gen, confidence: low`. After:
- 3 successful runs without contradiction → `confidence: medium` (skill auto-bumps)
- Human review (user opens the pack, removes warning banner) → `confidence: high, status: human-reviewed`

The index column should reflect the current status of each pack.
