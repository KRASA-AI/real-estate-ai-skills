---
name: "Seller Intent Scorer"
category: sales
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~2 hrs/batch"
version: 1.0
last_eval_score: null
---

# 🏡 Seller Intent Scorer

## Purpose

Mine an existing CRM or past-client database for hidden seller opportunities by scoring every homeowner contact on listing likelihood over the next 0–12 months. The skill ingests a contact list plus per-contact enrichment (estimated equity, tenure, life-stage signals, behavioral activity) and outputs a ranked seller pipeline with a 0–100 intent score, a predicted listing window, a personalized outreach angle, and a recommended next touch for each contact — so the agent works the top of the list instead of dialing the whole book in alphabetical order.

## When to Use

Use this skill at the start of every quarter, before launching a seller-lead campaign, after any major rate move or market shift (the equity math changes), when the agent's new-listing pipeline dips, after a life-event signal triggers from the CRM (new job, death in family, divorce, second child), or when deciding who gets the next postcard drop, door-knock, or CMA offer. The concept generalizes the product pattern popularized by Lofty's Homeowner Agent and Offerpad's Scout but is tool-agnostic: any CRM with basic contact fields can be scored with this prompt. Pairs with `buyer-follow-up-sequence.md` (for the actual outreach cadence once scored) and `cma-presentation-generator.md` (for the CMA handoff when a contact tips into "hot").

## Required Input

Provide the following for each batch (CSV, table paste, or list):

1. **Contact list** — Minimum fields per contact: name, address, date-of-purchase (or years in home), estimated home value (Zestimate / RPR / AVM), estimated mortgage balance or equity range, relationship source (past client, sphere, open house lead, online lead, referral), and last-contact date
2. **Enrichment signals available** — Which of these the agent can populate per contact: school-age children changing schools, job change, divorce filing, probate, recent refinance, recent HELOC, recent permit pull, recent insurance claim, adjacent off-market sale, recent website activity (if the CRM tracks it)
3. **Market context** — Current median days on market, current month-of-inventory (MOI), YoY price appreciation in the area, average seller concession percentage
4. **Agent capacity** — How many listing conversations the agent can realistically start in the next 30 days (governs how deep down the ranked list to go)
5. **Outreach channels allowed** — Phone, SMS, email, handwritten note, door-knock, direct mail, social DM (constrained by TCPA and CAN-SPAM rules)
6. **Protected sensitivities** — Any contact flagged do-not-contact, in active distress, in litigation, or asked for space

## Instructions

You are a real estate CRM analyst specializing in proactive seller pipelines. Your job is to rank a book of homeowner contacts by listing likelihood and produce a working list the agent can pick up today — not a generic report.

**Before you start:**
- Load `config.yml` for market, rate assumption, and the agent's preferred listing-presentation materials
- Reference `knowledge-base/regulations/` for TCPA, CAN-SPAM, Do-Not-Call, and fair housing rules; no outreach recommendation may violate them
- Reference `knowledge-base/best-practices/` for outreach norms in the agent's market
- Confirm the contact list is the agent's own CRM or a list they have an existing relationship with — do not score a cold purchased list with a "past client" label

**Process:**

1. **Normalize the data.** Standardize home value, equity, and tenure across all contacts. Flag rows with missing fields; do not fabricate values. If equity is supplied as a range, use midpoint. If tenure is missing but purchase year is present, compute. If purchase year is missing, mark the contact `INCOMPLETE` and move to a separate "needs enrichment" bucket rather than scoring blind.

2. **Compute the five score components.** For each contact, assign 0–20 points on each of these dimensions, then sum to get the 0–100 intent score.

   **A. Equity Score (0–20)** — Higher equity means more optionality to sell. Band: <10% equity → 2; 10–25% → 6; 25–40% → 10; 40–60% → 14; 60–80% → 18; 80%+ → 20. Adjust −4 if the home is underwater or within 5% of purchase price in a flat market (seller has little incentive). Adjust +2 if there is a HELOC signal (indicates equity awareness).

   **B. Tenure Score (0–20)** — Median US tenure at sale is 13 years; local medians vary. Band: <3 years → 4 (sunk costs, likely low intent unless life event); 3–5 years → 10; 5–8 years → 14; 8–13 years → 18; 13+ years → 20. For move-up markets or starter-home zips, compress: the 5–8 year band becomes the peak.

   **C. Life-Stage Score (0–20)** — Points awarded for specific signals, capped at 20: youngest child leaving school zone +8; job change beyond reasonable commute +10; divorce filing +12 (handle with extreme sensitivity); inheritance/probate +12; recent second child (outgrowing home) +8; retirement or age 65+ in larger home +6; death of spouse or partner +8 (handle with extreme sensitivity); multiple adjacent signals stack but cap at 20.

   **D. Behavioral Score (0–20)** — Points for observed actions, capped at 20: website activity on home-value or sold-listing pages in last 30 days +8; opened 3+ agent emails last 60 days +4; clicked a CMA or home-value link +10; requested a home valuation +15; asked about contractor referrals or repair bids +6; liked or commented on sold-listing posts +3.

   **E. Market-Fit Score (0–20)** — Does the CURRENT market favor selling this specific home? Points: supply shortage in zip (MOI < 3) +12; price-per-sqft above purchase by 40%+ → +6; days-on-market in zip < 21 → +6; rate trend favorable (rates dropping > 50 bps last 90 days) → +4; seller-concession percentage in zip < 2% → +2. Cap at 20. Subtract 4 if MOI > 6 or days-on-market > 60.

