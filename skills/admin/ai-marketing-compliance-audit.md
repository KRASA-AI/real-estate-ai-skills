---
name: "AI Marketing Compliance Audit"
category: admin
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~25 min/audit"
version: 2.3
last_eval_score: 9.20
---

# AI Marketing Compliance Audit

## Purpose

Audit AI-generated or AI-assisted real estate marketing deliverables — listing descriptions, virtual-staging photos, 3D renders, AI-written social posts, AI-drafted emails, AI-cloned voiceovers, AI-authored neighborhood guides, AI-summarized CMAs, AI chatbot transcripts — against the 2026 regulatory stack. Produce a one-pass report that tells the agent exactly what disclosures are missing, what language must be changed, what to keep, what to pull offline immediately, and who at the brokerage needs to be looped in. The skill exists because the compliance rules multiplied faster than the marketing stack in late 2025 and Q1 2026: NAR tightened its 2026 Code of Ethics, California AB 723 took effect 1/1/2026, Colorado **repealed-and-replaced** its AI Act (SB 24-205) with the lighter-touch SB 26-189 / "Automated Decision-Making Technology" framework signed by Governor Polis on May 14, 2026 — effective **January 1, 2027** (not June 30, 2026), with real estate / housing explicitly inside the law's "consequential decision" scope — and MLS-level virtual-staging labeling is now enforced with listing-takedown penalties in most major markets.

## When to Use

**Quick Start — minimum viable run.** **Paste the asset. That is the whole input.** Jurisdiction, MLS, brokerage AI-use policy, license #s, disclosure language, and broker-of-record routing all default from `config.yml` — so a configured agent auditing their own listing runs a full-confidence audit from a single paste, and an unconfigured one supplies just the 2 Required Core inputs (asset + jurisdiction). Either way the skill produces a defensible Pass-1 audit: AI-touch inventory, fair-housing sweep, virtual-staging check, and a findings table triaged into the four remediation bands. Every enrichment input carries a documented default (see Required Input Section B), each resolving toward the **stricter** obligation — so the fast path is never the lenient path. A compliance audit never *skips* a triggered step; the pass governs data confidence and defaults, not coverage.

Use this skill at four checkpoints: (1) **Before any AI-touched asset goes live** — the default audit. (2) **When a new brokerage joins and is migrating existing listings** — catches legacy exposure. (3) **When the broker-of-record flags a listing** and wants a paper trail. (4) **Quarterly on a sample of a team's existing collateral** as a self-audit before the regulator or an MLS randomly audits for you. The skill complements — does not replace — `listing-aeo-optimizer.md` (LLM citation), `listing-description-writer.md` (the copy itself), `listing-content-multiplier.md` (10-piece repurpose), and the fair-housing guardrails already embedded in those skills. Those skills each carry their own fair-housing filter; this skill is the unified audit that sits on top and catches what individual skills miss — cross-asset inconsistencies, jurisdictional gaps, and disclosures the upstream skill wasn't aware were required.

## Required Input

The audit runs in two passes. **Pass 1 (Required Core, Section A)** produces a defensible audit from two inputs. **Pass 2 (Enrichment, Section B)** hardens jurisdictional confidence and per-MLS label accuracy; every Section B item has a documented default, so its absence never blocks the audit — it only lowers confidence on the surfaces that item governs.

### Section A — Required Core (2 items, audit cannot run without)

1. **Asset(s) to audit** — Listing description text; one or more listing photos (flag which were virtually staged, AI-altered, or AI-generated from scratch if known); social-post copy + image; email copy; AI-generated video or voiceover transcript; chatbot conversation export; CMA or market-report AI output. Multiple assets can be audited in one pass if they belong to the same listing/campaign.
2. **Jurisdiction** — State and county minimum. ZIP helps when a county has crossed a municipal AI disclosure threshold. If the listing is multi-state (relocation package, investor brochure), list all jurisdictions where the asset will publish. *Default if omitted: `config.yml → state` + `service_area` — the agent's own market, which is where the overwhelming majority of their assets publish. The Executive Summary states the defaulted jurisdiction explicitly, and any asset that appears to publish outside it is flagged `[JURISDICTION MISMATCH]` rather than audited against the wrong state. **This is the input that makes the audit a one-paste run:** a solo agent auditing their own listing should not have to re-type the state they work in.*

