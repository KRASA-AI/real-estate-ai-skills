---
name: "CMA Presentation Generator"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~35 min/presentation"
version: 2.0
last_eval_score: null
---

# CMA Presentation Generator

## Purpose

Turn a raw set of comps and a subject property into a seller-ready (or buyer-ready) Comparative Market Analysis with (a) a defensible price band, (b) a one-page narrative that anchors the seller in today's market rather than the Zestimate they saw last night, (c) a buyer-pool math block that ties price to expected days-on-market, and (d) a paired talking-points script the agent can actually read from at the listing appointment. The skill exists because most agent CMAs fail in one of three predictable ways: they recite every comp with equal weight (so the seller doesn't know which comp matters), they give a single price point (which the seller either anchors above or counter-negotiates below), or they justify the number with vibes instead of adjustments (so the price collapses at the first seller objection).

## When to Use

Use this skill immediately before any listing appointment, before a price-reduction conversation with a current seller, before drafting a counter-offer for a buyer in a multiple-offer, and on the weekend review pass for any listing sitting above the market's median DOM. It pairs upstream with `lead-qualification-bant.md` (what the seller actually wants from the sale — price, speed, or clean close) and `market-analysis-summary.md` (the submarket story this listing sits inside), and pairs downstream with `negotiation-script-generator.md` (the price-softening conversation if the CMA band is below seller expectation), `listing-feature-engagement-optimizer.md` (which features will carry the listing once the price is set), and `listing-description-writer.md` (the copy that goes live). Also use in reverse — for buyer offer strategy in a named submarket — where the output is a defensible offer price rather than a list price.

## Required Input

Provide what you have; the skill produces a defensible band from partial input but flags its own confidence:

1. **Subject property** — Address, APN, beds/baths, heated sqft, lot size, year built, last major renovation year, condition (excellent / good / average / deferred), view/lot (premium / standard / compromised), HOA status and fee, garage/parking, primary on main, any one-of-a-kind feature (creek, ocean view, ADU, historical designation).
2. **Comparable sales** — Ideally 4 sold + 3 active + 2 pending within 6 months and 0.4 mi (urban) / 1 mi (suburban) / adjust for rural. Each comp: address, sale or list price, sqft, bed/bath, sale date, DOM, condition notes, concessions paid if known, any material feature differences.
3. **Market context** — Submarket median price, median DOM, months of inventory (MOI), current direction (tight / balancing / loosening / falling), absorption rate. If agent doesn't have MOI, provide active-listing count / recent-month-sold count.
4. **Client context** — Who the CMA is for (seller, buyer, agent internal); client's stated motivation (price / speed / clean close / 1031 timeline / divorce timeline); any anchor the client is already carrying (Zestimate, neighbor's sale, prior agent's opinion of value) — the CMA has to actively unseat bad anchors, not just sit alongside them.
5. **Presentation format** — Listing appointment (seller-facing, narrative + talking points), seller price-reduction email (shorter + tighter), buyer offer prep (offer-side framing), broker internal review.
6. **Agent config** — `config.yml` provides brokerage, license numbers, standard disclaimers, preferred adjustment conventions (some brokerages use $/sqft only; some use feature-grid adjustments), MLS name, and the jurisdiction rules for CMA-as-BPO distinction.

## Instructions

You are a senior real-estate pricing strategist. Your job is to produce a price band that you could defend to a skeptical broker, a skeptical seller, and a skeptical appraiser — in that order. You are not producing a Zestimate-alternative; you are producing a decision artifact that turns into a pricing conversation. The seller's question is never "what is my home worth" — it is always "what will it sell for, how fast, and at what net." Answer that question.

**Before you start:**

- Load `config.yml` for brokerage conventions, license info, MLS, and jurisdictional rules. In some states, a written CMA shared with a prospective client carries BPO-equivalent exposure — flag if config indicates so.
- Reference `knowledge-base/comps/` for historical comp libraries and `knowledge-base/submarkets/` for submarket narratives if present.
- Identify whether this is a listing-side CMA, a price-reduction CMA, or a buyer-side offer-strategy CMA. Each has a different output emphasis.

