---
name: "Agent Discoverability Audit"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~3 hr/agent"
version: 1.0
last_eval_score: null
---

# Agent Discoverability Audit

## Purpose

Audit a real estate agent as an *entity* across the AI discovery layer — not a listing page, not a single bio, but the cross-surface footprint that determines whether ChatGPT, Perplexity, Google AI Overviews, Claude, Gemini, or Bing Copilot will name this agent when a buyer or seller asks "who's the best agent for [my situation] in [my market]?" Produces an **Off-Page Discoverability Score** (six audit surfaces × six AI engines), a **Content-Engine Taste Score** (five-dimension anti-slop rubric for AI-assisted personal-brand content), a **Specialization Ladder placement** (five tiers from Generalist → Luxury), a **Brand-Voice + Voice-Clone Asset Inventory** (three-tier discipline shared with `listing-video-workflow.md`), a **6-check compliance sweep**, and a **90-day Action Plan** sequenced across three phases (Stabilize 0–30, Differentiate 30–60, Compound 60–90). The skill is tool-agnostic — it governs the methodology decisions before HeyGen, ElevenLabs, Regen IO, Luxury Presence, Lofty, Sierra Interactive, or any vendor production.

The skill is anchored in three convergent April 2026 signals: HousingWire's 4/8/2026 framing that "personal branding only worked because very few agents were doing it well — visibility used to win, now it's just noise"; the FlyDragon 2026 Benchmark Report's finding that 91% of U.S. agents are effectively invisible to AI assistants and that 61.3% of buyer-side searches now begin in an AI search engine; and the 5WPR × Haute Residence "2026 Luxury Real Estate AI Discovery Report" framing of a "24-month window to own" the AI discovery layer in luxury real estate before the vertical fills. The dominant failure mode is *not* lack of content — it's lack of cross-surface entity coherence and lack of a defensible specialization tier.

## When to Use

