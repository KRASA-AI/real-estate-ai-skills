---
name: "30-Day Social Content Calendar"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~4 hrs/month"
version: 1.0
last_eval_score: null
---

# 🗓️ 30-Day Social Content Calendar

## Purpose

Generate a full 30-day cross-platform social media calendar for a real estate agent — with hooks, captions, CTAs, Reels concepts, carousel ideas, and a daily posting schedule — tuned to the agent's market, brand voice, and the current month's seasonal/market themes.

## When to Use

Use this skill at the start of each month, when onboarding a new agent who has no content plan, when entering a slow season and needing to stay visible, or when transitioning to a new neighborhood farm area and wanting a structured local-authority play. This skill is designed to produce a reusable plan — not individual posts — so pair it with `listing-content-multiplier.md` to fill any "active listing" slots and with `open-house-recap-email.md` for post-event content.

## Required Input

Provide the following:

1. **Agent profile** — Name, brokerage, primary farm area/neighborhoods, years in business, ideal client profile
2. **Brand voice** — 2–3 descriptors (e.g., "warm and local," "polished luxury," "data-driven," "energetic and millennial")
3. **Target month** — The calendar month the plan covers (affects seasonality and holidays)
4. **Active platforms** — Which channels the agent posts to (Instagram feed, Reels, TikTok, YouTube Shorts, Facebook, LinkedIn, email newsletter, blog)
5. **Posting goal** — Weekly post count target per platform (default: 5–7/week on primary platform, 2–3/week on secondary)
6. **Active listings or upcoming launches** — Any properties that need promotion during the month (dates, addresses, price points)
7. **Local events** — Known events in the farm area (farmers markets, school calendar, community events, seasonal openings)
8. **Current market context** — One-sentence summary (e.g., "buyer's market, rates dropped to 5.8%, inventory up 18% YoY")
9. **Content pillars** (optional) — If the agent already has defined pillars (e.g., "local guides / listings / process education / behind-the-scenes / client stories"), use them; otherwise recommend a set

## Instructions

You are a real estate content strategist and AI assistant. Your job is to produce a publish-ready 30-day calendar — not a generic template — that an agent could execute without further strategic decisions.

**Before you start:**
- Load `config.yml` from the repo root for brand voice, compliance rules, and company branding
- Reference `knowledge-base/best-practices/` for platform-specific cadence and format norms
- Reference `knowledge-base/regulations/` to ensure no fair housing trigger language slips into captions or video scripts
- Pull `knowledge-base/industry-overview.md` for seasonal context (spring buying season, fall inventory shifts, etc.)

**Process:**

1. **Establish or validate content pillars** — Every agent's calendar should rotate across 5 pillars:
   - **Local Authority** — Neighborhood guides, market stats, hidden-gem spots
   - **Active Inventory** — Just-listed, open houses, price changes, sold posts
   - **Process Education** — Buyer/seller tips, financing explainers, common-mistake posts
   - **Behind-the-Scenes** — A day in the life, prep work, honest moments
   - **Social Proof** — Client stories, testimonials, closing celebrations

   Confirm these pillars work for the agent's brand, or substitute per their input.

2. **Map the month** — Lay out 30 days. For each day, decide:
   - Which pillar it belongs to
   - Which primary platform gets a post
   - Which format (static image, carousel, Reel, Story-only, text post, email)
   - Whether it's tied to a listing/event/holiday/market moment

   Maintain roughly a 30/25/20/15/10 pillar mix (Local Authority / Active Inventory / Process Education / Behind-the-Scenes / Social Proof), adjusted for the agent's actual listing volume.

3. **Write every post** — For each scheduled day, produce:
   - **Hook** — The first 1–2 lines, designed to stop the scroll
   - **Caption** — 60–150 words depending on platform norms
   - **CTA** — Specific ask (comment, DM, save, click, book a call)
   - **Hashtags** — 5–10 researched tags mixing local, niche, and broad
   - **Visual direction** — What the photo/video should show (not just "photo of house")
   - **Reel/video scripts** — For video days, provide a timestamped script (hook, middle, CTA) with on-screen text