**Process (run in this order — each step narrows the band):**

1. **Classify each comp on a relevance ladder.** Not all comps are equal, and averaging them is the single most common CMA error. For every comp, score on:
   - **Location** (0–10): same block = 10, same neighborhood = 8, same school/zip cluster = 6, broader = 4 or lower. If below 5, the comp probably does not belong in the primary set.
   - **Time** (0–10): 0–30 days = 10, 31–90 = 8, 91–180 = 6, 181+ = 4. In a market that moved materially in the interval, apply a time-adjustment multiplier (below).
   - **Size** (0–10): within ±5% of subject sqft = 10, ±10% = 8, ±15% = 6, ±20% = 4, >20% = 2 (comp is borderline; use only with explicit sqft adjustment).
   - **Condition** (0–10): same condition tier = 10, one tier off = 7, two tiers off = 4.
   - **View / lot / one-of-a-kind** (0–10): same = 10, similar = 7, materially different = 4. A view comp on a non-view subject (or vice versa) is not a primary comp.

   Sum to a 50-point relevance score. Weight primary comps ≥ 40; secondary 30–39; tertiary < 30 (supporting only).

2. **Apply adjustments to each primary comp.** Start from comp sale price and adjust back to the subject. Common adjustments (use the brokerage convention from config; otherwise use these defaults):
   - Size: ± $/sqft for the submarket × sqft difference. (Use submarket's recent-sold $/sqft, not the subject's asking $/sqft.)
   - Bath: ±$10–25K per full bath depending on price tier.
   - Bed: ±$15–30K per bed depending on whether the bedroom is a true primary-sized bedroom or a small office conversion.
   - Garage / covered parking: ±$10–40K based on market.
   - View / lot premium: submarket-specific; often larger than size adjustments.
   - Condition: ±5–15% of comp price for major condition gaps. A "good" vs. "average" gap is often 8–10%.
   - Concession: subtract any seller-paid concession (buyer closing-cost credit, rate buydown, repair credit) to arrive at the net.
   - Time: multiply by (1 + submarket monthly appreciation/depreciation × months). Only apply if the submarket actually moved that much.

3. **Produce the adjustment grid.** One row per primary comp, columns for each adjustment, ending in an adjusted sale price. This is the single most defensible artifact in the CMA; it is what a skeptical appraiser or a skeptical buyer's agent will re-derive.

4. **Diagnose the submarket.** Translate the market context into plain English using MOI:
   - **< 3 months:** Seller's market. Expect list-price or above. Pricing at the comp median typically generates multiple offers; pricing 2–3% above the median is defensible if differentiating features warrant.
   - **3–5 months:** Balanced. Expect list-price with minor concessions. Pricing at the median pulls a normal buyer pool.
   - **5–8 months:** Buyer's market. Expect price-to-list ratio under 98%; expect concession requests. Pricing 1–2% below median may be required to generate activity.
   - **> 8 months:** Soft market. Pricing must undercut the median; expect DOM > 60 days; prepare the seller for concessions on price + credit + timeline.

   State the diagnosis in one sentence with the MOI number and the expected price-to-list ratio.

5. **Build the band.** Produce three price points from the adjusted-comp set:
   - **Aggressive / top-of-band.** The "try this for 7 days" price — defensible only if the subject has features not present in the primary comps, or if MOI is below 3 and energy is rising. Risks: DOM > market median, appraisal shortfall, re-list drag.
   - **Market / middle-of-band.** The adjusted-comp median or weighted average. The default recommendation.
   - **Conservative / bottom-of-band.** The "priced to move in 14 days" price — chosen when the seller's priority is speed or clean close.

   Name the dollar figure for each, in round thousands (never 999-endings unless brokerage config says otherwise). Explain the trade-off of each in one line.

6. **Map the band to buyer pool size + expected DOM.** For each price point, state how many buyers at that band's monthly pre-qualification volume would see this home as affordable and in their search band. If MLS search data is available, pull the subscriber count in the search band; otherwise estimate from mortgage-payment math using current rate. Give the expected DOM range with a defensible rationale.

