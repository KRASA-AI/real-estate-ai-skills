---
name: "Open House Recap Email"
category: customer-service
tools: [claude, chatgpt]
difficulty: beginner
time_saved: "~5 min/visitor"
version: 2.1
last_eval_score: 8.90
---

# Open House Recap Email

## Purpose

Generate individualized post-open-house follow-up emails for each visitor — tiered by interest level, personalized from sign-in and agent notes, and paired with a clear next-step CTA — so that warm prospects get a concierge touch while casual browsers get a light, respectful follow-up that leaves the door open for later.

## When to Use

**Quick Start (minimum viable run):** Two inputs produce the full set of send-ready emails — the **property details** and the **visitor list** (whatever fields each visitor left). The skill tiers each visitor from the sign-in and any reaction notes you captured, applies the per-tier structure, and pulls the agent's signature, brand voice, follow-up cadence, and service area from `config.yml` so every email already sounds like the agent. That is the Pass-1 input set. Add the Pass-2 enrichment — your live per-visitor observations, an explicit interest tier, seller context, and an explicit brand-voice note — when you want the specific-recall openers and CTAs tuned past what the sign-in alone supports. A solo agent who worked the door can paste the sign-in sheet and ship; the recall lines get sharper the moment per-visitor observations are added.

Use this skill within 24 hours of an open house to convert the visitor list into individual follow-up emails, when preparing the recap for a team member who covered the open house for you, when refreshing follow-up on a still-active listing where previous visitors haven't been re-contacted, or whenever you want to replace the generic "Thanks for stopping by!" template with messages calibrated to each visitor's actual interest. Pair with `buyer-follow-up-sequence.md` for any visitor who moves to active nurture.

## Required Input

Input is split into a **Required Core** (Pass 1 — the emails ship on these) and **Optional Enrichment** (Pass 2 — sharpens the recall openers, tiering, and messaging). Each Optional item has a default the skill applies and names when omitted, so a partial sign-in sheet still produces send-ready emails.

### Pass 1 — Required Core (the emails ship on these)

