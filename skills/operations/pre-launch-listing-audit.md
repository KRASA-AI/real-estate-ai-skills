---
name: "Pre-Launch Listing Audit"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30 min/listing"
version: 2.0
last_eval_score: null
---

# Pre-Launch Listing Audit

## Purpose

Turn a signed listing agreement into a coordinated, channel-by-channel launch package: a 14-day reverse-sequenced action plan, per-channel readiness checklists (MLS / Zillow / Realtor.com / brokerage site / Instagram / Facebook / email / signage), a fair-housing and compliance sweep, a Launch-Day Runsheet with hour-by-hour activations, and a 7-day post-launch monitoring plan — so the listing goes live on every channel within the same hour, the photography and copy reinforce the same engagement-driving features, and no missed disclosure or syndication setting becomes a re-list event two weeks in.

## When to Use

Use this skill the day a listing agreement is signed, before any photographer is booked or any caption drafted. Re-run it the day before go-live as a final readiness check. The skill complements `listing-description-writer.md` and `listing-feature-engagement-optimizer.md` (which produce the copy and feature-prioritization), `cma-presentation-generator.md` (which produces the pricing rationale), and `listing-content-multiplier.md` (which produces the channel-specific captions). The audit makes sure the assets those three skills produce are loaded into every channel, with the right metadata, in the right order, on the right day.

## Required Input

Provide the following:

1. **Property file** — Address, property type, MLS area, beds/baths/SF, list price, key features, hard constraints (seller-occupied vs. vacant, lockbox vs. appointment, pet present, tenant present)
2. **Timeline** — Listing agreement date, target go-live date, hard constraints (seller move-out, contractor finish, photographer earliest-available)
3. **Services booked or to be booked** — Photographer (with shot-list provider), videographer, drone, stager, cleaner, sign installer, brokerage marketing team
4. **Channel set** — Confirm which of: primary MLS (with named system), Zillow direct or via syndication, Realtor.com, brokerage website, agent website, Instagram, Facebook, TikTok, YouTube, sphere email list, brokerage email blast, paid digital (Meta / Google / display), Nextdoor, postcards, broker tour, agent caravan, public open house schedule
5. **Team roster** — Listing agent, transaction coordinator, marketing coordinator, showing partner, sign installer, lockbox installer; one named owner per channel
6. **Compliance context** — State (fair-housing rules vary on familial-status interpretation), MLS rules (any-AI-content disclosure, days-on-market reset rules, "coming soon" status duration), brokerage policies (broker-of-record approval thresholds, AI-content disclosure stance)
7. **Agent config** — `config.yml` for brokerage state, voice, default channel set

## Instructions

You are a senior listing launch coordinator on behalf of the agent. Your job is to produce a single audit document that the agent, TC, and marketing coordinator can each run their portion of without a coordination meeting. Every action item has a named owner, a deadline expressed in days-before-launch (D-14 through D+7), and a dependency chain. The output is the source of truth for launch — when the photographer slips, the audit gets updated and propagated; nothing else.

**Before you start:**
- Load `config.yml` for brokerage state, voice, and default channel set
- Reference `knowledge-base/terminology/` for state-specific MLS rules and disclosure conventions
- If a feature-engagement priority list has been produced upstream by `listing-feature-engagement-optimizer.md`, load it; the photo shot-list and copy hierarchy must mirror it
- If a CMA pricing rationale has been produced upstream by `cma-presentation-generator.md`, load it; the price-band selection must match what the audit shows on every channel

**Process:**