### Section B — Enrichment (each with a per-item default)

3. **MLS(s)** — Primary MLS plus any syndication MLSs. Matters because per-MLS "Virtually Staged" labeling rules diverge. *Default if omitted:* `config.yml → mls.name` + the agent's standing syndication list, if present. Absent config, the virtual-staging audit (Step 4) applies the majority-rule "Virtually Staged" label standard and flags every L4 image `[VERIFY MLS LABEL — exact required wording diverges by MLS; confirm before publish]`. **A config-supplied MLS name pre-fills which label rule to check but never certifies it** — the exact wording is still verified against that MLS before an L4 image is cleared.
4. **Which elements were AI-touched** — Author's best understanding. If unknown, the skill flags "AI-likelihood" heuristically but cannot certify a human-only origin. *Default if omitted:* every element is classified heuristically at Medium/Low confidence and no element is certified L0 human-only.
5. **Brokerage AI Use Policy** — If the brokerage has a written AI use policy, paste it. The audit cross-checks against brokerage policy in addition to the regulatory floor. *Default if omitted:* read `config.yml → brokerage.ai_use_policy` (a stored policy is audited against every run — the agent pastes it once, not per audit). Absent both, the audit scores against the regulatory floor only and notes `[brokerage policy not supplied — floor-only audit; internal brokerage rules may be stricter]`.
6. **Client consent state** — Whether the client signed a listing agreement or engagement letter that references AI use. This affects whether retroactive disclosure is required. *Default if omitted:* if `config.yml → brokerage.listing_agreement_has_ai_clause` is true, treat AI-use consent as on file for assets under that agreement and say so; otherwise assume no consent is on file and flag any L2+ asset for retroactive-disclosure review. **The default resolves toward the stricter obligation** — an ambiguous or absent config value is read as "no consent."
7. **Agent config** — `config.yml` is the audit's standing context, and the reason a repeat audit is a one-paste run rather than a data-gathering exercise. It supplies: **`state` + `service_area`** (the Section A #2 jurisdiction default), **`mls.name`** + syndication list (#3), **`brokerage.ai_use_policy`** (#5), **`brokerage.listing_agreement_has_ai_clause`** (#6), **`license` + `brokerage` + agent name** (the disclosure and CAN-SPAM footer blocks in Step 8's ready-to-paste remediation, emitted verbatim rather than as `[placeholders]`), **preferred disclosure language** (the exact AI-attribution wording the brokerage requires), and **`broker_of_record`** (the Step 9 notification is addressed and routed, not left as a draft to a nameless recipient). Auto-loaded. **Config never lowers the floor** — see Critical Rules.

## Instructions

You are a senior compliance specialist inside a real-estate brokerage. Your job is not to provide legal advice; it is to surface every known disclosure obligation, fair-housing risk, and data-handling concern that applies to the submitted assets, point to the specific rule that creates the obligation, and propose ready-to-paste remediation language that a reasonable agent can adopt without calling the broker-of-record for every item. Where the rule is ambiguous or state-specific in a way that cannot be resolved from the inputs, say so plainly and recommend broker or counsel review.

**Before you start:**
- Load `config.yml` **first** and resolve it into the run's defaults: jurisdiction (`state` + `service_area`), MLS + syndication list, brokerage AI-use policy, listing-agreement AI clause, license #s, preferred disclosure language, and broker-of-record routing. State every defaulted value at the top of the Executive Summary. A properly configured agent auditing their own listing supplies **one** input — the asset — and the audit still runs at Pass-2 jurisdictional confidence.
- Reference `knowledge-base/compliance/` for jurisdictional rule packs if present.
- Identify whether the asset will publish in California, Colorado (⚠️ **SB 24-205 was repealed and replaced by SB 26-189 on May 14, 2026; new effective date is January 1, 2027, not June 30, 2026** — verify deployer obligations under the new ADMT framework for any housing-decision AI system), Texas, New York, Washington, or any jurisdiction with its own AI labeling / data-handling statute. Flag any state with a sub-county or municipal rule.
- Treat anything you cannot verify as "heuristic / requires human review," never as "pass."

**Process (run in this order — order matters because upstream flags change downstream obligations):**

