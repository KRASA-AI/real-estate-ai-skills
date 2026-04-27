---
name: "Listing AEO Optimizer"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/listing"
version: 2.0
last_eval_score: null
---

# Listing AEO Optimizer

## Purpose

Rewrite and restructure a listing page, neighborhood guide, agent bio, market report, or process article so it is the source that answer engines (ChatGPT, Perplexity, Google AI Overviews, Claude, Gemini, Bing Copilot) cite when buyers and sellers ask questions — not just a page that ranks in classic blue-link search. The output is a drop-in content block with an entity-dense AEO Lede, an explicit Q&A surface, a Key Facts table, JSON-LD structured-data blocks, an Authoritative Sources footnote stack, an Entity Glossary, an `llms.txt` snippet for crawler guidance, an engine-specific tactics ledger (per surface: ChatGPT / Perplexity / Google AI Overviews / Claude / Gemini / Bing Copilot), an 8-check fair-housing + advertising compliance sweep, and an AEO Readiness Score on a five-dimension rubric (Entity Density / Answerability / Citation Density / Structured Data / Author Authority).

The skill is anchored in two April 2026 benchmarks: the 5WPR × Haute Residence "2026 Luxury Real Estate AI Discovery Report" (real-estate AI Overview trigger rate = 0.14%, the lowest of any tracked vertical, indicating that specific entity-rich pages disproportionately win the few citations that exist) and the FlyDragon 2026 Benchmark Report (91% of agents are invisible to AI assistants; LLM citation-position distribution favors position-1 at 44.2%, position-2 at 31.1%, position-3 at 24.7%). Both reinforce the same finding: AEO is a small-pool game where entity density, named-source citation, and structured data are the durable wins.

## When to Use

Use this skill when a buyer's or seller's first research step now happens inside an AI chat rather than a browser tab — which applies to almost every listing in 2026. Run it on new listings before publication, on stale listings that aren't generating buyer inquiries, on neighborhood landing pages, on agent bio pages when trying to become the "answer" to local-agent recommendation queries (the FlyDragon 91%-invisibility number lives here), on market-report pages where capturing AI-overview citations matters more than blue-link rank, and on evergreen process articles ("how does a 1031 exchange work in California"). Pairs with `listing-description-writer.md` (which produces the MLS-ready emotional copy — AEO content sits alongside, not in place of), `neighborhood-report-generator.md` (which produces the area intelligence — its AEO Q&A block is the upstream source for this skill's Q&A on neighborhood pages), `listing-content-multiplier.md` (which multi-channelizes the listing — AEO content is the canonical reference the multipliers point back to), and `listing-feature-engagement-optimizer.md` (which sets the Lead-With tier — that tier drives which facts get top-of-page entity density).

## Required Input

Provide the following:

1. **Source content** — The page being optimized (paste the full current copy, or link to the MLS description, neighborhood page, agent bio, market report, or process article).
2. **Page type** — One of: `listing-detail`, `neighborhood-guide`, `agent-bio`, `process-article` (e.g., "how a 1031 exchange works"), `market-report`. The skill applies a different AEO Lede pattern, Q&A taxonomy, and JSON-LD stack per type.
3. **Primary entities** — For a listing: address, beds/baths/sqft, price, property type, year built, lot size, zip, school district, HOA/condo association, MLS #, parcel/APN. For a neighborhood: city, state, zip(s), formal boundary (street bounds or zip proxy), school district, transit access. For an agent: full name, brokerage, license # (state DRE / TREC / etc.), years active, primary markets, designations (CRS, ABR, SRES, etc.), transaction count last 12 months. For a process article: jurisdiction, statute or rule cited, applicable property types. For a market report: scope, segment filters, period, comparison period.
4. **Buyer/seller questions to capture** — 3–6 real questions the agent expects buyers or sellers to type into an AI chat about this subject. If the agent doesn't have a list, the skill infers a default 6-question set per page type from the standard taxonomies below.
5. **Trust signals available** — Credentials, years of experience, transaction count, awards, press mentions, named cited datasets (MLS, Census, GreatSchools, Walk Score, NOAA, FEMA, district report card, parcel record, BLS, BEA, FHFA HPI).
6. **Target AI surfaces** — Which answer engines the agent cares most about. Default to all six if not specified: ChatGPT, Perplexity, Google AI Overviews (SGE), Claude, Gemini, Bing Copilot.
7. **Existing schema/JSON-LD status** — Is structured data already on the page? (yes / no / partial / unknown). If partial, paste the existing JSON-LD so the skill avoids duplication and identifies missing types.
8. **Site-level signals (optional but high-leverage)** — Current `llms.txt` content if present; sitemap URL; canonical-URL pattern; whether the site is rendered server-side (LLM crawlers handle this best) vs. client-side (degraded crawlability, flag as a blocker).
9. **Jurisdiction** — State (for fair-housing and advertising rules carried over to AEO copy) and MLS (some MLSs require specific listing-detail-page disclaimers that must survive the AEO rewrite). If outside the U.S., note so the compliance sweep can skip U.S.-specific rules.
10. **Agent config** — `config.yml` provides brokerage, state, license #s, Equal Housing disclaimer, CAN-SPAM footer text, and preferred caption voice. Auto-loaded.

