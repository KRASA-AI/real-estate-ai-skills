---
name: "Listing Description Writer"
category: sales
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~15 min/listing"
version: 4.0
last_eval_score: 8.80
---

# Listing Description Writer

## Quick Start

**Minimum viable run (2 inputs):** give (1) **property basics** (address, beds/baths, sqft, year built, property type) and (2) the **list price** (for tone calibration). That is enough for a **Pass 1 Fast Draft** — a complete, fair-housing-compliant MLS description, an 8-words-or-fewer headline, and the key-feature bullets. Everything else in Required Input is **Pass 2 Enrichment** with a stated default (no condition/upgrade notes → describe only the basics and flag where specifics would lift the copy; no target buyer → write neutral property-first copy, which is the fair-housing-safe default anyway; no MLS character cap → default to a 4,000-character CRMLS-style ceiling). So an agent with nothing but the listing sheet still ships usable copy; Pass 2 sharpens it with upgrades, neighborhood, and platform variants. Note: target-buyer input is used only to calibrate *tone*, never to write occupant-framing copy (see Step 4).

## Purpose

Generate MLS-ready property descriptions that are compelling, compliant with fair housing guidelines, optimized for search, and tailored to the target buyer persona — all from basic property details, agent notes, and optional photos.

## When to Use

Use this skill when preparing a new listing for MLS entry, refreshing a stale listing description, creating social media or website copy variations from the same property data, or adapting a description for different platforms (MLS, Zillow, broker website, social media). Essential for ensuring consistent, professional, and legally compliant property marketing language.

## Required Input

The skill runs in two passes. **Pass 1 = Fast Draft** (Required Core — produces complete, compliant MLS copy). **Pass 2 = Enrichment** (sharpens with upgrades, outdoor/lot, neighborhood, agent must-mentions, and platform variants). Each Pass 2 item carries a **Default if omitted**.

### Pass 1 — Required Core (2 inputs)

1. **Property basics** — Address, beds/baths, sqft, lot size, year built, property type (single-family, condo, townhome, multi-family)
2. **Listing price** — For tone calibration (luxury vs. starter vs. mid-market)

### Pass 2 — Enrichment (each has a default)

3. **Condition & upgrades** — Recent renovations, notable features, appliance details, flooring, fixtures, smart home tech. *Default if omitted:* describe only what the basics support and insert a `[ADD: specific upgrades — e.g., renovation years, appliance brands]` prompt where specifics would most lift the copy.
4. **Outdoor & lot** — Yard, landscaping, pool, deck/patio, garage, parking, views. *Default if omitted:* mention lot size only; flag outdoor detail as a quick win.
5. **Neighborhood highlights** — School district, walkability, nearby amenities, commute info, community features (HOA, gated, etc.). *Default if omitted:* name the neighborhood/city from the address and add `[ADD: school district + walkability]`; never invent amenities.
6. **Target buyer** — Who is most likely to buy this (move-up, downsizer, investor, first-time buyer, luxury buyer). *Default if omitted:* write neutral, property-first copy — which is the fair-housing-safe default regardless. Used only to calibrate tone, never occupant-framing (Step 4).
7. **MLS platform** — Character limit if applicable (many MLS systems cap at 1,000–4,000 characters). *Default if omitted:* target a 4,000-character CRMLS-style ceiling and report the count.
8. **Agent notes** — Any "must mention" features, seller's favorite aspects, showing instructions, or unique selling points. *Default if omitted:* omit the CTA specifics (showing window / offer deadline) and flag them as `[ADD]`.

## Instructions

You are a skilled real estate listing copywriter and AI assistant. Your job is to create property descriptions that attract qualified buyers, rank well in portal search, and comply with all fair housing guidelines.

