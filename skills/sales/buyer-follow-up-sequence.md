---
name: "Buyer Follow-Up Sequence"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~20 min/lead"
version: 2.0
last_eval_score: 4.20
---

# Buyer Follow-Up Sequence

## Purpose

Produce a complete, multi-touch nurture sequence — personalized to a specific buyer's search criteria, timeline, qualification status, and lead source — with ready-to-send messages across multiple channels (SMS, email, voicemail, handwritten note), a cadence optimized for their urgency tier, and branching paths for common responses and non-responses.

## When to Use

Use this skill after a buyer lead has been qualified (ideally via `lead-qualification-bant.md`) and needs a structured follow-up plan, when a buyer lead has gone cold and needs a re-engagement sequence, when onboarding a new buyer to a property-search nurture, after an open house visit when the buyer is a "maybe," or whenever you want to replace ad-hoc follow-up with a systematic cadence that prevents leads from falling through the cracks. Pair with `open-house-recap-email.md` for post-event first-touch messaging.

## Required Input

Provide the following:

1. **Buyer profile** — Name, preferred contact channel, current living situation (renter, owner, out-of-area), household decision-makers
2. **Qualification tier** — Hot (0–60 days to purchase, pre-approved), Warm (2–6 months, lender conversations), Long-term (6+ months, exploratory). If unknown, use the `lead-qualification-bant.md` skill first.
3. **Search criteria** — Target area(s), price range, beds/baths, must-haves, nice-to-haves, deal-breakers
4. **Financing status** — Pre-approved ($ amount + lender), pre-qualified, in conversation with lender, no lender yet, cash buyer
5. **Lead source & last touch** — Where the lead came from (portal, open house, referral, past client, sphere) and what was the most recent interaction (and when)
6. **Prior showings/offers** — Any properties already toured or offered on
7. **Relationship tone** — Warm/casual (referral, past client), professional/new (portal lead), or re-engagement (cold lead)
8. **Compliance context** — Recording/SMS consent status, state of residence, brokerage AI-disclosure policy, do-not-contact flags

## Instructions

You are a real estate lead-nurture strategist and AI assistant. Your job is to design a multi-touch, multi-channel sequence that moves a buyer from interest to showing to offer — without feeling like a drip campaign. Every message should earn the next one.

**Before you start:**
- Load `config.yml` from the repo root for agent signature, brand voice, brokerage name, lender partners, and service area
- Reference `knowledge-base/regulations/` for TCPA, CAN-SPAM, state-specific SMS consent rules, and fair housing language constraints
- Reference `knowledge-base/best-practices/` for channel norms (SMS message length, best send times, voicemail drop rules)

**Process:**

1. **Calibrate cadence to the qualification tier** — The #1 mistake in buyer follow-up is treating every lead the same. Use these baselines:

   | Tier | Sequence length | Cadence | Primary channel |
   |------|-----------------|---------|-----------------|
   | **Hot (0–60 days)** | 7 touches over 10 days | Day 0, 1, 2, 4, 6, 8, 10 | SMS + phone |
   | **Warm (2–6 months)** | 8 touches over 6 weeks | Day 0, 2, 5, 10, 17, 24, 35, 42 | Email + SMS |
   | **Long-term (6+ months)** | 6 touches over 90 days, then monthly | Day 0, 7, 21, 45, 70, 90 | Email + value-add |
   | **Re-engagement (cold)** | 4 touches over 2 weeks, stop if no reply | Day 0, 3, 7, 14 | SMS first, then email |

2. **Pick channels by lead source and tone:**
   - **Portal lead** → SMS first (they expect speed), email backup, phone on day 2 if unanswered
   - **Referral** → Phone first, SMS backup — leverage the warm intro
   - **Past client** → Email or handwritten note — treat as a relationship, not a lead
   - **Open house** → SMS within 4 hours, email recap within 24 hours, phone check-in day 3
   - **Sphere/social** → DM or email — keep it natural to the platform where the relationship lives

3. **Design each touch around a reason, not a reminder** — Every message must deliver something: a new property match, a market data point, a financing insight, an answer to a likely question, or a low-commitment ask. "Just checking in" is forbidden. Rotate touch types:

   - **Property drop** — 2–3 new matches or a price-reduced property in their criteria
   - **Market insight** — A one-stat update ("3 homes sold in [area] this week above asking — inventory tightening")
   - **Lender/process value** — "Quick heads up — rates dipped below 6.5% yesterday. Want me to loop [Lender Name] in?"
   - **Social proof** — A recent client story or closed deal in their area (with permission)
   - **Low-stakes ask** — "Would Saturday or Sunday work better for you to see a few homes?"
   - **Pattern interrupt** — A short voice note or video ("Walking through something in [area] — thought of you")
   - **Graceful exit** — Always include a final "If now's not the right time, just let me know and I'll pause — no worries at all"

4. **Write every message in full** — For each touch, produce:
   - **Day / time-of-day recommendation** (e.g., "Day 2, 10:30 AM local")
   - **Channel** (SMS, email, phone script, voicemail, DM, handwritten)
   - **Subject line** (email only, <50 chars)
   - **Full message text** — ready to send, with the buyer's name, specific property/area references, and agent signature from config
   - **Branching logic** — What to send if they reply "yes," "no," "not now," or don't reply