1. **Establish the launch date and lock the reverse calendar.** Convert the agreed go-live date into D-day. Build the calendar from D-14 through D+7. Common phasing:
   - **D-14 to D-10 — Property Prep:** seller move-out / decluttering / minor repairs / landscaping / professional cleaning. Confirm pet/tenant constraints. Schedule the photographer for D-7 minimum.
   - **D-9 to D-7 — Visual Asset Production:** photography, video, drone, floor plan, virtual staging if used. The shot list comes directly from the feature-engagement priority list — Lead-With features get hero shots, Support-With features get supporting shots, Deemphasized features are excluded from the lead carousel even if the seller likes them.
   - **D-7 to D-3 — Copy & Compliance:** listing description, MLS remarks (public + private), Q&A block (fed by `neighborhood-report-generator.md`), AEO-ready phrasing, channel-specific captions, signage proof, email-blast subject lines, broker-of-record review if required.
   - **D-2 — Setup Without Publish:** MLS entry in "incomplete" or "office-exclusive" status with photos uploaded; Zillow / Realtor.com / brokerage site entries staged; social posts scheduled but unpublished; email scheduled; sign installed (or scheduled for D-day morning); lockbox installed.
   - **D-1 — Final Readiness Audit:** re-run this skill with the photo, copy, and metadata stack in hand. Resolve every Blocking item.
   - **D-Day — Coordinated Activation.** Hour-by-hour runsheet (see Output Structure §6). The single most-missed item: confirm syndication feeds picked up the listing within 4 hours; if not, manually re-push.
   - **D+1 to D+7 — Performance Monitoring & Adjustments:** showing-volume cadence, Zillow saves/views, click-through rates on email, social engagement, broker-tour attendance. Trigger conditions for price/photography/copy adjustments.

2. **Run the per-channel readiness checklist.** Each channel below has its own minimum-required field set. The audit confirms every required field is populated, every required asset is uploaded, and every required setting is correct *before* publish.

   **MLS (primary system):**
   - Required address, APN/parcel, beds/baths (full/half/three-quarter), SF (with source: Tax / Owner / Appraisal / Builder), lot size, year built, zoning, school district, HOA name + dues + frequency
   - Public remarks (under MLS character limit, no protected-class language, no contact information per most MLS rules)
   - Private remarks (showing instructions, lockbox code routing, alarm codes route via secure channel only)
   - Required photo count, max photo count, hero photo position, video URL, virtual tour URL, floor plan URL
   - Status: "Coming Soon" duration limit (varies by MLS — most cap at 14 days), then auto-flip to Active
   - Compensation: cooperating compensation amount, dual-variable language if applicable
   - Showing instructions: ShowingTime / Aligned setup, appointment-required flag, lockbox type
   - Disclosures uploaded: TDS/SPDS, lead-paint (if pre-1978), HOA documents, NHD report, any state-required addenda
   - Verified — the cooperating compensation entered matches the listing agreement
   - Verified — the AI-content / virtual-staging / synthetic-media labels are set per local MLS rule

   **Zillow:**
   - Listing pulled in via syndication or direct (confirm which); Zillow agent profile claimed; agent contact correct; co-listing visibility correct
   - "Showcase" listing status if subscribed; Zillow video walkthrough uploaded if subscribed
   - Price history accuracy (Zillow auto-pulls — flag and request correction if Zestimate shows incorrect prior-sale data)
   - Open house calendar populated

   **Realtor.com:**
   - Pulled in via syndication; agent profile claimed; co-listing visibility correct
   - Photos uploaded in correct order (Realtor.com sometimes reorders — verify)
   - Open house calendar populated

   **Brokerage website + agent website:**
   - Featured-listing slot scheduled to flip on D-day morning
   - SEO meta title and description written (tied to listing-aeo-optimizer output)
   - Single-property landing page (if brokerage offers) built with full asset stack

   **Instagram:**
   - Hero post scheduled D-day 9:00 AM local
   - Reel scheduled D-day 12:00 PM local (hook and shot list per `listing-content-multiplier.md`)
   - Story carousel scheduled D-day 6:00 PM local
   - Caption compliant with fair housing language and AI-content disclosure stance
   - Geotag set; relevant local hashtags; agent handle visible

   **Facebook:**
   - Cross-posted from IG OR independently scheduled
   - Marketplace listing if brokerage policy permits
   - Sphere group post (if applicable) scheduled

   **Email:**
   - Sphere email scheduled D-day 8:00 AM local with single-property landing-page link
   - Brokerage blast (if available) scheduled D-day 10:00 AM local
   - Subject lines A/B-tested if list size > 1,000

   **Signage:**
   - Sign + rider scheduled for D-day morning install (or D-1 evening if seller permits)
   - Sign QR linking to the single-property landing page (not to a generic agent profile)

   **Broker tour / Agent caravan:**
   - Date set within the first 7 days of launch; food/drink confirmed; flyer printed

   **Open house:**
   - First public open house scheduled D+2 or D+3 weekend; sign rider added; promoted on IG, FB, Zillow, MLS

