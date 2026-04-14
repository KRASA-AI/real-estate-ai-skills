---
name: "Annual Business Plan Builder"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~4 hrs/year"
version: 1.0
last_eval_score: null
---

# 📈 Annual Business Plan Builder

## Purpose

Turn an agent's prior-year production, financial picture, personal goals, and preferred lead sources into a complete, one-page annual business plan that breaks an income target down into transaction count, lead-source quotas, weekly activities, and a personal-expense floor — and then cascades those numbers into quarterly, monthly, and weekly tracking. Produces a 1-3-5-style plan (one big goal, three priorities, five per-priority tactics) plus a scorecard the agent will actually reopen week after week rather than shelve in January.

## When to Use

Run this skill at the start of the year, at the start of a new quarter when the plan needs to be re-based after real results, after a major personal life event (marriage, new child, team move) that changes the earnings floor, when joining a new brokerage (new splits reshape the math), or whenever the agent says "I don't know what I'm supposed to be doing this week." Pairs with `30-day-social-content-calendar.md` (which populates the marketing tactics), `buyer-follow-up-sequence.md` and `seller-intent-scorer.md` (which operationalize the lead-gen activities), and `market-analysis-summary.md` (which supplies the market-pulse inputs). Re-run every quarter with updated actuals.

## Required Input

Provide the following:

1. **Prior-year actuals** — Gross closed volume, transaction count, GCI (gross commission income), average sale price, average commission rate, and lead-source split (what percent of closed deals came from each source)
2. **Personal financials** — Monthly personal living expenses (honest floor), monthly business expenses (CRM, tools, marketing, MLS, association dues, assistant), brokerage split schedule (with caps and post-cap rate), estimated tax rate, any owed debt or savings target, planned personal investments this year (new car, vacation, home purchase, retirement)
3. **Goal target** — The agent's target GCI or take-home for the coming year, plus any stretch goal. If only a volume target is supplied, work backward through average sale price and commission rate
4. **Lead-source preferences** — Which sources the agent intends to lean into (sphere of influence, past clients, open houses, online leads, geographic farm, social media, Zillow/Realtor.com premier, team leads, referrals, door-knocks, expired/FSBO, builder relationships) — with any budget allocation per source
5. **Capacity constraints** — Solo agent, team member, team lead; hours per week working; vacation weeks planned; any known leave or transitions
6. **Skills to improve** — Two or three skills the agent wants to develop this year (listing presentation, video, negotiation, farming, CRM discipline, running an ISA, recruiting)
7. **Personal goal alignment** — The 2–3 reasons the number matters (specific trip, debt payoff, savings milestone, family milestone) — keeps the plan emotionally anchored

## Instructions

You are a real estate business coach and planner. Your job is to produce a numerically honest plan — not a motivational document — that the agent can check weekly for the next 12 months.

**Before you start:**
- Load `config.yml` for brokerage split schedule, market averages, and any team-structure context
- Reference `knowledge-base/best-practices/` for local market norms (commission rate, average sale price, typical lead-source mix)
- Do not flatter the prior year. Do not flatter the goal. Work the math both ways and tell the agent if the plan is off.

**Process:**

1. **Diagnose the prior year.** Produce three honest observations: what worked (sources above their share), what didn't (sources below expectation), and where the time leaked (agents typically over-invest in one low-ROI source). Tag each observation with a number. No generic "you did great" framing — either the prior year was profitable or it wasn't.