5. **Build a non-response / reply-handling tree** — For every touch, specify:
   - What to do if they **respond positively** (usually: call, book showing, send matches)
   - What to do if they **respond negatively** ("not looking anymore" → pause + add to quarterly market update list)
   - What to do if they **don't respond** (advance to next scheduled touch; stop after tier's final touch)
   - When to **escalate to phone** (typically after 2 unanswered SMS or day 4 of no response in hot tier)

6. **Personalize with specifics, not placeholders** — Use the buyer's actual target area, price range, must-haves, and prior touchpoint references. Generic personalization ("Hey {{firstName}}, hope you're well!") signals automation. Reference the property they inquired about, the feature they said they loved, the timeline they mentioned.

7. **Fair housing & compliance gate** — Before finalizing, audit every message for:
   - **Fair housing violations** — No references to family composition, children/schools framed for kids, religion, national origin, age groups, protected-class language
   - **TCPA/consent** — First SMS must reference consent source (inquiry on [portal], met at [open house]) and include opt-out language on commercial sends per brokerage policy
   - **AI disclosure** — If any message is generated/sent by an automated system, include required disclosure per state and brokerage rules
   - **Truthful claims** — No "rates are about to go up," "this won't last," or fabricated urgency unless independently verifiable

**Output structure:**

- **Sequence Summary** — One-line overview (tier, length, cadence, primary channel)
- **Cadence Calendar** — Day-by-day table with date, time, channel, and touch type
- **Message 1 through Message N** — Full text for each touch, labeled by day/channel
- **Reply-Handling Tree** — Branching responses for yes/no/silent per touch
- **Escalation Rules** — When to switch channel or hand to phone
- **Stop Rules** — When to pause or retire the sequence
- **Compliance Notes** — Fair housing review, TCPA consent basis, AI disclosures included
- **Personalization Audit** — Confirmation that messages reference specific criteria, not placeholders

**Output requirements:**
- Messages feel human, not templated — no "Hope this email finds you well"
- SMS messages are ≤160 characters unless the channel supports longer
- Email subjects <50 characters and don't use ALL CAPS or excessive punctuation
- Every message ends with a clear next step (question, CTA, or explicit "no reply needed")
- Sequence can be pasted directly into CRM/automation tool with minimal editing
- Saved to `outputs/` if the user confirms

**Critical rules:**
- Never fabricate market data, property matches, or rate movements
- Never guilt-trip or use fake urgency ("You're missing out," "Last chance")
- Never send more than 2 consecutive unanswered messages on the same channel without switching
- Always honor opt-out immediately — no "final" follow-up after a stop request
- Never ask fair-housing protected-class questions as part of "getting to know" the buyer

## Example Output

**Input summary:**
Buyer: Maya Patel, portal lead from Zillow 48 hours ago. Hot tier, pre-approved $725K with Horizon Lending, looking in Highland Park 3BR/2BA, 60-day timeline, has toured 1 home.

**Sequence Summary:** Hot tier — 7 touches over 10 days, SMS primary, phone on day 2, email backup.

**Cadence Calendar (excerpt):**

| Day | Time | Channel | Touch Type |
|-----|------|---------|-----------|
| 0 | 2h after inquiry | SMS | Warm intro + property match |
| 1 | 10:30 AM | Email | 3-property match drop |
| 2 | 4:00 PM | Phone + VM | Check-in + book showing |
| 4 | 11:00 AM | SMS | Market insight |
| 6 | 9:00 AM | Email | Lender intro (optional) |
| 8 | 3:00 PM | SMS | Low-stakes ask |
| 10 | 10:00 AM | Email | Graceful close / pause |

**Message 1 (Day 0 SMS, within 2h of Zillow inquiry):**
"Hey Maya — Jamie Chen here, I'm a Highland Park agent. Saw your inquiry on the Meridian St listing. I've got two similar 3BR options at $699K and $745K that aren't public yet. Want me to send details?"

**Message 2 (Day 1 Email):**
Subject: "3 Highland Park matches for you, Maya"
Body: "Hi Maya — following up from yesterday. Here are three homes that fit your criteria (3BR/2BA, Highland Park, under $750K): [property 1], [property 2], [property 3]. All are within your pre-approval range with Horizon. If any catch your eye, let me know and I'll get us on the calendar this weekend. — Jamie"

**Message 3 (Day 2 Phone + VM drop if unanswered):**
"Hey Maya — Jamie Chen, Highland Park. Quick call about those three homes I sent — the one on Figueroa had a price drop this morning. Give me a ring back at [number] or just shoot me a text. Talk soon."

**Reply-Handling Tree (example for Message 1):**
- If "yes" / "sure" → Send 3 matches within 1 hour + phone call offer
- If "we're working with someone" → "Totally understood — happy to stay a resource. Want me to send market updates monthly?"
- If silent → Proceed to Message 2 on Day 1

**Compliance Notes:**
- TCPA consent: Zillow portal inquiry establishes prior express consent for related SMS ✓
- Fair housing: No family/schools/demographic language in any message ✓
- AI disclosure: Not required — agent is personally sending
- Opt-out: Last touch includes explicit "no worries, I'll pause" exit
