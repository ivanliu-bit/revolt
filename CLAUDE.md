# GreenVolt — Device Buyback & Component Resale Platform

Student-founded circular-economy startup (SHAD 2026, University of Alberta, Team Green). Buys broken phones/small electronics from consumers, harvests reusable components, resells to repair shops/refurbishers/manufacturers, and routes true scrap through certified domestic recycling instead of informal export.

This repo currently holds a **single-file static demo** (`index.html`) built for Demo Day, not the real product. See `README.md` for how to run/edit it.

**Source of truth:** the team's business-plan doc (Executive Summary, Lean Canvas, SHAD Team Agreement) supersedes earlier estimates in this file where the two conflict. See "Superseded figures" at the bottom for what changed and why.

## Mission & vision

- **Mission:** to make recycling broken or surplus mobile devices effortless, sustainable, and financially rewarding for the consumer through component recovery.
- **Vision:** to be the world's most accessible and sustainable service for recycling unwanted electronic devices.

## Problem

- On the consumer side, there's no financial incentive to return dead/outdated devices, so they sit idle while people keep buying new ones. **35% of Canadians report their old mobile devices are left idle in their homes** (source: seprosystems.com/the-facts-and-figures-of-e-waste). This withholds valuable metals/components that end up in landfills instead of being recycled, and props up the cost of electronic goods.
- On the manufacturer side, electronics makers depend on raw materials from environmentally damaging third parties, an energy-intensive refining process with a large carbon footprint, forced labor and debt bondage in global electronics supply chains (source: danwatch.dk), and global shipping networks. This conflicts with modern sustainability standards and brand expectations.
- Globally, approximately **5.3 billion phones were discarded in 2022** (source: BBC, bbc.com/news/science-environment-63245150, citing the WEEE Forum).

## Core business model

1. **Intake** — user submits a broken device via the website (photos + condition questions), receives cashback.
2. **Grading** — three tiers by condition:
   - **Tier 1** — battery fault only, everything else functional
   - **Tier 2** — screen cracked, everything else functional
   - **Tier 3** — beyond economical repair (BER) / multi-fault, metals recovery only
3. **Collection** — free pickup scheduled by the customer on the website, shipped via standard couriers (FedEx, DHL, Purolator) to the facility.
4. **Inspection** — IMEI lookup for basic device info, then Phonecheck (phone diagnostic software) tests 60+ hardware parameters: battery cycle count/power %, display (dead pixels, colour accuracy), touchscreen glass condition, cameras, speakers, microphones, charging ports, buttons, vibration motor, Face ID/fingerprint, GPS, accelerometer, gyroscope, compass, proximity sensor, ambient light sensor, SIM reader, storage, water-damage indicators (LCI/corrosion), housing/frame condition.
5. **Disassembly** — components harvested and stored: screen, battery, camera module, logic board, and others; tested, graded, and repaired where appropriate.
6. **Packaging & transport (dangerous goods compliant)** — before packaging, complete devices are sorted/labeled by manufacturer, model, and quality. Batteries and hazardous components go in flame-retardant bulk bags. Terminals covered with non-conductive material; bubble wrap/foam prevents shifting or crushing; no shipping of bulged, leaking, or damaged batteries; batteries (especially >80% charged) packed individually. Governed by Canada's Transportation of Dangerous Goods Regulations (tc.canada.ca).
7. **Resale** — harvested components sold B2B to repair shops, refurbishers, and manufacturers (see Revenue Streams).
8. **Disposal of true scrap** — certified domestic recyclers (Call2Recycle for batteries, EPRA for other e-waste), funded by upstream producer Environmental Handling Fees, not export to informal channels.

## Unique value proposition

We sustainably turn dead mobile devices into cash. Unlike typical trade-in businesses that only take and resell fully functional devices, GreenVolt pays consumers a cut from every component, working or not.

## Unfair advantage

Industry giants like Apple's Trade In program (apple.com/shop/trade-in) pay nothing for a device if it's dysfunctional, treating it as waste. GreenVolt targets exactly the segment those programs ignore: dead and broken devices, by recognizing the resale/recycling value in their individual components.

## Differentiation

- Existing players are either heavy-asset car-battery services (AAA, Batteries911) or large device-resale platforms (Batteries Plus, 转转/Zhuanzhuan) that only monetize whole, working devices, same gap the "unfair advantage" above describes. Nobody does light-asset, component-level, certified/traceable matching specifically for consumer electronics.
- Core B2B value prop: **verified, traceable sourcing** — a large share of aftermarket batteries in the market today are counterfeit/substandard, and this is what GreenVolt sells against.

## Customer segments

- **Supply side:** individuals with dead or old unused phones sitting in drawers.
  - Primary target ages 18–49, reached via social media and YouTube advertising.
  - Elderly customers reached via door-to-door service.
- **Demand side:**
  - Manufacturers of LED lights and power banks (second life for dead phone batteries).
  - Repair shops needing screens, cameras, vibration motors, haptic feedback sensors, and other components.

## Channels

Social media (broad accessibility across age ranges), YouTube/video ads, door-to-door outreach (especially early-stage, to remove friction and build word-of-mouth/referral in local areas), celebrity collaborations and press releases considered for later-stage growth.

## Key metrics

- **Phones collected per month/year** — leading indicator of brand growth/reputation.
- **Average payout vs. average revenue** — the gap between the two is the health signal; revenue must exceed payout, and a widening gap is a positive sign.
- **% of phone mass resold to manufacturers** — efficiency metric; should trend up as the operation matures.

## Revenue streams