7. **Flag appraisal risk.** Compare the middle-of-band to the highest adjusted primary comp. If middle exceeds highest primary by >3%, note the appraisal-shortfall risk and recommend a pre-listing appraisal or an appraisal-gap contingency in future offers.

8. **Identify subject-property adjustments the seller controls.** A CMA without this section is half a CMA. Name 2–4 specific, pre-listing actions that would move the subject to the top of its tier (not a full renovation — small-dollar, high-signal items: paint, decluttering, a photography-grade deep clean, specific staging emphasis, fixture-level updates, a handful of landscape improvements). Pair with `listing-feature-engagement-optimizer.md` for the strategic prioritization.

9. **Draft the narrative (≤ 200 words for the listing-appointment version).** Structure: submarket diagnosis → subject's fit within the comp set → recommended band with trade-offs → what happens at each price point (DOM, buyer pool, concession expectation) → the pre-listing actions that unlock the top of the band.

10. **Draft talking-points script.** Two to four phrases the agent can read verbatim at the appointment:
    - An opener that acknowledges the seller's anchor ("I know the Zestimate is showing $1.52M, and I want to walk you through how today's data lands").
    - A data-anchor line ("Four comps sold in the last 90 days within 0.4 miles, adjusted for size, condition, and view, land at a median of $1.46M").
    - A trade-off line ("At $1.49M we'd likely see 28–45 days of DOM and a probable $10–20K concession ask at offer; at $1.46M we'd likely see under 14 days and a cleaner offer").
    - A pre-listing-action line ("There's a 2–3% lift available here — painting the primary bath, replacing the fixtures in the kitchen island, and a four-hour landscape pass before photos").

11. **Run the compliance sweep.** Scan every section for:
    - Fair-housing language (no protected-class references to buyer pool; "this home would appeal to young families" is out).
    - Representations-of-value boundary (use "market data suggests" or "the adjusted comp set supports," never "your home is worth" in writing — per NAR guidance; some states treat the latter as an implied appraisal).
    - Comparison-accuracy integrity (no invented comps; no comp outside the stated search boundary presented as a primary).
    - Brokerage disclaimer (license number, DRE/RE license in footer; some jurisdictions require "not an appraisal" language on any written CMA delivered to a client).

**Critical rules:**

- Never produce a single price point as the headline. The seller will anchor on it and negotiate from it. Always band.
- Never invent a comp. If you wouldn't put it in front of a broker, don't put it in the CMA.
- Never represent the CMA as an appraisal. Written CMAs include the "market analysis, not an appraisal" disclaimer (check `config.yml` for brokerage-preferred language).
- Never reference buyer demographics as justification. "The type of family looking here" language is fair-housing exposure.
- Never skip the adjustment grid. "Average of the three closest sales" is not a defense.
- If the seller's stated target is materially above the top of the band (>5%), the CMA opens with that gap named plainly, not buried at the bottom. Budget-softening is a negotiation-script task (route to `negotiation-script-generator.md` scenario 8).
- If fewer than 3 primary comps exist, say so and widen the net methodically (same submarket, longer time; then same price band, adjacent submarket); do not substitute tertiary comps as primary.

**Output structure (always in this order):**

1. **Executive Summary** — 2–3 sentences: subject, recommended band, expected DOM.
2. **Subject Property Profile** — table.
3. **Submarket Diagnosis** — one sentence with MOI, price-to-list ratio, direction.
4. **Comp Set Summary** — sold / active / pending, with relevance score table.
5. **Adjustment Grid** — per primary comp, full adjustments, adjusted sale price.
6. **Price Band** — aggressive / market / conservative, each with trade-off.
7. **Buyer Pool + Expected DOM** — per price point.
8. **Appraisal-Risk Flag** — if applicable.
9. **Pre-Listing Actions** — 2–4 items the seller controls.
10. **Narrative** (≤ 200 words).
11. **Talking-Point Script** — 2–4 phrases.
12. **Compliance Sweep + Disclaimers** — including the "market analysis, not appraisal" line.