3. **Run the visual-asset audit.** Pull the feature-engagement priority list and confirm:
   - Hero photo features the #1 Lead-With feature, taken at the time of day specified by the photographer's lighting plan
   - First 5 photos cover all Lead-With features
   - Photos 6–15 cover all Support-With features
   - Deemphasize features are not in the first 10 photos and may be omitted entirely
   - Video walkthrough hits the same feature hierarchy
   - Drone if used shows lot/view/neighborhood, not just rooftop
   - Floor plan is to-scale and labeled
   - Virtual staging — if used, every staged image carries the MLS-required virtual-staging disclosure
   - At least one photo of every room buyers expect (kitchen / primary bath / primary bedroom / living / dining / outdoor)

4. **Run the copy audit.** Pull the listing description, MLS public remarks, captions, email subject lines, signage rider, and Q&A block. Confirm:
   - Lead with the #1 Lead-With feature in every channel-appropriate length
   - Fair-housing-compliant language: no "family-friendly," "perfect for kids," "great schools" without grade citation, "safe neighborhood" without crime-stat citation, "walkable" without WalkScore reference
   - No protected-class proxies; no demographic descriptors
   - AI-content disclosure consistent across channels (per CA AB 723 / brokerage policy / MLS rule)
   - Price reflects the CMA pricing rationale
   - Open-house dates consistent across MLS, Zillow, Realtor, IG, brokerage site, email
   - Contact information included where allowed; excluded where MLS forbids in public remarks
   - Spell-check, brand consistency, address accuracy verified

5. **Run the compliance sweep.** This is the section the audit exists for — it is the single most missed step in self-serve launches.
   - **Fair Housing:** every channel scanned for protected-class language and proxies. Route remediation through `ai-marketing-compliance-audit.md` if findings exceed Advisory.
   - **MLS rules:** Coming Soon duration, days-on-market reset, AI-content label, virtual-staging label, contact information rules, photo-edit rules (no removed features without disclosure)
   - **State law:** CA AB 723 (where applicable) AI-disclosure on synthetic media; CO AI Act (where applicable) for substantive AI involvement; state agency-disclosure forms attached
   - **NAR Code of Ethics:** Article 12 (truthful advertising), Article 15 (no false/misleading statements), Article 11 (competence)
   - **Federal:** Fair Housing Act, lead-paint disclosure for pre-1978 buildings, ADA accessibility statements where applicable
   - **TCPA / CAN-SPAM:** email unsubscribe, physical postal address, opt-in records for any SMS
   - **Brokerage:** broker-of-record approval threshold (if list price exceeds policy threshold, BOR must initial), commission disclosure consistency

6. **Build the Launch-Day Runsheet.** A single one-page table, in local time, hour-by-hour, with named owners and the immediate "if this slips" fallback. The runsheet is what the team works off on D-day; nothing else.

7. **Build the post-launch monitoring plan.** D+1 to D+7 dashboard:
   - **Showing volume:** count, comparable-listing benchmark, trigger to escalate (< 50% of comp-set in first 72 hours = price or photography signal)
   - **Zillow performance:** views, saves, save-rate, share-of-voice in submarket
   - **Email performance:** open rate, click rate, replies
   - **Social performance:** Reel views, IG saves, comments
   - **Broker tour attendance:** number of agents, agent feedback
   - **Open house traffic:** registered attendees, agent-accompanied, repeat visits
   - **Adjustment triggers:** D+7 with no offer activity → photography refresh, copy refresh, or price reduction conversation (route to `cma-presentation-generator.md` for the price-reduction CMA)

8. **Compile the downstream handoffs.** A one-paragraph TC summary for `transaction-coordinator-brief.md`, a one-line CRM status, and a per-channel asset inventory for the marketing coordinator.

**Critical rules:**

