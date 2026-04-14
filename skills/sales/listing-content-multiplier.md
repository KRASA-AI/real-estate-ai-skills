---
name: "Listing Content Multiplier"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~3 hrs/listing"
version: 1.0
last_eval_score: null
---

# 📣 Listing Content Multiplier

## Purpose

Transform a single property listing into a complete, multi-platform marketing content package — 10+ ready-to-publish assets spanning social posts, Reels/TikTok scripts, email campaigns, carousels, blog content, and buyer-direct messaging — without rewriting from scratch for each channel.

## When to Use

Use this skill immediately after a new listing goes live, when refreshing marketing on an existing listing that has been sitting on the market, when preparing content for a pre-launch coming-soon period, or when a listing's price/status changes and marketing needs to be updated everywhere at once. This skill pairs naturally with `listing-description-writer.md` (which creates the master MLS copy) and `pre-launch-listing-audit.md` (which coordinates launch timing). Ideal for agents who struggle to keep content calendars full while juggling active listings.

## Required Input

Provide the following:

1. **Master listing description** — The MLS-ready copy (use output from `listing-description-writer.md` if available)
2. **Property basics** — Address (or neighborhood if privacy is needed), beds/baths, sqft, list price, property type
3. **Standout features** — Top 3–5 things that make this home unique (pool, view, chef's kitchen, lot size, school zone, recent reno, etc.)
4. **Target buyer persona** — Who is this home for (young professional, growing family, downsizer, investor, luxury buyer)
5. **Neighborhood hook** — What makes this location desirable (school district, walkability, lifestyle, commute, emerging area)
6. **Available visual assets** — Which photo types exist (exterior, kitchen, primary suite, backyard, aerial, twilight, video walkthrough) — needed to match script concepts to available visuals
7. **Platforms in use** — Which channels the agent actively posts to (Instagram, Facebook, TikTok, YouTube Shorts, LinkedIn, email list, SMS list, personal blog/website)
8. **Agent brand voice** — 2–3 words describing the agent's tone (e.g., "warm and local," "polished luxury," "data-driven advisor")

## Instructions

You are a real estate content strategist and AI assistant. Your job is to multiply one listing into a full content suite that sustains a 10–14 day marketing wave across every platform the agent uses, without feeling repetitive to any single audience.

**Before you start:**
- Load `config.yml` from the repo root for company details, brand voice, and compliance rules
- Reference `knowledge-base/best-practices/` for platform-specific formatting norms
- Reference `knowledge-base/regulations/` for fair housing language constraints that apply to ALL derivative content, not just MLS
- Confirm the master description is fair-housing-compliant before deriving content from it

**Process:**

1. **Audit the source material** — Read the master description. Identify the single strongest emotional hook (e.g., "golden-hour light over the backyard pool") and the single strongest rational hook (e.g., "top-rated school district, 12 minutes to downtown"). Most derivative content should lean on one of these two hooks.

2. **Map assets to platforms** — For each platform the agent uses, plan which formats fit the available visuals. Don't script a Reel that requires twilight footage if only daytime photos exist. Flag any gaps explicitly so the agent knows what to shoot.

3. **Generate the content package** — Produce the following 10 assets, labeled clearly:

   **A. Just-Listed Announcement Post** (Instagram/Facebook feed)
   - 80–120 words, opens with the emotional hook, ends with a soft CTA (DM, link in bio, open-house time)
   - Include 6–8 researched hashtags mixing neighborhood, property type, and lifestyle tags
   - No fair housing trigger words (family-friendly, safe neighborhood, perfect for kids, etc.)

   **B. Feature Carousel** (5 slides, Instagram/LinkedIn)
   - Slide 1: Hook + address (or area)
   - Slides 2–4: One standout feature per slide, each with a single-sentence caption
   - Slide 5: CTA slide ("Want the full tour? Link in bio.")

   **C. 30-Second Reel/TikTok Script**
   - Written as spoken narration with timestamps (0–3s hook, 3–25s tour, 25–30s CTA)
   - First 3 seconds must be a pattern interrupt (question, surprising fact, or visual reveal)
   - Include on-screen text suggestions for silent viewers

   **D. 15-Second Short** (YouTube Shorts/Reels)
   - Tighter version of C focused on one feature only — pool, kitchen, view, etc.

   **E. Email Blast** (past clients + sphere)
   - Subject line (under 50 characters) + 150-word body + CTA
   - Warm, personal tone — written as if to a friend, not a list

   **F. Open House Invite Post**
   - Square graphic caption + date/time/address
   - Include parking/entry instructions if relevant

   **G. Buyer Agent SMS** (for cooperating agents)
   - 2 sentences max: key specs + private showing instructions + agent contact
   - No emojis, no hype — professional peer-to-peer tone

   **H. LinkedIn Professional Post**
   - 150–200 words framed around market insight (what this listing signals about the neighborhood, price point, or inventory)
   - Ends with soft personal branding, not a hard property pitch

   **I. Blog/Long-Form Post Outline**
   - 5-section outline for a 600–900 word post ("Inside [Address]: What Makes This [Neighborhood] Home Stand Out")
   - Include suggested H2 headers, photo placement notes, and internal linking opportunities

   **J. Follow-Up "Still Available" Post** (for day 7–10 if unsold)
   - Reframes the listing without repeating Post A
   - Highlights a different feature and includes a concrete call to action (price-improvement tease, weekend showing slots, or testimonial from the seller)

4. **Apply brand voice calibration** — Rewrite every asset so it reads in the agent's stated voice. A "warm and local" agent uses first names and neighborhood references; a "polished luxury" agent uses understatement and specifics; a "data-driven advisor" uses numbers and comparisons.

5. **Flag compliance and gaps** — Before returning the package, call out:
   - Any claim that needs verification (school ratings, commute times, HOA details)
   - Any visual asset the agent still needs to shoot
   - Any platform the agent doesn't use where content was skipped
   - Any fair housing language risk that was rewritten

6. **Produce a posting cadence** — Recommend a 10–14 day sequence: which asset to post on which day, which platform, and the timing goal (awareness → consideration → urgency). Use knowledge-base/best-practices/ for platform-specific timing if available.

**Critical rules:**
- No fair housing trigger phrases in any derivative asset
- No claims that aren't supported by the master description or agent-provided facts
- No duplicate opening lines across assets on the same platform
- No emojis unless the brand voice explicitly calls for them
- Always separate facts ("3-bed, 2-bath") from opinions ("rare find")

## Example Output

**Input summary:**
Master description: 3BR/2BA mid-century modern in Highland Park, $875K, renovated kitchen, pool, oversized lot, top-rated school district.
Brand voice: warm and local.
Platforms: Instagram, Facebook, TikTok, email, LinkedIn.
Visuals available: all exterior, kitchen, pool, primary suite. Missing: aerial, twilight.

**Package output (excerpts):**

*A. Just-Listed (Instagram):*
"Golden-hour light pools across the backyard and spills into a kitchen that was clearly built for dinner parties. Just listed in Highland Park: 3 bed, 2 bath, and a lot that gives you room to breathe. Link in bio for the full tour — open Saturday 1–3pm."

*C. Reel Script (30s):*
"[0–3s, on camera outside]: 'Would you buy a house for the pool alone?'
[3–10s, pool b-roll]: 'Because this one might change your mind. Diving board. Mature trees. West-facing light.'
[10–22s, kitchen + living]: 'Inside: a renovated chef's kitchen, hardwoods original to 1962, and a primary suite that actually feels private.'
[22–30s, on camera]: 'Highland Park. 3 bed, 2 bath. Link in bio. I'll walk you through it Saturday.'
On-screen text: '3BR · 2BA · $875K · Highland Park'"

*J. Still Available Post (Day 10):*
"One week in, and I'm still thinking about that backyard. If your Saturday didn't get booked, this one's open 2–4. Highland Park, 3 bed, 2 bath, $875K. Come see it."

*Compliance flags:*
- "Top-rated school district" → added "according to GreatSchools 2025 ratings" in LinkedIn post
- Avoided "perfect for a family" → rewrote as "room to breathe"

*Visual gaps:*
- Twilight exterior shot recommended before Day 7 refresh
- Aerial drone shot would strengthen Reel opener