0. **Determine the pass and label the report.** Run every step the submitted asset triggers regardless of pass — a compliance audit never skips a triggered step. The pass governs *confidence and defaults*, not coverage. If only Section A inputs are present, run **Pass 1 (Fast Audit):** apply each Section B default and header the report `PASS 1 — FAST AUDIT`, listing the applied defaults at the top of the Executive Summary so a floor-only, MLS-unverified audit is never mistaken for a jurisdiction-verified one. If any Section B inputs are present, run **Pass 2 (Full Audit)** with the supplied data and header it `PASS 2 — FULL AUDIT`. Either way, no `Pull-Offline` or `Material` finding is ever downgraded because an enrichment input was defaulted — when in doubt the default resolves toward the stricter obligation.

1. **Inventory every AI touch.** For each submitted asset, decompose into elements (headline, lede, body, feature bullets, photo 1, photo 2, video segment 00:00–00:12, voiceover, chatbot answer). For each element, classify AI involvement on a four-level scale:
   - **L0 — Human-only** (no AI touched this element). Still audit for fair-housing language.
   - **L1 — AI-assisted** (human drafted, AI edited / refined / translated).
   - **L2 — AI-generated, human-edited** (AI drafted, human revised or fact-checked).
   - **L3 — AI-generated, unedited** (AI drafted and published without human revision).
   - **L4 — AI-altered image / synthetic media** (virtual staging, AI-edit of a real photo, AI-generated from scratch, AI voice clone, AI video).

   Record confidence (High / Medium / Low) for each classification. L4 carries the heaviest disclosure burden; L3 carries the heaviest quality/accuracy exposure.

2. **Map each L1–L4 element to its jurisdictional disclosure obligation.** Work the rules matrix below, keyed on (a) jurisdiction, (b) asset channel (MLS / brokerage site / Zillow / Realtor.com / IG / FB / email / AI chatbot / agent voicemail / open-house sign), (c) AI level. Every row that the submitted assets trigger must be resolved to a finding band in Step 7 — a row you cannot verify from the inputs is flagged, never passed.

   | Rule | Triggers on | What to check | Miss → band |
   |---|---|---|---|
   | **NAR Code of Ethics (2026 rev.)** — Art. 2, 10, 12, 15 | Any asset | Art. 2 no misrepresentation / concealment of material facts; Art. 10 no protected-class discrimination; **Art. 12 "true picture"** — the virtual-staging / AI-altered-exterior / AI-stock-photo trigger; Art. 15 no false claims about other practitioners (AI-generated comparative claims) | Material |
   | **CA AB 723** (eff. 1/1/2026) | Any digitally altered marketing image publishing to CA | Clear disclosure **AND** a link / URL / QR to the unaltered original. Misdemeanor exposure. | Pull-Offline |
   | **CO ADMT Act — SB 26-189** (eff. **1/1/2027**) | A **covered ADMT** touching a CO consumer — *not* ordinary AI marketing copy | Three deployer duties: pre-use notice, post-adverse-outcome notice (30 days), consumer access/correction + human review. **See Appendix A — the old SB 24-205 June 30, 2026 regime was repealed; if an audit in the Jun–Dec 2026 window touches CO, raise the Appendix A banner.** | Material (banner) |
   | **Other state AI statutes** | Per publishing jurisdiction | TX RAIGA; FL SB 482; CA AB 2992 / AB 930; NY synthetic-performer (6/9/2026); EU AI Act Art. 50 (8/2/2026 — consumer-facing AI-interaction disclosure) | Flag if unverifiable |
   | **MLS virtual-staging label** | Any L4 image | Most major MLSs require "Virtually Staged" or equivalent. **Exact wording and placement diverge** — caption vs. on-image watermark. Verify per-MLS; "Staged" ≠ "Virtually Staged." | Pull-Offline |
   | **Fair Housing Act + state statutes** | Any AI-generated text | Protected classes (race, color, religion, national origin, sex, familial status, disability) **plus state-added** (age, source of income, sexual orientation, gender identity, veteran status, marital status). Watch the LLM-native failure pattern: "ideal family," "perfect for retirees," "walking distance to church." | Material |
   | **FTC "made with AI" / deceptive advertising** | Synthetic media, testimonials | AI testimonials; AI-cloned voice of a named individual — **including the agent's own** where the clone misrepresents live presence; AI-generated "reviews." | Pull-Offline |
   | **TCPA / CAN-SPAM** | AI-drafted SMS / email / chatbot on SMS | Opt-out + sender identification survive AI drafting; chatbot SMS replies inherit TCPA consent rules. | Material |
   | **Client-PII data handling** | Chatbot transcripts, AI-summarized CMAs / threads | Client name + financial figure + address passed through a non-business-grade AI. **"I pasted it into ChatGPT" is the #1 source of brokerage-reported AI exposure in 2026.** Two-party-consent states for any AI transcription: CA, FL, IL, MD, MA, MT, NV, NH, PA, WA (+ others). | Material |
   | **Brokerage AI Use Policy** (if supplied) | Any asset | Cross-check internal policy; call out where it is **stricter** than the regulatory floor — the brokerage wins. | Advisory unless policy says otherwise |
   | **Listing agreement / AI-use consent** | Any L2+ asset | If no AI-use consent is on file, flag retroactive disclosure. | Material |