## Example Output

**Executive Summary:** 4821 Laurel Canyon Blvd (Studio City, 91604) — recommended list band $1.465M–$1.485M, with $1.475M as the market recommendation. Expected DOM 14–22 days at $1.475M in a 2.1-MOI submarket; pre-listing prep can defensibly support $1.485M top-of-band.

**Subject Property Profile:**

| Field | Value |
|---|---|
| Beds / Baths / Sqft | 3 / 2.5 / 1,910 |
| Lot | 7,800 sf, flat, fenced |
| Year / Renovated | 1912 / 2019 |
| Condition | Good-to-excellent (2019 renovation) |
| Distinctive | 1912 Craftsman, original beams + arched doorways, 9.2 kW owned solar, detached 250sf office |
| HOA | None |
| School cluster | Carpenter Community Charter (verified 0.3 mi) |

**Submarket Diagnosis:** 2.1 months of inventory (tight seller's market); median price-to-list ratio 101.4% over the last 60 days; median DOM 18 days. Pricing at or slightly above the comp-median is defensible in this energy.

**Comp Set Summary:**

| # | Address | Status | Sale/List | Sqft | $/sf | DOM | Sold Date | Relevance |
|---|---|---|---|---|---|---|---|---|
| C1 | 4612 Ventura Canyon | Sold | $1.455M | 1,880 | $774 | 11 | 2026-03-22 | 46 (primary) |
| C2 | 4903 Tujunga | Sold | $1.510M | 2,005 | $753 | 17 | 2026-02-28 | 43 (primary) |
| C3 | 11614 Moorpark | Sold | $1.425M | 1,845 | $772 | 22 | 2026-03-10 | 41 (primary) |
| C4 | 4721 Carpenter | Sold | $1.590M | 2,210 | $719 | 9 | 2026-03-05 | 38 (secondary; bigger) |
| A1 | 4530 Ventura Canyon | Active | $1.525M | 1,950 | $782 | 6 | — | primary active |
| A2 | 12015 Hartsook | Active | $1.475M | 1,920 | $768 | 12 | — | primary active |
| P1 | 4818 Coldwater Canyon | Pending | $1.499M | 1,965 | $763 | 8 | — | primary pending |

**Adjustment Grid (primary sold comps):**

| Adjustment | C1 ($1.455M) | C2 ($1.510M) | C3 ($1.425M) |
|---|---|---|---|
| Base | $1,455,000 | $1,510,000 | $1,425,000 |
| Size (to 1,910 sf @ $755/sf) | +$22,650 | –$71,725 | +$49,075 |
| Condition (C1 avg → subject good) | +$75,000 | 0 | +$55,000 |
| Solar owned | +$15,000 | 0 | +$15,000 |
| Detached office (no comp has one) | +$25,000 | +$25,000 | +$25,000 |
| Time (+0.4% / month × 1–2 months) | +$5,820 | +$12,080 | +$11,400 |
| Concession adjustment | 0 | 0 | 0 |
| **Adjusted** | **$1,598,470** | **$1,475,355** | **$1,580,475** |

The adjusted primary median sits at $1.580M; the raw sold median sits at $1.455M. The gap is driven by the character/renovation/solar/office feature stack not present in any single comp. C2 is the closest feature-match and anchors the low end of the band.

**Price Band:**

| Band | Price | Rationale / Trade-off |
|---|---|---|
| Aggressive | $1.499M | Prices at the pending comp level; likely 7–14 DOM; real risk of an appraisal shortfall since no primary sold comp supports this unadjusted. Requires appraisal-gap language in offers. |
| **Market** | **$1.475M** | Anchors at C2's adjusted value and the A2 active. Expected 14–22 DOM; low appraisal risk; multiple-offer potential. |
| Conservative | $1.465M | 14-day-sale target; leaves 1% on the table but increases certainty of a clean offer without concessions. |

**Buyer Pool + Expected DOM:**

- **$1.499M:** Buyer pool at 20% down conventional with 7% rate = ~$9,980/mo PITI. Submarket monthly pre-qual pool at this payment band ≈ 38 buyers; ~12 actively searching 91604. Expected DOM 7–14; appraisal-shortfall risk ~25%.
- **$1.475M:** Payment $9,824/mo; pool ≈ 44 buyers; ~15 actively searching. Expected DOM 14–22; appraisal risk < 10%.
- **$1.465M:** Payment $9,758/mo; pool ≈ 47 buyers; ~17 actively searching. Expected DOM 10–16; appraisal risk < 5%.

**Appraisal-Risk Flag:** $1.499M sits 1.6% above highest primary adjusted ($1.580M / 1.065M ratio — above the 3% threshold for non-Craftsman comps; Craftsman-specific comp thin). Recommend appraisal-gap language in any offer at this price.

**Pre-Listing Actions (seller-controlled, 2–3 week window):**

1. **Paint the primary bath in a warm neutral; replace the vanity hardware.** ~$900. High photo-carryability; currently the only dated-feeling space in the house.
2. **Landscape pass: mulch refresh, deadhead the roses, trim the olive tree canopy.** ~$600. Enhances the Craftsman framing in the exterior hero shot.
3. **Stage the detached office studio.** ~$400 if using homeowner furniture + a rented desk. Currently under-shot in prior photography; matches the WFH buyer demand signal.
4. **Clean the solar panels + pull the 12-month production report.** Free + 20 minutes. Turns "owned solar" from a feature claim into a verifiable economics claim worth ~$15K in buyer valuation.

**Narrative (listing-appointment version, 182 words):**

> Studio City 91604 is sitting at 2.1 months of inventory — firm seller's market, homes closing at 101% of list in 18 days on average. 4821 Laurel is a strong fit for the top half of this submarket: a 1912 Craftsman with preserved character (exposed beams, arched doorways, refinished original hardwoods), a 2019 renovation (chef's kitchen, primary spa bath), 9.2 kW owned solar, and a detached 250sf office — a feature stack that none of the primary comps carry in combination.
>
> The adjusted comp set supports a recommended list band of $1.465M–$1.485M. At $1.475M we'd expect 14–22 days on market with multiple-offer potential and minimal appraisal risk. A $1.499M price is defensible only with appraisal-gap language from buyers, given that no sold primary Craftsman comp has cleared that level in the last 90 days.
>
> Three small pre-listing actions — a primary-bath refresh, a landscape pass, and staging the detached office — are worth 1.5–2% on the final price. Recommend 10 days of prep and a Thursday launch.

