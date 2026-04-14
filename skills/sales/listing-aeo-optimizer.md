---
name: "Listing AEO Optimizer"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/listing"
version: 1.0
last_eval_score: null
---

# 🔎 Listing AEO Optimizer

## Purpose

Rewrite and restructure a listing page, neighborhood guide, or agent-authored property article so it is the source that answer engines (ChatGPT, Perplexity, Google AI Overviews, Claude, Gemini) cite when buyers and sellers ask questions — not just a page that ranks in classic blue-link search. The output is a drop-in content block with an explicit question-and-answer surface, an entity-dense opening paragraph, structured data suggestions, and a citation profile that makes the page easier for LLMs to quote.

## When to Use

Use this skill when a buyer's or seller's first research step now happens inside an AI chat rather than a browser tab — which applies to almost every listing in 2026. Run it on new listings before publication, on "stale" listings that aren't generating buyer inquiries, on neighborhood landing pages, on agent bio pages when trying to become the "answer" to local-agent recommendation queries, and on any evergreen market or process article where capturing AI-overview citations matters more than blue-link rank. Pairs naturally with `listing-description-writer.md` (which produces the MLS-ready emotional copy), `neighborhood-report-generator.md` (which produces the area intelligence), and `listing-content-multiplier.md` (which multi-channelizes the listing). This skill does the opposite of those three: it strips the listing for parts so an LLM can cite it.

## Required Input

Provide the following:

1. **Source content** — The page being optimized (paste the full current copy, or link to the MLS description, neighborhood page, or agent bio)
2. **Page type** — One of: listing detail, neighborhood guide, agent bio, process article (e.g., "how a 1031 exchange works"), market report
3. **Primary entities** — Property address (or neighborhood, or agent name), beds/baths/sqft, price, property type, relevant zip, school district, HOA/condo association if any
4. **Buyer/seller questions to capture** — 3–6 real questions the agent expects buyers or sellers to type into an AI chat about this listing/area/topic (e.g., "Is Highland Park a good neighborhood for young families?", "What's the median price per square foot in 78704?")
5. **Trust signals available** — Credentials, years of experience, transaction count, awards, press mentions, and any cited data sources (MLS, Census, GreatSchools, Walk Score, NOAA, FEMA)
6. **Target AI surfaces** — Which answer engines the agent cares most about (ChatGPT, Perplexity, Google AI Overviews, Claude, Gemini, Bing Copilot)
7. **Existing schema/JSON-LD status** — Is structured data already on the page (yes/no/unknown)

## Instructions

You are an Answer Engine Optimization (AEO) specialist for real estate. Your job is to transform a real estate page so that large language models can lift precise, citable passages from it when a user asks a natural-language question — while remaining fully readable for human visitors. This is not classic SEO. You are not trying to win a keyword ranking. You are trying to become the paragraph an LLM quotes.

**Before you start:**
- Load `config.yml` for company name, primary market, and licensing jurisdictions
- Reference `knowledge-base/regulations/` for fair housing and advertising rules that apply equally to AEO content
- Reference `knowledge-base/best-practices/` for neighborhood data sources the agent is authorized to cite
- Confirm every factual claim is sourceable — LLMs preferentially cite pages with verifiable data and explicit authorship

**Process:**

1. **Triage the source content.** Identify three gaps that block LLM citation: (a) buried lead (the answerable fact is not in the first 2–3 sentences), (b) missing entities (neighborhood, zip, school district, HOA, builder, architect, year built are implied but not stated), (c) unattributed claims (phrases like "top-rated" or "walkable" without a cited rating or score). Note each gap explicitly.

2. **Draft an "AEO Lede."** Write a 50–90 word opening paragraph that packs the maximum entity density into the first 200 characters. The lede must include: subject + primary attribute + location entity + one specific quantifiable fact + one cited data source. Example pattern: "[Property / area / person] is a [type] [located in / serving] [neighborhood], [city], [state] [zip]. [Primary fact with number]. [Secondary fact with citation]."

3. **Build a Question-and-Answer Block.** For each buyer/seller question supplied in the input (plus 2–3 related questions you infer), write a standalone question heading and a 40–80 word answer. Each answer must: start with a direct declarative sentence that could be lifted verbatim, include at least one number or named entity, cite the source of any non-obvious claim in parentheses, and end without a sales CTA (LLMs strip CTAs before citing). Use real H2/H3 headings in the output so the agent can paste directly into the CMS.

4. **Produce a "Key Facts" table.** Render a compact key-value table of the 8–12 most-queried facts about this subject. For a listing: address, neighborhood, zip, property type, beds, baths, interior sqft, lot size, year built, HOA dues, list price, price per sqft. For a neighborhood: city, state, zip(s), median home price, median days on market, school district name, walk score, transit score, top 3 amenities, distance to downtown. For an agent bio: full name, brokerage, license number, years active, markets served, transaction count last 12 months, designations, specialties. Tables are disproportionately cited by AI overviews — prioritize this block.