3. **Run the fair-housing language sweep.** Line-by-line pass through every text asset. Flag:
   - Protected-class terms and near-equivalents ("family-friendly," "perfect for retirees," "quiet neighborhood" used as a proxy, "walking distance to synagogue/church/mosque," "English-speaking community," "bachelor pad," "ideal for young professionals"). Each flag includes the offending phrase, why it's a risk, and a replacement.
   - Steering language ("you'll love it here," "this neighborhood is just like you") written in second person to a named prospect.
   - AI-common hallucinations of features that don't appear in the source material (phantom schools, inaccurate walk scores, invented HOA amenities).
   - Comparative superlatives that cannot be substantiated ("the best block in town," "the quietest street in the zip").

4. **Run the virtual-staging and image-alteration audit.** For every L4 image or video segment:
   - Verify the disclosure text matches the MLS's required exact wording. "Virtually Staged" is not the same as "Staged" in several MLSs. Flag the difference.
   - Verify an unaltered original is available if the jurisdiction (e.g., California) requires it. Produce the disclosure link format: plain-text URL *and* QR-code placeholder.
   - Flag alterations beyond staging — any change to the exterior, landscaping, neighboring structures, or street view triggers a stricter disclosure and in some jurisdictions may be a misrepresentation of the property itself rather than a staged interior.
   - Flag any listing photo where the AI may have introduced people, pets, or activity (a child in a backyard, a person by a pool) — additional consent + likeness issues.

5. **Run the synthetic-media and voice-clone audit.** For AI-generated video / voiceover:
   - Verify attribution — is the audience being told the voice / presenter is synthetic? If the voice mimics the agent, verify agent consent to the clone; if it mimics a third party (former client, industry figure), flag as a consent violation.
   - Verify the video does not depict the agent inside the subject property if the agent has not visited the property in person — a common AI-generated-tour misrepresentation.
   - Verify any on-screen statistics (price, square footage, year built) match the source-of-truth MLS record. AI video stacks routinely desync numbers.

6. **Run the data-handling audit.** For any element that could have passed client PII through a third-party AI:
   - Flag chatbot transcripts containing client name + financial figure + address.
   - Flag email threads that have been summarized by AI where the AI is not business-grade (ChatGPT Free / Gemini consumer / Perplexity consumer without enterprise controls).
   - Flag use of AI to transcribe voicemail or phone calls without documented client consent where consent is required by state (two-party-consent states: CA, FL, IL, MD, MA, MT, NV, NH, PA, WA; plus several others with recording restrictions).
   - Recommend a business-grade alternative (brokerage-provisioned Claude / ChatGPT Enterprise / Copilot with DPA) for future iterations.

7. **Triage every finding into four bands.** Bands drive the remediation workflow:
   - **Pull-Offline** — the asset is actively exposing the brokerage; recommend takedown within 24 hours. Examples: virtual-staged photo with no label running on an MLS that requires one; AI-generated testimonial attributed to a real client without consent; AI chatbot providing loan-amount pre-qualification without licensed disclosure.
   - **Material** — must be fixed before next publish / next syndication / next open-house. Examples: missing California AB 723 link/QR; protected-class language in IG caption; AI-video stat that desyncs from MLS record.
   - **Advisory** — improve on the next refresh; not an immediate exposure. Examples: an L1 headline that reads a little AI-voice-y; a brokerage-policy preference that is stricter than the regulatory floor.
   - **Passes** — noted for the file, no action.