2. **Compute the goal math from both directions.**

   **Top-down:** goal GCI → divide by average commission per transaction (avg sale price × commission rate × agent's split) → transaction count needed → transactions per month → required pipeline at each conversion stage.

   **Bottom-up:** sum the realistic annual transaction count the agent can produce from each lead source given historical conversion rates and planned activity levels → compute the GCI that produces.

   Compare the two. If top-down exceeds bottom-up by more than 20%, flag the goal as aggressive and propose either (a) a raised activity plan, (b) a raised quality plan (target higher price points), or (c) a lowered goal with a stretch target retained. Show the exact math in a 4–6 row summary table.

3. **Build the lead-source quota.** For each preferred source, specify: transactions targeted, leads needed to produce them (apply realistic conversion rates), activities required per week to generate those leads, and the budget commitment. Typical conversion anchors (flag and override if the agent has personal data):
   - SOI / past clients: 8–15% repeat/referral rate
   - Open house: 1 lead per 8 visitors; 1 closed deal per 25–40 leads
   - Online buyer leads: 1 closed deal per 40–60 leads
   - Geographic farm: 1 listing per 100 homes per year after 18 months of consistency
   - Expireds/FSBO: 1 closed listing per 80–120 contacts made
   Include a "what this actually looks like on a Tuesday" line for each source — e.g., "8 SOI calls + 2 handwritten notes every weekday" — so the plan converts into calendar time.

4. **Write the 1-3-5 summary.** One annual theme (e.g., "Double listing share in 78703"). Three priorities that roll up to the theme (e.g., "1. Own the 78703 farm. 2. Systematize listing presentation. 3. Build a CRM-driven seller pipeline."). Five tactics under each priority, each concrete and verbable. 15 tactics total. Anything that doesn't map to a tactic is NOT in the plan this year.

5. **Cascade into quarters and months.** Produce a quarterly scoreboard with target transactions, target GCI, target pipeline additions, and 1–2 capability investments per quarter (training, coach, tool). Then a monthly activity cadence: lead-gen hours, listing appointments, buyer consultations, CMAs delivered, client events, video assets produced. Monthly numbers should sum to the quarterly targets. Quarterly sums to annual. Verify arithmetic before shipping.

6. **Produce the weekly scorecard.** A single table the agent prints and posts. Columns: Day, Lead-Gen Activities, Client Work, Admin, Learning. Rows: Mon–Fri, with Saturday as a showing/open-house day and Sunday as a planning day. Fill specific numbers: "M: 15 SOI calls, 2 CMAs refreshed, 1 listing presentation prep, 1 chapter of [book]." The scorecard is the plan's only weekly artifact — the rest is reference material.

7. **Financial floor check.** Compute monthly after-tax income needed to cover personal + business expenses and contribute to the stated savings/debt goals. Translate that back into the monthly transaction count that is the FLOOR (not the target). If floor monthly transactions > half of target monthly transactions, warn the agent that the plan has no margin — any bad month is a financial problem, not a morale problem. Propose a 90-day rolling reserve target.

8. **Surface risk and accountability.** Before shipping, call out:
   - Over-concentration risk (more than 40% from a single lead source)
   - Single-point-of-failure on any tool, platform, or referral partner
   - Seasonal dip months (summer for some markets, winter for others) and how the plan absorbs them
   - Skill gap vs. the plan (a video-heavy plan from an agent who has never produced video, for instance)
   - Accountability mechanism: who the agent reports weekly numbers to — if nobody, flag and recommend a coach, team lead, or peer

9. **Deliver the one-pager.** The final output is a single printable one-page plan with: theme, three priorities, 15 tactics, annual GCI math, quarterly scoreboard, and the weekly scorecard. Everything else is appendix.

**Critical rules:**
- Math must reconcile: weekly × weeks per quarter = quarterly × 4 = annual, with explicit allowance for vacation weeks
- Do not assume conversion rates better than the agent's own prior-year data; use the lower number
- Do not produce a plan that collapses on one bad month — require a reserve line
- Personal expenses are the floor, not a footnote. Plans that don't cover them are flagged aggressively.
- Every tactic has a measurable outcome. "Do more social media" is not a tactic. "Post 3 Reels/week to Instagram and track save-rate" is.
- Do not fabricate average sale price, commission rates, or conversion anchors — use supplied values or clearly flag the anchors as market defaults

## Example Output

**Prior-year diagnosis:**
- Worked: SOI produced 9 of 14 closed deals (64%) on $3,200 in spend — clearly highest-ROI and under-invested
- Didn't work: $18,000 spent on online leads produced 2 closed deals at a $9,000 blended cost of acquisition against an average GCI per deal of $9,800 — near-break-even
- Leak: 11 hours/week on Instagram without tracking save-rate or DM conversion — unmeasured, likely overspent attention

**Goal math (top-down vs bottom-up):**
| | Value |
|---|---|
| Target GCI | $180,000 |
| Avg sale price | $540,000 |
| Avg commission rate (side) | 2.75% |
| Split after cap | 90% / 10% |
| Avg GCI per deal (post-split) | ~$13,365 |
| Transactions needed (top-down) | 13.5 → plan 14 |
| Bottom-up capacity | SOI 10 + OH 2 + Farm 1 + Referral 1 = 14 |
| Reconciled | Plan is feasible but tight — farm assumption is the softest number |

**1-3-5 (excerpt):**
- **Theme:** Become the obvious agent for Highland Park sellers in 2026
- **Priority 1:** Own the SOI — 5 tactics: 36-touch plan, quarterly client event, Q1 value-drop campaign, handwritten birthdays, past-client CMAs twice a year
- **Priority 2:** Systematize listings — 5 tactics: pre-launch audit on every listing, listing-presentation rehearsal monthly, post-close seller survey, referral ask at 30 days, listing case-study blog quarterly
- **Priority 3:** Build a seller pipeline — 5 tactics: CRM seller-intent scoring quarterly, farm mailer monthly, "just-sold" video in zip monthly, expireds outreach 5/week Tue/Thu, FSBO outreach 3/week

**Quarterly scoreboard:**
| Q | Closings | GCI | Pipeline adds | Capability investment |
|---|---|---|---|---|
| Q1 | 2 | $26.7K | 40 SOI conversations | Video coach |
| Q2 | 4 | $53.5K | 30 seller prospects | Listing-pres coach |
| Q3 | 5 | $66.8K | 25 new leads | Market-analysis training |
| Q4 | 3 | $40.1K | 30 Q1-next-year primer | Annual review prep |
| **Total** | **14** | **$187.1K** | | |

**Weekly scorecard (excerpt):**
| Day | Lead-Gen | Client Work | Admin | Learning |
|---|---|---|---|---|
| Mon | 15 SOI calls | 2 CMA refreshes | CRM hygiene 30 min | 1 chapter |
| Tue | 5 expireds + 3 FSBOs | Listing prep | Accounting 45 min | Coach call |
| Wed | 20 farm door-hangers | Showings | — | Video edit |
| Thu | 5 expireds + 3 FSBOs | Buyer consults | Transaction updates | 1 chapter |
| Fri | Content block (2 hrs) | Weekly review with spouse | Invoices | — |
| Sat | 1 open house | Showings | — | — |
| Sun | Plan next week | — | — | Financial review |

**Financial floor:**
- Personal + business monthly outflow: $9,400
- Tax allocation: 28%
- Monthly GCI floor: ~$13,100 → 1 closed deal per month is the break-even
- Target average: 1.17 deals/month (plan runs thin — recommend 90-day reserve of $28K)

**Risk flags:**
- 71% of planned GCI concentrates in Q2–Q3 — recommend rolling reserve to cover slow Q1 and Q4
- Q3 requires 5 closings while agent is planning a July family trip — move 1 closing into Q2 pipeline
- Plan depends on video production the agent has not yet built — Priority 2 requires video coach to derisk
- No accountability partner identified — recommend 30-min weekly review with team lead or peer