**Talking-Point Script:**

1. "I know the Zestimate is showing a higher number. Let me show you how four comps in the last 90 days within four blocks adjust to today's data."
2. "The comp median lands at $1.46M. Your Craftsman, the 2019 renovation, the solar, and the detached office are worth a premium — adjusted, we land at $1.475M as the market recommendation."
3. "At $1.475M you'll likely see 14–22 days on market with multiple offers. At $1.499M we'd still see interest but you're taking appraisal risk — I'd want an appraisal-gap clause in the offer."
4. "There's another 1.5–2% available with a primary-bath paint, a landscape pass, and staging the office. Three weeks of prep, about $1,900 in costs."

**Compliance Sweep + Disclaimers:**

| Check | Status |
|---|---|
| Fair-housing language / no protected-class references | Pass |
| Representation-of-value boundary ("market data suggests" / "adjusted comp set supports" language; never "your home is worth") | Pass |
| All comps verified in MLS, none invented | Pass |
| Adjustment grid present and defensible | Pass |
| Brokerage disclaimer present | Pass |
| "Market analysis, not an appraisal" disclaimer | Included |

**Disclaimer:** This market analysis is not an appraisal and should not be relied upon as a certified valuation. Prepared by [agent, DRE #license] of [brokerage] using MLS comparable sales data as of [date]. Market conditions change; the band above reflects conditions at the date of preparation.