4. **Sequence for momentum** — Don't front-load the calendar. Spread listing promos across launch windows, cluster educational posts mid-week, save vulnerable/behind-the-scenes posts for Sundays (highest engagement for personal content), and keep Fridays light or market-recap focused.

5. **Add a weekly theme** — Give each of the 4–5 weeks a light unifying thread (e.g., "Week 1: What's new in [farm area]," "Week 2: Buyer prep series," "Week 3: Behind a listing launch," "Week 4: Local businesses I love"). Themes make the calendar feel intentional without constraining flexibility.

6. **Build the posting schedule** — Output a calendar table with columns:
   - Date + day of week
   - Platform(s)
   - Pillar
   - Format
   - Hook (first line only, for quick scanning)
   - Post-time recommendation
   - Prep required (photo shoot, data pull, graphic design)

7. **Flag prep and dependencies** — Before the output is final, call out:
   - What photography or video needs to be captured ahead of time
   - Any data the agent needs to pull (new market stats, school rankings, testimonial approval)
   - Any holidays or local events that a post depends on
   - Any platform where the agent doesn't have enough content and a pillar was reduced or reallocated

8. **Provide a "repurposing map"** — For at least 5 of the 30 posts, show how the same core idea can be re-expressed across 2–3 platforms with different formats (e.g., Monday's Reel becomes Wednesday's LinkedIn text post becomes Friday's email newsletter section).

**Critical rules:**
- No fair housing trigger language in any caption or script (no "family-friendly," "safe neighborhood," "perfect for families," "exclusive community" framed by demographics, etc.)
- No claims about market conditions that aren't supported by the agent-provided context
- No borrowed hooks from named competitors or recognizable viral formats
- Every Active Inventory post must include a compliance-safe address-or-area treatment (follow brokerage rules on disclosing specific addresses)
- Sunday posts default to lighter, more personal content unless the agent specifies otherwise

## Example Output

**Input summary:**
Agent: Jamie Chen, Coldwell Banker, farms Highland Park + Eagle Rock (LA), 6 years in business.
Voice: warm and local.
Month: May 2026.
Platforms: Instagram (feed + Reels), TikTok, email newsletter.
Target: 6 posts/week IG, 4/week TikTok, 1 email.
Active listing: 4829 Glenalbyn Dr (Highland Park, $875K), open May 4.
Market: buyer's market, inventory up 12% YoY, rates 6.1%.

**Output excerpts:**

*Weekly themes:*
- Week 1 (May 1–3): "What's moving in Highland Park this spring"
- Week 2 (May 4–10): "Inside a listing launch" — built around Glenalbyn open house
- Week 3 (May 11–17): "Buyer prep intensive"
- Week 4 (May 18–24): "The local list" — favorite neighborhood spots
- Week 5 (May 25–31): "Month in review + what's coming"

*Sample day (Tuesday, May 5 — Reel):*
- Pillar: Active Inventory
- Platform: Instagram Reel + TikTok
- Hook: "The kitchen in this Highland Park listing is 60 years old. And it's probably the best room in the house."
- Script (30s):
  - 0–3s: Agent on camera in kitchen. "60 years old. Best room in the house."
  - 3–20s: B-roll of kitchen details — original cabinetry, new counters, light through the window.
  - 20–30s: "Open Saturday, 1–3. 4829 Glenalbyn. Link in bio."
- On-screen text: "3BR · 2BA · $875K · Highland Park"
- Post time: 7:30 AM
- Prep: shoot 20-sec kitchen b-roll Monday morning

*Sample day (Sunday, May 10 — Behind the Scenes):*
- Pillar: Behind-the-Scenes
- Platform: Instagram feed (single photo)
- Hook: "Open house number 184. Still a little nervous every time."
- Caption (90 words): warm reflection on what the job still feels like after 6 years, ending with "If you're thinking about listing this year, that care is what you're hiring."
- Post time: 6:00 PM

*Prep flagged:*
- Schedule photo shoot for Glenalbyn listing by May 2
- Pull Highland Park May comps by May 25 for month-in-review post
- Confirm client permission to share closing photo (testimonial post, May 22)

*Repurposing map (partial):*
- Tuesday's kitchen Reel → Wednesday TikTok → Thursday email newsletter "Listing of the Week"
- Week 3's buyer prep carousel → LinkedIn text post → blog post later in month
