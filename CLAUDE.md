# GreenVolt — Device Buyback & Component Resale Platform

Student-founded circular-economy startup (SHAD 2026, University of Alberta, Team Green). Buys broken phones/small electronics from consumers, harvests reusable components, resells to repair shops/refurbishers, and routes true scrap through certified domestic recycling instead of informal export.

This repo currently holds a **single-file static demo** (`index.html`) built for Demo Day — not the real product. See `README.md` for how to run/edit it.

## Core business model

1. **Intake** — user submits a broken device, receives cashback.
2. **Grading** — three tiers by condition:
   - **Tier 1** — battery fault only, everything else functional
   - **Tier 2** — screen cracked, everything else functional
   - **Tier 3** — beyond economical repair (BER) / multi-fault, metals recovery only
3. **Disassembly** — components harvested and stored: screen, battery, camera module, logic board.
4. **Resale** — harvested components sold B2B to repair shops, refurbishers, other buyers.
5. **Disposal of true scrap** — certified domestic recyclers (Call2Recycle for batteries, EPRA for other e-waste), funded by upstream producer Environmental Handling Fees, not export to informal channels.

## Differentiation

- Existing players are either heavy-asset car-battery services (AAA, Batteries911) or large device-resale platforms (Batteries Plus, 转转/Zhuanzhuan). Nobody does light-asset, component-level, certified/traceable matching specifically for consumer electronics.
- Core B2B value prop: **verified, traceable sourcing** — a large share of aftermarket batteries in the market today are counterfeit/substandard, and this is what GreenVolt sells against.

## Policy tailwinds (positioning, not yet product features)

- Canadian right-to-repair legislation (federal C-244/C-294; Ontario Bill 91 in progress) pushing toward mandated parts access and anti-parts-pairing rules.
- Ontario's Battery Regulation (EPR) makes producers responsible for battery end-of-life — potential future B2B compliance-service revenue line.
- Basel Convention 2025 e-waste amendments + EU export bans are closing informal export channels — reinforces demand for compliant domestic channels like this one.
- Lithium battery transport is regulated under Canada's TDG (Transportation of Dangerous Goods) — anyone on the team handling batteries needs TDG training.

## Financial model — illustrative only, not validated

- Blended gross profit per device: ~$38 (revenue ~$59, cashback ~$9, processing/shipping ~$12)
- Break-even: ~53–61 devices/month depending on fixed costs included
- Startup capital: ~$3,000–8,000 CAD

These are team estimates for pitch purposes. **Do not treat them as ground truth** — they have not been validated against real pilot data, and the site's fake activity stats (see "Known fake data" below) should not be confused with these financial assumptions.

## Known open risks (unsolved, not to be papered over)

- Real conversion rate (people who hear about this → actually mail in a device) is unverified.
- The $59/device average B2B resale value has not been confirmed with real buyers.
- Lithium battery handling safety/liability, and the labor economics of testing/grading low-value consumer batteries, are real unresolved weaknesses.

## Open product design question: camera-based valuation

The team wants a feature where a user photographs their device and the site estimates cashback value. **Founder's own stated concern:** a photo only captures exterior condition (cracks, scratches) — it can't verify internal condition (battery health, logic board function, water damage). A phone can look fine externally and be dead internally, or look wrecked but have healthy internals.

This is a product design problem, not a solved one. Directions worth reasoning through with the founder before building, not assuming:

- Should the camera estimate be explicitly framed as a **rough/preliminary quote only**, with binding valuation happening after physical receipt and testing?
- Should intake also ask simple yes/no diagnostics (powers on? screen responds to touch? battery health % from phone settings?) alongside the photo, to reduce reliance on visual-only assessment?
- How to set expectations up front (e.g. "final payment may differ from your estimate after inspection") so users aren't surprised later?
- Should the Tier 1/2/3 grading system map directly onto the intake flow, or is grading a separate post-receipt step?

**Do not silently pick one of these and build past it — surface the tradeoff to the user.**

## Other structural site elements (to expand with founder, not assumed complete)

- User intake flow (photo upload + device info + estimated cashback)
- Shipping/drop-off instructions once a user accepts an offer
- A way to communicate certification/traceability to B2B buyers — likely a separate section or flow, since B2B buyers and individual consumers are different audiences with different needs

## Known fake/placeholder data in `index.html`

The current demo hardcodes fabricated numbers to look like a live product. These need founder input before they can be made honest (see conversation for the discussion) — do not silently invent replacement numbers:

- Hero stat counters: `12,483` phones rescued, `3,100 kg` e-waste diverted, `$186k` paid out (search `data-target`)
- A `setInterval` in `<script>` that randomly increments the phones-rescued counter every ~3s to fake live activity
- Team section: 5 members all named `[Name]` (README also flags this under "Common edits")