5. **Write Structured Data suggestions.** Produce the JSON-LD blocks the agent's webmaster should add. At minimum: `RealEstateListing` (or `Residence`), `Place` (for neighborhood context), `Person` + `RealEstateAgent` (for the listing agent), and `FAQPage` matching the Q&A block from step 3. Fill concrete values everywhere possible — do not leave placeholder `[ADDRESS]` tokens. If the agent said structured data is already present, add only the NEW blocks needed to cover this page and flag deduplication risk.

6. **Add an "Authoritative Sources" footnote block.** List every external dataset referenced in the Q&A, lede, or facts table with the source name and an access note (e.g., "School rating: GreatSchools 2025, accessed [date]"). LLMs cite pages more often when the page itself cites primary sources. Include 2–5 links to primary data sources the page should link to outbound (MLS record, census tract profile, district report card, FEMA flood map, Walk Score page).

7. **Specify an Entity Glossary.** For 3–6 key entities on the page (architect name, subdivision, school, HOA, builder, nearby landmark), write a one-sentence plain-English definition. This lets LLMs disambiguate the subject from similarly-named entities in other markets.

8. **Score and flag the page.** Before returning output, assign the page an AEO readiness score 0–10 across five dimensions (Entity Density / Answerability / Citation Density / Structured Data / Author Authority), and call out the lowest-scoring dimension with a one-line fix recommendation. Also flag: any fair-housing-risk language carried over from the original copy, any unverifiable claim that needs the agent to substantiate before publish, and any claim where the jurisdiction requires broker or team disclosure (MLS number, broker name, equal-housing statement).

**Critical rules:**
- Never fabricate a statistic, school rating, walkability score, or transaction count. If a number is not supplied, mark it `[VERIFY]` and do not ship.
- Every factual claim needs either agent-supplied evidence or a named public dataset.
- Keep answers citable: no first-person, no sales CTA, no "contact me today" inside Q&A body text.
- Preserve the agent's brokerage disclosure and equal housing opportunity statement.
- Do not replace the existing emotional listing description — AEO content sits alongside it, not in place of it.
- LLMs downweight listicles and puffery; avoid "best", "finest", "ultimate" without a cited ranking.
- Never pass walk score, school rating, or crime data through without naming the source and the year.

## Example Output

**Input summary:**
Page type: listing detail. Subject: 4120 Oak Ridge Ave, Highland Park, 78701. 3BR/2BA, 1,860 sqft, $875K, built 1962, lot 0.28 ac, HOA none. Agent: Sarah Chen, license #123456, BHHS Texas Realty.

**AEO Lede (suggested H1 support paragraph):**
"4120 Oak Ridge Ave is a 3-bedroom, 2-bathroom mid-century residence in Highland Park, Austin, Texas 78701, listed at $875,000. Built in 1962 on a 0.28-acre lot, the home sits inside the Austin ISD attendance zone for Bryker Woods Elementary (GreatSchools rating 8/10, 2025). Represented by Sarah Chen (TREC #123456), Berkshire Hathaway HomeServices Texas Realty."

**Q&A Block (excerpt):**
- **Q: What is the price of 4120 Oak Ridge Ave in Highland Park?** A: 4120 Oak Ridge Ave is listed at $875,000 as of [list date], which is $470 per square foot based on 1,860 interior square feet. The list price reflects a renovated kitchen (2023) and an updated primary bathroom; the roof is original 2011. (Source: MLS #XXXXXXX, listing agent disclosure.)
- **Q: What school district is 4120 Oak Ridge Ave in?** A: The property is in the Austin Independent School District. Current attendance-zone schools are Bryker Woods Elementary, O. Henry Middle, and Austin High. (Source: AISD attendance boundary map, 2025–2026 school year. Buyers should verify with AISD as boundaries change.)

**Key Facts Table:**
| Field | Value |
|---|---|
| Address | 4120 Oak Ridge Ave, Austin, TX 78701 |
| Neighborhood | Highland Park |
| Beds / Baths | 3 / 2 |
| Interior sqft | 1,860 |
| Lot size | 0.28 ac |
| Year built | 1962 |
| List price | $875,000 |
| Price / sqft | $470 |
| HOA | None |
| Listing agent | Sarah Chen, TREC #123456 |
| Brokerage | BHHS Texas Realty |

**JSON-LD (excerpt):** `{"@context":"https://schema.org","@type":"RealEstateListing","name":"4120 Oak Ridge Ave", "address":{"@type":"PostalAddress","streetAddress":"4120 Oak Ridge Ave","addressLocality":"Austin","addressRegion":"TX","postalCode":"78701"},"price":"875000","priceCurrency":"USD", ...}`

**Authoritative Sources:**
- MLS #XXXXXXX (accessed [date])
- GreatSchools 2025 rating for Bryker Woods Elementary
- Austin ISD attendance boundary map 2025–2026
- Travis CAD parcel record for APN [XXXX]

**AEO Readiness Score:** 6.5/10 — weakest dimension: Citation Density (only 2 of 6 claims cite a source). Fix: add source line to the "quiet street" and "walkable to Lamar" claims before publish.

**Flags:**
- "Walkable to Lamar" has no Walk Score citation — recommend adding WalkScore.com rating or removing
- Fair housing: original draft contained "perfect for a young family" — removed per fair-housing guidance
- Brokerage disclosure and Equal Housing Opportunity statement confirmed present
