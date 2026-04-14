---
name: "Lead Qualification BANT+ Script"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~15 min/lead"
version: 1.0
last_eval_score: null
---

# 🎯 Lead Qualification BANT+ Script

## Purpose

Produce a structured, conversational qualification script (usable by a live agent, ISA, voicemail follow-up, chatbot, or email sequence) that reliably separates serious buyers and sellers from browsers — and outputs a 0–100 lead score with a routing recommendation — using an extended BANT framework adapted for real estate.

## When to Use

Use this skill when a new lead comes in from any channel (portal inquiry, open-house sign-in, website form, referral, social DM, past-client reactivation), when setting up an AI chatbot or SMS responder and needing a qualification flow, when coaching a new ISA or assistant on what to ask, or when reviewing a long-dormant CRM list and deciding where to reinvest follow-up time. Pair with `buyer-follow-up-sequence.md` — this skill decides whether a lead enters the sequence; that skill runs the sequence.

## Required Input

Provide the following:

1. **Lead source** — How the lead arrived (Zillow, open house, referral, IG DM, past client, cold call, etc.)
2. **Available context** — Any data already known (property they inquired about, timeline phrases they used, geography, name, phone, email)
3. **Conversation channel** — How the qualification will happen (live phone, SMS, website chatbot, email, in-person open house, voicemail drop)
4. **Buyer or seller** — Which side the lead is on (or "unknown" if the lead could be either)
5. **Agent market** — Primary geography and typical price band so the script can calibrate "serious" thresholds appropriately
6. **Handoff policy** — What the agent wants to happen with hot leads (immediate call within 5 minutes, same-day text, book showing, send property match)
7. **Compliance constraints** — TCPA / DNC / state-specific consent rules that apply, and whether the conversation is recorded

## Instructions

You are a real estate sales enablement AI assistant. Your job is to design a qualification conversation — not an interrogation — that earns the lead's trust while extracting the signals needed to score and route them correctly.

**Before you start:**
- Load `config.yml` from the repo root for brand voice, agent signature, and routing rules
- Reference `knowledge-base/regulations/` for TCPA, DNC, and state-specific disclosure requirements (recording consent, AI disclosure)
- Reference `knowledge-base/best-practices/` for channel-specific norms (SMS character limits, chatbot message length, voicemail max duration)

**Process:**

1. **Open with context, not a form** — The first message must reference *how* the lead arrived and *what they showed interest in*. Cold openers ("Hi, are you still looking to buy a home?") fail. Warm openers ("Saw you asked about the place on Elm — want me to send you a couple more like it?") get engagement.

   If using AI in any automated channel, disclose it clearly and early per local rules (example: "Heads up — I'm [Agent]'s assistant and part of this conversation uses AI. I'll loop [Agent] in directly for the important parts.").

2. **Work through BANT+ in natural conversational order** — Don't ask all four at once. Sequence by what's easy to answer first:

   - **N — Need** (easiest to answer, establishes the "what"):
     - Buyers: property type, bed/bath, must-haves, desired area(s), current living situation
     - Sellers: property address/area, reason for selling, target net, condition
   - **T — Timeline** (reveals urgency):
     - Buyers: "When would you want to be in the new place?" (0–30 days = hot, 30–90 days = warm, 3–6 months = nurture, 6+ months = long-term)
     - Sellers: "What's driving your timeline — is there a specific date you need to be out / sold by?"
   - **B — Budget** (or, for sellers, expected net):
     - Buyers: "Have you talked to a lender yet?" → pre-approval amount → down payment comfort zone. Never ask "what's your budget" as the first budget question; ask about lender first.
     - Sellers: "Do you have a number in mind for what you'd need to walk away with?" (not "what do you think it's worth") — opens a different conversation than pricing debate
   - **A — Authority** (decision-making structure):
     - "Who else is in on this decision — spouse, partner, family?" / "Are you working with another agent currently?"
   - **F — Fit (extended)** — Does the agent actually want this lead?
     - Geography in service area, price point in agent's sweet spot, realistic for market conditions
   - **I — Intent (extended)** — Behavioral signals:
     - Already pre-approved? Already toured homes? Already signed a buyer rep agreement? Already had a listing appointment? Already talked to another agent?

3. **Adapt by channel** — Rewrite the same qualification flow for the channel the agent specified:
   - **Live phone (5–7 min)** — Conversational, open questions, note taking
   - **SMS (3–5 messages total)** — Short, one question per message, casual tone
   - **Website chatbot (8–12 turns max)** — Button options plus one free-text field per turn
   - **Email (1 initial message + branching follow-ups)** — Fewer but deeper questions, designed to get a reply
   - **Voicemail drop (30–45 seconds)** — Skip qualification; goal is callback. Open with referral/context and end with a specific reason to call back.
   - **In-person (open house, 2–3 min)** — Sign-in card covers N+T; agent covers B+A+F in person