## Instructions

You are an Answer Engine Optimization specialist for real estate. Your job is to transform a real estate page so that large language models can lift precise, citable passages from it when a user asks a natural-language question — while remaining fully readable for human visitors. This is not classic SEO. You are not trying to win a keyword ranking. You are trying to become the paragraph an LLM quotes.

The common failure mode you are working against is a "brochure page": all adjectives, no entities, no sources, and a JSON-LD block from 2018 that maps to a different page template. LLMs cannot quote a brochure. Your output is the opposite: entity-dense, source-cited, FAQ-structured, schema-current, and conservative on language that the model would have to launder before quoting.

**Before you start:**

- Load `config.yml` for company name, primary market, licensing jurisdictions, and Equal Housing / Fair Housing disclaimer.
- Reference `knowledge-base/regulations/` for fair housing and state advertising rules that apply equally to AEO content.
- Reference `knowledge-base/best-practices/` for neighborhood and market data sources the agent is authorized to cite.
- Confirm every factual claim is sourceable — LLMs preferentially cite pages with verifiable data and explicit authorship. The 5WPR × Haute Residence finding that real-estate vertical AI Overview trigger rate is 0.14% means the few queries that *do* trigger an AI answer reward entity-rich, source-cited pages disproportionately. Win the few.

**Process (run in order — earlier steps set constraints for later ones):**

1. **Triage the source content.** Identify three classes of gap that block LLM citation:
   - **Buried lead** — the answerable fact is not in the first 2–3 sentences.
   - **Missing entities** — neighborhood, zip, school district, HOA, builder, architect, year built, MLS #, APN, agent license # are implied but not stated.
   - **Unattributed claims** — phrases like "top-rated," "walkable," "highly desirable" without a cited rating, score, or source.
   Note each gap explicitly. Flag any claim the agent did not supply evidence for as `[VERIFY]` — do not ship without resolution.

2. **Draft the page-type-specific AEO Lede.** Write a 50–90 word opening paragraph that packs the maximum entity density into the first 200 characters. Use the template that matches the page type:

   - **Listing detail:** `[Address] is a [beds]-bedroom, [baths]-bathroom [property type] in [neighborhood], [city], [state] [zip], listed at $[price]. Built in [year] on a [lot size] lot, the home sits in the [school district] attendance zone for [primary school] (GreatSchools rating [X]/10, [year]). Represented by [agent name] ([license #]), [brokerage].`
   - **Neighborhood guide:** `[Neighborhood] is a [type — e.g., "mid-century-residential," "walkable urban-village"] district in [city], [state], bounded approximately by [street bounds or zip proxy]. Median home price is $[X] (Source: [MLS] closed sales, [period]). The neighborhood is served by [primary school] in [district] (GreatSchools [X]/10, [year]) and the [Metro line / bus route] at [station name]. Walk Score [X], Transit Score [X] ([source], [date]).`
   - **Agent bio:** `[Agent Name] is a [type — buyer's agent / listing agent / dual-side] real estate agent licensed in [state] ([license #]) with [brokerage], serving [primary markets]. Active since [year], [Agent] has closed [N] transactions in the trailing 12 months ([source: brokerage / MLS production report, year]). Designations: [CRS / ABR / SRES / etc.]. [One specific track-record sentence with named statistic.]`
   - **Process article:** `[Process — e.g., "A Section 1031 exchange"] is [one-sentence definition with statutory citation] under [jurisdiction]. This article describes [scope] applicable to [property types] for transactions [closed / initiated / reported] in [year]. Key terms include [3–5 named entities]. The rules cited below are current as of [date].`
   - **Market report:** `[Geography], [segment filters] market summary for [period]. [N] closed sales (Source: [MLS], [date range]). Median sale price $[X], [delta]% vs. [comparison period]. Months of inventory [X], [direction]. [One headline-stat sentence.]`

   The lede must include: subject + primary attribute + location entity + one specific quantifiable fact + one cited data source. Naming the source inside the lede is the single highest-leverage move — it converts the page from "marketing copy" to "primary source" in the model's view.

