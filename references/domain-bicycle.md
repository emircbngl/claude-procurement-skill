# Domain: Bicycle

## Research dimensions
- **functional_specs**: frame material, geometry (reach/stack/wheelbase/headtube angle), drivetrain speed (1×11/2×11/1×12), brake type (rim/disc, hydraulic/mechanical), wheel size (700c/650b/27.5"/29"), tire clearance (mm), weight, suspension (none/front/full + travel mm)
- **quality_signals**: groupset tier (Shimano: Tourney→Claris→Sora→Tiagra→105→Ultegra→Dura-Ace; SRAM: Apex→Rival→Force→Red; MTB Shimano: Altus→Acera→Alivio→Deore→SLX→XT→XTR), wheel brand, frame warranty, owner reviews
- **economic**: MSRP vs street price, used market depth, expected service cost per year, consumables (chain ~3000–5000 km, cassette ~3 chains, tires)
- **usage_fit**: commute / road / endurance road / gravel / cyclocross / XC MTB / trail MTB / enduro MTB / DH / e-bike / cargo / kids

## Required user inputs (overrides universal)
- Rider weight + height (for frame size + wheel/tire selection)
- Terrain (paved % vs gravel % vs single-track %)
- Annual mileage estimate (for component wear / TCO)
- Existing parts to reuse (wheels, drivetrain components, saddle, pedals)
- Storage situation (apartment elevator? garage? bike room?)
- LBS access (local bike shop nearby for service?)

## Standards & compatibility axes

| Axis | Values | Compat rule |
|------|--------|-------------|
| **Bottom bracket shell** | BSA 68/73, BSA 100 (fat), T47, BB86, BB30, PF30, PF30A, BB386 EVO, BBright, PF92 | Crankset spindle + BB cups must match shell standard |
| **Rear axle (frame)** | QR 130 (road) / QR 135 (MTB) / TA 142×12 (road/gravel) / TA 148×12 Boost (MTB) / TA 157×12 SuperBoost (MTB DH/some gravel) | Hub spacing must match frame dropouts |
| **Front axle (fork)** | QR 100 / TA 100×12 (road/gravel) / TA 100×15 (MTB) / TA 110×15 Boost (MTB) | Hub spacing must match fork dropouts |
| **Brake mount (frame/fork)** | Post mount (PM), Flat mount (FM), IS mount (legacy) | Caliper mount must match frame/fork; adapters exist FM↔PM in some directions |
| **Brake rotor mount** | Centerlock, 6-bolt | Hub interface must match rotor; adapters exist 6-bolt→Centerlock |
| **Rotor diameter** | 140/160/180/203 mm | Caliper-to-frame adapter sets rotor diameter; check fork/frame max rotor spec |
| **Drivetrain speed** | 6/7/8/9/10/11/12-sp + electronic (Di2, AXS, EPS) | Chain + cassette + shifter + derailleur must all agree on speed (cross-brand mostly incompatible at 12sp) |
| **Front derailleur** | Top-pull / bottom-pull / dual-pull, braze-on / clamp 28.6/31.8/34.9 | Cable pull direction + clamp diameter must match frame |
| **Tire (ETRTO)** | width × bead diameter (e.g., 32-622 = 32mm tire on 700c rim) | Rim internal width + bead seat diameter must match; check frame/fork clearance for tire OD |
| **Tubeless** | Tubeless-Ready (TLR), Universal System Tubeless (UST), non-tubeless | Tubeless setup needs TR-marked rim + tire + sealant + valve |
| **Cassette body / freehub** | Shimano HG (8–11sp), Shimano Micro Spline (12sp MTB), SRAM XD/XDR (1×11/12sp road/gravel/MTB), Campagnolo N3W | Cassette body on hub must match cassette type |
| **Headset** | EC34/EC44 (external), ZS44/ZS56 (zero-stack), IS41/IS52 (integrated), tapered (1⅛" → 1½") | Frame head tube standard determines headset cup type; fork steerer determines top |
| **Seatpost diameter** | 27.2, 30.9, 31.6, 34.9 mm | Frame seat tube ID determines seatpost diameter; shims can adapt within limits |
| **Saddle rail** | round 7mm, oval, carbon 7×9 | Seatpost clamp must support rail shape |
| **Pedals** | 9/16" (adult), 1/2" (kids/BMX), platform / SPD / SPD-SL / Look / Crank Bros / Speedplay | Thread to crank standard; cleat compatibility per pedal |
| **e-bike motor** | mid-drive (Bosch / Shimano EP / Brose / Yamaha / Bafang) vs hub-drive | Motor is frame-integrated; not swappable |

## Common upgrade pitfalls

- **11sp shifter on 12sp cassette** → won't index. Cross-brand 12sp also doesn't mix (Shimano 12sp ≠ SRAM 12sp).
- **Boost hub on non-Boost frame** → won't fit (148 vs 142 = 6mm too wide).
- **Flat-mount caliper on post-mount frame** → needs adapter; some directions impossible.
- **Press-fit BB on a frame designed for it = ongoing creak risk**; many owners regret it (T47 + threaded conversions exist for some standards).
- **6-bolt rotor on Centerlock hub** → needs adapter.
- **Tubeless rim + non-tubeless tire** = won't seal reliably; needs proper TR tire.
- **SRAM Eagle 12sp Micro Spline mismatch** — XD freehub doesn't mount Micro Spline cassettes; verify hub.
- **Carbon seatpost on frame requiring grip paste** — non-paste install can slip; check frame manual.
- **Disc-brake frame with rim-brake fork** (or vice versa) — incompatible system; both ends must match.
- **e-bike battery proprietary to motor brand** — not interchangeable; sizing battery for range vs weight is the upgrade lever.

## Trusted sources for web fallback

- [BikeRadar](https://www.bikeradar.com), [Cyclingnews](https://www.cyclingnews.com)
- [Shimano compatibility chart](https://bike.shimano.com) — first source for Shimano interop
- [SRAM AXS compatibility](https://www.sram.com) — first source for SRAM
- [GCN YouTube](https://www.youtube.com/c/gcn) — workshop and buying videos
- [Park Tool repair help](https://www.parktool.com/blog) — technical reference
- Regional pricing: for any country, search `"bike <country> price comparison"` to find the local cycling-retailer aggregator (e.g., BikeRadar's retailer pages, Wiggle / Bike-Discount / R&A in EU, REI / Backcountry / Competitive Cyclist in US, etc.)
- [Pinkbike](https://www.pinkbike.com) (MTB), [r/cycling](https://reddit.com/r/cycling), [r/bicycling](https://reddit.com/r/bicycling)
- [Weight Weenies forum](http://weightweenies.starbike.com/forum/) — for very specific component data