- The audit lists every channel, even those marked "not in use" — explicitly excluding a channel is a documented decision, not an omission
- Every action item has exactly one named owner. "Marketing team" is not a name. "Sarah Chen, marketing coordinator" is
- A "go-live" without confirmed syndication is not a go-live — flag any channel that is not visible within 4 hours of MLS publish as a launch incident
- Lockbox codes, alarm codes, and showing-instruction PINs never appear in MLS public remarks, signage, or any social post. Flag as fraud-risk if found
- Protected-class language is treated as Blocking, not Material. The launch does not happen with "family-friendly" in the description
- Coming-Soon-status overruns are MLS violations and trigger days-on-market resets — track the exact day count and auto-flip
- This skill produces an audit, not legal advice. Compliance findings get routed to the broker, the brokerage compliance officer, or counsel; resolution is theirs
- A pre-launch audit with more than five Blocking items is not a launch — it's a re-prep. Tell the agent plainly rather than producing a Runsheet that will collapse on D-day

**Output structure (always in this order):**

1. **Launch Identifier** — address, list price, target launch date, channels in use, named owners
2. **Reverse-Sequenced Action Plan (D-14 to D+7)** — phase / item / owner / deadline / dependency
3. **Per-Channel Readiness Checklist** — pass/fail per field, per channel
4. **Visual Asset Audit** — feature-engagement compliance check
5. **Copy Audit** — fair-housing, AI-disclosure, channel consistency
6. **Compliance Sweep** — Blocking / Material / Advisory with citations
7. **Launch-Day Runsheet** — hour-by-hour with owners and fallbacks
8. **Post-Launch Monitoring Plan** — D+1 to D+7 dashboard and adjustment triggers
9. **TC Handoff Paragraph + CRM Status Line**

## Example Output

**Launch Identifier:** 4821 Laurel Canyon Blvd, Studio City CA 91604. List price $1,495,000. Target launch: Thursday, May 7, 2026, 9:00 AM PT. MLS: TheMLS / CLAW. Channels in use: TheMLS, Zillow, Realtor.com, brokerage site, agent site, Instagram, Facebook, sphere email, sign + rider, broker tour. Channels excluded: TikTok (audience mismatch), Marketplace (brokerage policy). Owners: Listing Agent — Abe Clark; TC — Devon Park; Marketing Coord — Sarah Chen; Photographer — Mike Otsu (booked D-7 = 4/30); Sign Install — Studio City Signs (booked D-1 evening = 5/6).

**Reverse-Sequenced Action Plan (excerpt):**

| Phase | D-day | Item | Owner | Deadline | Depends On |
|---|---|---|---|---|---|
| Prep | D-14 (4/23) | Seller declutter primary bedroom + office (Lead-With features per engagement scorer) | Seller / stager | 4/24 EOD | Listing agreement signed |
| Prep | D-12 (4/25) | Touch-up paint in office (chip behind door) | Seller's handyman | 4/26 EOD | Stager walkthrough |
| Prep | D-10 (4/27) | Professional clean | ABC Cleaning | 4/29 by noon | Painting cure |
| Visual | D-7 (4/30) | Photo shoot — golden hour exterior, midday interior | Mike Otsu | 4/30 EOD | Cleaning complete, stager final |
| Visual | D-7 (4/30) | Drone (lot + canyon view) | Mike Otsu | 4/30 EOD | Permit on file (FAA Part 107) |
| Visual | D-6 (5/1) | Floor plan production | Mike Otsu's vendor | 5/2 EOD | Photo shoot complete |
| Copy | D-5 (5/2) | Listing description (per `listing-description-writer.md`) | Sarah Chen | 5/3 EOD | Feature engagement scorer output |
| Copy | D-4 (5/3) | MLS public + private remarks | Sarah Chen | 5/4 EOD | Listing description |
| Copy | D-4 (5/3) | Q&A block (per `neighborhood-report-generator.md`) | Sarah Chen | 5/4 EOD | — |
| Copy | D-3 (5/4) | Channel-specific captions (per `listing-content-multiplier.md`) | Sarah Chen | 5/5 EOD | Listing description |
| Compliance | D-3 (5/4) | Run `ai-marketing-compliance-audit.md` on full asset set | Sarah Chen | 5/5 EOD | All copy drafts complete |
| Compliance | D-2 (5/5) | Broker-of-record review (BOR threshold: $1.5M; this list is below threshold but BOR aware) | BOR | 5/6 EOD | Compliance audit clean |
| Setup | D-2 (5/5) | MLS entry in "Incomplete" status with photos and remarks | Devon Park | 5/6 EOD | All copy + photos approved |
| Setup | D-2 (5/5) | Zillow / Realtor / brokerage site entries staged | Sarah Chen | 5/6 EOD | MLS entry started |
| Setup | D-2 (5/5) | IG / FB posts scheduled (unpublished) | Sarah Chen | 5/6 EOD | Captions approved |
| Setup | D-2 (5/5) | Sphere email scheduled in MailerLite | Sarah Chen | 5/6 EOD | Single-property URL live |
| Setup | D-1 (5/6) | Sign installed | Studio City Signs | 5/6 6:00 PM | Seller permission |
| Setup | D-1 (5/6) | Lockbox installed | Devon Park | 5/6 EOD | Seller permission, codes routed via secure channel |
| Audit | D-1 (5/6) | Final readiness re-run of this skill | Abe Clark | 5/6 EOD | All above complete |
| Launch | D-day (5/7) | See Launch-Day Runsheet | various | 5/7 hourly | — |
| Monitor | D+2 (5/9) | First public open house | Showing partner | 5/9 1–4 PM | Sign rider, signage |
| Monitor | D+4 (5/11) | Broker tour | Abe + Sarah | 5/11 11:00 AM | Calendar invites sent D-3 |
| Monitor | D+7 (5/14) | Performance review meeting; trigger price/copy/photo adjustments | Abe + Sarah | 5/14 EOD | Dashboard pulled |

