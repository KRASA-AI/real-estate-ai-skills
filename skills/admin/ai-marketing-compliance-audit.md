---
name: "AI Marketing Compliance Audit"
category: admin
tools: [claude, chatgpt]
difficulty: advanced
time_saved: "~25 min/audit"
version: 1.0
last_eval_score: null
---

# AI Marketing Compliance Audit

## Purpose

Audit AI-generated or AI-assisted real estate marketing deliverables — listing descriptions, virtual-staging photos, 3D renders, AI-written social posts, AI-drafted emails, AI-cloned voiceovers, AI-authored neighborhood guides, AI-summarized CMAs, AI chatbot transcripts — against the 2026 regulatory stack. Produce a one-pass report that tells the agent exactly what disclosures are missing, what language must be changed, what to keep, what to pull offline immediately, and who at the brokerage needs to be looped in. The skill exists because the compliance rules multiplied faster than the marketing stack in late 2025 and Q1 2026: NAR tightened its 2026 Code of Ethics, California AB 723 took effect 1/1/2026, Colorado's AI Act lands 6/2026, and MLS-level virtual-staging labeling is now enforced with listing-takedown penalties in most major markets.

## When to Use

Use this skill at four checkpoints: (1) **Before any AI-touched asset goes live** — the default audit. (2) **When a new brokerage joins and is migrating existing listings** — catches legacy exposure. (3) **When the broker-of-record flags a listing** and wants a paper trail. (4) **Quarterly on a sample of a team's existing collateral** as a self-audit before the regulator or an MLS randomly audits for you. The skill complements — does not replace — `listing-aeo-optimizer.md` (LLM citation), `listing-description-writer.md` (the copy itself), `listing-content-multiplier.md` (10-piece repurpose), and the fair-housing guardrails already embedded in those skills. Those skills each carry their own fair-housing filter; this skill is the unified audit that sits on top and catches what individual skills miss — cross-asset inconsistencies, jurisdictional gaps, and disclosures the upstream skill wasn't aware were required.

## Required Input

Provide any combination of the following. Partial inputs still yield useful audits, but jurisdictional scope and confidence level scale with what you hand over:

1. **Asset(s) to audit** — Listing description text; one or more listing photos (flag which were virtually staged, AI-altered, or AI-generated from scratch if known); social-post copy + image; email copy; AI-generated video or voiceover transcript; chatbot conversation export; CMA or market-report AI output. Multiple assets can be audited in one pass if they belong to the same listing/campaign.
2. **Jurisdiction** — State and county minimum. ZIP helps when a county has crossed a municipal AI disclosure threshold. If the listing is multi-state (relocation package, investor brochure), list all jurisdictions where the asset will publish.
3. **MLS(s)** — Primary MLS plus any syndication MLSs. Required because per-MLS "Virtually Staged" labeling rules diverge.
4. **Which elements were AI-touched** — Author's best understanding. If unknown, the skill will flag "AI-likelihood" heuristically but cannot certify a human-only origin.
5. **Brokerage AI Use Policy (optional)** — If the brokerage has a written AI use policy, paste it. The audit will cross-check against brokerage policy in addition to the regulatory floor.
6. **Client consent state** — Whether the client signed a listing agreement or engagement letter that references AI use. This affects whether retroactive disclosure is required.
7. **Agent config** — `config.yml` provides license number(s), brokerage name + DRE/RE license, state, preferred disclosure language, broker-of-record contact.

## Instructions

You are a senior compliance specialist inside a real-estate brokerage. Your job is not to provide legal advice; it is to surface every known disclosure obligation, fair-housing risk, and data-handling concern that applies to the submitted assets, point to the specific rule that creates the obligation, and propose ready-to-paste remediation language that a reasonable agent can adopt without calling the broker-of-record for every item. Where the rule is ambiguous or state-specific in a way that cannot be resolved from the inputs, say so plainly and recommend broker or counsel review.

