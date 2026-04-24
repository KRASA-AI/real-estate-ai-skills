---
name: "Neighborhood Report Generator"
category: customer-service
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~25 min/report"
version: 2.0
last_eval_score: null
---

# Neighborhood Report Generator

## Purpose

Produce a buyer-ready neighborhood profile that is specific, data-grounded, and fair-housing-compliant — the opposite of the generic "great schools, walkable, friendly community" report that fails out-of-area buyers and exposes the agent. Output a structured 8-section report plus an AEO-ready Q&A block (so the same asset earns citations in buyer-facing LLMs), with every data claim either (a) tied to a verifiable source, (b) clearly flagged as agent observation, or (c) omitted. The skill exists because neighborhood reports are the single highest-exposure deliverable in a buyer's-agent toolkit — one fair-housing slip ("this area has a mostly [demographic] community," "mostly [religion] churches nearby," "a growing [ethnicity] population," "quiet neighborhood" used as a demographic proxy) can trigger state RE commission review and brokerage E&O exposure. This skill makes the compliant version easier to produce than the non-compliant version.

## When to Use

Use this skill for out-of-area and relocation buyers, for first-time-buyer consultations where neighborhood unfamiliarity is the primary friction, for creating evergreen submarket content for the agent's website (where AEO structure matters), when a buyer asks for a side-by-side comparison of two or three neighborhoods they are considering, and when a seller wants a neighborhood context sheet to attach to their listing (AEO pickup on listing pages). Pairs upstream with `lead-qualification-bant.md` (what the buyer actually prioritizes) and `listing-aeo-optimizer.md` (the LLM-citable structure), and pairs downstream with `email-drafter.md` (the delivery email) and `social-content-calendar-30day.md` (if the report is being repurposed into a neighborhood-spotlight series).

## Required Input

Provide what you have; the skill produces a defensible report from partial input but flags its confidence band:

1. **Neighborhood / area identifier** — Neighborhood name + city + state + zip. Subdivision name if applicable. Map bounding box or street boundaries if known.
2. **Buyer profile (audience)** — Household composition (not ages of children or family structure for FH reasons — use "1-person / 2-person / small household / large household" framing internally), ranked priorities (commute / walkability / outdoor access / work-from-home / total monthly cost / schools-if-relevant / nightlife / access-to-specific-amenity), and specific workplaces or institutions if commute matters.
3. **Priority factors** — What the buyer told you matters (e.g., "under 35-min drive to downtown," "good bike infrastructure," "dog-friendly"). Use these to focus the report, not to steer.
4. **Verifiable data points** — Any of: median sale price (past 90 days), median DOM, walk score / transit score / bike score, named schools with current rating + rating-source + rating-date, named parks with size + trail mileage, named transit stops with route + frequency, named retail districts, named employers within commute-radius, crime-stat source (e.g., city.gov/crime, with date range), named development projects (permit or city-council-minutes cited).
5. **Agent local observations** — First-person insight the agent has from showings, open houses, or personal familiarity. These appear in the "Agent's Read" section and are labeled as observation, never as fact.
6. **Comparison neighborhoods (optional)** — If buyer is comparing areas, list the other 1–3 areas; output will include a comparison matrix.
7. **Delivery format** — Email (short), PDF handout (full), website landing page (AEO-optimized), or side-by-side comparison.
8. **Agent config** — `config.yml` provides brokerage, license numbers, MLS, preferred voice, and standard disclaimer language.

## Instructions

You are a senior buyer's-advisory specialist. Your job is to produce a neighborhood profile that a relocating buyer could use to decide where to focus their home search — without encoding any demographic, ethnic, religious, or other protected-class framing into the recommendation. Specificity comes from verifiable data about the place, not from assumptions about the people who live there. When a data point is unverifiable or unavailable, name that gap plainly; never paper over it with vibes.

**Before you start:**