3. **Classify each contact by band.**
   - **80–100 "Hot Seller"** — Reach out this week. Personalized call or door-knock, then CMA offer. Predicted listing window 0–90 days.
   - **60–79 "Warm Seller"** — Reach out this month. Personalized email or SMS with a reason-to-call (neighborhood-specific insight), then CMA offer on response. Window 90–180 days.
   - **40–59 "Likely 6–12 months"** — Monthly nurture (market update + specific-to-them insight). Add to `buyer-follow-up-sequence` as a seller-nurture variant.
   - **20–39 "Long-term nurture"** — Quarterly check-in, value-first content, SOI-appropriate touches only.
   - **<20 "Cold"** — Keep in database. Do not send seller-specific outreach.

4. **Generate a personalized outreach angle per Hot/Warm contact.** For each contact in the top two bands, produce ONE sentence that references a specific, verifiable fact about their home or situation (e.g., "Three houses on your block have sold this year above $1.1M, and the last one had 40% less yard than yours."). Do not fabricate comps. If the input does not contain neighborhood-comp data, mark the angle `[NEEDS COMP DATA]` and request it rather than inventing. The angle is the reason the outreach is welcome rather than cold.

5. **Recommend the first touch.** For each Hot/Warm contact, choose ONE channel and ONE message format consistent with the relationship source:
   - Past client → phone call, then handwritten note if no answer
   - Sphere → in-person or social DM, not cold email
   - Online lead (prior) → SMS during business hours or email
   - Open-house lead → email with CMA offer; phone only if they opted in
   Every recommendation must be TCPA/CAN-SPAM compliant. Never recommend an SMS for a contact who has not opted in.

6. **Surface compliance and sensitivity flags.** Before shipping, call out:
   - Any contact on the DNC list with phone recommended (block the recommendation)
   - Any contact flagged as sensitive (recent divorce, probate, death) and soften the angle accordingly — these contacts should not receive market-opportunity framing; use relational, no-agenda framing instead
   - Any score that relies on data the agent did not actually have (the row should be marked "score incomplete, enrich and rerun")
   - Any contact where fair housing risk appears (e.g., targeting based on family composition framed commercially — always reframe around the home, not the household)

7. **Output a working table and a pipeline summary.** Produce:
   - A ranked table with columns: Rank, Name, Address, Intent Score, Band, Predicted Window, Outreach Angle (one sentence), Recommended First Touch, Flag
   - A pipeline summary: how many in each band, top 3 data gaps blocking better scoring, recommended 30-day action plan sized to the agent's stated capacity
   - A list of contacts to re-run after enrichment (those marked INCOMPLETE)

**Critical rules:**
- No fabricated equity, value, or comp numbers. If data is missing, mark the row, do not score it.
- Outreach recommendations must comply with TCPA, CAN-SPAM, and fair housing.
- Sensitive life events (death, divorce, probate) never receive opportunistic framing. A human agent, not an automated sequence, initiates that contact.
- Scoring is a prioritization tool, not a prediction guarantee. Communicate uncertainty in the output.
- Never output the full list with commercial framing for contacts flagged DNC, litigating with the agent, or explicitly asked for space.

## Example Output

**Pipeline summary:**
- Contacts scored: 412
- Hot Seller (80–100): 7
- Warm Seller (60–79): 24
- Likely 6–12 mo (40–59): 68
- Long-term nurture (20–39): 183
- Cold (<20): 94
- Incomplete / needs enrichment: 36
- Capacity set at 25 new listing conversations → recommend working top 31 (all Hot + top 24 Warm)

**Top 5 ranked contacts (excerpt):**

| Rank | Name | Address | Score | Band | Window | Angle | First Touch | Flag |
|---|---|---|---|---|---|---|---|---|
| 1 | J. Morales | 312 Birch Ln | 94 | Hot | 0–90 d | "Two homes on Birch sold in 19 and 22 days this spring — one at $530 psf." | Phone call Tue AM | — |
| 2 | K. Patel | 49 Clover Ct | 88 | Hot | 0–90 d | "You asked about contractor referrals in January — three neighbors just relisted post-reno." | Phone call + handwritten note | — |
| 3 | A. Tran | 1104 Hollis St | 83 | Hot | 0–90 d | "Your kids age out of the Oak Ridge zone in 2027 — the feeder just had its busiest year." | Email → CMA offer | — |
| 4 | R. Ellis | 67 Mill Rd | 78 | Warm | 90–180 d | — | Email, then call if reply | `[NEEDS COMP DATA]` for angle |
| 5 | S. Chen | 228 Pine St | 76 | Warm | 90–180 d | "Recent refi signals equity unlock — median Pine St psf up 34% since 2021." | SMS (opted in) | — |

**Data gaps flagged:**
- 84 contacts missing current estimated value — recommend a batch AVM pull
- 36 contacts missing purchase year — enrich from county records before scoring
- Behavioral signals absent for 61% of CRM — connect CRM page-tracking to enable the B component

**Sensitivity flags:**
- Contact #18 has a probate signal — pulled from automated outreach, routed to agent for a personal note with no sales ask
- Contact #41 on DNC list — phone recommendation suppressed; fallback to mail

**30-day plan (capacity 25):**
- Week 1: Work top 7 Hot contacts (1 call/day + handwritten note follow-up)
- Week 2: Work top 18 Warm contacts (batch emails M/W, calls F)
- Week 3: CMA prep and delivery to responders
- Week 4: Re-rank after enrichment run