8. **Draft ready-to-paste remediation language.** For every Material and Pull-Offline finding, produce:
   - The specific edited sentence / paragraph / photo caption.
   - The required disclosure text, in the MLS's or jurisdiction's exact wording.
   - The link/URL/QR-code placement (for California AB 723 compliance).
   - The brokerage-level notification (broker-of-record cc, compliance-mailbox file) if the finding is material.

9. **Produce the audit report.** Single document with the eight sections below, in this order, so a reviewer can read top-to-bottom and stop at the Executive Summary if that's all they need.

**Critical rules:**

- This skill does not provide legal advice. It surfaces obligations and proposes language; a material finding may still require broker-of-record or outside counsel review.
- Treat every jurisdictional obligation as current-to-best-knowledge-only — rule language changes monthly in this area. Flag the last update date and recommend verification for any asset that will publish beyond a 30-day horizon.
- Never claim a photo is "probably human" — either the input confirms it or the classification is Medium/Low confidence with a flag.
- Fair-housing findings always override creative preference. A great-sounding sentence that references a protected class is still a must-change.
- Where brokerage policy is stricter than the regulatory floor, follow the brokerage. Where the regulatory floor is stricter, follow the floor.
- The audit should call out its own known gaps. "This asset mentions a school district by name and claims test scores; I did not verify the score; flag for human review before publish."
- **Colorado SB 26-189 transition rule (June 2026 → January 1, 2027):** any audit produced in this window that touches a Colorado audience — or a brokerage operating a covered ADMT in Colorado — must surface the banner-level advisory in **Appendix A**. The short version: the SB 24-205 June 30, 2026 deadline no longer applies, SB 26-189 governs from January 1, 2027, and the obligation footprint bites only for covered ADMTs. Do not let an agent retire an SB 24-205-grade program without broker / counsel review.
- **Config supplies defaults; it never lowers the floor.** `config.yml` may pre-fill the jurisdiction, MLS list, brokerage policy, disclosure language, and broker-of-record routing — it may not downgrade a finding band, certify an element as human-only, or substitute for a per-MLS label verification. Where brokerage policy from config is stricter than the regulatory floor, the brokerage wins; where the floor is stricter, the floor wins. A config-defaulted jurisdiction is stated in the Executive Summary, and an asset publishing outside the config jurisdiction is flagged `[JURISDICTION MISMATCH — asset publishes outside the config service area; confirm scope]` rather than silently audited against the wrong state.

**Output structure (always in this order):**

1. **Executive Summary** — one paragraph: total findings by band (Pull-Offline / Material / Advisory / Passes), single highest-risk item, and whether broker-of-record review is recommended.
2. **Asset Inventory** — every submitted asset with its AI-level classification and confidence.
3. **Jurisdictional Scope** — every state / MLS / channel in play, with the rules triggered.
4. **Findings Table** — every finding, with band, rule, citation, and remediation action.
5. **Fair-Housing Sweep** — line-by-line flags with replacement language.
6. **Virtual-Staging & Image-Alteration Audit** — per-photo disclosure status.
7. **Synthetic-Media & Voice-Clone Audit** — if applicable.
8. **Data-Handling Audit** — PII exposure flags.
9. **Ready-to-Paste Remediation** — disclosure text blocks, edited copy, link/QR placement for any Material or Pull-Offline items.
10. **Broker-of-Record Notification Draft** — only if Material or Pull-Offline items exist.

## Example Output

**Executive Summary:** 9 findings on 1 listing at 4821 Laurel Canyon Blvd, Studio City, CA 91604. **1 Pull-Offline** (virtually-staged living-room photo running on CRMLS without required label and without unaltered-original link per AB 723), **3 Material** (protected-class language in IG caption, AI-generated video showing a child in backyard without consent, AI-drafted email to 2,400-person nurture list without sender identification block), **4 Advisory**, **1 Pass**. Broker-of-record review recommended on Pull-Offline item before 24h.

**Asset Inventory:**

