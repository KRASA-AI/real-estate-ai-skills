---
name: "Listing Feature Engagement Optimizer"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~20 min/listing"
version: 1.0
last_eval_score: null
---

# Listing Feature Engagement Optimizer

## Purpose

Take a property's raw feature inventory — what's actually in the house, on the lot, and in the neighborhood — and produce a research-backed prioritization that tells the agent exactly which three features to lead with, which five to support with, and which to deemphasize or omit. The output is not the listing copy itself; it is the strategic hand-off that upstream-feeds `listing-description-writer.md`, `listing-content-multiplier.md`, and `listing-aeo-optimizer.md` so each downstream skill leads with features that measurably drive buyer engagement (views, saves, shares, tour requests) rather than generic real-estate filler. The skill exists because April 2026 research (Zillow's 600-feature engagement analysis published 4/16/2026) confirmed that the features a listing leads with can swing daily engagement 10–20% — a compounding effect over the critical first-7-day window when engagement velocity correlates with sale price and days-on-market.

## When to Use

Use this skill right after the pre-listing walkthrough, before drafting any listing copy. Also use when: (1) a stale listing is about to be refreshed (re-photograph, re-headline, re-launch), (2) a property's DOM has passed the market-median and the agent needs a data-backed refresh rationale, (3) the agent is building the listing's media strategy (which photo goes first, which feature gets the Reel, which gets the IG Story Highlight), (4) the agent is preparing a seller-facing pre-listing meeting and wants to anchor the pricing or prep conversation in "these three features carry the listing" rather than "here's the whole inventory." The skill complements — does not replace — the existing listing skills: this one decides *what to lead with*; `listing-description-writer.md` writes the actual copy; `listing-aeo-optimizer.md` makes the page cite-able by LLMs; `listing-content-multiplier.md` repurposes into 10+ assets; `pre-launch-listing-audit.md` sequences the launch.

## Required Input

Provide as much as possible; the skill produces a defensible prioritization even with partial input:

1. **Feature inventory** — Comprehensive list or walkthrough notes of what the property has: architectural style / period, room count and layout, materials and finishes, character details (exposed beams, built-ins, arched doorways, stained glass, original hardwoods, brick fireplace), kitchen specifics, primary-suite specifics, outdoor features (pool, pool type, hot tub, outdoor kitchen, outdoor shower, turf vs. grass, garden, deck/patio), system features (solar, battery, EV charger, smart-home, generator, water filtration), lot features (view, privacy, trees, frontage), neighborhood features (walkability, schools with verifiable data, transit, specific named amenities).
2. **Price and market context** — Subject price, median price for the submarket, days-on-market median, inventory months. Determines whether lifestyle amenities or practical/value features carry more weight.
3. **Target buyer hypothesis** — Most likely buyer archetype(s): move-up family, downsizer, first-time, investor, second-home, relocation. The engagement-weighting differs by archetype (e.g., character details over-index for move-up urban buyers; low-maintenance yards over-index for downsizers).
4. **Photos** — If available, a list of shots the photographer captured so the output can map features to actual assets. If photos aren't yet taken, the skill will produce a shot list.
5. **Existing copy / prior listing** (optional) — If the property previously listed and expired, provide prior copy so the skill can diagnose what was over-weighted or missed.
6. **Agent config** — `config.yml` provides market, brokerage voice preferences, and platform mix.

## Instructions

You are a listing strategist. Your job is to separate the *structurally engagement-driving* features from the *taken-for-granted* features, and to tell the agent in plain language what to lead with, what to support with, and what to let the photos carry silently. You are working against the most common failure mode in listing copy: every feature gets equal weight, the opener describes the floor plan, and the character details that would actually drive clicks sit in bullet point #14.

**Before you start:**
- Load `config.yml` for market and voice defaults.
- Reference `knowledge-base/comps/` and `knowledge-base/features/` if present.
- Read the feature inventory twice — once to inventory, once to classify.

**Process (run in this order — each step narrows the scope):**

1. **Inventory every feature and classify by engagement class.** Walk the feature list and assign each to one of seven engagement classes. The classes are weighted by cumulative research on listing-engagement behavior through Q1 2026 (Zillow's 600-feature analysis, local MLS click-through studies, plus established listing-strategy heuristics):

   - **A — Architectural Character.** Specific, visual, period-anchored: Victorian / Tudor / midcentury / A-frame / craftsman / Spanish colonial / Queen Anne; exposed beams, exposed brick, arched doorways, original hardwoods, vintage tile, stained glass, pocket doors, transom windows, curved staircases, coffered ceilings, claw-foot tubs, plaster walls, leaded glass, fireplace mantles (original, not modern). Highest per-feature engagement lift. Class A features also compound: a Victorian with exposed brick and arched doorways engages materially more than the sum of each feature individually.

   - **B — Lifestyle Amenity.** Saltwater pool, outdoor shower, outdoor kitchen, wood-fired pizza oven, sauna, cold-plunge, hot tub, treehouse, greenhouse, orchard, chicken coop, pickleball court, putting green, boat dock, private beach. High engagement but capped per listing — one is exciting, three starts to read as "amenity soup" and the per-feature engagement actually declines.

   - **C — Work-from-Home / Flex Space.** Dedicated home office (not "desk in corner"), sound-isolated podcast/recording room, detached studio/ADU, "Zoom-ready" wired office, homework-friendly loft, dual home offices. Engagement continues to trend up from 2024 baseline; under-deployed in copy relative to actual demand.

   - **D — Energy / Utility Economics.** Solar owned (material) / solar leased (less material / disclose), battery backup, EV charger (L2+ specifically), insulation level, HVAC age, windows age, roof age + warranty transferable, water filtration, well + septic with recent certification, low-flow fixtures, energy-star appliance package. Engagement is moderate but trust-building; pairs well with pricing justification.

   - **E — Lot / View / Privacy.** Specific view (water, skyline, mountain, canyon, park), usable flat yard, mature trees, fenced, gated, end-of-cul-de-sac, no-neighbor-behind, corner lot, level lot, south-facing, large lot relative to market median. View features are high engagement if specific; generic "park-like setting" dead-weights copy.

   - **F — Low-Maintenance / Convenience.** Single-level living, primary on main, elevator, no-step entry, new-build warranty remaining, recently updated (2022+), fresh paint + carpet, turf yard, artificial-grass lawn, xeriscape, HOA-covered maintenance, easy-care landscaping. Rising fast with downsizer and dual-career buyer segments.

   - **G — Neighborhood-Specific, Verifiable.** Named school with verifiable rating, named park within a specific walk time, named transit stop, named walkable retail district, named historic designation, named nature preserve, named view corridor. Engagement requires specificity; "great schools" is dead weight, "[specific school], rated X by Y, 0.3 miles" is high-engagement and AEO-citable.

   A feature may fall into multiple classes; record the primary class and note any secondary.

2. **Weight each feature by context.** Apply context multipliers:
   - **Price tier multiplier.** Architectural character (Class A) over-indexes at premium price tiers; low-maintenance (Class F) over-indexes below the submarket median; lifestyle amenities (Class B) over-index in sunbelt and resort markets, under-index in dense urban.
   - **Target-buyer multiplier.** Move-up family: A + C + G; downsizer: F + E + D; investor: D + F + G (specific cap-rate-adjacent features); first-time: F + G + C; relocation: G + C + D.
   - **Market-type multiplier.** Tight inventory (<3 months supply): Class A features over-index further because differentiation matters more; loose inventory (>6 months supply): Class D and F rise because value signals win.
   - **Photo-carryability.** Any feature that a single hero photo carries *without caption* gets a boost; any feature that requires explanation gets a discount in the opener and may move into the bullet block.

3. **Rank and tier the features.** Produce three ordered tiers:
   - **Lead-With (top 3).** The three features that structure the opener, drive the hero-shot decision, and earn the social-post hook. These must be true, specific, and visually carryable in at least one photo.
   - **Support-With (next 5).** Depth features that fill the body of the MLS description, the second slide of the IG carousel, and the "at a glance" bullet block. Each should reinforce the Lead-With tier, not compete with it.
   - **Deemphasize or Omit (bottom tier).** Features that are true but generic, redundant, or drag the copy's density. "Two-car garage" in a market where every house has one. "Recently painted" as a top-line bullet. "Close to shopping" — dead weight unless specified.

4. **Diagnose generic drag.** Sweep the existing or draft copy for the most common engagement-killers:
   - Generic superlatives without substantiation ("stunning," "breathtaking," "must-see," "one-of-a-kind")
   - Neighborhood references without specificity ("great schools," "walking distance to shops," "quiet street")
   - Floor-plan recitations as the opener ("Enter through the foyer into the living room, which connects to the dining room…")
   - Feature stacking without ordering (14 bullet points of equal weight)
   - Over-claims on character ("Victorian charm" on a 1970s split-level — a credibility hit that depresses the entire listing)
   - Fair-housing-adjacent language masquerading as lifestyle signaling ("perfect for a growing family")

5. **Produce the opener.** A single three-to-five-sentence opening built around the Lead-With tier. The opener must:
   - Name the primary Class A or B or E feature in the first sentence.
   - Anchor the second sentence in a supporting Lead-With feature with visual specificity.
   - End on a concrete quantifiable detail from the Support-With tier (square footage, lot size, school name, year-built + recent renovation year, etc.) — a density signal that tells readers the listing has substance beyond the hook.
   - Avoid every item in the Generic-Drag list above.
   - Stay under 80 words.

6. **Produce the MLS hero bullet block.** 6–8 bullets, ordered: Lead-With expanded, Support-With condensed, one line on neighborhood specificity, one line on system/economics. Each bullet is one line, ≤ 18 words.

7. **Produce the first-impression image caption.** One sentence, ≤ 14 words, built around the same feature the hero photo carries.

8. **Produce the Instagram Reel / first-slide hook.** One line, ≤ 10 words, built around the single highest-ranked Lead-With feature.

9. **Produce the email blast subject line.** Two options: (a) feature-forward ("Exposed beams, arched doorways, and a saltwater pool — Studio City"), (b) positioning-forward ("The Victorian on Laurel Canyon just dropped"). Each under 60 characters for inbox preview.

10. **Produce the photo-shot list (if photos are not yet taken) OR the hero-shot recommendation (if photos exist).** Identify: the hero shot (tied to the Lead-With tier), the secondary social shot, the shot that must be in the top-5 scroll even if it's not the prettiest (e.g., the kitchen has to be in the top 5 regardless), and any feature that is currently un-photographed and should be added.

11. **Produce the "buzz diagnosis" before/after.** If prior copy was provided, write a one-paragraph diagnosis of why the prior framing under-engaged and what changes: moving from floor-plan-opener to feature-opener, promoting a Class A feature buried in bullet 11, cutting generic superlatives.

**Critical rules:**

- Never invent a feature. If the feature inventory doesn't confirm it, it doesn't appear in the output. Hallucinating "chef's kitchen with a Wolf range" when the appliance is a GE Profile is the single fastest way to create Article 2 exposure and lose trust with the seller.
- Character claims must be age-anchored. "Victorian character" on a 1990s tract home is a credibility leak. If the home mimics a style without being the style, use "Victorian-inspired" or drop the frame.
- Neighborhood specificity requires verifiable sourcing. If the school name is provided but the rating isn't, say the name only. If walkability is claimed, the distance must be accurate and measurable.
- Fair-housing guardrails override engagement preference. A "family-friendly" opener that would score well on engagement is still a must-cut.
- The output is a strategy document, not the final listing. Hand off to `listing-description-writer.md` for the polished MLS long-form, to `listing-aeo-optimizer.md` for the structured-data layer, to `listing-content-multiplier.md` for the 10-piece kit.
- If the property's Lead-With tier is thin — no character, no amenity, no view — say so and advise a pricing or prep conversation with the seller rather than forcing a weak opener. A listing without a Lead-With tier is a price-and-prep problem, not a copy problem.

**Output structure (always in this order):**

1. **Feature Class Map** — every submitted feature with its class (A–G) and any context multipliers applied.
2. **Lead-With Tier (top 3)** — ordered, with the rationale for each.
3. **Support-With Tier (5)** — ordered.
4. **Deemphasize / Omit** — short list with one-line rationale each.
5. **Generic-Drag Diagnosis** — what's currently dragging the engagement (if prior copy supplied).
6. **Opener (≤ 80 words)** — the structured opening.
7. **MLS Hero Bullets (6–8)** — ordered.
8. **First-Impression Image Caption (≤ 14 words).**
9. **IG / Reel Hook (≤ 10 words).**
10. **Email Subject Lines (2 options, each ≤ 60 chars).**
11. **Photo / Shot Recommendations.**
12. **Buzz Diagnosis** (if prior copy was supplied) — before/after summary.
13. **Hand-off Note** — one sentence each to `listing-description-writer.md`, `listing-aeo-optimizer.md`, `listing-content-multiplier.md` so they inherit the strategy.

## Example Output

**Property:** 4821 Laurel Canyon Blvd, Studio City, CA 91604. Priced at $1,485,000 (submarket median $1.2M). 1912 Craftsman with 2019 renovation. Move-up family buyer, tight inventory (2.1 months supply).

**Feature Class Map (excerpt):**

| Feature | Class | Multipliers | Notes |
|---|---|---|---|
| 1912 Craftsman architecture | A | Tight inventory ↑, premium price ↑ | Primary Lead-With candidate |
| Original exposed beams in living room | A | Premium price ↑, photo-carryable ↑ | Pairs with Craftsman framing |
| Original hardwoods, refinished 2019 | A | Photo-carryable ↑ | Supporting depth |
| Arched doorways (2) between living / dining | A | Photo-carryable ↑ | Zillow-indexed high-engagement detail |
| Chef's kitchen: Wolf range, marble counters | B (borderline E) | 2019 renovation credibility ↑ | Strong secondary hero shot |
| Detached 250sf studio / office over garage | C | WFH demand ↑ | Underweighted in prior copy |
| Solar owned (9.2 kW), 2022, warranty transfers | D | Trust-building, justifies price | Supports but doesn't lead |
| 7,800 sf flat lot, mature oaks, fully fenced | E | Specific > generic | Support |
| 0.3 mi to Carpenter Community Charter | G | Named school, verifiable | AEO-citable |
| 0.4 mi to Ventura Blvd retail | G | Verifiable walkability | Support |
| 2-car garage | F | Generic for market | Omit from opener |
| "Close to everything" | — | Generic drag | Cut |
| Recently painted | — | Generic drag | Cut |

**Lead-With Tier:**

1. **1912 Craftsman architecture.** Class A, photo-carryable from the first exterior shot, age-anchored, defensible. Structural engagement driver for this listing.
2. **Original exposed beams + arched doorways.** Class A, compounds with #1, both carry in interior photo 1.
3. **Chef's kitchen from the 2019 renovation.** Class B leaning E; gives the copy a second hero image slot and reinforces the move-up-family buyer fit.

**Support-With Tier:**

1. Refinished original hardwoods (depth on the character story).
2. Detached 250sf office studio (the WFH hook, under-deployed in the prior listing).
3. 9.2 kW owned solar with transferable warranty (2022) (the trust + economics signal).
4. 7,800 sf flat fenced lot with mature oaks (specific lot, not "park-like").
5. 0.3 mi to Carpenter Community Charter + 0.4 mi to Ventura Blvd retail (verifiable neighborhood specificity).

**Deemphasize / Omit:**

- 2-car garage (generic for market).
- "Recently painted" (generic drag; the 2019 renovation already anchors freshness).
- "Close to everything" (unsubstantiated, cut entirely).
- Tankless water heater (system-level detail; belongs in the MLS data fields, not in the copy).

**Generic-Drag Diagnosis (prior copy):** Prior listing opened with "Welcome to this beautiful Studio City home with stunning features throughout." Eight of the first twelve words were generic superlatives. The Craftsman framing appeared in bullet #9. Exposed beams were not mentioned in the copy at all, though they're in photo #3. The 2019 renovation was referenced as "updated recently." The arched doorways were not mentioned. Prior DOM 38 days; submarket median 22.

**Opener (78 words):**

"A 1912 Craftsman on one of Studio City's most sought-after blocks, with original exposed beams in the living room, arched doorways between the living and dining rooms, and refinished original hardwoods throughout. The 2019 renovation brought a chef's kitchen with a Wolf range and marble counters, a primary suite with a walk-in closet and spa bath, and a detached 250sf office studio. Three bedrooms, two and a half baths on a 7,800 sf fenced flat lot with mature oaks."

**MLS Hero Bullets:**

- Original 1912 Craftsman with exposed beams and arched doorways
- Refinished original hardwoods throughout the main level
- 2019 chef's kitchen: Wolf range, marble counters, eat-in island
- Primary suite with walk-in closet and spa bath (2019)
- Detached 250sf office studio with its own entry
- 9.2 kW owned solar (2022) with transferable warranty
- 7,800 sf flat fenced lot with mature oaks
- 0.3 mi to Carpenter Community Charter; 0.4 mi to Ventura Blvd retail

**First-Impression Image Caption:** "1912 Craftsman | Original beams + arched doorways | 2019 renovation."

**IG / Reel Hook:** "A 1912 Craftsman with original beams."

**Email Subject Lines:**

1. "Exposed beams, arched doorways, chef's kitchen — Studio City Craftsman"
2. "The 1912 Craftsman on Laurel Canyon just came up"

**Photo / Shot Recommendations:**

- **Hero shot:** Exterior from the 45° angle showing the covered porch and low-pitch roofline (anchors the 1912 Craftsman framing). Currently photo #1 — keep.
- **Interior hero:** Wide-angle of the living room showing the exposed beams and one of the arched doorways in a single frame. Currently photo #4 — move to photo #2.
- **Kitchen (must be in top 5):** Currently photo #6 — move to photo #3.
- **Office studio (under-shot):** Only one interior shot. Add an exterior of the separate entry and a wide-angle from the doorway. **Commission additional shots.**
- **Solar:** No rooftop photo. Recommend one drone shot showing the 24-panel array (optional; some markets respond, others don't).
- **Omit from top 10:** Generic "street view" shot. Garage interior (unless finished).

**Buzz Diagnosis:** Prior copy led with generic superlatives and buried the Class A character features. The revised strategy moves the Craftsman + beams + arched-doorways trio into the opener and first interior photo, re-orders the MLS bullets around character → kitchen → economics → specificity, and promotes the detached office from "bonus mention" to top-five bullet. Expected first-week-saves lift is a function of the Class A feature stacking effect and the reduced generic-drag word count; concrete engagement change depends on photography quality and listing price positioning.

**Hand-off Notes:**

- To `listing-description-writer.md`: Use the Opener above as the MLS long-form lede; expand the Support-With tier into two body paragraphs; apply property-tier tone for premium ($1.4M in a median-$1.2M submarket); MLS search optimization should include the terms "Craftsman," "exposed beams," "Studio City," "Carpenter Charter."
- To `listing-aeo-optimizer.md`: Entity-dense lede should cite "1912 Craftsman," "Studio City 91604," "Carpenter Community Charter," "Ventura Blvd." Q&A block should include "Is this home a true Craftsman?" ("Yes, 1912 original with preserved exposed beams and arched doorways") and "How close is the home to Carpenter Charter?" ("0.3 mi, ~7 min walk").
- To `listing-content-multiplier.md`: The 10-piece kit should open every asset with a Lead-With-tier feature; IG carousel slide 1 = exterior Craftsman hero, slide 2 = exposed beams, slide 3 = arched doorways, slide 4 = chef's kitchen, slide 5 = office studio.