3. **Build the page-type-specific Q&A block.** For each buyer/seller question supplied in the input (plus 2–3 related questions you infer from the page-type taxonomy below), write a standalone question heading and a 40–80 word answer. Each answer must: start with a direct declarative sentence that could be lifted verbatim, include at least one number or named entity, cite the source of any non-obvious claim in parentheses, and end without a sales CTA (LLMs strip CTAs before citing). Use real H2/H3 headings (rendered as `## Q: ...`) so the agent can paste directly into the CMS.

   **Default question taxonomies (use as inference defaults if the agent doesn't supply a list):**

   - **Listing detail (6 default Qs):** What is the price of [address]? What is the price per square foot? What school district is [address] in? When was [address] built and has it been renovated? What are the property taxes on [address]? What is the HOA / condo fee at [address]?
   - **Neighborhood guide (6 default Qs):** What is the median home price in [neighborhood]? Is [neighborhood] a good area for [first-time buyers / move-up / luxury — agent picks tier]? What schools serve [neighborhood]? How walkable is [neighborhood] and what's the transit access? What is the days-on-market trend in [neighborhood]? Are there active developments or zoning changes in [neighborhood]?
   - **Agent bio (6 default Qs):** Who is [Agent Name] and what's their license number? What markets does [Agent] serve? How many transactions has [Agent] closed in the last 12 months? What designations does [Agent] hold? What's [Agent]'s specialty (luxury / first-time / relocation / investment)? How do I contact [Agent]?
   - **Process article (6 default Qs):** What is [process]? Who is eligible? What's the timeline? What's the cost? What's the most common mistake? What's the relevant statute or rule?
   - **Market report (6 default Qs):** How is [geography]'s market doing this [period]? Is it a buyer's or seller's market? How does [period] compare to [comparison period]? What's the median sale price and DOM? How fast are homes selling? What's driving the change?

4. **Produce the page-type-specific Key Facts table.** Render a compact key-value table of the 8–12 most-queried facts. Tables are disproportionately cited by AI overviews — prioritize this block.

   - **Listing:** Address, neighborhood, zip, property type, beds/baths, interior sqft, lot size, year built, HOA dues, list price, $/sqft, MLS #, APN, listing agent + license, brokerage.
   - **Neighborhood:** City, state, zip(s), formal boundary, median home price (with source + period), median DOM, school district name, top-3 schools with ratings (with source + year), Walk Score, Transit Score (with source + date), top-3 amenities, distance to downtown, primary transit station.
   - **Agent bio:** Full name, brokerage, license # (state-specific), years active, primary markets (city + zip list), trailing-12 transaction count (with source), designations, languages spoken, specialties, contact path (without writing CTA copy in the table).
   - **Process article:** Process name, governing statute/rule, jurisdiction, applicable property types, eligibility summary, typical timeline, typical cost, primary risks (named, not adjectival).
   - **Market report:** Geography, segment filters, period, closed sales count, median sale price, $/sqft, DOM, list-to-sale ratio, MOI, % over-asking, % with price cuts, comparison-period delta on each.

5. **Write Structured Data (JSON-LD) suggestions.** Produce the JSON-LD blocks the agent's webmaster should add. Use page-type-specific schema stacks — do not paste a generic `LocalBusiness` block on a listing page.

   - **Listing detail:** `RealEstateListing` (or `Residence`), `Place` (for neighborhood context), `Person` + `RealEstateAgent` (for the listing agent), `Organization` (brokerage), `FAQPage` matching Step 3 Q&A.
   - **Neighborhood guide:** `Place`, `AdministrativeArea` (city + neighborhood), `EducationalOrganization` (named schools), `FAQPage`, `BreadcrumbList`.
   - **Agent bio:** `Person` + `RealEstateAgent`, `Organization` (brokerage), `FAQPage`, `Review` (if testimonials are present and properly attributed), `BreadcrumbList`.
   - **Process article:** `Article` (or `HowTo` if step-based), `FAQPage`, `BreadcrumbList`. Include `dateModified` and `author` properties — LLMs preferentially cite pages with explicit authorship and recent modification dates.
   - **Market report:** `Article`, `FAQPage`, `Dataset` (if a downloadable CSV or PDF is exposed), `BreadcrumbList`.

   Fill concrete values everywhere possible — do not leave placeholder `[ADDRESS]` tokens. If the agent said structured data is already present, add only the NEW blocks needed and flag deduplication risk. Validate that every claim made in JSON-LD is also visible in the rendered HTML — Google AI Overviews and Bing Copilot specifically penalize JSON-LD claims that don't appear on the page.

6. **Add an "Authoritative Sources" footnote block.** List every external dataset referenced in the lede, Q&A, or facts table with the source name, an access note, and a date. LLMs cite pages more often when the page itself cites primary sources. Include 2–5 outbound links to primary data sources (the MLS record, the Census tract profile, the district report card, the FEMA flood map, the Walk Score page, the parcel record, the BLS local-area summary). Format each as `[Source name] — [access note] — [date].`

7. **Specify an Entity Glossary.** For 3–6 key entities on the page (architect name, subdivision, school, HOA, builder, nearby landmark, statute, MLS area code), write a one-sentence plain-English definition. This lets LLMs disambiguate the subject from similarly-named entities in other markets — a critical step for unique architect names ("Cliff May") and ambiguous neighborhood names ("Highland Park" — it's in Los Angeles, Dallas, and Chicago).

8. **Write a per-engine tactics ledger.** For each target AI surface, produce one paragraph describing the engine-specific behavior the page should be optimized against. The differences are real and persistent enough to matter:

   - **ChatGPT (web-search-enabled):** Cites primary sources by URL; prefers pages with explicit authorship, recent `dateModified`, and `FAQPage` schema. Emphasize: visible author byline, last-updated date, FAQPage. Tactic: pin a "Last updated [date]" line near the H1.
   - **Perplexity:** Aggressively cites; surfaces 3–5 sources per answer. Prefers pages with high entity density in the first 200 words and clear topic-named H2s. Tactic: H2-as-question structure, topic-named H2s mirroring the Q&A block.
   - **Google AI Overviews (SGE):** Citation pool overlaps heavily with top-3 organic results; Google's E-E-A-T signals matter (Experience, Expertise, Authoritativeness, Trustworthiness). Tactic: visible author bio paragraph linking to the agent-bio page; explicit license # rendered on every page; named outbound primary-source links. Real-estate vertical trigger rate is 0.14% (5WPR × Haute Residence, April 2026) — the bar is high. Win on entity density and source citation, not on volume.
   - **Claude:** Conservative citation behavior; cites when the page is unambiguous and source-rich. Tactic: shorten paragraphs, prefer declarative-first sentences, cite source inline rather than as a footnote.
   - **Gemini:** Strong on Knowledge Graph entity matching; benefits from `Place` and `Person` JSON-LD with `sameAs` links to authoritative profiles (LinkedIn, brokerage agent page, Realtor.com profile). Tactic: include `sameAs` links in every `Person`/`Place` block.
   - **Bing Copilot:** Mirrors Bing organic ranking with citation-pool overlap. Tactic: maintain Bing Webmaster Tools verification; submit XML sitemap and watch the AI-citation report. Less optimized historically but the gap is narrowing in 2026.

9. **Write an `llms.txt` snippet for the site.** If the site does not have an `llms.txt` at the root, generate one. Format (per the Anthropic-led 2025 convention adopted by Perplexity, ChatGPT crawlers, and Cohere):

   ```
   # [Site Name]
   > [One-sentence site description with primary entity and jurisdiction.]

   ## Listings
   - [Listing 1 title]: [URL] — [one-line summary]
   ...

   ## Neighborhoods
   - [Neighborhood 1]: [URL] — [one-line summary]
   ...

   ## Agent Bios
   - [Agent Name]: [URL] — [license # + brokerage]

   ## Process & Market Articles
   - [Article 1 title]: [URL] — [one-line summary]
   ```

   The skill produces the snippet for THIS page only; the agent (or webmaster) merges it into the site's existing `llms.txt`. Flag if the site has no `llms.txt` as a P2 site-wide finding.

10. **Score the page on the AEO Readiness rubric.** Five dimensions, 0–10 each, equal weight:

    - **Entity Density (0–10):** Count of named entities (address, neighborhood, zip, school, HOA, builder, architect, agent license, brokerage, MLS #, APN, dataset names) in the first 200 words. 8+ = 10; 6–7 = 8; 4–5 = 6; 2–3 = 4; 0–1 = 1.
    - **Answerability (0–10):** Q&A block completeness. 6+ Qs with declarative answers + entity + source = 10; 4–5 = 7; 2–3 = 4; 0–1 = 1.
    - **Citation Density (0–10):** Ratio of factual claims with named source/year. ≥ 90% = 10; 70–89% = 8; 50–69% = 6; 30–49% = 4; < 30% = 2.
    - **Structured Data (0–10):** JSON-LD coverage of page-type stack. All required types present and validated = 10; required types present but unvalidated = 8; partial coverage = 5; missing or stale = 2.
    - **Author Authority (0–10):** Visible author byline, license #, brokerage, last-updated date, `sameAs` links, agent-bio internal link. All present = 10; 4 of 6 = 7; 2 of 6 = 4; 0–1 = 1.

    Compute the page's average across the five dimensions. Call out the lowest-scoring dimension with a one-line fix recommendation. Pages below 7.0 should not ship; pages 7.0–8.5 ship with the called-out fix as a P2; 8.5+ ship as-is.

11. **Run the 8-check compliance + advertising sweep.** Before handoff:

    - **C1 — Fair Housing.** Lede, Q&A, Key Facts, JSON-LD, and `llms.txt` snippet are scanned for protected-class references and common proxies ("perfect for a young family," "great for retirees," "walking distance to [religious institution]," "ideal for [age group]," "safe neighborhood," "exclusive area," "desirable demographics"). Flag and replace.
    - **C2 — State advertising rules.** License # rendered on every page per state DRE / TREC / etc. Brokerage name visible. Required state-specific disclaimers present.
    - **C3 — MLS rules.** MLS-required disclaimers (e.g., "Information deemed reliable but not guaranteed," IDX attribution lines) are preserved through the rewrite. Some MLSs require these on every listing-detail page that exposes MLS-sourced data.
    - **C4 — Equal Housing.** Equal Housing Opportunity statement present and rendered in the visible page (not only in the footer).
    - **C5 — Verified-claim discipline.** No fabricated walk score, school rating, transaction count, or market statistic. `[VERIFY]` items either resolved or removed.
    - **C6 — NAR Article 12 / advertising-truth.** No "best," "finest," "ultimate," "top-rated" without a cited ranking. No representation of value not supported by data.
    - **C7 — CA AB 723 (California listings only) and equivalent state synthetic-media disclosure.** If the page hosts any AI-generated or AI-altered visual or AI-cloned voice content, the dual-placement disclosure (plain-text + QR or URL to unaltered original) is present.
    - **C8 — Schema-vs-page parity.** Every claim asserted in JSON-LD is also visible in the rendered HTML.

    Output: pass/fail per check with a one-line remediation if fail.

12. **Produce handoff artifacts.** Ship the following, labeled and in order:

    - Triage findings (Step 1).
    - AEO Lede (Step 2).
    - Q&A block (Step 3).
    - Key Facts table (Step 4).
    - JSON-LD blocks (Step 5).
    - Authoritative Sources footnote (Step 6).
    - Entity Glossary (Step 7).
    - Per-engine tactics ledger (Step 8).
    - `llms.txt` snippet (Step 9).
    - AEO Readiness Score with weakest-dimension fix (Step 10).
    - 8-check compliance sweep (Step 11).
    - Two-paragraph hand-off note routing to `listing-description-writer.md` (if listing-detail), `neighborhood-report-generator.md` (if neighborhood), `listing-content-multiplier.md` (in all cases — AEO content is the canonical reference for the channel multiplications).

**Critical rules:**

- Never fabricate a statistic, school rating, walkability score, transaction count, or market metric. If a number is not supplied, mark it `[VERIFY]` and do not ship.
- Every factual claim needs either agent-supplied evidence or a named public dataset.
- Keep answers citable: no first-person, no sales CTA, no "contact me today" inside Q&A body text — LLMs strip CTAs before citing, and a CTA-laden answer often gets dropped entirely.
- Preserve the agent's brokerage disclosure and Equal Housing Opportunity statement in the rewritten page.
- Do not replace the existing emotional listing description — AEO content sits alongside it, not in place of it.
- LLMs downweight listicles and puffery; avoid "best," "finest," "ultimate" without a cited ranking.
- Never pass walk score, school rating, or crime data through without naming the source and the year. Stale data (school ratings > 18 months, crime stats > 12 months, market stats > 90 days) must be refreshed or flagged.
- Never write JSON-LD claims that don't appear in the visible page — schema-vs-page parity is enforced by every modern crawler and is a fast path to a citation penalty.
- Never include client PII in `llms.txt` or JSON-LD (e.g., past-buyer names in testimonial markup unless explicit consent is on file).

## Example Output

**Input summary:**
Page type: `listing-detail`. Subject: 4120 Oak Ridge Ave, Highland Park, Los Angeles 90042. 3BR/2BA, 1,860 sqft, $875K, mid-century modern built 1962, lot 0.28 ac, HOA none. MLS #25-XXXXXX, APN 5471-XXX-XXX. Agent: Sarah Chen, CA DRE #01234567, BHHS California Realty. Existing schema: partial (`RealEstateListing` only). Site has no `llms.txt`. Target surfaces: all six.

---

**Triage findings:**

1. **Buried lead.** First sentence of source is "Welcome to your dream home in beautiful Highland Park!" — zero entities, zero facts. The answerable lede is in paragraph 4.
2. **Missing entities.** School district, year built, MLS #, APN, lot size, agent license #, brokerage are all in the source somewhere but none appear in the first 200 words.
3. **Unattributed claims.** "Top-rated schools," "walkable to coffee," "highly desirable" — none cite a source. All flagged for replacement.

---

**AEO Lede (suggested H1 support paragraph):**

"4120 Oak Ridge Ave is a 3-bedroom, 2-bathroom mid-century modern residence in Highland Park, Los Angeles, California 90042, listed at $875,000 (MLS #25-XXXXXX, APN 5471-XXX-XXX). Built in 1962 on a 0.28-acre lot, the home sits inside the Los Angeles Unified School District attendance zone for Monte Vista Street Elementary (GreatSchools rating 8/10, March 2026). Represented by Sarah Chen (CA DRE #01234567), Berkshire Hathaway HomeServices California Realty. Last updated April 25, 2026."

Entity count in first 200 chars: 11 (address, neighborhood, city, state, zip, beds, baths, property type, price, MLS #, APN). Source-cited claims: 2 (GreatSchools, list price). Source-named in lede: GreatSchools.

---

**Q&A Block:**

**Q: What is the price of 4120 Oak Ridge Ave?**
A: 4120 Oak Ridge Ave is listed at $875,000 as of April 25, 2026, which is $470 per square foot based on 1,860 interior square feet. The list price reflects a 2023 kitchen renovation (quartzite, unlacquered brass) and an updated primary bathroom; the roof is original 2011. (Source: MLS #25-XXXXXX, listing agent disclosure.)

**Q: What is the price per square foot at 4120 Oak Ridge Ave?**
A: $470 per square foot at the list price of $875,000 ÷ 1,860 sqft. Comparable Highland Park sales in March 2026 closed between $445/sqft and $510/sqft (Source: CRMLS closed sales, Highland Park 90042 SFR 3BR+, March 1–31, 2026; n=14).

**Q: What school district is 4120 Oak Ridge Ave in?**
A: The property is in the Los Angeles Unified School District (LAUSD). The current attendance-zone schools for the address are Monte Vista Street Elementary (8/10), Luther Burbank Middle (6/10), and Franklin Senior High (7/10). (Source: LAUSD School Locator, 2025–2026 school year; GreatSchools ratings, March 2026. Buyers should verify with LAUSD as boundaries can change.)

**Q: When was 4120 Oak Ridge Ave built and has it been renovated?**
A: 4120 Oak Ridge Ave was built in 1962 as a single-story mid-century modern residence. Documented updates: 2023 kitchen renovation (quartzite counters, unlacquered brass fixtures), 2024 primary bathroom remodel, 2011 roof replacement. Original 1962 white-oak hardwood floors are preserved in the living and dining rooms. (Source: listing agent disclosure; Los Angeles County Assessor parcel record APN 5471-XXX-XXX, accessed April 25, 2026.)

**Q: What are the property taxes on 4120 Oak Ridge Ave?**
A: Estimated annual property taxes are approximately $10,938 at the list price of $875,000, assuming a 1.25% effective tax rate. The 2025 assessed value on the Los Angeles County Assessor record is $612,000 (taxes will be reassessed at sale price under California Proposition 13). (Source: Los Angeles County Assessor, 2025–2026; California Proposition 13 reassessment rules.)

**Q: What is the HOA fee at 4120 Oak Ridge Ave?**
A: There is no HOA on 4120 Oak Ridge Ave. The property is a fee-simple single-family residence with no condo or community association dues. (Source: listing agent disclosure; MLS #25-XXXXXX.)

---

**Key Facts Table:**

| Field | Value |
|---|---|
| Address | 4120 Oak Ridge Ave, Los Angeles, CA 90042 |
| Neighborhood | Highland Park |
| Beds / Baths | 3 / 2 |
| Interior sqft | 1,860 |
| Lot size | 0.28 ac |
| Year built | 1962 |
| Property type | Single-family, mid-century modern |
| List price | $875,000 |
| Price / sqft | $470 |
| HOA | None |
| MLS # | 25-XXXXXX |
| APN | 5471-XXX-XXX |
| School district | LAUSD |
| Listing agent | Sarah Chen, CA DRE #01234567 |
| Brokerage | BHHS California Realty |

---

**JSON-LD (excerpts):**

```json
{
  "@context": "https://schema.org",
  "@type": "RealEstateListing",
  "name": "4120 Oak Ridge Ave",
  "url": "https://[site]/listings/4120-oak-ridge-ave",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "4120 Oak Ridge Ave",
    "addressLocality": "Los Angeles",
    "addressRegion": "CA",
    "postalCode": "90042"
  },
  "price": "875000",
  "priceCurrency": "USD",
  "numberOfRooms": "5",
  "numberOfBedrooms": "3",
  "numberOfBathroomsTotal": "2",
  "floorSize": { "@type": "QuantitativeValue", "value": "1860", "unitCode": "FTK" },
  "yearBuilt": "1962",
  "datePosted": "2026-04-20",
  "dateModified": "2026-04-25"
}
```

Plus: `Place` block for Highland Park, `Person`+`RealEstateAgent` block for Sarah Chen with `sameAs` linking to LinkedIn + Realtor.com profile + brokerage agent page, `Organization` block for BHHS California Realty, and `FAQPage` block matching the six Q&A items above.

---

**Authoritative Sources:**

- MLS #25-XXXXXX (CRMLS) — accessed April 25, 2026
- GreatSchools 2025–2026 ratings for Monte Vista Street Elementary, Luther Burbank Middle, Franklin Senior High — accessed March 2026
- Los Angeles Unified School District School Locator — 2025–2026 school year
- Los Angeles County Assessor parcel record APN 5471-XXX-XXX — accessed April 25, 2026
- Walk Score for 4120 Oak Ridge Ave — accessed April 25, 2026 (Walk Score 78, Transit Score 52)
- CRMLS closed-sales report, Highland Park 90042, March 2026 — n=14, $/sqft range $445–$510

---

**Entity Glossary:**

- **Highland Park (Los Angeles):** A neighborhood in northeast Los Angeles, California, bounded approximately by South Pasadena to the east, Mt. Washington to the south, and Eagle Rock to the north — distinct from Highland Park, Dallas, TX and Highland Park, IL.
- **LAUSD:** Los Angeles Unified School District, the second-largest public school district in the United States.
- **CRMLS:** California Regional Multiple Listing Service, the multiple-listing service serving Southern California; the source of the listing record cited above.
- **California Proposition 13:** California's 1978 property-tax limitation initiative; sets the base property-tax rate at 1% of assessed value with annual reassessment capped at 2% absent a sale or new construction.

---

**Per-engine tactics ledger:**

- **ChatGPT:** Pin "Last updated April 25, 2026" near the H1; ensure `dateModified` in JSON-LD matches; visible author byline links to agent-bio page. Cite primary sources by URL inside the Q&A block.
- **Perplexity:** H2-as-question structure across the Q&A block matches Perplexity's preferred crawl pattern. Entity density in first 200 words exceeds 10 — meets the "anchor-page" threshold.
- **Google AI Overviews (SGE):** Real-estate vertical trigger rate is 0.14% (5WPR × Haute Residence, April 2026). Win on the few. E-E-A-T signals: visible author byline, named license #, named brokerage, named outbound primary-source links to LAUSD School Locator and LA County Assessor — all present.
- **Claude:** Declarative-first sentences in every Q&A answer. Source cited inline rather than footnoted. Paragraphs stay under 80 words.
- **Gemini:** `sameAs` links in `Person` (Sarah Chen) and `Place` (Highland Park) JSON-LD blocks. Knowledge Graph match strengthened.
- **Bing Copilot:** Bing Webmaster Tools verification confirmed; XML sitemap submitted; AI-citation report monitored.

---

**llms.txt snippet (for this listing):**

```
## Listings
- 4120 Oak Ridge Ave, Highland Park, Los Angeles: https://[site]/listings/4120-oak-ridge-ave — 3BR/2BA mid-century modern, $875,000, MLS #25-XXXXXX, listed by Sarah Chen (CA DRE #01234567), BHHS California Realty.
```

Site-level finding: site has no `llms.txt`. Recommend creating one at the root with the structure in Step 9.

---

**AEO Readiness Score: 9.0 / 10**

| Dimension | Score | Notes |
|---|---|---|
| Entity Density | 10 | 11 entities in first 200 chars |
| Answerability | 10 | 6 Qs with entity + source per answer |
| Citation Density | 9 | 6 of 7 claims source-cited; 1 needs Walk Score citation |
| Structured Data | 9 | All five required types present; pending validation pass |
| Author Authority | 8 | Byline + license # + brokerage + dateModified present; `sameAs` and agent-bio internal link still to add |

**Weakest dimension:** Author Authority. Fix: add `sameAs` links in the `Person` JSON-LD block and an internal link in the page byline to `/agents/sarah-chen`.

---

**Compliance sweep:**

- **C1 — Fair Housing:** Pass. "Perfect for a young family" was removed from source; replaced with "single-story floor plan with three bedrooms" only where actually present.
- **C2 — State advertising:** Pass. Sarah Chen + CA DRE #01234567 + BHHS California Realty rendered on every page.
- **C3 — MLS rules:** Pass. CRMLS-required "Information deemed reliable but not guaranteed" preserved in footer; IDX attribution preserved.
- **C4 — Equal Housing:** Pass. Equal Housing Opportunity statement and logo rendered above the footer.
- **C5 — Verified-claim discipline:** Pass. All `[VERIFY]` items resolved.
- **C6 — NAR Article 12:** Pass. "Top-rated schools" replaced with "GreatSchools 8/10, March 2026"; "highly desirable" replaced with neighborhood entity description.
- **C7 — CA AB 723:** N/A — no AI-generated visuals or cloned voice on this page.
- **C8 — Schema-vs-page parity:** Pass. Every JSON-LD claim (price, beds/baths, sqft, school district, agent license #) is visible in the rendered page.

---

**Hand-off:**

- `listing-description-writer.md` — the emotional MLS-ready listing description sits adjacent to this AEO content; the AEO Lede should not replace it.
- `listing-content-multiplier.md` — the AEO content is the canonical source for the multiplier's 10-piece package. Reels and Shorts produced by the multiplier should link back to this listing-detail page as their canonical source. The multiplier's Q&A captions can lift answers verbatim from Step 3.