Use this skill once per agent per quarter — and on these triggers: a new agent joining a brokerage; an existing agent whose lead flow has flattened despite consistent content output; an agent considering a luxury, niche, or relocation specialization; a brokerage onboarding a class of new agents simultaneously; preparation for a new market expansion (the agent enters a metro where no AI engine knows them); preparation for an annual business plan session (pair with `annual-business-plan-builder.md` — the audit findings become the AI-discoverability section of the plan); a brand refresh; a brokerage or team move (the agent's `sameAs` graph fragments and needs reconstruction); a media or designation milestone (a new CRS / ABR / SRES / press mention is a citation-density opportunity); after a public mistake or removed listing where reputation reconstruction matters. Pairs with `listing-aeo-optimizer.md` (page-level on-page AEO — this skill is the off-page complement; the two together cover the "AEO surface area" of a real estate practice), `social-content-calendar-30day.md` (the 90-day Action Plan's content-engine outputs feed the calendar), `listing-video-workflow.md` (the L0–L3 voice-clone discipline is shared verbatim — same controlled-asset posture), `neighborhood-report-generator.md` (the geo-specialization tier in the Ladder pulls from the agent's neighborhood authority work), `annual-business-plan-builder.md` (the discoverability findings are an input to the annual plan), `ai-marketing-compliance-audit.md` (downstream — any AI-generated bio, video, or voice-clone content the audit recommends routes through the compliance audit before publication).

## Required Input

Provide the following:

1. **Agent identity** — Full name, current brokerage (and prior brokerages within 36 months), state license # (CA DRE, TX TREC, FL DBPR, etc.), years active, primary metros (city + zip list), designations (CRS, ABR, SRES, CIPS, GRI, RENE, etc.), and trailing-12 transaction count with source (brokerage report, MLS production report, REAL Trends, Adwerx, etc.).
2. **Current digital footprint** — URLs for: brokerage agent page, Zillow profile, Realtor.com profile, Homes.com profile, LinkedIn, agent website (if separate from brokerage), Instagram handle, YouTube/Vimeo channel, podcast (if any), Google Business Profile (GBP) URL, and any other portal where the agent has a claimed profile (Compass, eXp, Side, BHHS, Coldwell Banker, etc.).
3. **Specialization claim** — One sentence describing what the agent wants to be the "answer" to in their market. Example: "Mid-century modern listings in Highland Park, Los Angeles" or "Relocation buyers from NYC moving to Westchester" or "First-time buyers under $600K in Austin." If the agent doesn't have a claim, the skill produces three candidate tier placements after the audit.
4. **Content-engine inventory** — Which AI tools the agent currently uses for content, branded by name (HeyGen, ElevenLabs, Regen IO, Synthesia, Pictory, Descript, Opus, Castmagic, Canva, ChatGPT, Claude, Gemini, Perplexity, RPR, Restb.ai, Rechat, Lofty, Sierra Interactive, kvCORE, Follow Up Boss, etc.). Note voice-clone use (yes/no/unsure), AI avatar use (yes/no), AI-syndication tool use (yes/no).
5. **Trust signals available** — Press mentions (publication, date, URL), podcast appearances (host, date, URL), listicle inclusions (publication, year — REAL Trends "America's Best," Hour Detroit "Top Agent," local "Best Of" awards), reviews count + average per portal (Zillow, Realtor.com, GBP, Yelp), backlinks count (if known via Ahrefs/SEMrush/Moz), and any earned-media artifacts (op-eds, expert quotes, conference talks).
6. **Competitive context** — 2–3 named local competitors the agent loses to in AI-engine recommendation queries (the agent runs the prompt "Who is the best [specialty] agent in [metro]?" across ChatGPT and Perplexity and reports who got named). If the agent hasn't run the query, the skill prompts it as the first audit step.
7. **Constraints** — Brokerage branding rules (eXp, Compass, Side, KW, Anywhere all have specific bio + photo + license-display requirements); state advertising rules (CA, TX, NY, FL most-restrictive jurisdictions); time budget the agent commits to the 90-day plan (low: < 2 hrs/wk; medium: 2–5 hrs/wk; high: 5+ hrs/wk).
8. **Voice-clone consent + brokerage policy** — Has the agent recorded a voice clone (ElevenLabs, HeyGen, Resemble, Play.ht, Descript Overdub)? Is there a vendor "do-not-train" clause in place? Does the brokerage permit AI voice or avatar use? (If unknown, the skill defaults to the most conservative tier.)
9. **Jurisdiction** — State (for advertising-rule overlays), and whether the agent works in any of the AI-disclosure-strict jurisdictions (CA AB 723, IL HB 4762, UT SB 149, CO SB24-205 once effective, TX HB 149, FL SB 442, etc.). The compliance sweep adapts.
10. **Agent config** — `config.yml` provides brokerage name, state, license #, Equal Housing disclaimer, CAN-SPAM footer, and preferred caption voice. Auto-loaded.

## Instructions

You are an Agent Discoverability auditor. Your job is to produce the highest-resolution view possible of how a single real estate agent is currently visible to AI assistants, what specifically is broken, and a 90-day plan to fix it. You are working against the failure mode that HousingWire flagged on April 8, 2026: visibility used to win; now it's just noise. The agents who win in the AI-discovery era are not the loudest — they are the most coherent across surfaces and the most defensible inside a specialization tier.

You are *not* writing the agent's content. You are *not* picking the tools. You are auditing entity coherence, scoring discoverability, placing the agent on a specialization ladder, inventorying the brand-voice and voice-clone assets, sweeping for compliance, and producing the 90-day plan. The downstream skills (`listing-aeo-optimizer.md` for on-page bio, `social-content-calendar-30day.md` for cadence, `listing-video-workflow.md` for video production) execute against the plan you produce.

**Before you start:**

- Load `config.yml` for brokerage, state, license, Equal Housing language, and caption voice.
- Reference `knowledge-base/regulations/` for state-specific advertising and AI-disclosure rules.
- Reference `knowledge-base/best-practices/` for the agent-bio entity inventory standards.
- Confirm the agent has run the recommendation query in at least two AI engines (ChatGPT + Perplexity at minimum) and reported who got named. If they haven't, prompt them to run it before proceeding — the audit's baseline depends on this observation.

**Process (run in order — earlier steps set inputs for later ones):**

1. **Run the Recommendation Query Baseline.** Have the agent run these four queries in ChatGPT (with web search enabled), Perplexity, Google AI Overviews (via google.com search bar), and Claude (with web search), then paste the responses verbatim:
   - "Who is the best [specialization] real estate agent in [primary metro]?"
   - "Recommend a real estate agent in [primary zip] who specializes in [specialization]."
   - "[Agent's full name] real estate agent — what should I know about them?"
   - "Top real estate agents in [primary metro] for [specialization] in 2026."
   Tabulate: which queries surfaced the agent (Y/N), which competitor was named instead, and what specific source the engine cited (brokerage page, Zillow, REAL Trends listicle, the agent's own site, a third-party blog). The cited sources are the discoverability surfaces the audit must strengthen.

2. **Off-Page Discoverability Audit — six surfaces.** For each surface, note presence (Y/N), entity completeness (license # / brokerage / years active / transaction count / designations / specialization / `sameAs` outbound links), reviews count, and last-updated date if visible. Score each surface 0–10:
   - **S1 — Google Business Profile (GBP):** claimed; categories include "Real Estate Agent"; service area is named (cities + zips); 25+ photos; reviews count; Q&A populated; posts in last 30 days. 10 = all eight present; 6 = five of eight; 0 = unclaimed.
   - **S2 — Zillow profile:** claimed; bio includes license # + brokerage + specialization; reviews count; past sales count visible; specialty tags set; profile photo + cover photo; team affiliation correct.
   - **S3 — Realtor.com profile:** claimed; same fields as Zillow plus markets-served zip list.
   - **S4 — Homes.com profile:** claimed; bio + transaction count + reviews. (Per RISMedia 4/25/2026 reporting that Homes.com agent subscriptions are growing fast, this surface is moving from "optional" to "table stakes" in 2026.)
   - **S5 — LinkedIn:** complete profile including headline that names specialization + metro; license # in About; brokerage in current role; at least one weekly post; recommendations from past clients; `sameAs`-grade external links to brokerage page, Zillow, Realtor.com.
   - **S6 — Brokerage page + agent's own site (if separate):** entity-complete bio per the `listing-aeo-optimizer.md` agent-bio Lede pattern; visible last-updated date; outbound links to GBP + Zillow + Realtor.com + LinkedIn; `Person` + `RealEstateAgent` JSON-LD with `sameAs` graph.

   Compute the average S1–S6 score. Anything below 7 on any single surface gets a P1 fix in the 90-day plan; anything below 4 gets a P0 fix in the first 14 days.

3. **Per-Engine Discoverability Tactics ledger.** Cross-tabulate the six audit surfaces against the six AI engines from `listing-aeo-optimizer.md` (ChatGPT, Perplexity, Google AI Overviews, Claude, Gemini, Bing Copilot). For each engine, name the two highest-leverage surfaces and the one specific tactic per engine:
   - **ChatGPT:** prefers brokerage page + LinkedIn for agent recommendation; tactic = visible last-updated date + `dateModified` JSON-LD on brokerage page; LinkedIn About populated with license # and specialization in the first 200 characters.
   - **Perplexity:** prefers third-party listicles (REAL Trends, Hour Detroit, local "Best Of") + Zillow review density; tactic = pursue at least one named-publication listicle inclusion per year; respond to every Zillow review within 7 days to keep activity recency high.
   - **Google AI Overviews (SGE):** prefers GBP + brokerage page (mirrors top-3 organic; E-E-A-T weighted); tactic = GBP weekly Posts + monthly photo additions; brokerage page visible byline + license # rendered above the fold.
   - **Claude:** prefers source-rich, declarative-first content; tactic = bio paragraphs source-cite transaction counts (REAL Trends 2025, MLS production report 2025) inline rather than as footnotes.
   - **Gemini:** strong on Knowledge Graph entity matching with `sameAs` links; tactic = `Person` JSON-LD on agent-bio page with `sameAs` array linking to LinkedIn + Zillow + Realtor.com + GBP + brokerage profile + Wikipedia (if applicable) — every internal `sameAs` strengthens the Knowledge Graph match.
   - **Bing Copilot:** mirrors Bing organic; tactic = Bing Webmaster Tools verification on the agent's site + XML sitemap; check the AI-citation report monthly.
   The output is a 6×2 matrix (engine → top two surfaces + one tactic). This becomes the targeting layer of the 90-day plan.

4. **Specialization Ladder placement.** Place the agent on the five-tier ladder. Each higher tier compounds AI-discoverability returns because the entity space narrows and the named-source citations become more findable.
   - **T1 — Generalist:** "[Name], real estate agent in [metro]." AI engines cannot disambiguate from 50–500 other agents in the same metro. Lowest discoverability ceiling. Default tier for new agents.
   - **T2 — Geo specialist:** "[Name], real estate agent specializing in [neighborhood] / [zip cluster] in [metro]." Ladder rung where neighborhood-page authority (`neighborhood-report-generator.md`) compounds.
   - **T3 — Property-type specialist:** "[Name], real estate agent specializing in [property type — mid-century modern / new construction / waterfront / historic / condos / multi-family] in [metro]." Ladder rung where photo + listing-video specificity compounds.
   - **T4 — Buyer/Seller-segment specialist:** "[Name], real estate agent specializing in [segment — relocation / first-time buyer / move-up / downsizing / divorce / probate / military VA / 1031 exchange / investor / international buyer] in [metro]." Ladder rung where named-process article authority (`process-article` page type from `listing-aeo-optimizer.md`) compounds.
   - **T5 — Luxury-tier specialist:** "[Name], luxury real estate agent specializing in [price band, e.g., $5M+ / $10M+] [property-type or neighborhood] in [metro]." Ladder rung where the 5WPR × Haute Residence "24-month window" framing applies most directly. The price-band entity is the disambiguating fact.

   Output: current tier (with the cited evidence), recommended tier (the next defensible rung up), and the three specific entity additions needed to hold the recommended tier in AI-engine recommendation responses. If the agent is already T4 or T5, the recommendation is to deepen rather than climb (e.g., add a property-type qualifier inside a luxury tier: "luxury mid-century-modern specialist, $3M+, in Highland Park").

5. **Content-Engine Taste Audit — anti-slop rubric.** Score the agent's current AI-assisted content engine on five dimensions, 0–10 each:
   - **D1 — Voice fidelity:** Does the AI-generated content sound like the agent or like ChatGPT default voice? 10 = a past client could not tell which posts were AI-assisted; 5 = identifiable AI cadence in some posts; 0 = obvious AI cadence in most posts.
   - **D2 — Fact density:** Does the content carry named entities (specific addresses, neighborhoods, schools, statutes, market stats with sources) or generic adjectives? 10 = ≥ 3 named entities per post; 0 = adjective-driven puffery.
   - **D3 — Visual taste:** Are images and video well-composed and brand-consistent, or stock-AI-generic (the "headshot in front of a fictional skyline" tell)? 10 = brand-consistent and discriminative; 0 = generic AI-stock tells visible.
   - **D4 — Voice-clone discipline:** If the agent uses ElevenLabs / HeyGen / Resemble for voice or avatar, does the use match the L0–L3 ladder defined in Step 6 below, with disclosure where required? 10 = full discipline applied; 0 = clone used in first-person sales communication without disclosure.
   - **D5 — Cadence honesty:** Is the content cadence sustainable by the agent's actual time budget, or is it visibly throttle-by-AI to a degree that erodes trust (the "10 reels per day" tell)? 10 = cadence matches stated time budget; 0 = volume signals zero human curation.

   Compute the D1–D5 average. Anything below 7 routes to a P1 fix in the 90-day plan. The Content-Engine Taste Score is named explicitly in the audit output because the HousingWire 4/8/2026 framing makes clear that volume without taste actively destroys the brand.

6. **Brand-Voice + Voice-Clone Asset Inventory (L0–L3).** Inventory the agent's voice and avatar assets on the same four-tier ladder used by `listing-video-workflow.md`. Sharing the ladder means a single decision about voice-clone use governs both listing video and personal-brand content:
   - **L0 — Live agent voice on camera, no AI processing.** No disclosure needed. Default for first-person sales communication, listing-appointment videos, client check-ins, and any content where personal trust is the deliverable.
   - **L1 — Pre-recorded agent voice (real, not cloned), reused across pieces.** No disclosure needed. Default for brand-anchor pieces (about-me video, specialization explainer, market-update voiceover).
   - **L2 — Cloned agent voice (ElevenLabs / HeyGen / Resemble / Play.ht), used for content production at scale.** Disclosure required on first frame or in caption: "Voiceover by [Agent Name]'s authorized AI voice." Vendor must have a "do-not-train" clause and a revocation path. The L2 clone is a controlled asset — it is the same asset an attacker would weaponize at closing (cross-link to `ai-fraud-defense-playbook.md`'s passphrase protocol; the L2 clone must NEVER be used in first-person closing communications, wire-instruction confirmations, or escrow conversations).
   - **L3 — Stock synthetic voice (not the agent's clone, e.g., a stock ElevenLabs voice or HeyGen avatar).** Cannot speak in first person. Disclosure required: "Voiced by AI." Useful for market-update narration, neighborhood-overview narration, process-explainer narration where the deliverable is information, not relationship.

   Output: which of the agent's existing content sits at each tier, which tier the brokerage permits, which tier each downstream content type should default to, and any L2 use that needs immediate disclosure correction. Pair this output with `listing-video-workflow.md` so the same voice-clone consent governs both listing video and personal brand.

7. **6-Check Compliance Sweep.** Pre-publication for any audit-recommended bio, video, voice-clone, or syndication action:
   - **C1 — License + brokerage display.** License # rendered on every audit-touched surface (GBP, Zillow, Realtor.com, Homes.com, LinkedIn About, brokerage page, agent site bio). Brokerage name visible.
   - **C2 — Fair Housing.** All audit-recommended bio + post copy scanned for protected-class proxies. Specialization claims that imply protected-class targeting ("perfect for young families," "established neighborhoods," "exclusive enclaves") flagged and rewritten.
   - **C3 — NAR Article 12 truthfulness.** "Top," "best," "#1," "leading" claims must cite a named ranking (REAL Trends "America's Best," Hour Detroit "Top Agent," brokerage internal ranking with the year). Unsubstantiated superlatives flagged.
   - **C4 — AI synthetic-media disclosure.** Per the L0–L3 ladder, every L2 (cloned voice) and L3 (stock synthetic) use carries the required first-frame or caption disclosure. CA AB 723 + state equivalents apply if the content is used in property advertising.
   - **C5 — Brokerage advertising rules.** Brokerage-specific bio/photo/disclaimer rules (eXp, Compass, Side, KW, Anywhere variants) honored. The agent's brokerage compliance officer is the final reviewer for any L2 or L3 voice/avatar deployment.
   - **C6 — `sameAs` graph integrity.** Every `sameAs` link in the agent's `Person` JSON-LD points to a profile the agent actually owns and maintains. Stale links (former brokerage page, deactivated Twitter, inactive YouTube) flagged for removal — broken `sameAs` links degrade Knowledge Graph match in Gemini specifically.

   Output: pass/fail per check with one-line remediation if fail.

8. **90-Day Action Plan — three phases.** Sequence the audit findings into a calendar with explicit owners (agent, brokerage marketing, agent's VA, agent's videographer, agent's web developer):
   - **Phase 1: Stabilize (Days 0–30).** Fix every P0 / surface-score-below-4 finding. Typical: claim missing portal profiles; add license # to surfaces missing it; populate GBP categories + service-area + 25 photos; rewrite the brokerage-page bio per the `listing-aeo-optimizer.md` agent-bio Lede pattern; add `Person` + `RealEstateAgent` JSON-LD to the agent's site if missing. Cap: 8 actions max (otherwise the agent does none of them).
   - **Phase 2: Differentiate (Days 30–60).** Fix every P1 / surface-score-below-7 finding and execute the Specialization Ladder placement. Typical: add the recommended-tier specialization claim to GBP, Zillow, Realtor.com, Homes.com, LinkedIn, and the brokerage page in coordinated language; pursue the first named-publication listicle inclusion; add `sameAs` links across the `Person` JSON-LD; respond to every backlog Zillow + GBP review; publish the first specialization-anchor piece (a `process-article` for T4, a neighborhood-guide for T2, a property-type explainer for T3, a price-band-anchored market report for T5). Cap: 10 actions.
   - **Phase 3: Compound (Days 60–90).** Stand up the content engine inside the time-budget constraint. Typical: deploy the L0–L3 ladder per Step 6; if voice-clone is in scope, configure ElevenLabs + HeyGen with the "do-not-train" clause and the disclosure default; route all output through `social-content-calendar-30day.md`; set the monthly tactical review (re-run the recommendation queries from Step 1; re-score surfaces; track listicle-pursuit pipeline). Cap: 8 actions.

   For each action, assign: owner, deliverable (the specific artifact, not "improve LinkedIn"), date, dependency, and the specific surface or engine score it lifts. Total plan: 26 actions max across 90 days.

9. **Produce handoff artifacts.** Ship the following, labeled and in order:
   - Recommendation Query Baseline table (Step 1).
   - Off-Page Discoverability Score (Step 2) — six-surface table with current score, target score, and gap.
   - Per-Engine Discoverability Tactics matrix (Step 3) — 6×2 engine-to-surfaces with the one tactic per engine.
   - Specialization Ladder placement (Step 4) — current tier, recommended tier, three entity additions needed.
   - Content-Engine Taste Score (Step 5) — D1–D5 table with D-low fix.
   - Brand-Voice + Voice-Clone Asset Inventory (Step 6) — L0–L3 inventory with reassignment recommendations.
   - 6-Check Compliance Sweep (Step 7) — pass/fail per check.
   - 90-Day Action Plan (Step 8) — three-phase, 26-action calendar.
   - Two-paragraph hand-off note routing to `listing-aeo-optimizer.md` (for the on-page agent-bio rewrite specifically), `social-content-calendar-30day.md` (for the Phase 3 content engine), `listing-video-workflow.md` (for the L0–L3 voice-clone discipline alignment), `annual-business-plan-builder.md` (so the audit findings become the AI-discoverability section of the annual plan), and `ai-marketing-compliance-audit.md` (for any L2 or L3 voice-clone deployment review).

**Critical rules:**

- Never fabricate a transaction count, listicle inclusion, designation, press mention, or review count. If a number is not supplied or verifiable from the cited surface, mark it `[VERIFY]` and do not score it.
- Never recommend an L2 voice-clone deployment without confirming the brokerage permits it AND the vendor has a "do-not-train" clause AND a revocation path. If any of the three are missing, recommend L1 instead.
- Never recommend a Specialization Ladder tier the agent cannot defend with at least three named-entity citations (transactions in the tier, named publications covering the tier, designations specific to the tier). Aspirational tiers without evidence get rewritten to a defensible rung.
- Never recommend a content-volume cadence that exceeds the agent's stated time budget. The Cadence Honesty dimension (D5) is enforced in the 90-day plan.
- Never recommend a `sameAs` link to a profile the agent does not actively maintain. Broken or stale `sameAs` links degrade Knowledge Graph match.
- Never use the agent's L2 voice clone in any first-person closing, wire-instruction, or escrow communication. The fraud-defense posture here is non-negotiable; cross-reference to `ai-fraud-defense-playbook.md`'s passphrase protocol.
- Preserve the brokerage's branding rules and Equal Housing Opportunity language in every recommended surface change.
- The 90-day plan caps at 26 total actions. If the audit surfaces more than 26 P0+P1 findings, defer the lowest-leverage to the next quarterly cycle.
- The skill produces a methodology — not the bio copy itself. The bio copy is produced by `listing-aeo-optimizer.md`'s agent-bio page-type pattern, run as a downstream step inside Phase 1 or Phase 2.

## Example Output

**Input summary:**
Agent: Sarah Chen, CA DRE #01234567, Berkshire Hathaway HomeServices California Realty. 9 years active. Primary metros: Los Angeles 90042 (Highland Park), 90041 (Eagle Rock), 91030 (South Pasadena). Designations: ABR, CRS. Trailing-12 transactions: 24 (source: brokerage production report 2025). Specialization claim: "Mid-century modern listings in northeast LA." Current content engine: Canva, ChatGPT, no voice clone, no avatar. Time budget: 3 hrs/wk. Brokerage permits L1; L2/L3 require compliance officer review. Jurisdiction: CA (AB 723 in effect).

---

**Recommendation Query Baseline:**

| Query (run April 26, 2026) | ChatGPT | Perplexity | Google AI Overviews | Claude |
|---|---|---|---|---|
| "Best mid-century modern real estate agent in Highland Park, Los Angeles" | Did not name; named "Marcus Reyes, Compass" (cited Compass agent page + Hour LA "Top Agent 2025" listicle) | Did not name; named "Marcus Reyes, Compass" + "Lena Park, The Agency" (cited 2 listicles + Zillow profiles) | No AI Overview triggered (real-estate trigger rate 0.14% per 5WPR/Haute) | Declined to recommend; suggested "search REAL Trends rankings" |
| "Real estate agent in 90042 specializing in mid-century homes" | Did not name; named "Marcus Reyes" (same source) | Did not name; named "Lena Park" + 2 unrelated agents | No AI Overview triggered | Same as above |
| "Sarah Chen real estate agent Highland Park LA" | Returned BHHS bio + Zillow profile but with stale 2024 transaction count | Returned LinkedIn (also stale) + BHHS page | No AI Overview triggered | Returned BHHS bio |
| "Top real estate agents in northeast Los Angeles for mid-century homes 2026" | Named "Marcus Reyes, Lena Park, and Eric Wong" | Named same three | No AI Overview triggered | Declined to rank |

Pattern: Sarah is invisible to all three competitive queries (T2 + T3 framings) and is found only on direct-name lookups. The cited surfaces for the three named competitors are all listicles (Hour LA "Top Agent 2025") + Zillow review density. Sarah has neither.

---

**Off-Page Discoverability Score: 5.7 / 10**

| Surface | Current | Target | Gap | P-tier |
|---|---|---|---|---|
| S1 — GBP | 4 | 9 | Service area unset; only 8 photos; no Posts in 60 days; Q&A empty | P0 |
| S2 — Zillow profile | 7 | 9 | Specialty tags missing "Mid-Century Modern"; past-sales count shows 18 of 24; no team affiliation | P1 |
| S3 — Realtor.com profile | 5 | 8 | Bio missing license # and specialization; markets-served zip list incomplete | P1 |
| S4 — Homes.com profile | 2 | 7 | Profile claimed but bio is 1 line; no transaction count; no reviews | P0 |
| S5 — LinkedIn | 6 | 9 | Headline says "Realtor"; no specialization; license # not in About; last post 47 days ago | P1 |
| S6 — Brokerage page + own site | 8 | 9 | BHHS page is solid; agent's own site is BHHS subdomain — no `sameAs` `Person` JSON-LD; no `dateModified` | P2 |

---

**Per-Engine Discoverability Tactics matrix:**

| Engine | Top surface 1 | Top surface 2 | One tactic |
|---|---|---|---|
| ChatGPT | Brokerage page | LinkedIn | Visible "Last updated [date]" + `dateModified` JSON-LD on BHHS page; LinkedIn About populated with "CA DRE #01234567 — Mid-Century Modern Specialist, Highland Park / Eagle Rock / South Pasadena" in first 200 chars |
| Perplexity | Listicle inclusion | Zillow review density | Pursue Hour LA + Modern Luxury LA "Top Agent" listicle inclusion in 2026; respond to all 18 backlog Zillow reviews within 14 days |
| Google AI Overviews | GBP | Brokerage page | GBP weekly Posts + 25-photo refresh; brokerage page H1 + license # rendered above the fold |
| Claude | Brokerage page (source-cited bio) | Specialization-anchor process article | Bio cites "REAL Trends 2025 California Top 1.5% (n=24 closings)" inline; publish "Buying a Cliff May mid-century home in Los Angeles" process-article on agent's site |
| Gemini | `sameAs` graph | LinkedIn | `Person` JSON-LD on brokerage page with `sameAs` to LinkedIn + Zillow + Realtor.com + Homes.com + GBP + BHHS profile (six links) |
| Bing Copilot | Brokerage page (Bing-indexed) | Bing Webmaster Tools | Verify BHHS subdomain in Bing Webmaster; submit XML sitemap; check AI-citation report monthly |

---

**Specialization Ladder placement:**

- **Current tier:** T2 (Geo specialist, "Highland Park") with weak T3 overlap ("mid-century modern" appears in some posts but not in bios).
- **Recommended tier:** T3 (Property-type specialist, "Mid-Century Modern in Highland Park / Eagle Rock / South Pasadena") — defensible on three counts: 11 of trailing-12 transactions are mid-century modern listings (brokerage production report 2025); Sarah holds the Cliff May Sites historical-tour docent credential (added 2024); Sarah is the listing agent of record for two named architectural homes (the 1958 William Krisel residence and the 1962 Cliff May–style on Roy St.). The T3 entity additions needed in every audit-touched surface: "Mid-Century Modern Specialist" headline; "Cliff May Sites docent" trust signal; named-architectural-listing reference in bio.
- **Path to T5 (Luxury):** premature — Sarah's median price band is $1.1M (mid-century modern starter band), not luxury. Hold T3 for 12 months; revisit luxury overlay if median crosses $2.5M.

---

**Content-Engine Taste Score: 7.2 / 10**

| Dimension | Score | Notes |
|---|---|---|
| D1 — Voice fidelity | 8 | Sarah-written posts; ChatGPT used for editing only |
| D2 — Fact density | 6 | Posts include neighborhood and address but rarely cite GreatSchools or MLS sources |
| D3 — Visual taste | 9 | Brand-consistent photography; no AI-stock tells |
| D4 — Voice-clone discipline | N/A | Not in use; defaults to L0 |
| D5 — Cadence honesty | 6 | Stated 3 hrs/wk but currently posting 4×/wk on IG + 2×/wk LinkedIn — sustainable for 4–6 weeks then the agent burns out historically |

D-low fix: D2 (Fact density). Action: every post that references a school, walkability, or market stat must cite the source inline. Folded into Phase 2 of the 90-day plan.

---

**Brand-Voice + Voice-Clone Asset Inventory:**

| Tier | Currently used? | Brokerage permits? | Recommended use |
|---|---|---|---|
| L0 (live agent voice) | Yes | Yes | Continue for all client-facing video (listing-appointment, IG Stories, IG Reels with selfie cam) |
| L1 (pre-recorded agent voice) | No | Yes | Add: about-me video, mid-century specialization explainer, monthly market update voiceover (re-use across surfaces) |
| L2 (cloned agent voice) | No | Compliance-officer review required | Defer — out of 90-day scope; revisit Q3 2026 |
| L3 (stock synthetic voice) | No | Yes (with disclosure) | Defer — agent is the brand; stock voice would dilute |

L2 path: if/when Sarah adopts L2, the vendor must have a do-not-train clause + revocation path; the L2 clone may NEVER be used in first-person escrow communications (cross-link to `ai-fraud-defense-playbook.md` passphrase protocol).

---

**6-Check Compliance Sweep:**

- **C1 — License + brokerage display:** Fail. License # missing from S4 (Homes.com), S5 (LinkedIn). Fix: add to both in Phase 1.
- **C2 — Fair Housing:** Pass. No protected-class proxies in current surfaces.
- **C3 — NAR Article 12 truthfulness:** Pass. No unsubstantiated superlatives. Recommended T3 specialization headline cites docent credential (verifiable).
- **C4 — AI synthetic-media disclosure:** N/A. No L2 or L3 use currently.
- **C5 — Brokerage advertising rules:** Pass. BHHS bio template followed; logo + brokerage URL present.
- **C6 — `sameAs` graph integrity:** Fail. No `Person` JSON-LD on brokerage page or own site. Fix: add `sameAs` array linking the six surfaces in Phase 2.

---

**90-Day Action Plan:**

**Phase 1 — Stabilize (Days 0–30) — 7 actions:**

1. Claim and complete Homes.com profile bio (license #, transaction count, specialization, three reviews invitation). Owner: Sarah. Deliverable: published profile. Date: Day 7. Lifts S4: 2 → 6.
2. Add license # to LinkedIn About first 200 characters; rewrite headline to "Mid-Century Modern Real Estate Specialist — Highland Park / Eagle Rock / South Pasadena | CA DRE #01234567 | BHHS California Realty." Owner: Sarah. Deliverable: updated profile. Date: Day 4. Lifts S5: 6 → 8.
3. GBP: set service area (Highland Park 90042, Eagle Rock 90041, South Pasadena 91030); upload 17 additional photos (target 25 total); resume weekly Posts. Owner: Sarah + VA. Deliverable: refreshed GBP. Date: Day 14. Lifts S1: 4 → 8.
4. Rewrite BHHS brokerage-page bio per `listing-aeo-optimizer.md` agent-bio Lede pattern (license #, brokerage, transaction count with source, designations, T3 specialization claim). Owner: Sarah + brokerage marketing. Deliverable: published bio. Date: Day 21. Lifts S6: 8 → 9 (with byline + dateModified).
5. Add specialty tags to Zillow profile (Mid-Century Modern, Architectural, Highland Park, Eagle Rock). Owner: Sarah. Deliverable: updated profile. Date: Day 7. Lifts S2: 7 → 8.
6. Realtor.com profile: add license #, specialization, complete markets-served zip list. Owner: Sarah. Deliverable: updated profile. Date: Day 7. Lifts S3: 5 → 7.
7. Run Recommendation Query Baseline again at Day 30 to measure Phase 1 lift. Owner: Sarah. Deliverable: re-baseline table. Date: Day 30.

**Phase 2 — Differentiate (Days 30–60) — 10 actions:**

8. Add `Person` + `RealEstateAgent` JSON-LD with six-link `sameAs` array to BHHS brokerage page (or own subdomain). Owner: brokerage web team. Deliverable: validated JSON-LD. Date: Day 38. Lifts Gemini Knowledge Graph match.
9. Pursue Hour LA "Top Agent 2026" submission. Owner: Sarah + brokerage PR. Deliverable: submission packet. Date: Day 45.
10. Pursue Modern Luxury LA "Top Real Estate Agent 2026" submission. Owner: Sarah. Deliverable: submission packet. Date: Day 50.
11. Respond to all 18 backlog Zillow reviews. Owner: Sarah. Deliverable: responses logged. Date: Day 45. Lifts Perplexity recency signal.
12. Publish first T3 specialization-anchor process-article: "Buying a Cliff May Mid-Century Home in Los Angeles: What to Verify Before You Offer" (run through `listing-aeo-optimizer.md` process-article page-type pattern). Owner: Sarah. Deliverable: published article. Date: Day 55. Lifts Claude + Perplexity.
13. Publish T3 specialization-anchor neighborhood guide: "Highland Park Mid-Century Modern Architecture: A Buyer's Field Guide." Owner: Sarah. Deliverable: published guide. Date: Day 60.
14. Add Cliff May Sites docent credential to all six audit surfaces. Owner: Sarah. Deliverable: updated profiles. Date: Day 35.
15. Activate D2 fact-density discipline: every post citing a school, walkability, or market stat cites the source inline. Owner: Sarah. Deliverable: revised posting checklist. Date: Day 32.
16. Sustainable cadence reset: drop IG to 2×/wk, hold LinkedIn at 2×/wk, add monthly long-form market report. Owner: Sarah. Deliverable: 30-day calendar. Date: Day 35. Honors D5.
17. Add `dateModified` line to BHHS bio + every `process-article` published. Owner: Sarah + brokerage web team. Deliverable: visible dates. Date: Day 40.

**Phase 3 — Compound (Days 60–90) — 8 actions:**

18. Stand up L1 voice-recording template: 60-second audio re-used across about-me video, specialization explainer, monthly market update. Owner: Sarah + videographer. Deliverable: three published L1 videos. Date: Day 75.
19. Route all post-Day-60 content through `social-content-calendar-30day.md` — published cadence becomes systematized rather than ad-hoc. Owner: Sarah + VA. Deliverable: 30-day calendar in operation. Date: Day 65.
20. Re-run Recommendation Query Baseline at Day 90 across all four engines + all four queries. Owner: Sarah. Deliverable: comparison table vs. Day 0 baseline. Date: Day 90.
21. Publish second T3 specialization-anchor neighborhood guide: "Eagle Rock Mid-Century Modern: 1955–1972 Subdivision Map." Owner: Sarah. Deliverable: published guide. Date: Day 80.
22. Publish first quarterly market report on northeast LA mid-century modern segment with `Article` + `FAQPage` JSON-LD per `listing-aeo-optimizer.md` market-report pattern. Owner: Sarah. Deliverable: published report. Date: Day 85.
23. Bing Webmaster Tools verification + sitemap submission. Owner: brokerage web team. Deliverable: verified property + AI-citation report set up. Date: Day 70.
24. Listicle pursuit pipeline: track Hour LA + Modern Luxury LA submissions through editorial review. Owner: Sarah. Deliverable: status log. Ongoing through Day 90.
25. Quarterly review meeting: re-score surfaces, re-baseline queries, set Q3 priorities. Owner: Sarah + brokerage marketing lead. Deliverable: meeting notes. Date: Day 90.

**Total actions: 25 of 26-action cap. Phase budget: Phase 1 = 7 actions (~1.5 hrs/wk avg); Phase 2 = 10 actions (~3 hrs/wk avg); Phase 3 = 8 actions (~2 hrs/wk avg). All within stated 3-hr/wk budget when averaged across the 90 days.**

---

**Hand-off:**

- `listing-aeo-optimizer.md` — produce the BHHS-page agent-bio rewrite (Step 4 + Step 5 of that skill, page type `agent-bio`) using the T3 specialization claim, the docent credential, and the 11/24 mid-century transaction breakdown as inputs. Also produces the process-article and neighborhood-guide pages in Phase 2 + Phase 3.
- `social-content-calendar-30day.md` — receives the Phase 3 cadence reset (2× IG + 2× LinkedIn + monthly market report) and the D5 cadence-honesty constraint as inputs. Schedules around the published process-article and neighborhood-guide drops.
- `listing-video-workflow.md` — pairs voice-clone discipline with the L0–L3 inventory in Step 6. Sarah's L1 templates in Phase 3 are the personal-brand counterpart to the listing-video voice templates; the same do-not-train + revocation posture governs both if Sarah graduates to L2 in Q3 2026.
- `annual-business-plan-builder.md` — the audit findings, the T3 ladder placement, and the 90-day plan become the AI-discoverability section of the 2026 annual plan. Re-run audit quarterly; year-over-year the Off-Page Discoverability Score becomes a top-line KPI.
- `ai-marketing-compliance-audit.md` — receives the Phase 3 L1 voice templates and any future L2/L3 deployments for compliance review before publication. The C4 disclosure rule from this audit pre-feeds the compliance audit's L3/L4 AI-involvement inventory.