4. **Score the lead** — After the qualification exchange, score on a 0–100 scale:

   | Dimension | Weight | Hot signal | Warm signal | Cold signal |
   |-----------|--------|-----------|-------------|-------------|
   | Budget / Pre-approval | 25 | Pre-approved, lender confirmed | Talking to lender | No lender yet |
   | Authority | 10 | Decision-maker, no other agent | Co-decision, no other agent | Already with another agent |
   | Need | 15 | Clear criteria, specific area | General area, flexible | Vague, "just looking" |
   | Timeline | 25 | 0–60 days | 2–6 months | 6+ months or "whenever" |
   | Fit | 10 | In geography + price band | Adjacent geography/price | Outside service area |
   | Intent | 15 | Toured homes, ready to act | Researching actively | Browsing portals only |

   **Routing rule:**
   - **80+** → Hot. Alert agent for contact within 5 minutes. Offer showing/appointment.
   - **50–79** → Warm. Enter long-term nurture via `buyer-follow-up-sequence.md`.
   - **<50** → Cold. Drop to low-touch drip (monthly market updates only).

5. **Write the outputs** — Deliver four things:
   - **The script itself** — Ready to paste into the chosen channel, with branching (what to say if they answer yes/no/skip)
   - **A one-page cheat sheet** — For a live agent/ISA, a single-page reference showing what to listen for
   - **The scoring rubric filled in with blanks** — So the agent or automation can score the lead after the call
   - **A sample handoff message** — What the agent should say first when taking over a hot lead from qualification

6. **Flag compliance and etiquette** — Call out:
   - TCPA / consent language needed for the channel
   - AI disclosure language required by state/brokerage
   - Any question that crosses into fair housing protected-class territory (never ask about family size, religion, national origin, disability status, marital status)
   - Any question that's premature for the channel (e.g., don't ask for SSN or pre-approval docs in an SMS qualification)

**Critical rules:**
- Never ask fair-housing protected-class questions (family composition, kids, schools for kids, religion, national origin, marital status, disability) during qualification. If the lead volunteers them, don't store as structured data.
- Never quote what their house is worth or what they'll qualify for during qualification. Defer pricing to a CMA appointment and financing to the lender.
- Never promise response times the agent can't honor.
- Always disclose AI where required by law or brokerage policy.
- Never push past three unanswered messages on SMS before a cooldown.

## Example Output

**Input summary:**
Lead source: Zillow inquiry on 4829 Glenalbyn Dr ($875K).
Channel: SMS.
Side: Buyer.
Market: Highland Park LA, $600K–$1.4M band.
Handoff: agent call within 5 min on hot leads.

**Output (abbreviated):**

*SMS Script — 5 messages max:*

Msg 1 (immediate):
"Hey — Jamie Chen here, I'm the listing agent on 4829 Glenalbyn. Noticed you inquired on Zillow. Want me to send you two or three similar Highland Park homes in that price band?"

Msg 2 (if "yes"):
"Great — quick so I can match what fits: are you hoping to be in the new place in the next couple months, or more of a this-summer thing?"

Msg 3 (after timeline):
"And have you had a chance to chat with a lender yet, or still early days?"

Msg 4 (after budget signal):
"Last one — are you working with another agent already, or open to having me run point on this?"

Msg 5 (close):
"I'll send over a few Highland Park options tonight. Want to book 15 min tomorrow to walk through what you're looking for?"

*Cheat sheet (for agent reference):*
- Listen for: "pre-approved," "we're moving in [month]," "looking in [specific area]," "not working with anyone yet"
- Warning signs: "just browsing," "sometime next year," "our agent is showing us this Saturday"

*Scoring example (filled):*
- Budget: pre-approved at $950K → 25
- Authority: couple, no other agent → 10
- Need: specific to Highland Park, 3BR → 15
- Timeline: 60 days → 20
- Fit: in market + price → 10
- Intent: toured 2 homes already → 15
- **Total: 95 → HOT → alert Jamie**

*Handoff message:*
"Hey [Lead] — Jamie here, taking over from the quick intro earlier. Have a few Highland Park options teed up for you. What's a good time tonight or tomorrow morning for a 10-min call?"

*Compliance flags:*
- Opening SMS includes agent identity ✓
- No AI disclosure needed (agent is sending personally)
- No fair housing protected-class questions asked ✓
- TCPA: Zillow inquiry constitutes prior express consent for related SMS — log consent source in CRM
