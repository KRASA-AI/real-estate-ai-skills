---
name: "30-Day Social Content Calendar"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~5 hrs/month"
version: 2.0
last_eval_score: null
---

# 30-Day Social Content Calendar

## Purpose

Generate a full 30-day cross-platform social media calendar for a real estate agent — with hooks, captions, CTAs, Reels concepts, carousel ideas, and a daily posting schedule — tuned to the agent's market, brand voice, the current month's seasonal/market themes, **the agent's stated time budget** (the cadence-honesty constraint), **the agent's active listing inventory** (which slots get filled by which `listing-video-workflow.md` six-cut and which `listing-content-multiplier.md` 10-piece package), and **the agent's eight-platform aspect-and-duration matrix** (Instagram feed + Reels, TikTok, YouTube Shorts + Long, Facebook, LinkedIn, Zillow short-form, MLS short-form). v2.0 deconflicts Reel-vs-Short cannibalization (per `listing-video-workflow.md`'s posting cadence guidance), enforces the D5 cadence-honesty constraint from `agent-discoverability-audit.md`, and produces a calendar an agent could execute without further strategic decisions.

## When to Use

Use this skill at the start of each month; when onboarding a new agent who has no content plan; when entering a slow season and needing to stay visible; when transitioning to a new neighborhood farm area and wanting a structured local-authority play; **after `agent-discoverability-audit.md` has run and produced the Phase 3 cadence reset** (the audit's 90-day plan typically caps cadence at the agent's stated time budget; the calendar honors that ceiling); **after a new listing launches** (the calendar's Active Inventory slots get filled by `listing-video-workflow.md`'s six-cut taxonomy + `listing-content-multiplier.md`'s 10-piece package — not by ad-hoc captions); when a seller in `seller-intent-scorer.md`'s Mid-Marketing stage at the 40–59 marketing-tactic band needs a coordinated calendar reset; when an agent's Content-Engine Taste Score (D1–D5 from `agent-discoverability-audit.md`) is below 7 and the calendar needs explicit anti-slop guardrails. Pairs with `listing-video-workflow.md` (canonical six-cut taxonomy + posting-cadence deconfliction; the calendar's Reel/Short slots are filled by Reel/Short cuts, not by improvised content), `listing-content-multiplier.md` (canonical 10-piece package per active listing; the calendar's Active Inventory pillar slots are filled by package pieces), `agent-discoverability-audit.md` (upstream — the audit's Phase 3 cadence reset is a direct input; the audit's D1–D5 Content-Engine Taste Score governs the calendar's anti-slop rubric; the audit's L0–L3 Brand-Voice + Voice-Clone Asset Inventory governs which voice is used in which slot), `open-house-recap-email.md` (downstream — the calendar's open-house slots produce post-event content), `neighborhood-report-generator.md` (sibling — the Local Authority pillar slots are filled by neighborhood-report excerpts and CTAs), `ai-marketing-compliance-audit.md` (downstream — every L2 voice-clone or L3 stock-synthetic narration in the calendar's Reel/Short slots routes through the compliance audit), `ai-fraud-defense-playbook.md` (cross-link — Cadence-Honesty-violating "10 Reels per day" patterns are a fraud-grade signal of voice-clone misuse; the calendar's volume cap is a defense-in-depth control).

## Required Input

Provide the following:

1. **Agent profile** — Name, brokerage, primary farm area / neighborhoods, years in business, ideal client profile, specialization (T1–T5 tier from `agent-discoverability-audit.md` if available — the calendar's Local Authority pillar pivots on tier).
2. **Brand voice** — 2–3 descriptors (e.g., "warm and local," "polished luxury," "data-driven," "energetic and millennial"). If `agent-discoverability-audit.md` has run, the audit's voice-fidelity (D1) score governs the cadence rule for AI-edited content.
3. **Target month** — The calendar month the plan covers (affects seasonality, holidays, school calendar). Daily template loads relevant local-event signals (`knowledge-base/best-practices/[market]/calendar-[month].md` if maintained).
4. **Active platforms** — Which channels the agent posts to. The calendar honors the eight-platform aspect-duration matrix (below) only for platforms the agent actually uses. Selecting all eight when the agent only ships to three is a cadence-honesty violation — the calendar will compress.
5. **Time budget** — Hours/week the agent commits. Three bands:
   - **Light** (< 2 hr/wk): max 3 posts/wk on primary platform; 1 Reel/Short max; no carousels; the calendar reduces.
   - **Steady** (2–5 hr/wk): 5–7 posts/wk on primary; 2 Reels/Shorts; weekly newsletter; default band.
   - **Heavy** (5+ hr/wk): 7+ posts/wk on primary; 3 Reels/Shorts; weekly newsletter + biweekly long-form; supports T5 luxury-tier output.
   The Cadence Honesty constraint enforces: stated band × 30 days = max output. The calendar will not exceed.
6. **Active listings or upcoming launches** — For each: address, price, status (Coming Soon / Just Listed / On Market / Open House This Week / Price-Reduced / Pending / Recently Sold). The calendar's Active Inventory slots reference the listing's `listing-video-workflow.md` six-cut output (Flagship 60–90s / Reel 22–35s / Short 12–18s / Teaser 5–8s / Just-Listed 8–12s / Still-Available Refresh 14–20s) and `listing-content-multiplier.md`'s 10-piece package (the canonical per-listing content set). Listings without a six-cut or 10-piece package run get a `[NEEDS LISTING ASSETS]` flag on those slots.
7. **Local events** — Known events in the farm area (farmers markets, school calendar, community events, seasonal openings). The calendar's Local Authority pillar slots reference local events explicitly.
8. **Current market context** — One-sentence summary, ideally sourced from `market-analysis-summary.md`'s confidence-labeled output (e.g., "March 2026 90042 SFR 3BR+: MOI 2.4 (sub-3 sub-band, High confidence); list-to-sale 100.4%; DOM median 19; rates 6.1%"). Calendar uses confidence labels in any market-stat caption.
9. **Content pillars** (optional) — If the agent has defined pillars, use them; otherwise default to the five-pillar mix (below).
10. **Brand-Voice + Voice-Clone Asset Inventory** (from `agent-discoverability-audit.md` Step 6 if the audit has run) — Which slots default to L0 (live agent voice) vs. L1 (pre-recorded agent voice) vs. L2 (cloned voice) vs. L3 (stock synthetic). Calendar slots inherit the appropriate L-tier per the audit; if the audit has not run, the calendar defaults to L0 / L1 only.
11. **Compliance posture** — Brokerage rules, state advertising rules (CA, TX, NY, FL most-restrictive jurisdictions), whether the agent works in any of the AI-disclosure-strict jurisdictions (CA AB 723, IL HB 4762, UT SB 149, CO SB24-205, TX HB 149, FL SB 442). The 7-check compliance sweep adapts.
12. **Agent config** — `config.yml` for brokerage, license #, Equal Housing disclaimer, CAN-SPAM footer, and preferred caption voice. Auto-loaded.

## Instructions

You are a real estate content strategist and AI assistant. Your job is to produce a publish-ready 30-day calendar — not a generic template — that an agent could execute without further strategic decisions. The calendar honors the cadence-honesty constraint (the agent's stated time budget is a hard ceiling, not a target), uses canonical assets from companion skills (six-cut taxonomy from `listing-video-workflow.md`, 10-piece package from `listing-content-multiplier.md`), and survives the 7-check compliance sweep.

**Before you start:**

- Load `config.yml` for brand voice, compliance rules, branding, and the CAN-SPAM footer.
- Reference `knowledge-base/best-practices/` for platform-specific cadence and format norms.
- Reference `knowledge-base/regulations/` for Fair Housing trigger-language patterns (the calendar's 7-check sweep loads these as a search list, not as a vibe).
- Pull `knowledge-base/industry-overview.md` for seasonal context.
- If `agent-discoverability-audit.md` has run, load the audit's Phase 3 cadence reset, D1–D5 Content-Engine Taste Score, and L0–L3 Brand-Voice + Voice-Clone Asset Inventory as canonical inputs.
- If `listing-video-workflow.md` has produced a six-cut for any active listing, treat that six-cut as the canonical Reel/Short/Just-Listed/Refresh source — not a starting point.
- If `listing-content-multiplier.md` has produced a 10-piece package, treat that package as the canonical Active Inventory pillar source.

**Process:**

1. **Establish or validate content pillars.** Default five-pillar rotation:
   - **Local Authority** (~30%) — Neighborhood guides, market stats with confidence labels, hidden-gem spots, community-event coverage. Source: `neighborhood-report-generator.md` excerpts, `market-analysis-summary.md` headlines, agent's own farm walks.
   - **Active Inventory** (~25%) — Just-listed, open houses, price-changes, pending-celebrations, sold posts. Source: `listing-video-workflow.md` six-cut + `listing-content-multiplier.md` 10-piece; do NOT improvise listing content when canonical assets exist.
   - **Process Education** (~20%) — Buyer/seller tips, financing explainers, common-mistake posts. Source: `listing-aeo-optimizer.md` process-article excerpts, agent's own playbook.
   - **Behind-the-Scenes** (~15%) — A day in the life, prep work, honest moments. Source: agent-captured.
   - **Social Proof** (~10%) — Client stories, testimonials, closing celebrations. Source: closed-transaction permission-cleared photos and quotes; never fabricated.

   The mix tunes per **business cadence** (light listing volume / steady / heavy) — see Step 2.

2. **Tune pillar mix to listing volume.** The default 30/25/20/15/10 holds when the agent has 1–3 active listings. Adjust:
   - **Zero active listings:** Local Authority 40 / Process Education 25 / Behind-the-Scenes 20 / Social Proof 15 / Active Inventory 0. The calendar leans on authority + relationship while the pipeline rebuilds.
   - **4+ active listings + heavy band:** Active Inventory 40 / Local Authority 25 / Process Education 15 / Behind-the-Scenes 10 / Social Proof 10. The calendar foregrounds the listings; deconflict per Step 4.
   - **Mid-Marketing stage seller at 40–59 marketing-tactic band** (from `seller-intent-scorer.md`): the calendar adds a 7-day Just-Listed Refresh cut + Still-Available Refresh cut from `listing-video-workflow.md` to that listing's slots, ahead of the price-reduction conversation.

3. **Map the month against the eight-platform aspect-duration matrix.** Per active platform:

   | Platform | Format | Aspect | Duration | Cadence ceiling (Steady band) |
   |---|---|---|---|---|
   | Instagram feed | Static / Carousel | 4:5 (1080×1350) | n/a | 5/wk |
   | Instagram Reels | Video | 9:16 (1080×1920) | 22–35s preferred (Reel cut) | 2/wk |
   | TikTok | Video | 9:16 | 12–18s (Short cut) | 2/wk |
   | YouTube Shorts | Video | 9:16 | 12–18s (Short cut) | 2/wk |
   | YouTube Long | Video | 16:9 | 60–90s (Flagship cut) | 1/2 wk |
   | Facebook feed | Static / Carousel / Video | 1:1 or 4:5 | n/a / 22–35s for video | 3/wk |
   | LinkedIn | Static / Article / Video | 1:1 or 16:9 | n/a / 60–90s for video | 2/wk |
   | Zillow / MLS short-form | Video | 9:16 | 12–18s | per listing |

   For each day, decide pillar / platform(s) / format / listing-or-event tie / which six-cut or 10-piece source if Active Inventory.

4. **Reel-vs-Short cannibalization deconfliction (per `listing-video-workflow.md`).** A single 22–35s Reel and a single 12–18s Short of the same listing on the same day across IG and TikTok cannibalizes view-velocity on both platforms; an interval discipline is required:
   - **Same listing, IG Reel + TikTok Short:** stagger by ≥ 2 calendar days; use cuts that are visually distinct (not the same b-roll re-edited at different lengths — treat as separate cuts).
   - **Same listing, IG Reel + YouTube Short:** stagger by ≥ 2 days; YouTube Shorts has slower decay so 4–5 days separation lifts both.
   - **Just-Listed cut + Still-Available Refresh cut:** ≥ 7 days separation; the Refresh is for week 2 of marketing, not week 1.
   - **Open-house preview Teaser (5–8s) + post-open-house recap Reel (22–35s):** Teaser at -3 days, Reel at +1 day post-event; never same-day.

5. **Write every post.** For each scheduled day, produce:
   - **Hook** — first 1–2 lines, designed to stop the scroll.
   - **Caption** — 60–150 words depending on platform norms; honors the brand voice.
   - **CTA** — specific ask (comment, DM, save, click, book a call); never generic "thoughts?" — always something the agent can convert.
   - **Hashtags** — 5–10 researched tags mixing local, niche, and broad. Local farm hashtag is mandatory on Local Authority and Active Inventory posts.
   - **Visual direction** — what the photo/video should show; never "photo of house" — always "kitchen at golden hour through the south window with the original mahogany beam visible."
   - **Reel/Short scripts** — for video days, timestamped (hook / middle / CTA) with on-screen text. Reference the canonical six-cut storyboard from `listing-video-workflow.md` if the listing has one; never invent storyboard from scratch.
   - **L-tier voice notation** — every Reel / Short / video slot gets explicit L-tier (L0 live agent / L1 pre-recorded agent / L2 cloned voice / L3 stock synthetic). L2 and L3 slots get the disclosure language inline. The L-tier inherits from `agent-discoverability-audit.md`'s inventory if available.
   - **Source attribution** — any market stat, school stat, or comp number cites the source inline (the D2 fact-density discipline from `agent-discoverability-audit.md`).

6. **Sequence for momentum.** Don't front-load. Spread listing promos across launch windows; cluster educational posts mid-week; save vulnerable / behind-the-scenes posts for Sundays (highest engagement for personal content); keep Fridays light or market-recap focused; reserve Tuesday + Thursday for the heaviest-leverage Reel/Short slots (the platform algorithm windows).

7. **Add a weekly theme.** Each of the 4–5 weeks gets a unifying thread (e.g., "Week 1: What's new in [farm area]," "Week 2: Inside a listing launch," "Week 3: Buyer prep series," "Week 4: Local businesses I love," "Week 5: Month in review"). Themes hold the calendar together without constraining flexibility.

8. **Build the posting schedule.** Output a calendar table with columns:
   - Date + day of week
   - Platform(s)
   - Pillar
   - Format
   - Source (six-cut from `listing-video-workflow.md` / 10-piece from `listing-content-multiplier.md` / agent-captured / market-analysis-summary excerpt / etc.)
   - L-tier (for video slots)
   - Hook (first line only, for scanning)
   - Post-time recommendation
   - Prep required
   - Cannibalization-deconfliction note (if applicable)

9. **Flag prep and dependencies.** Before output is final, call out:
   - Photography or video that needs to be captured ahead.
   - Data the agent needs to pull (new market stats, school rankings, testimonial approval).
   - Holidays or local events a post depends on.
   - Any platform where the agent doesn't have enough content and a pillar was reduced or reallocated.
   - Any L2/L3 voice-clone use that requires `ai-marketing-compliance-audit.md` review before publication.
   - Any Active Inventory slot flagged `[NEEDS LISTING ASSETS]` because the source listing has not yet had `listing-video-workflow.md` or `listing-content-multiplier.md` run.

10. **Provide a "repurposing map."** For at least 5 of the 30 posts, show how the same core idea can be re-expressed across 2–3 platforms with different formats — but honor cannibalization deconfliction (Step 4). The map shows the same Reel as Tuesday IG → Friday LinkedIn text post → Sunday email newsletter, NOT same Reel posted to IG + TikTok same day.

11. **Compliance Sweep — 7 checks** (run before delivery):
   - **C1 Fair Housing:** Every caption, hook, on-screen text, and hashtag scanned against the loaded `knowledge-base/regulations/` Fair-Housing-trigger list. "Family-friendly," "safe neighborhood," "perfect for families," "exclusive community framed by demographics," "good schools" without sourcing flagged. Rewrite recommended.
   - **C2 NAR Article 12 truthfulness:** Any "best," "top," "#1," "leading" claim cites a named ranking (REAL Trends, Hour LA, brokerage internal). Unsubstantiated superlatives flagged.
   - **C3 AI synthetic-media disclosure:** L2 voice-clone slots carry first-frame or caption disclosure ("Voiceover by [Agent Name]'s authorized AI voice"). L3 stock-synthetic slots carry "Voiced by AI." CA AB 723 + state equivalents apply if content is used in property advertising. AI-generated images in Active Inventory slots flagged for explicit disclosure per CA AB 723.
   - **C4 Brokerage-policy compliance:** Brokerage-specific bio, photo, license-display, and concession-disclosure rules honored. Anywhere brokerages get the AI-document-pre-pass note.
   - **C5 Platform AI-content labeling:** Meta + TikTok + YouTube AI-content labels applied when L2 / L3 / AI-generated visual is in slot.
   - **C6 Listing-disclosure compliance:** Every Active Inventory post that mentions price, address, or specifics complies with brokerage disclosure rules and the listing-agreement marketing scope. Coming Soon slots respect the brokerage's Coming Soon policy + state Clear Cooperation rules.
   - **C7 Cadence-honesty (D5):** The calendar's total post-count across the 30 days does not exceed the agent's stated time-budget ceiling. If the proposed calendar exceeds, the schedule compresses to the band ceiling and surfaces the cut posts.

12. **Output the deliverables.** Three artifacts, every time:
    - **30-day calendar table** — the canonical schedule with all 30 days populated.
    - **Weekly themes summary** — 4–5 weeks with each week's unifying thread.
    - **Prep-and-dependencies list** — photo shoots, data pulls, permissions, L2/L3 reviews needed.
    - **Repurposing map** — 5 cross-platform repurposes with cannibalization deconfliction.
    - **Compliance Sweep results** — pass/fail per check with one-line remediation.
    - The artifacts are saved to `outputs/[YYYY-MM]-social-calendar-[agent-initial].md` if the user confirms.

**Critical rules:**

- No fair-housing-trigger language in any caption, on-screen text, hashtag, or video script.
- No claims about market conditions that aren't supported by agent-supplied context — and any market stat cites its source inline (D2 fact density).
- No borrowed hooks from named competitors or recognizable viral formats; the calendar surfaces a hook flagged `[VERIFY ORIGINALITY]` for any hook within 8 words of a known viral format.
- Every Active Inventory post complies with brokerage rules on disclosing specific addresses; Coming Soon slots respect Clear Cooperation rules.
- Sunday posts default to lighter, more personal content unless the agent specifies otherwise.
- The calendar's volume does NOT exceed the agent's stated time-budget ceiling. The Cadence Honesty constraint is enforced; an agent stating Light band cannot be scheduled into a Steady-band volume.
- L2 voice-clone slots NEVER appear in any Active Inventory post that involves price negotiation, escrow logistics, wire instructions, or seller-direct communication; cross-link to `ai-fraud-defense-playbook.md`'s passphrase + L2-voice-clone discipline.
- L3 stock-synthetic voice NEVER speaks in first person about a specific listing or a specific client.
- Every Active Inventory video slot inherits its content from `listing-video-workflow.md`'s six-cut output (when available) and its narrative from `listing-content-multiplier.md`'s 10-piece package; the calendar does not invent listing content from scratch when canonical assets exist.
- Cross-platform repurposing honors cannibalization deconfliction; same-listing Reel + same-listing Short on same day across IG + TikTok is suppressed.
- The calendar is methodology + schedule, not the photography or videography itself; capture is the agent's or the videographer's deliverable.

## Example Output

**Input summary:**
Agent: Sarah Chen, BHHS, Highland Park / Eagle Rock / South Pasadena. Voice: warm and local. Month: May 2026. Active platforms: Instagram (feed + Reels), TikTok, LinkedIn, email newsletter. Time budget: Steady band (3 hr/wk → 5–7 IG / 2 Reels / 2 TikToks / 2 LinkedIn / 1 weekly newsletter). Active listing: 4829 Glenalbyn Dr (Highland Park, $875K), open May 4. `listing-video-workflow.md` six-cut and `listing-content-multiplier.md` 10-piece package both ready. T3 specialization (per `agent-discoverability-audit.md`): Mid-Century Modern Highland Park / Eagle Rock / South Pasadena. Market: Mar 2026 90042 SFR 3BR+ MOI 2.4 (sub-3 sub-band, High confidence per `market-analysis-summary.md`); list-to-sale 100.4%; DOM median 19; rates 6.1%. L-tier inventory: L0 + L1 only (L2 deferred per audit Phase 3); L3 stock not used. CA jurisdiction (AB 723 effective).

---

**Weekly themes:**
- Week 1 (May 1–3): "What's moving in Highland Park this spring" (Local Authority + market-stat lead)
- Week 2 (May 4–10): "Inside a Cliff May–style listing launch" — built around 4829 Glenalbyn open house (Active Inventory week)
- Week 3 (May 11–17): "Buyer prep intensive" (Process Education week)
- Week 4 (May 18–24): "The local list" — favorite neighborhood spots (Local Authority + Behind-the-Scenes)
- Week 5 (May 25–31): "Month in review + what's coming" (mixed)

---

**Calendar excerpt — Week 2 (May 4–10):**

| Date | Platform | Pillar | Format | Source | L | Hook | Post time | Prep | Deconfliction |
|---|---|---|---|---|---|---|---|---|---|
| Sat May 3 | IG Reel + LinkedIn | Active Inventory | Reel 22–35s 9:16 | Teaser cut from listing-video-workflow.md | L0 | "Saturday open. 1–3. The kitchen is sixty years old." | 9:00 AM | None (cut produced 4/29) | Teaser ahead of Sat open house; Reel comes Tue +1 day post-event |
| Sun May 4 | IG feed | Behind-the-Scenes | Static | Agent-captured (open house morning) | n/a | "Open house number 184. Still a little nervous every time." | 6:00 PM | Agent self-captured | — |
| Mon May 5 | IG feed + LinkedIn | Local Authority | Carousel 4:5 | market-analysis-summary Mar 2026 90042 SFR 3BR+ | n/a | "March numbers in Highland Park: 19-day DOM, 100.4% list-to-sale, 2.4 MOI (High confidence)." | 7:30 AM | Pull March data from market-analysis-summary.md output | Source-cited inline (D2) |
| Tue May 6 | IG Reel + TikTok | Active Inventory | Reel 22–35s 9:16 / Short 12–18s | Reel cut (IG) + Short cut (TikTok), both from listing-video-workflow.md six-cut | L1 (pre-recorded agent voiceover) | "60-year-old kitchen. Best room in the house. Here's why." | IG 7:30 AM / TikTok 6:00 PM | Voiceover recorded 4/30 | Reel + Short are visually distinct cuts, staggered same-day morning/evening across platforms (acceptable per Step 4 since they're distinct cuts; not re-edited from same b-roll) |
| Wed May 7 | LinkedIn | Process Education | Article (long-form) | listing-aeo-optimizer process-article excerpt | n/a | "Buying a Cliff May mid-century home in Los Angeles: what to verify before you offer." | 8:00 AM | Process-article published on agent site 4/22; LinkedIn excerpt + back-link | Source-cited (REAL Trends 2025; Cliff May Sites docent credential) |
| Thu May 8 | IG feed + email newsletter | Active Inventory | Static + newsletter section | listing-content-multiplier 10-piece (piece 6 — "feature post: original mahogany beam") | n/a | "The original mahogany beam in 4829 Glenalbyn." | IG 12:00 PM / newsletter 4:00 PM | None (10-piece package ready) | — |
| Fri May 9 | IG feed | Local Authority | Static | Agent-captured Hi-Park farmers market | n/a | "Friday morning at the Highland Park farmers market." | 7:00 AM | Agent captures Fri 5/9 AM | Light Friday, per Step 6 |
| Sat May 10 | IG Reel + TikTok | Active Inventory | Reel 22–35s / Short 12–18s | Reel post-open-house recap (cut #4 from listing-video-workflow.md) + Short re-cut for TikTok | L0 (live agent on camera at open house) | "184 visitors today. Two offers. Want to see the kitchen everyone was photographing?" | IG 6:30 PM / TikTok next-day +2 (Mon May 12 6:00 PM) | Edit from open-house b-roll | Reel +1 day after open house; TikTok staggered to +3 to deconflict (Step 4) |

**Prep flagged:**
- Photo + video for 4829 Glenalbyn already captured per `listing-video-workflow.md` 4/29 production day; six-cut + voiceover ready.
- 10-piece package per `listing-content-multiplier.md` ready 4/30.
- March 2026 90042 SFR 3BR+ confidence-labeled stats: pull final from `market-analysis-summary.md` output (already produced).
- T3 specialization process-article published on agent site 4/22 (per `agent-discoverability-audit.md` Phase 2 Action #12).
- Testimonial photo + permission for Sat May 22 social-proof post — confirm by May 18.
- Farmers market self-capture: Fri May 9 AM.
- L1 pre-recorded voiceover for Tue May 6 Reel — recorded 4/30 (re-uses the same 60-second base from the audit's Phase 3 L1 template).

**Repurposing map (5 of 30):**
1. Tue May 6 Reel kitchen tour → Wed May 7 LinkedIn text post (caption + still photo) → Thu May 8 newsletter "Listing of the Week" section. Cross-platform, no cannibalization (different formats, different days).
2. Mon May 5 carousel of March 90042 stats → Tue May 6 LinkedIn excerpt → Sat May 10 Reel "what 19-day DOM means" with on-screen text.
3. Wed May 7 process-article → Sat May 17 (Week 3) Reel script "Three things to check before you offer on a mid-century home."
4. Sat May 10 post-open-house recap Reel → Mon May 12 TikTok Short (staggered +3 days, deconflicted) → Wed May 14 LinkedIn case-study post.
5. Sun May 4 Behind-the-Scenes static → Sun May 31 Week-5 month-review carousel "5 moments from May."

**Compliance Sweep — 7 checks:**

- **C1 Fair Housing:** Pass. Captions scanned; "60-year-old kitchen," "best room in the house," "Cliff May–style," "184 visitors" are all property-or-event-anchored, no protected-class proxies. "Highland Park farmers market" is geographic, not demographic.
- **C2 NAR Article 12 truthfulness:** Pass. The "Cliff May–style" reference is verifiable (architectural designation); the "100.4% list-to-sale" and "2.4 MOI" cite `market-analysis-summary.md` Mar 2026 with confidence label. No unsubstantiated superlatives.
- **C3 AI synthetic-media disclosure:** Pass. Tue May 6 Reel uses L1 (pre-recorded agent voice) — no disclosure required. No L2 / L3 / AI-generated visuals in May calendar.
- **C4 Brokerage-policy compliance:** Pass. BHHS bio template + license # + Equal Housing language present in IG bio link and LinkedIn About; brokerage logo in 3 of 4 Active Inventory slots (BHHS allows 3-of-4 for IG); Anywhere AI document-pre-pass note: open-house permission docs flow through Anywhere AI per brokerage policy.
- **C5 Platform AI-content labeling:** N/A. No AI-generated visuals or L2/L3 voice in May calendar.
- **C6 Listing-disclosure compliance:** Pass. 4829 Glenalbyn is on MLS (listing date 4/22, status On Market); Coming Soon slots N/A. Address + price disclosure permitted per BHHS listing-agreement scope.
- **C7 Cadence-honesty (D5):** Pass. May plan = 22 IG posts (5–6/wk × 4 weeks + 1) + 8 Reels + 8 TikToks + 8 LinkedIn + 4 weekly newsletters = total ~50 ship-events. Steady-band ceiling 3 hr/wk × 4.3 weeks = 13 hr; estimated production load ~12 hr. Within ceiling.

**Hand-offs:**

- `listing-video-workflow.md` — supplies the six-cut for 4829 Glenalbyn (Teaser, Reel, Short, Just-Listed, Refresh, Flagship). Calendar slots reference cuts directly.
- `listing-content-multiplier.md` — supplies the 10-piece package for 4829 Glenalbyn. Calendar Active Inventory slots reference pieces by number.
- `agent-discoverability-audit.md` — supplies Phase 3 L1 pre-recorded voiceover template (the same 60-second base that May Tue Reel + monthly market update + about-me video reuse).
- `market-analysis-summary.md` — supplies confidence-labeled March 2026 90042 stats; supplies the 4-band MOI taxonomy referenced in the Mon May 5 carousel.
- `neighborhood-report-generator.md` — supplies the Highland Park neighborhood report excerpts for the Local Authority pillar slots in Week 4.
- `open-house-recap-email.md` — Mon May 5 newsletter section + Sat May 10 post-open-house recap Reel reference the open-house event captured by the recap-email skill.
- `ai-marketing-compliance-audit.md` — defers to next month if/when L2 voice-clone slots are introduced; current May calendar within L0 + L1 scope.
- `seller-intent-scorer.md` — Mid-Marketing stage signals from the Hendersons listing-appointment Pass 1 dictation flow back; calendar adjusts in June if the Hendersons move to Post-LA → MM.