**Per-Channel Readiness Checklist (excerpt — TheMLS):**

| Field | Status | Notes |
|---|---|---|
| Address + APN | Pass | 4821 Laurel Canyon Blvd / 2370-018-044 |
| Beds / Baths | Pass | 4 / 3 (2 full, 1 three-quarter); SF source = Owner |
| SF | **Material** | Owner-source SF (2,612) is 87 SF below tax-record (2,699). Add SF source disclaimer in MLS public remarks |
| HOA | Pass | None |
| Public Remarks | Pass | 1,420 chars / 1,500 limit. Lead-With opens with Craftsman architecture + canyon view |
| Private Remarks | Pass | Showing via ShowingTime, lockbox via TC; codes routed Twilio not embedded |
| Photo count | Pass | 32 photos uploaded, 25 will publish (limit 50). Hero is golden-hour exterior |
| Status | Pass | Coming Soon scheduled to flip Active 5/7 09:00 AM |
| Compensation | Pass | 2.5% co-op, matches MLS variable rate language |
| AI-content label | Pass | One virtually-staged photo flagged per CLAW rule |
| Disclosures | **Blocking** | NHD report ordered 5/2 but not yet in escrow file. ETA 5/5. Cannot publish without |

(Per-channel rows continue for Zillow, Realtor.com, brokerage site, agent site, IG, FB, email, signage, broker tour, open house — abbreviated here.)

**Visual Asset Audit:**

Feature-engagement priority (from `listing-feature-engagement-optimizer.md`):
- Lead-With: Craftsman architecture, canyon view, primary suite, dedicated office (WFH)
- Support-With: solar panels, EV charger, tankless water heater, mature lot, two-car garage
- Deemphasize: shared driveway, original kitchen (functional but not luxury), small primary closet

Photo audit:
- Hero: golden-hour exterior with Craftsman detail and canyon backdrop. **Pass.**
- Photos 1–5: exterior, primary suite, office, canyon view, kitchen. **Lead-With features covered. Pass.**
- Photos 6–15: solar (close + roof drone), EV charger, second/third bedrooms, primary bath, dining, living. **Support-With covered. Pass.**
- Shared driveway not in first 10 photos. **Pass.**
- Original kitchen has only 2 photos (not 4 as photographer initially staged). **Pass — adjusted.**
- Floor plan to-scale, labeled. **Pass.**
- Virtually-staged: one office image (currently empty room). Disclosed per CLAW rule. **Pass.**

**Copy Audit (excerpt):**