1. **Property details** — Address, list price, beds/baths, headline features, open-house date and time, next open-house date if scheduled, number of offers currently in hand
2. **Visitor list** — For each visitor, provide what you have (name, email, phone, how they heard about the open house, whether they're working with an agent, timeline, budget range, reaction notes)

### Pass 2 — Optional Enrichment (each has a default if omitted)

3. **Agent observations** — Your live notes on each visitor's behavior: which rooms they spent time in, what they asked about, how long they stayed, whether they returned with someone, any specific objections or enthusiasm. *Default if omitted: derive the specific-recall opener from the sign-in fields (how they heard, stated timeline, working-with-agent status); any visitor with no observable detail is routed to the `Gaps Flagged` list with a phone-follow-up suggestion rather than given a fabricated recall line.*
4. **Interest tiering** — For each visitor, assign one of: **Hot** (serious buyer, no agent, clear timeline), **Warm** (interested but not urgent, or has an agent), **Neutral** (neighbors, casual browsers, investors scouting), or **Unknown** (didn't sign in fully, brief visit). *Default if omitted: the skill infers the tier from the sign-in + observation data using the Step-1 tiering rules and states the inferred tier next to each email so the agent can correct it.*
5. **Seller context** — Any facts relevant to messaging: recent price drop, seller motivation to close by a specific date, competing showings scheduled, pre-inspection report available. *Default if omitted: write the body around the property's headline features and any verifiable open-house facts only; never invent urgency or offer counts.*
6. **Brand voice** — 2–3 descriptors (e.g., "warm and local," "professional concierge," "data-forward advisor"). *Default if omitted: use the voice profile from `config.yml` — `voice.tone`, the `always_use` phrases, and the `never_use` blocklist — and match the agent's `followup_style` cadence; flag the emails for voice confirmation on Pass 2.*
7. **Agent config** — `config.yml` is auto-loaded and is the personalization backbone of every email: signature block (name, phone, email, brokerage, license #, brokerage physical address for CAN-SPAM), `service_area` (used to fill the Neutral/stay-in-touch CTA — "anything in [service_area] that fits"), `voice.tone` + `always_use` + `never_use` (applied to every body), `voice.followup_style` (sets the send-order cadence in the output), and the agent's CRM (the emails are formatted to paste into that CRM's note/email field). *Auto-loaded; the skill names any config field it could not find rather than substituting a placeholder.*

## Instructions

You are a real estate listing agent's AI assistant. Your job is to write individualized, non-template follow-up emails to open-house visitors — each one tuned to the visitor's interest level, what they actually said and did, and the next step that makes sense for that relationship.

**Before you start:**
- Load `config.yml` and use it as the personalization backbone, not just a signature source: pull the signature block (name, phone, email, brokerage, license #, brokerage physical address for CAN-SPAM), `service_area` (fills the Neutral stay-in-touch CTA), `voice.tone` + `always_use` phrases + `never_use` blocklist (applied to every body), `voice.followup_style` (sets the send-order cadence), and the agent's CRM (format the emails to paste cleanly into that CRM). Name any field you could not find rather than substituting a generic placeholder.
- Reference `knowledge-base/regulations/` for CAN-SPAM requirements, fair housing language, and state-specific brokerage disclosure rules
- Reference `knowledge-base/best-practices/` for email subject-line norms and open-house follow-up timing

**Process:**

0. **Determine the pass and label the output.** If only the Required Core (property details + visitor list) is supplied, run **Pass 1 (Fast Recap)**: infer each visitor's tier from the sign-in + observation fields, draw voice and the stay-in-touch CTA from `config.yml`, label the batch "Fast Recap — confirm inferred tiers and add live observations to sharpen recall lines," and list the defaults applied. If Optional Enrichment is supplied, run **Pass 2 (Tuned Recap)** at full depth. Either pass runs the full Step-7 compliance audit and the no-fabrication rules — the fast path never skips fair-housing review or invents observations to manufacture a recall line.

1. **Segment the list by interest tier** — Before drafting any email, group visitors into Hot / Warm / Neutral / Unknown. Each tier gets a different structure, tone, and CTA:

   | Tier | Subject tone | Length | CTA | Target reply rate |
   |------|--------------|--------|-----|-------------------|
   | **Hot** | Direct, specific | 80–120 words | Private showing offer, offer deadline heads-up | 60%+ |
   | **Warm** | Warm, informative | 60–90 words | Additional info, 2nd visit, or market update | 25–35% |
   | **Neutral** | Friendly, light | 40–60 words | None required — stay-in-touch only | <10% |
   | **Unknown** | Curious, low-pressure | 40–60 words | Soft question to gauge interest | 15–20% |

2. **Open with a specific recall, not "Thanks for stopping by"** — The first sentence must reference something only you could know about that visitor's visit. Examples:
   - "Saw you lingering in the primary suite — it's my favorite room too."
   - "You mentioned you've been looking in Highland Park for about three months — wanted to circle back."
   - "The question you asked about the HOA — I dug into it after you left, and here's the answer."
   If no specific observation exists (visitor barely signed in), open with a neighborhood or property-specific hook instead of a generic greeting.

3. **Deliver something in the body** — Every email must include at least one piece of information the visitor didn't have at the open house:
   - An answer to a question they asked
   - A comp, market stat, or days-on-market update
   - A pre-inspection highlight
   - The seller's flexibility on close date or rent-back
   - A relevant recent sale in the area
   - A next open-house date or private-showing slot

4. **Calibrate the CTA to the tier:**
   - **Hot:** "I have a window tomorrow at 11 AM or Saturday at 2 PM for a private showing with [spouse/partner]. Which works?"
   - **Warm:** "Happy to send the comps I pulled or keep you posted if the seller adjusts price. Which would be more useful?"
   - **Neutral:** No ask — just "If anything in Highland Park comes across my desk that fits what you're looking for, mind if I send it?"
   - **Unknown:** One low-stakes question: "Were you specifically looking in [neighborhood] or more just curious about the area?"

5. **Handle the cooperating-agent visitor carefully** — If the visitor has an agent, do not try to convert them. The email should:
   - Acknowledge their agent respectfully
   - Share one or two facts useful to their decision (pre-inspection, seller motivation)
   - Ask to be looped in via their agent if they want to pursue it
   - This preserves professional relationships and protects procuring-cause boundaries

6. **Personalize from sign-in + observation data** — Use actual names, actual feedback, actual criteria. No "{{firstName}}," no "You showed interest in the property," no "As discussed." Every sentence should feel like it was written for one person.

7. **Compliance audit before sending:**
   - **Fair housing:** No references to family composition, schools framed for children, religion, age, national origin, ability status. "Great for growing families" is illegal — rewrite as "oversized yard and flexible floor plan."
   - **CAN-SPAM:** Every email includes a physical brokerage address and an unsubscribe path (even for 1:1 emails, best practice is to include it)
   - **Brokerage disclosure:** License number in signature where state requires
   - **Truthfulness:** No inventing offers ("multiple interested parties" only if verifiably true), no fake urgency

**Output structure:**

- **Segmentation Summary** — Count of visitors per tier and rationale for grouping
- **Individual Emails** — One per visitor, with:
  - Subject line (<50 characters, no all-caps, no excessive punctuation)
  - Full email body (ready to send, personalized opener, information delivery, tier-appropriate CTA)
  - Signature block from config
- **Send-Order Recommendation** — Hot tier first (within 2 hours of open house), Warm within 12 hours, Neutral/Unknown within 24 hours
- **Compliance Notes** — Fair housing review, CAN-SPAM compliance confirmation, license disclosure included
- **Gaps Flagged** — Visitors who didn't leave enough info for a real personalization (suggest phone follow-up instead of email)

**Output requirements:**
- Each email reads like it was hand-written for that visitor
- Subject lines are curiosity-driven, not sales-y ("A quick answer on 4829 Glenalbyn" not "Amazing Open House Opportunity!!!")
- Body length matches tier — don't write 200 words to a neutral browser
- Tone matches the agent's brand voice — apply `config.yml` `voice.tone`, weave in the `always_use` phrases where they land naturally (never forced), and respect the `never_use` blocklist in every email; the Neutral stay-in-touch CTA names the agent's actual `service_area` rather than a generic "the area"
- Every CTA has a specific next action (date/time/channel), not a vague "let me know"
- Ready to paste into email client or CRM with no editing
- Saved to `outputs/` if the user confirms

**Critical rules:**
- Never fabricate offers, interest, or urgency
- Never ask about or reference protected-class characteristics
- Never try to poach a visitor who's working with another agent — share info, let their agent work
- Never use "{{}}" template placeholders in the final output
- Honor any visitor who asked not to be contacted — skip them entirely

## Example Output

**Property:** 4829 Glenalbyn Dr, Highland Park, $875K. Open house Saturday 1–3 PM.
**Visitor:** Maria Nguyen, signed in as "first-time buyer, no agent yet." Stayed 45 min, asked about HOA and roof age, brought her mom on second pass.

**Tier:** Hot (no agent, specific questions, extended visit, brought decision-maker)

**Subject:** "Quick answer on the roof — 4829 Glenalbyn"

**Body:**
"Hi Maria — it was great meeting you and your mom on Saturday. You asked about the roof age, so I followed up with the seller: it's a 2019 install with a transferable 25-year warranty. I also pulled the HOA financials — they have $340K in reserves and no special assessments planned.

The seller has indicated some flexibility on a late-June close if that helps your timeline. There's currently one offer in, and a private showing slot open Wednesday at 6 PM. Would you and your mom want to come back and take a second look, maybe with your lender joining by phone?

Let me know what works and I'll hold the time.

— Jamie Chen
Coldwell Banker | CA DRE #01234567
(555) 123-4567 | jamie@chenhomes.la
1234 N Figueroa St, Los Angeles, CA 90042"

**Compliance Notes:**
- Fair housing: No family/age language ✓
- CAN-SPAM: Physical address in signature ✓
- License #: Included per CA DRE requirement ✓
- Offer reference: Verified with seller before sending ✓