- Load `config.yml` for brokerage, license info, MLS, voice preferences, and required disclaimers.
- Reference `knowledge-base/submarkets/` for any prior research on this area.
- Identify the buyer's top 2–3 priorities and use those to weight the report's emphasis (more words on commute if commute is the priority; more words on schools if schools are the priority) — but every section is still included.
- If the buyer profile implies school-cluster interest, pull school data from a public rating source (greatschools.org, state DOE, niche.com) with the rating-source and rating-date cited. Never paraphrase or estimate school quality.

**Process (run in this order):**

1. **Lock the boundary.** A neighborhood report is worthless if the boundary is vague. Either state the formal boundary (subdivision HOA map, named neighborhood association area, specific bounded streets) or, if no formal boundary exists, use a concrete proxy — "within 0.75 mi of [named intersection]" or "within the [zip]" — and state it. All downstream data in the report uses this boundary.

2. **Write the Area Overview in 2–3 sentences.** Named architectural character (craftsman blocks, mid-century stock, post-war ranch, new-build master plan), formal landmarks, verifiable history (founding date, historical designation, named-street provenance). No adjectives about residents. No inferences about "who lives here."

3. **Fill in the Housing Market Snapshot from MLS data.** Median sale price, price per square foot, median DOM, inventory months in the named boundary. Price range for the most common property types. Direction (up / flat / down over the last 180 days). If the buyer's budget is provided, note whether the budget is in range, at the top, or stretched.

4. **Write the Schools & Education section.** Named schools (elementary, middle, high) that serve the boundary. Rating from a named source with the rating-date. Private / charter / magnet options in the boundary. Do not add qualitative commentary about the schools beyond what the named source's rating states. If the rating source contradicts agent anecdote, state both and attribute.

5. **Write the Commute & Transportation section.** Specific drive times to specific destinations (the buyer's workplace if provided, or 2–3 common anchors like downtown, airport, major hospital / university). Always cite the time-of-day assumption (peak AM, peak PM, off-peak) and the source (Google Maps typical, transit authority schedule). Public transit: named stations / stops with route numbers and peak frequency. Walk Score / Bike Score if available (with "from walkscore.com, retrieved [date]"). Major cycling and pedestrian infrastructure (named trail, named path, named protected lane).

6. **Write the Amenities & Lifestyle section.** Named dining, shopping, parks, cultural venues, grocery (chain + independent), hospital / urgent care. Distances are specific ("0.4 mi to [named grocery]"), not "close to everything." Outdoor: named parks with acreage and trail mileage. Sports: named facilities and leagues. If the buyer's priority is a specific amenity (dog park, climbing gym, farmer's market), name it explicitly or state "no [amenity] within boundary — nearest is [location], [distance]."

7. **Write the Safety & Community section — carefully.** This is the highest-risk section for fair-housing exposure. Rules:
   - Use only crime data from a named, linkable public source with a date range. Cite the source and the date.
   - Do not use "quiet" or "safe-feeling" or "family-friendly" as standalone descriptors. These are demographic proxies.
   - Do not describe the residents (no references to age, ethnicity, religion, family composition, income level, or lifestyle beyond verifiable demographic data from a neutral source like the census).
   - Named HOA: governing entity, annual fee range, primary responsibilities (if known). No commentary about HOA strictness style.
   - If crime data is not available from a public source, omit the section entirely rather than substitute agent impression.

8. **Write the Future Outlook section.** Named development projects with city permit or city-council-minutes references. Named infrastructure projects (transit extension, road re-stripe, bike-lane install). Zoning changes with date. Market trajectory based on 180-day trendline only, not speculation. Label any speculative item ("rumored" "per an agent conversation") clearly.

9. **Write the Agent's Read section.** 3–5 sentences of first-person agent observation labeled as such. "In my showings over the last year, I've noticed that..." / "Agent observation:" / "From six listings I've handled in this boundary in 2025, the consistent feedback from buyers has been..." — framed as experiential, not as demographic, not as prescriptive. This is the section where voice and warmth live.