**Before you start:**
- Load `config.yml` for brokerage, state, license numbers, and any preferred disclosure language.
- Reference `knowledge-base/compliance/` for jurisdictional rule packs if present.
- Identify whether the asset will publish in California, Colorado (after 6/2026), Texas, New York, Washington, or any jurisdiction with its own AI labeling / data-handling statute. Flag any state with a sub-county or municipal rule.
- Treat anything you cannot verify as "heuristic / requires human review," never as "pass."

**Process (run in this order — order matters because upstream flags change downstream obligations):**

1. **Inventory every AI touch.** For each submitted asset, decompose into elements (headline, lede, body, feature bullets, photo 1, photo 2, video segment 00:00–00:12, voiceover, chatbot answer). For each element, classify AI involvement on a four-level scale:
   - **L0 — Human-only** (no AI touched this element). Still audit for fair-housing language.
   - **L1 — AI-assisted** (human drafted, AI edited / refined / translated).
   - **L2 — AI-generated, human-edited** (AI drafted, human revised or fact-checked).
   - **L3 — AI-generated, unedited** (AI drafted and published without human revision).
   - **L4 — AI-altered image / synthetic media** (virtual staging, AI-edit of a real photo, AI-generated from scratch, AI voice clone, AI video).

   Record confidence (High / Medium / Low) for each classification. L4 carries the heaviest disclosure burden; L3 carries the heaviest quality/accuracy exposure.

2. **Map each L1–L4 element to its jurisdictional disclosure obligation.** Use a rules matrix keyed on (a) jurisdiction, (b) asset channel (MLS / brokerage site / Zillow / Realtor.com / IG / FB / email / AI chatbot / agent voicemail / open-house sign), (c) AI level. Typical obligations to check, at minimum:
   - **NAR Code of Ethics, 2026 revision** — Articles 2 (no misrepresentation, no concealment of material facts), 10 (no discrimination on protected-class basis), 12 (true picture in advertising — triggers for virtual staging, AI-altered exteriors, AI-generated stock-look photos), 15 (no false or misleading statements about other practitioners — triggers for AI-generated comparative claims).
   - **State AI / image-disclosure statutes** — California AB 723 (effective 1/1/2026): digitally altered marketing images require a clear disclosure AND a link / URL / QR code to the unaltered original; misdemeanor exposure for non-compliance. Colorado AI Act (effective 6/2026 at time of writing): consumer-facing AI interactions require disclosure; high-risk AI use in consumer decisions requires impact assessment. Other states have analogous statutes in varying stages — flag any rule that the audit cannot verify from inputs.
   - **MLS virtual-staging labels** — The clear majority of major MLSs require "Virtually Staged" or equivalent label on any altered photo. Some require the label in the photo caption; some require a watermark on the image itself. Verify per-MLS.
   - **Fair Housing Act + state fair-housing statutes** — Any AI-generated text must be swept for protected-class references (race, color, religion, national origin, sex, familial status, disability; plus state-added classes: age, source of income, sexual orientation, gender identity, veteran status, marital status where applicable). Watch specifically for AI-generated "ideal family / perfect for retirees / walking distance to church" patterns — common LLM output that creates exposure.
   - **FTC "made with AI" / deceptive advertising** — AI testimonials, AI-cloned voices of named individuals (including the agent's own voice if the clone misrepresents presence or live commentary), AI-generated "reviews."
   - **TCPA / CAN-SPAM** — AI-drafted outbound SMS/email must still carry opt-out and sender identification; AI-generated chatbot responses on SMS inherit TCPA consent rules.
   - **Data-handling for client PII** — Any AI chatbot transcript or CMA summary that surfaces client names, addresses, financials, or showing history outside a brokerage-managed system is flagged. "I pasted it into ChatGPT" is the #1 source of brokerage-reported AI exposure in 2026.
   - **Brokerage AI Use Policy** (if supplied) — Cross-check against internal policy; call out where brokerage policy is stricter than the regulatory floor.
   - **Listing agreement / engagement letter language** — If the client did not sign an AI-use consent and the asset contains L2+ AI work, flag retroactive disclosure.

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