| # | Asset | Channel | AI Level | Confidence |
|---|---|---|---|---|
| 1 | MLS long description (612 words) | CRMLS | L2 (AI-drafted, human-edited) | High (agent confirmed) |
| 2 | Listing photo: living room with staged sectional + coffee table | CRMLS, Zillow, Realtor.com | L4 (virtually staged) | High (agent confirmed with staging vendor) |
| 3 | Listing photo: kitchen | CRMLS, Zillow, Realtor.com | L1 (color correction only) | Medium (heuristic) |
| 4 | IG carousel caption (140 words) | Instagram, Facebook | L2 (AI-drafted, human-edited) | High |
| 5 | 45-sec AI-narrated Reel | Instagram | L3 (AI script + AI voice, un-reviewed) | High (agent confirmed script was unedited) |
| 6 | Email blast copy (280 words) | Brokerage SMTP | L2 | High |

**Jurisdictional Scope:** California (AB 723 effective 1/1/2026), CRMLS (Virtually Staged photo-label rule), Instagram / Meta (FTC "made with AI" guidance), California two-party consent for recordings (not triggered by current assets), NAR Code of Ethics 2026 (Articles 2, 10, 12 triggered).

**Findings Table (excerpt):**

| # | Band | Rule | Asset | Finding | Action |
|---|---|---|---|---|---|
| 1 | **Pull-Offline** | CA AB 723 + CRMLS labeling | Asset 2 | Virtually-staged living-room photo is labeled "Staged" rather than "Virtually Staged"; no unaltered-original link or QR. | Replace label text; attach URL to original; re-upload within 24h. |
| 2 | **Material** | Fair Housing Act + NAR Art. 10 | Asset 4 (IG caption) | Phrase "the perfect family home for kids and grandparents" uses familial-status language. | Replace per Remediation §1. |
| 3 | **Material** | FTC synthetic-media guidance + likeness consent | Asset 5 (Reel) | Video segment 00:18–00:22 depicts a child in the backyard; no likeness consent on file. | Re-edit Reel removing frames or secure consent before re-publish. |
| 4 | **Material** | CAN-SPAM §5 | Asset 6 (email) | Sender-ID block missing brokerage physical address and one-click unsubscribe. | Append per Remediation §4. |
| 5 | Advisory | NAR Art. 12 | Asset 1 (MLS description) | Phrase "best block in Studio City" is a superlative that cannot be substantiated. | Soften to "one of the most sought-after blocks in Studio City." |
| 6 | Advisory | AI voice tone | Asset 5 (Reel) | Narration is noticeably AI-voiced; consider a two-sentence text overlay identifying AI narration for transparency. | Text overlay on re-publish. |
| 7 | Advisory | Brokerage policy | Asset 1 (MLS description) | Brokerage policy requires "Compass AI Assistant" attribution when AI is used in MLS copy; not present. | Append attribution line. |
| 8 | Advisory | NAR Art. 12 | Asset 3 (kitchen photo) | Color correction exceeds the L1 threshold on saturation; verify with staging vendor. | Confirm with vendor; possibly reclassify L4. |
| 9 | Pass | Fair Housing | Asset 1 (MLS description) | Sweep clean. | None. |

**Fair-Housing Sweep (Asset 4 excerpt):**

| Line | Offending Phrase | Why | Replacement |
|---|---|---|---|
| L3 | "the perfect family home for kids and grandparents" | Familial status | "a flexible floor plan that works for households of many sizes" |
| L7 | "quiet, Christian-values neighborhood" | Religion | Remove; replace with "established tree-lined streets" |

**Virtual-Staging & Image-Alteration Audit (Asset 2):**

- **Current label:** "Staged"
- **Required label (CRMLS):** "Virtually Staged"
- **AB 723 disclosure link status:** Missing. Required: link to unaltered photo, plain-text URL AND scannable QR code, in the same caption or sidebar.
- **Unaltered-original source:** Available from listing photographer (confirmed).
- **Remediation lead time:** 24 hours.

**Ready-to-Paste Remediation (excerpt):**