- Resale margin model: customers get a percentage cut of what each component sells for.
  - Battery cells (tested + graded) → LED manufacturers
  - Screens, cameras, ports → repair shops
  - Circuit boards → precious-metal recovery firms
  - Aluminum + glass → material recyclers
- B2B collection drives: schools/companies pay for e-waste pickup + an impact report.
- **Named B2B buyers/distributors** (per team's revenue-stream research): MobileSentrix, MobiPhix, Nexus Cellar, all based in the Toronto area, within ~22km of the team's main warehouse (reduces shipping costs). **Do not publish these specific partner names on the public-facing website** without the partners' knowledge/consent, this is internal business-plan detail, not public marketing copy.

## Cost structure

Advertising (e.g. YouTube ad placements), materials for stripping/testing batteries, staff to disassemble/organize parts, transport (fuel, vehicles, drivers) for both inbound device collection and outbound shipments to manufacturers.

## Financial model — illustrative only, not validated against real pilot data

- Launch-year target: **~$40,000 revenue, ~$10,000 profit**, assuming a minimum of **350 phones processed** (< 1 device/day; most customers submit multiple phones per order, so device count ≠ order count).
- Startup capital: ~$3,000–8,000 CAD (earlier team estimate, not addressed in the newer business-plan doc, kept as-is).
- Long-range/lean-canvas aspiration: "estimated lifetime value ~$11 billion, similar scale to Best Buy." This is a directional, very-long-term ambition from the Lean Canvas, not a near-term planning number, don't treat it as comparable to the launch-year figures above, and don't let it leak into near-term pitch materials without heavy caveats.

These are team estimates for pitch purposes. **Do not treat them as ground truth.** The $59/device and $38/device figures from an earlier team estimate (see "Superseded figures" below) implied roughly double the per-device revenue in the newer doc's $40,000-for-350-phones math, that gap is unresolved, not averaged away.

## Known open risks (unsolved, not to be papered over)

- Real conversion rate (people who hear about this → actually mail in a device) is unverified.
- Per-device B2B resale value has not been confirmed with real buyers, and the team's own two internal estimates for it disagree by roughly 2x (see "Superseded figures").
- The claim that 350 phones/year is enough to be profitable has not been reconciled with the separate estimate that break-even alone requires ~53–61 devices/**month** (~636–732/year), a ~2x gap in required volume. Pick one before this goes in front of judges.
- Lithium battery handling safety/liability, and the labor economics of testing/grading low-value consumer batteries, are real unresolved weaknesses.
- **Facility location is unresolved**: the team's SHAD program cohort is University of Alberta (Edmonton), but the revenue-stream research assumes a warehouse in the Toronto area (~22km from named distributors). The demo site's shipping label currently reflects Toronto-area placeholder details, pending a real decision on where the business would actually operate. SHAD cohort location and business operating location are two different facts and are not inherently contradictory, but they haven't been explicitly reconciled.

## Open product design question: camera-based valuation

The team wants a feature where a user photographs their device and the site estimates cashback value. **Founder's own stated concern:** a photo only captures exterior condition (cracks, scratches), it can't verify internal condition (battery health, logic board function, water damage). A phone can look fine externally and be dead internally, or look wrecked but have healthy internals.

Current resolution (implemented in the demo): photos are collected as supporting evidence for **manual human review**, not run through any automated vision analysis, and the displayed number is explicitly framed as a preliminary estimate ("ESTIMATED PAYOUT," "~$X") pending confirmation. This still doesn't use the Tier 1/2/3 grading system as an input to the intake flow itself; that remains a real gap, the live quote calculator's per-model pricing and the CLAUDE.md tiers are two separate systems that aren't yet unified.

## Other structural site elements (to expand with founder, not assumed complete)

- Shipping/drop-off instructions once a user accepts an offer (implemented, no facility location resolved, see above).
- A way to communicate certification/traceability to B2B buyers, likely a separate section or flow, since B2B buyers and individual consumers are different audiences with different needs. Not yet built.

## Superseded figures (what changed, and why)

The team's SHAD business-plan doc (Executive Summary/Lean Canvas/Team Agreement) is the newer, more authoritative source. Where it conflicted with this file's earlier estimates:

- ~~Break-even: ~53–61 devices/month~~ → superseded by "350 phones/year for profit," **but the two were never reconciled** (see Known open risks). Do not quote the old 53–61/month figure as current.
- ~~Blended gross profit per device: ~$38 (revenue ~$59, cashback ~$9, processing/shipping ~$12)~~ → superseded by the $40,000-revenue/$10,000-profit-per-350-phones math (~$114 revenue/device, ~$28.57 profit/device implied), **also not reconciled with the old figures**, roughly a 2x gap on revenue/device specifically.
- Team name/roster: the About page previously showed 5 generic role slots, all named `[Name]`. Real roster (SHAD Team Agreement): Ivan Liu, Emily Cai, Lucas Penlington, Anjola Shyllon, Miranda Yong, Mihir Mahabal, Saahas Chahal (Team Liaison). Roles: Lucas, Financials; Ivan & Miranda, Prototyping; Anjola, Pitch Deck; Saahas & Mihir, Problem Solving and Ideation; Emily's specific role wasn't named in the "Roles and Contribution" breakdown ("All" own the Report collectively), don't invent a title for her that the source doc didn't state.

## Known fake/placeholder data in `index.html`

- The hero stat counters were originally fabricated (`12,483` phones rescued, etc.); they now display real, cited facts instead (search `data-target`), see git history for the fix.
- Team section previously had 5 `[Name]` placeholders; being replaced with the real roster above.