- Listing description: Lead-With opener uses "1928 Craftsman" + "canyon-overlooking" — no protected-class proxies. **Pass.**
- "Quiet street" — flagged. **Material.** Replace with "low-traffic per LAPD CompStat 2025" or remove. Owner: Sarah Chen.
- "Walkable to Studio City Farmers Market" — has WalkScore citation in long-form, missing from MLS public remarks. **Advisory.** Add citation.
- "Family-friendly" — not present in any draft. **Pass.**
- "Great schools" — replaced with "Carpenter Community Charter (GreatSchools 9/10, rating date 2/2026)" per `neighborhood-report-generator.md`. **Pass.**
- AI-disclosure: virtually-staged image labeled in MLS, Zillow, Realtor, brokerage site. Missing on IG hero post (CA AB 723 question). **Material.** Add disclosure to IG caption.

**Compliance Sweep:**

- **Blocking**
  1. NHD report not in escrow file (5/2 order). Cannot publish without.
- **Material**
  1. SF discrepancy between owner (2,612) and tax (2,699). Add source disclaimer.
  2. "Quiet street" descriptor in current draft. Replace or remove.
  3. AI-disclosure missing on IG virtually-staged image.
- **Advisory**
  1. WalkScore citation in long-form only — add to MLS public remarks for AEO.
  2. Open-house dates (currently D+2 only) — consider adding D+3 for higher attendance.

**Launch-Day Runsheet:**

| Time (PT) | Action | Owner | If This Slips |
|---|---|---|---|
| 06:30 | Devon confirms lockbox + alarm codes; ShowingTime live | TC | Use backup lockbox, push showing window to 14:00 |
| 07:00 | Sarah verifies all scheduled posts and email are armed | Marketing | Manual publish at posted times |
| 08:00 | Sphere email sends | Marketing (via MailerLite) | Manual resend at 10:00 |
| 08:30 | Final compliance scan (this skill, fast pass) | Abe | Hold launch until clean |
| 09:00 | MLS flips Coming Soon → Active | TC | Manual click in MLS; backup contact at TheMLS desk |
| 09:00 | Brokerage site featured listing flips | Marketing | IT ticket; backup is agent site |
| 09:00 | IG hero post publishes | Marketing | Manual post at 09:30 |
| 09:30 | Confirm Zillow + Realtor.com syndication picked up | Marketing | If not visible by 13:00, manual push via Zillow agent dashboard |
| 12:00 | IG Reel publishes | Marketing | Manual post at 13:00 |
| 13:00 | Confirm sign install live | TC | Backup installer |
| 16:00 | Showing volume snapshot — first 7 hours | Abe | Adjust open-house promotion if low |
| 18:00 | IG Story carousel publishes | Marketing | Manual post next morning |
| 18:00 | Day-1 dashboard pulled (views, saves, scheduled showings) | Abe | — |

**Post-Launch Monitoring Plan (D+1 to D+7):**

| Day | Metric | Trigger | Action |
|---|---|---|---|
| D+1 | Zillow saves/views | < 50 saves in 24 hrs at this price band = signal | Photography or copy refresh review |
| D+2 | Open house attendance | < 12 registered = below comp-set | Promote D+3 second open house harder |
| D+3 | Showing volume | Showing volume vs. comp-set median | Pace check |
| D+4 | Broker tour attendance | < 8 agents = poor agent interest | Add second broker preview |
| D+5 | Email open rate, IG saves | Open rate < 22% on sphere = subject-line issue | Resend with new subject |
| D+7 | All metrics + offer status | No offer + below-comp-set showings = price/photo/copy review | Trigger `cma-presentation-generator.md` for price-reduction CMA |

**TC Handoff Paragraph + CRM Status Line:**

> 4821 Laurel Canyon Blvd Studio City — list $1.495M — launch Thursday 5/7 9:00 AM PT — Coming Soon flips to Active 5/7 — first open 5/9 1–4 PM, broker tour 5/11 — 1 Blocking (NHD report due 5/5) and 3 Material to clear by D-1 — full audit at `Listings/4821-Laurel-Canyon/pre-launch-audit-2026-04-23.md`.

> CRM: 4821 LC · Coming Soon → Active 5/7 9AM · NHD pending · BOR aware · 1B/3M open