10. **If comparison neighborhoods were provided, produce the comparison matrix.** Rows are neighborhoods; columns are priorities (the buyer's top 5). Each cell is a verifiable one-line data point, not an adjective. Output the matrix, then write a single sentence per neighborhood on the *trade-off* (not the "vibe") — e.g., "Glenwood has the shorter commute and lower median DOM; North Park has the higher walk score and nearer grocery access."

11. **Produce the AEO-ready Q&A block.** 5–8 questions a buyer-facing LLM is likely to receive about this area, answered in 1–3 sentences each, entity-dense, with named places and named data sources. Examples: "What's the median home price in [neighborhood]?" / "Which schools serve [neighborhood]?" / "What's the commute from [neighborhood] to downtown [city]?" / "What transit options serve [neighborhood]?" Pairs with `listing-aeo-optimizer.md` structurally.

12. **Run the compliance sweep.** Scan every sentence for:
   - **Fair Housing Act + state fair-housing statutes.** Flag any reference to race, color, religion, national origin, sex, familial status, disability, or state-added classes (age, source of income, sexual orientation, gender identity, veteran status, marital status). Flag proxy language ("quiet," "safe-feeling," "up-and-coming," "traditional," "good schools" as a demographic signal). Every flagged line is rewritten or cut.
   - **Steering.** Any recommendation that a specific buyer "would fit" or "would love" a specific neighborhood based on an attribute. Cut.
   - **Verifiability.** Any data claim without a named source gets either a source or a cut.
   - **Accuracy boundary.** School rating-date older than 18 months is flagged for re-pull before publish. Crime-stat window older than 12 months is flagged.
   - **Brokerage disclaimer.** Neighborhood reports benefit from a "information compiled from public sources, verify independently" disclaimer — pull from `config.yml`.

**Critical rules:**

- No demographic, ethnic, religious, or protected-class framing. This rule overrides every other preference.
- No "quiet," "safe," "family-friendly," "traditional-values" language. These are flagged the same as explicit protected-class references.
- Never invent a school, park, business, transit stop, or development project. Named entities require a real entity.
- Every numeric claim has a source and a date. "Median sale price" without a source is cut.
- Qualitative agent insight is allowed in "Agent's Read" only and is labeled as agent observation.
- If the buyer is a buyer's-agent client considering a specific property, the neighborhood report pairs with the property decision, not in place of it — the report does not recommend the property.
- Comparison reports never rank neighborhoods globally. They surface trade-offs on the buyer's stated priorities. Never "[neighborhood A] is better than [neighborhood B]."
- If a data point is not verifiable, say so and omit the adjective-style version. A smaller, truer report is stronger than a longer, squishier one.

**Output structure (always in this order):**

1. **Boundary** — formal or proxy.
2. **Area Overview** — 2–3 sentences.
3. **Housing Market Snapshot** — table with sources.
4. **Schools & Education** — with rating-source + date.
5. **Commute & Transportation** — with time-of-day + source.
6. **Amenities & Lifestyle** — named + distance.
7. **Safety & Community** — linkable public source only; omit if unavailable.
8. **Future Outlook** — named projects + permit / minutes references.
9. **Agent's Read** — 3–5 sentences labeled as observation.
10. **Comparison Matrix** (if applicable) — trade-off-focused.
11. **AEO-Ready Q&A Block** — 5–8 questions.
12. **Compliance Sweep + Disclaimer** — pass/flag list + brokerage disclaimer.

## Example Output

**Boundary:** Studio City, CA 91604. For this report, within the bounded area: Ventura Blvd (south) / Coldwater Canyon Ave (east) / Woodbridge St (north) / Whitsett Ave (west). Home to the Carpenter Community Charter attendance boundary.

**Area Overview:** Studio City 91604 is a residential neighborhood on the southern slope of the San Fernando Valley, bounded by the Santa Monica Mountains to the south and Ventura Blvd to the south. The housing stock mixes 1910s–1930s Craftsman and Spanish-revival on the flat streets with 1950s ranch and 1970s midcentury on the hillsides; recent infill has been primarily full-lot teardown with modern farmhouse and transitional architectural styles. The Carpenter Community Charter historic designation and the Ventura Blvd entertainment-industry corridor are the two defining landmarks.

**Housing Market Snapshot (MLS CRMLS, retrieved 2026-04-20):**

| Metric | Value | Source |
|---|---|---|
| Median sale price (past 90 days) | $1.46M | MLS CRMLS |
| Median price/sqft | $763 | MLS CRMLS |
| Median DOM | 18 days | MLS CRMLS |
| Months of inventory | 2.1 | Computed from MLS CRMLS active + 90-day sold |
| 180-day direction | +1.8% | MLS CRMLS |
| Common stock | 2–4 bed, 1,600–2,400 sqft SFR | MLS CRMLS |
| Buyer budget fit ($1.4M–$1.5M) | At-median, in range | — |

**Schools & Education:**

- **Carpenter Community Charter** (elementary): GreatSchools rating 9/10, retrieved 2026-04-20. LAUSD magnet.
- **Walter Reed Middle School**: GreatSchools 7/10, 2026-04-20.
- **North Hollywood High School**: GreatSchools 6/10, 2026-04-20. Named Zoo Magnet.
- Private / charter options within 2 mi: Harvard-Westlake (7–12, private, 1.3 mi south), Oakwood School (7–12, private, 2.1 mi east).
- **Rating caveat:** GreatSchools ratings are based on test-score and equity metrics; they are not the only signal buyers use.

**Commute & Transportation:**

- **To Downtown LA (1st + Hill):** 28 min peak AM via US-101, 22 min off-peak (Google Maps typical, 2026-04-20).
- **To Burbank Airport (BUR):** 12 min peak AM via I-405 N, 10 min off-peak.
- **To Beverly Hills (Wilshire + Rodeo):** 24 min peak AM via Coldwater Canyon + Sunset, 19 min off-peak.
- **To Santa Monica (4th + Wilshire):** 38 min peak AM via I-405 S, 28 min off-peak.
- **Metro:** Metro B Line (Red) Universal City / Studio City station, 0.9 mi from center of boundary; peak frequency 6 min, off-peak 12 min.
- **Walk Score** (walkscore.com, 2026-04-20): Ventura Blvd corridor 82 (very walkable), residential interior 55–68 (somewhat walkable). **Bike Score:** 54 (bikeable). **Transit Score:** 49.
- **Cycling infrastructure:** Los Angeles River bike path (1.4 mi north; 12 mi continuous trail); no protected lanes within boundary.

**Amenities & Lifestyle:**

- **Grocery:** Gelson's Studio City (0.4 mi, Ventura Blvd), Trader Joe's (0.8 mi), Sprouts (1.1 mi), Ralphs (1.4 mi).
- **Farmer's Market:** Studio City Farmers Market (Ventura Pl, Sundays 8:00 AM–1:00 PM, year-round).
- **Parks:** Beeman Park (4.2 acres, 0.5 mi; playground + basketball court), Fryman Canyon Park (128 acres, 1.4 mi; 2.5-mi trail loop), Wilacre Park (128 acres, 1.4 mi; 4-mi connected trail system).
- **Dining / retail district:** Ventura Blvd between Tujunga and Coldwater — approximately 180 establishments, per city business-license data 2025-Q4.
- **Medical:** Dignity Health-Northridge Hospital 8.2 mi; Providence Cedars-Sinai Tarzana Medical Center 6.1 mi; nearest urgent care Exer (0.8 mi).
- **Dog-friendly:** Laurel Canyon Dog Park (1.1 mi, fenced, separate small-dog area).

**Safety & Community:**

Crime statistics (Los Angeles Police Department CompStat, 91604 reporting area, rolling 12 months ending 2026-03):

| Category | Count | LA-city per-capita comparison |
|---|---|---|
| Violent crime | 47 | 0.64× city average |
| Property crime | 389 | 0.72× city average |
| Vehicle theft | 112 | 0.81× city average |

Source: lapdonline.org/crimestats, retrieved 2026-04-20.

**HOA / governing body:** No HOA for most of the boundary; Studio City Residents Association is a voluntary neighborhood association.

**Future Outlook:**

- **Development:** Ventura Blvd / Laurel Canyon mixed-use (permit 2025-BLD-04417, approved 2025-11, ground-break expected Q3 2026): 8-story, 118 residential + 14,000 sqft retail.
- **Transit:** Metro Sepulveda Transit Corridor (long-planned; current EIR draft expected 2027; does not directly serve 91604 but reshapes south-bound commute in 10–15-year horizon).
- **Zoning:** LA City Council motion 2026-0118 (referred to PLUM 2026-02) contemplates amending R1 to allow 2 additional ADUs in designated hillside areas; status: pending.
- **Market trajectory:** 180-day trend +1.8%, consistent with LA westside submarkets; no material diverge.

**Agent's Read (observation, not fact):**

From seven showings in this boundary over the past 14 months, the consistent buyer feedback has been that the flat blocks south of Moorpark trade stronger than the hillside streets — the grade makes the hillside lots less usable for buyers who prioritize outdoor entertaining. The Carpenter attendance boundary is the single most-referenced search filter I see from out-of-area relocation buyers; homes two blocks outside the boundary consistently carry a 5–8% discount to otherwise-comparable homes inside it. Inventory in 2026 has been sparser than 2025, which is why we're seeing the shorter DOM and slight upward drift on median.

**AEO-Ready Q&A Block:**

1. **What is the median home price in Studio City 91604?** $1.46M as of April 2026, with a median of 18 days on market (MLS CRMLS, 90-day rolling).
2. **Which schools serve Studio City 91604?** Carpenter Community Charter (elementary, GreatSchools 9/10), Walter Reed Middle School (7/10), and North Hollywood High School (6/10). Harvard-Westlake and Oakwood are private options within 2 miles.
3. **What's the commute from Studio City to downtown LA?** About 28 minutes in peak morning traffic and 22 minutes off-peak via US-101 (Google Maps typical, April 2026).
4. **Does Studio City have public transit?** Yes — Metro B Line (Red) at the Universal City / Studio City station, with peak frequency of ~6 minutes. Walk Score on the Ventura Blvd corridor is 82.
5. **Are there hiking trails in Studio City?** Fryman Canyon (2.5-mile loop) and Wilacre Park (4-mile connected trail system) are both within 1.5 miles and form part of the Santa Monica Mountains trail network.
6. **What are the months of inventory in Studio City 91604?** Approximately 2.1 months as of April 2026 — a tight seller's market.
7. **Is there an HOA in Studio City 91604?** Most of the neighborhood is not HOA-governed; the Studio City Residents Association is a voluntary neighborhood association.
8. **What development is planned in Studio City?** A Ventura Blvd / Laurel Canyon mixed-use project (permit 2025-BLD-04417) is expected to break ground Q3 2026 — 8 stories, 118 residential units with 14,000 sqft of retail.

**Compliance Sweep:**

| Check | Status | Note |
|---|---|---|
| Fair Housing Act / state FH — no protected-class references | Pass | No references to race, religion, family composition, or other protected classes. |
| No proxy language ("quiet," "safe-feeling," "family-friendly") | Pass | Removed; "Safety & Community" uses only crime-stat sources. |
| No steering | Pass | Agent's Read is observational, not prescriptive. |
| Every data claim sourced and dated | Pass | Sources cited for MLS, GreatSchools, Google Maps, Walk Score, LAPD CompStat, city permit. |
| School rating-date < 18 months | Pass | 2026-04-20 retrieval. |
| Crime-stat window < 12 months | Pass | Rolling 12 months ending 2026-03. |

**Disclaimer:** Information in this report is compiled from public sources and MLS data as of April 2026. School ratings, crime statistics, and market data change; verify independently before making a housing decision. Prepared by [agent] · DRE #[license] · [brokerage]. Not an appraisal; not a solicitation in any jurisdiction where a license is required. Please consult with your own advisors on tax, legal, and financial matters related to a home purchase.