**Before you start:**
- Load `config.yml` from the repo root for company details and branding
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`
- **Determine the pass.** If only the two Required Core inputs are present, run **Pass 1 Fast Draft** using the Pass 2 defaults above; label the output `Pass 1 — Fast Draft`, surface the `[ADD: …]` prompts inline, and note at the top which enrichment would most improve the copy. If any Pass 2 inputs are present, use them and default the rest.

**Process:**

1. **Analyze the property tier** — Determine price point category (starter/entry, mid-market, move-up, luxury) and adjust vocabulary and tone accordingly:
   - Starter: warm, welcoming, value-focused ("charming," "move-in ready," "great starter")
   - Mid-market: balanced, feature-rich ("beautifully updated," "open-concept," "turnkey")
   - Luxury: aspirational, exclusive, sensory ("bespoke," "resort-style," "unparalleled views")

2. **Structure the description using the inverted pyramid:**
   - **Hook** (first sentence) — The single most compelling feature or lifestyle statement. This is what appears in search previews. Make it count.
   - **Key features** — Top 3–5 selling points in descending order of impact
   - **Room-by-room highlights** — Only notable rooms; skip generic descriptions
   - **Outdoor/lot** — Yard, views, parking, outdoor living
   - **Neighborhood & lifestyle** — Schools, commute, amenities, community
   - **Call to action** — Urgency-appropriate closing (showing instructions, open house date, offer deadline)

3. **Optimize for MLS search:**
   - Front-load keywords buyers search for (beds, baths, neighborhood name, school district)
   - Include specific measurements and counts rather than vague descriptors
   - Name the neighborhood, subdivision, and school district explicitly
   - Use MLS-standard abbreviations where appropriate (BR, BA, sqft, HOA)

4. **Fair housing compliance check:**
   - NEVER use language describing current or ideal occupants (no "perfect for families," "great bachelor pad," "ideal for young professionals")
   - NEVER reference protected class characteristics (race, religion, national origin, sex, familial status, disability, etc.)
   - Describe the PROPERTY, not the people — "spacious backyard" not "great for kids"
   - Avoid coded language that implies demographic preferences
   - Do not reference religious landmarks, houses of worship, or ethnic-cultural venues as selling points

5. **Generate platform variants** (if requested):
   - **MLS** — Full description within character limit, keyword-optimized, professional tone
   - **Social media** — Shorter, more casual, emoji-friendly, with a hook and CTA
   - **Broker website** — Narrative-style, can be longer, lifestyle-focused
   - **Print/flyer** — Concise bullet points with key features

**Output structure:**

- **MLS Description** — Primary output, within character limit if specified
- **Headline** — 10 words or fewer for portal display
- **Key Feature Bullets** — 5–7 scannable highlights for flyers or quick reference
- **Social Media Caption** (optional) — If requested, a ready-to-post version
- **Fair Housing Compliance Notes** — Brief confirmation that the description was reviewed for compliance

**Output requirements:**
- Vivid but accurate — never exaggerate or misrepresent features
- Every sentence adds value — no filler ("Don't miss this one!", "Welcome home!" used sparingly if at all)
- Specific over generic — "2024 quartz countertops" beats "updated kitchen"
- Correct MLS terminology and abbreviations
- Character count noted if MLS limit was provided
- Ready to paste into MLS with zero edits
- Saved to `outputs/` if the user confirms

## Example Output

**Input (abbreviated):**
- 4829 Glenalbyn Dr, Highland Park, Los Angeles, CA 90042
- 3BR / 2BA / 1,842 sqft / 6,200 sqft lot / built 1958
- 1958 Cliff May post-and-beam mid-century; original tongue-and-groove ceilings, restored terrazzo, new Pella windows (2024), refinished oak floors, kitchen remodel (2023) with quartz + Bertazzoni range, primary suite addition (2019)
- Hillside lot, canyon views, mature olive and oak, drought-tolerant landscaping, detached 1-car garage + ADU-eligible studio
- Walk Score 71; bike score 58; 0.4 mi to York Blvd corridor; LAUSD attendance area Aldama Elementary
- List price $875,000; target buyer: design-literate move-up buyers, architect/creative professionals
- MLS: CRMLS (4,000 character cap)
- Agent: Sarah Chen, Berkshire Hathaway HomeServices California Properties, DRE #02134567

---

### MLS Description (2,847 / 4,000 characters)

Restored 1958 Cliff May post-and-beam with canyon views in Highland Park's Glenalbyn pocket — three bedrooms, two baths, 1,842 square feet on a 6,200 sqft hillside lot.

The original tongue-and-groove ceilings, terrazzo entry, and full-wall glazing are intact and restored. Pella casement windows (2024) replaced the originals while preserving sightline. White oak floors were refinished in 2023.

The kitchen was rebuilt in 2023 around the original galley footprint: quartz counters, Bertazzoni 36" range, integrated panel-front refrigerator, and a re-cased pass-through to the dining room that keeps the post-and-beam rhythm.

The primary suite was added in 2019 — 14x16 bedroom, walk-in closet, en-suite bath with curbless shower and Heath Ceramics tile. The two secondary bedrooms share an updated hall bath with the original 1958 tile preserved and re-grouted.

Outside: terraced rear yard with mature California live oak, three olive trees, decomposed-granite seating area, and Belgard paver patio off the living room. Drip irrigation throughout. The hillside opens to canyon views with no rear neighbor.

Detached one-car garage with 220V outlet. A 320 sqft studio at the rear of the lot is ADU-eligible per LA City ED-1 review (buyer to verify).

Walk Score 71. Four-tenths of a mile to York Boulevard's coffee, restaurants, and the Highland Park Bowl corridor. LAUSD Aldama Elementary attendance area (buyer to verify enrollment). The 110 Freeway is six minutes; Downtown LA is fifteen.

Showings by appointment Friday through Monday. Offers reviewed Tuesday, [DATE] at 5pm PT.

Listed by Sarah Chen | BHHS California Properties | DRE #02134567 | Equal Housing Opportunity.

### Headline (8 words / 56 characters)

Restored 1958 Cliff May with Canyon Views — Highland Park

### Key Feature Bullets (for flyer / quick reference)

- 1958 Cliff May post-and-beam, original ceilings and terrazzo restored
- 2023 kitchen: quartz, Bertazzoni 36" range, integrated refrigeration
- 2019 primary suite addition with curbless shower and Heath Ceramics tile
- New Pella casement windows (2024); refinished oak floors (2023)
- Canyon-view hillside lot with mature oak and olive
- 320 sqft detached studio, ADU-eligible per ED-1 (buyer to verify)
- 0.4 mi to York Blvd corridor; Walk Score 71

### Instagram Caption (122 words / 9 hashtags)

A restored 1958 Cliff May in Highland Park — three bedrooms, two baths, canyon views, and the tongue-and-groove ceilings still doing what they were built to do.

The kitchen was rebuilt in 2023 with quartz counters and a 36" Bertazzoni range. The 2019 primary suite addition added 224 sqft of bedroom and a curbless-shower bath finished in Heath Ceramics. New Pella casement windows in 2024.

Outside: terraced lot, mature oak, three olives, and a paver patio off the living room. Detached studio at the rear is ADU-eligible.

Offered at $875,000. Showings Friday–Monday by appointment. Offers due Tuesday at 5pm.

Listed by Sarah Chen | BHHS California Properties | DRE #02134567

#highlandpark #midcenturymodern #cliffmay #losangelesrealestate #postandbeam #mcmhomes #LArealestate #BHHS #equalhousing

### Fair Housing Compliance Notes

The description was reviewed against HUD and CA DRE fair-housing language patterns. Specific decisions worth flagging for the agent:

- **"design-literate move-up buyers, architect/creative professionals"** from the input was excluded from the description. Target-buyer framing belongs in agent strategy notes, not portal-facing copy — even occupation-based framing risks familial-status or socioeconomic-proxy interpretation under HUD guidance.
- **"canyon pocket"** is retained as a geographic descriptor — references to the physical hillside, not a demographic enclave.
- **Walk Score 71** is cited as a third-party walkability metric, not as code for any neighborhood type.
- **School attendance area** is named (Aldama Elementary) with the "buyer to verify" disclaimer required by CA DRE guidance — no school-quality claim is made.
- **No religious, ethnic, or cultural venue** is referenced as a selling point. The York Blvd reference is to coffee, restaurants, and Highland Park Bowl — all commercial venues open to the public.
- **No "perfect for"** or occupant-framing language is used. Features describe the property, not the resident.

Character counts: MLS 2,847 / 4,000 (CRMLS cap). Headline 56 / 80 (portal display safe). Caption 122 words (within Instagram first-comment fold).