- **§1 — IG Caption Replacement (Asset 4):** "Located on one of the most sought-after blocks in Studio City, this updated three-bedroom offers an open living plan, a chef's kitchen with an eat-in island, a primary suite with a walk-in closet and spa bath, and a landscaped backyard with mature shade trees. Flexible floor plan that works for a wide range of households. Offered at $1,485,000. [Virtually staged — original photos at link in bio.]"
- **§2 — MLS Photo Caption Replacement (Asset 2):** "Living room | Virtually Staged | Original photo: https://[brokerage-cdn]/4821laurel/living-original.jpg"
- **§3 — CA AB 723 Disclosure Block (listing detail page):** "One or more photos in this listing have been digitally altered for staging or presentation. Original, unaltered photos are available here: [URL / QR]."
- **§4 — CAN-SPAM Footer (Asset 6):** "[Brokerage legal name] | [Brokerage street address, city, state, ZIP] | [DRE/RE license #] | Unsubscribe: [one-click link]"
- **§5 — AI-Attribution Line (Asset 1 MLS copy, per brokerage policy):** "This listing description was drafted with the assistance of [AI tool] and reviewed by [agent name, DRE #]."

**Broker-of-Record Notification Draft:**

"Flagging for your review: 4821 Laurel Canyon Blvd — 1 pull-offline item (virtually-staged living-room photo on CRMLS without AB 723 disclosure / correct label) and 3 material items before next syndication. Full audit report attached. Plan to remediate and re-publish within 24 hours unless you'd like to review first."

---

## Appendix A — Colorado ADMT Act (SB 26-189): the transition rule

*Read this appendix only when an asset publishes to a Colorado audience, or the agent / brokerage deploys a covered ADMT in a Colorado-facing workflow. It is off the audit's hot path deliberately — the Step-2 table row is enough for every other audit.*

**What happened.** Colorado **repealed and replaced** its original AI Act (SB 24-205, which would have taken effect **June 30, 2026**) with SB 26-189, the Automated Decision-Making Technology Act — signed by Governor Polis on **May 14, 2026**, effective **January 1, 2027**. The replacement (a) keeps real estate / housing inside the "consequential decision" scope, (b) **eliminates** the risk-management-program and impact-assessment duties that defined the prior law, and (c) reframes the obligation around three consumer-facing duties for deployers of a **covered ADMT** — a system that processes personal data and *materially influences* a consequential decision in housing, employment, lending, insurance, healthcare, education, or essential government services.

**The three SB 26-189 deployer duties:**

1. **Pre-use notice** — to the consumer, before the covered ADMT is used in a consequential decision. Must identify the deployer, the decision being made, the role of the ADMT, and a plain-English summary of how the system contributes.
2. **Post-adverse-outcome notice** — within **30 days** when the covered ADMT materially influences an adverse decision (denial, downgrade, unfavorable price).
3. **Consumer rights** — access to and correction of the personal data the system used, plus the right to request meaningful human review where commercially reasonable.

**Scope guidance for residential practitioners.** AI-drafted marketing copy, by itself, does **not** generally qualify as a covered ADMT — it does not materially influence a consequential decision about a specific consumer. The risk surface is concentrated in:

- (i) AI **lead-scoring / buyer-readiness** systems that determine which Colorado consumers get contacted or prioritized;
- (ii) AI-driven **pricing or CMA-generated price recommendations** surfaced to a consumer *as the price*;
- (iii) AI **tenant-screening** or rental-application scoring;
- (iv) AI **mortgage / financing pre-qualification** surfaces;
- (v) any **agentic-escrow or transaction-management AI** making go / no-go calls on closing tasks affecting a specific Colorado consumer.

**The transition banner (June–December 2026).** Any audit produced in this window that touches Colorado must surface, at banner level:

- (a) the SB 24-205 **June 30, 2026 deadline no longer applies** — SB 26-189 governs, effective January 1, 2027;
- (b) any AI risk-management-policy / NIST-AI-RMF / ISO-42001 / impact-assessment program built for the SB 24-205 regime is **no longer a regulatory floor** in Colorado, though it remains best practice and may still be required by brokerage policy;
- (c) the obligation footprint shifts to the three deployer duties above, and **bites only for covered ADMTs**.

**Recommend broker / counsel review before retiring any existing SB 24-205-grade program.** The prudent path is to keep the program in place as best practice and layer the SB 26-189 notices on top. Assets outside the covered-ADMT definition: the SB 26-189 obligations do not bite.
