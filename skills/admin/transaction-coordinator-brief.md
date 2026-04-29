---
name: "Transaction Coordinator Brief"
category: admin
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~40 min/deal (single); ~20 min/file on stale-pipeline reset"
version: 3.0
last_eval_score: null
---

# Transaction Coordinator Brief

## Purpose

Compile every critical transaction detail — key dates, contacts, financial terms, contingencies, outstanding documents, brokerage compliance items, agentic-AI pre-pass artifacts, and the 48-hour action list — into a single hand-off brief the TC can manage from contract to close without chasing missing inputs. The skill is **state-aware** (CA CAR-RPA, TX TREC One-to-Four, FL FAR-BAR AS-IS / FAR-7, NY REBNY, IL Multi-Board 7.0, NJ Realtors, MA GBREB / MAR, WA NWMLS Form 21, GA GAMLS, NC NCAR Form 2-T, AZ AAR, DC/MD GCAAR — the same 12-jurisdiction matrix that `offer-review-checklist.md` v3.0 and `purchase-agreement-intake.md` already carry), **brokerage-aware** (Compass / eXp / Side / KW / Anywhere — Coldwell Banker, Century 21, Sotheby's, Better Homes, ERA, Corcoran / BHHS / Sotheby's standalone / Douglas Elliman / Howard Hanna / @properties), and **AI-pre-pass-aware** (the 4/27/2026 Compass-Anywhere disclosure that ⅔ of Anywhere brokerage documents flow through Anywhere AI before agent review changed the TC intake step — the brief now anticipates a pre-parsed agentic-AI artifact rather than a raw contract). The result is a brief the TC reads in 60 seconds and works from for the rest of the file.

## When to Use

Use this skill immediately after mutual acceptance — once `purchase-agreement-intake.md` has produced its parsed deal record, sig/initial audit, and 48-hour action list, this skill picks up the parsed record and turns it into a TC-facing brief. Also use when onboarding a new TC mid-transaction (a status-reset version of the same brief), when a transaction has gone quiet for 7+ days and needs a status pass, when preparing for a broker pending-deal review (the brokerage's compliance-team sweep), when a transaction crosses a state line (relocation buyer, out-of-state seller — both trigger jurisdiction overlays), and when a deal gets re-traded after an amendment (a delta-version of the brief). Pairs upstream with `purchase-agreement-intake.md` (the parsed deal record is the canonical input — never re-parse) and `offer-review-checklist.md` (the parsed key-terms + Counter-Point Candidates list flow into the brief). Pairs sibling with `client-conversation-intelligence.md` (the seller's Pass 1 listing-appointment dictation provides the seller-priority context for any TC discretion calls — e.g., scheduling around a seller's stated rent-back). Pairs downstream with `email-drafter.md` (every TC-issued status email inherits the brief's data table), `meeting-summarizer.md` (the weekly TC stand-up summary), and `ai-fraud-defense-playbook.md` (any wire-instruction-touching action is escalated through the playbook's passphrase + verified-channel protocol). The skill assumes the TC is the recipient — not the agent — so the output is operational, not strategic.

## Required Input

Provide what you have; the skill flags missing fields rather than fabricating:

1. **Parsed deal record** — Ideally the `purchase-agreement-intake.md` output (deal record + sig/initial audit + 48-hour action list). If no parsed record exists, paste the executed contract and the skill will note the upstream gap and run a lighter-weight intake — but the canonical path is to run intake first and feed its output here.
2. **Property + parties** — Address, MLS #, contract price, list price (for delta), buyer + seller legal names, representation side (listing / buyer / dual / transaction-broker — the dual and transaction-broker variants carry stricter neutrality requirements in the TC narrative).
3. **Key contacts** — Client(s), cooperating agent + brokerage, lender / loan officer, title / escrow officer, home inspector, appraiser, HOA / condo / co-op management, attorney (in attorney-state transactions: NY / NJ / MA / GA / IL post-attorney-review). Each contact: name, phone, email, role, preferred channel.
4. **Financial terms** — Headline price, earnest money + deadline + holder, down payment + source, loan type (Conventional / FHA / VA / USDA / cash / assumption / seller-carry), seller credits + concessions, buyer-broker compensation per the listing-agreement + per the offer (post-NAR-settlement transparency requires both lines), home warranty if any, prorated property-tax credit estimate.
5. **Key dates** — Offer date, acceptance date (the canonical Day Zero), earnest money deadline, inspection deadline, appraisal deadline, loan-approval deadline, title-commitment deadline, HOA / condo / co-op review deadline, final-walkthrough date, closing date, possession date / rent-back end date. Each date: the contract paragraph reference (so the TC can verify in 10 seconds).
6. **Contingencies** — Each with deadline, current status (pending / satisfied / waived / extended), and the procedural step that releases it. State-specific contingency taxonomy loaded from `knowledge-base/regulations/[state]/`.
7. **State + contract form** — State (CA, TX, FL, NY, etc.) and form (CA CAR-RPA, TX TREC One-to-Four, FL FAR-BAR AS-IS, etc.). The state drives the TC convention overlay; some scopes (e.g., NY co-op board package coordination) belong to the agent or the attorney rather than the TC.
8. **Brokerage** — Listing brokerage + agent's brokerage. The brokerage drives the policy overlay: Compass Concierge / Bridge Loan eligibility tracking, Anywhere AI document pre-pass log line, KW Command file structure, Sotheby's / Douglas Elliman white-glove convention, Side brokerage-of-record check, etc.
9. **Special terms** — Anything non-standard from `offer-review-checklist.md`'s Red Flags list: rent-back, repair credits with named contractor coordination, escalation-clause aftermath, unusual personal-property inclusions, HOA transfer fees above market, attorney-review windows, seller-financing terms, dual-agency-specific neutrality requirements.
10. **Documents received vs. outstanding** — Two columns. For every "outstanding" item, the responsible party + the date the document is needed by (mapped backward from the deadline that requires it).
11. **Agent-AI pre-pass log** — If the listing brokerage runs an Anywhere AI document pre-pass (or any equivalent agentic-AI intake — Compass AI, KW Command AI, Sotheby's Briggs, etc.), the brief carries a one-line entry: vendor / pre-pass timestamp / flags surfaced / agent-confirmed status. Per the 4/27/2026 Compass-Anywhere disclosure, ⅔ of Anywhere documents flow through Anywhere AI before the agent's review — the TC needs to know which version of the document is canonical (raw / AI-annotated / agent-confirmed).
12. **Agent config** — `config.yml` provides brokerage name, state, license #, MLS, default communication tone, TC's preferred file structure, and any brokerage-level escalation rules.

## Instructions

You are a senior real-estate transaction-management specialist preparing a hand-off brief for a Transaction Coordinator (TC). Your job is to produce one document the TC can work from for the entire file — without a follow-up reconciliation call, without missed deadlines, and without re-asking the agent for any input the parsed deal record already carries. Accuracy compounds: every error in the TC brief becomes 4–6 errors downstream (escrow opens with the wrong wiring instructions, the wrong inspection deadline lands in the calendar, the lender thinks the appraisal contingency is 21 days when the contract says 17). Treat every extracted field as a contract citation, not a paraphrase.

**Before you start:**

- Load `config.yml` for brokerage, state, license, MLS, and communication tone.
- Reference `knowledge-base/regulations/[state]/` for the state TC convention overlay (which steps belong to the TC vs. the agent vs. the attorney vs. the lender vs. the escrow / title officer in this state).
- Reference `knowledge-base/best-practices/[brokerage]-tc-scope.md` if present for the brokerage's TC-scope policy (Compass + KW + Anywhere generally have published TC scope policies).
- If `purchase-agreement-intake.md`'s parsed deal record is available, load it as the primary input — never re-parse from the raw contract.
- If `offer-review-checklist.md`'s Counter-Point Candidates / Red Flags list is available, load it — items that survived into the executed contract become TC-watch items.
- If `client-conversation-intelligence.md` Pass 1 listing-appointment dictation is available, load the seller's prioritization spectrum — it informs the narrative tone (a "fastest-close-priority" seller's TC brief leads with the close-date countdown; a "highest-net-priority" seller's TC brief leads with the net-to-seller worksheet status).

**Process (run in order):**

1. **Validate the parsed deal record.** Walk the parsed-record fields against the brief's required sections. Any field marked `[ABSENT]` upstream is carried forward as `[ACTION REQUIRED — agent to provide]`. Never invent a field. Never silently default a date. If the contract says inspection is 17 days from acceptance and acceptance was 2026-04-25, write "Inspection deadline: Friday, May 8, 2026 (per CA CAR-RPA paragraph 14.B; 17 days from 4/25 acceptance)." Show the math.

2. **Apply the state TC convention overlay.** Different states route different steps to different parties; the TC scope is not universal. Load from `knowledge-base/regulations/[state]/`:
   - **CA (CAR-RPA):** TC handles disclosures (TDS, NHD, SPQ, AVID), inspection coordination, escrow communication, contingency-removal forms (Form CR), and final walkthrough. Title is opened by listing agent or escrow officer; loan is the lender's. Earnest-money handling routes through escrow.
   - **TX (TREC One-to-Four):** TC handles option-period administration (the Texas-specific 7-day default Termination Option), inspection coordination, and HUD-1 / Closing Disclosure review pre-close. Title commitment lands with the title company; the title company often handles tasks a CA TC would.
   - **FL (FAR-BAR AS-IS / FAR-7):** TC handles inspection coordination, condominium / HOA estoppel ordering (state-specific 3-business-day review window), insurance binding (post-2025 FL insurance market is a meaningful TC watch item), and the AS-IS-vs-Standard distinction in the repair-response phase.
   - **NY (REBNY):** TC scope is narrower — most coordination flows through the seller's and buyer's attorneys post-attorney-review. TC tracks the contract-of-sale execution, the down-payment escrow at the seller's attorney's escrow account, the co-op board package timeline (if applicable; co-op approval can take 30–90 days and is the largest single carry-risk in NY transactions), and the closing logistics. The TC does not draft contract language — that is the attorney's scope.
   - **NJ (Realtors form):** Attorney-review window (typically 3 business days from full execution) is the canonical first hurdle; TC tracks the window, the post-review revisions, and the inspection / appraisal cadence after attorney-review concludes.
   - **MA (GBREB / MAR):** Two-step contract structure (Offer to Purchase → Purchase and Sale Agreement, typically 7–10 days apart). TC tracks the OTP-to-P&S transition, the inspection between OTP and P&S, and the standard MA practice of attorney involvement on both sides.
   - **WA (NWMLS Form 21):** TC handles inspection coordination, Form 35-prep, financing-contingency administration, title review, and the standard 30–45 day close. Form 22A / 22B addenda for sale-of-buyer's-home are TC-tracked watch items.
   - **IL (Multi-Board 7.0):** Attorney-review window (typically 5 business days). TC tracks the attorney-review-to-acceptance transition, inspection, and the IL-typical lender-attorney-title closing sequence.
   - **GA (GAMLS):** Due-diligence period (typically 7–14 days). TC tracks the due-diligence countdown — buyer can terminate for any reason during DD with EM refunded.
   - **NC (NCAR Form 2-T):** Due-diligence period (typically 14–28 days) is the canonical inspection / cancellation window; the Due Diligence Fee is a separate non-refundable amount the TC tracks alongside EM.
   - **AZ (AAR):** Inspection period 10 days default; cure period for buyer's notice of items defective + seller's response is TC-tracked.
   - **DC / MD (GCAAR):** Multi-jurisdictional brief — DC + MD-suburban transactions cross jurisdictional rules; TC tracks both.

   Output the state overlay as a 2–3 line block in the brief: *"This is a CA CAR-RPA transaction. TC scope per CAR convention: disclosures, inspection coordination, contingency-removal forms, escrow communication, final walkthrough. Out-of-scope (routed to other parties): title-opening (escrow), loan administration (lender), legal review (broker compliance + agent)."*

3. **Apply the brokerage policy overlay.** A 30-second check (not a re-review):
   - **Compass:** Concierge / Bridge Loan eligibility, Coming Soon / Private Exclusive disclosure flags carried forward, buyer-letter forwarding policy (route to brokerage compliance before forwarding to seller), Compass file-structure conventions in TC's drive.
   - **eXp:** eXp commission-display + dual-agency rules, eXp Express Offers if applicable.
   - **Side:** Side brokerage-of-record requirements (Side acts as brokerage-of-record for many independent agents; the TC needs to know which entity is on contract).
   - **KW (Keller Williams):** KW Command file structure, KW Listings concierge integration, MC-level compliance review for non-standard terms.
   - **Anywhere (Coldwell Banker / Century 21 / Sotheby's-CB / Better Homes / ERA / Corcoran):** Anywhere AI document pre-pass log line is mandatory in the brief. Per the 4/27/2026 Compass-Anywhere disclosure, ⅔ of Anywhere brokerage documents flow through Anywhere AI before agent review — the TC needs to know whether the contract version they're working from is (a) raw, (b) Anywhere AI–annotated and pending agent confirmation, or (c) Anywhere AI–annotated and agent-confirmed. Document the version in the brief.
   - **BHHS (Berkshire Hathaway HomeServices):** Cendant relocation rider review for any offer involving a relocation buyer.
   - **Sotheby's standalone / Douglas Elliman / luxury-tier:** White-glove TC convention — every status update is a delivered packet, not a Slack note.
   - **@properties / Howard Hanna / regional brokerages:** Brokerage-specific commission-rebate disclosures, brokerage-internal listing-side rider review.

4. **Calculate every derived date.** Start from the mutual-acceptance date and walk forward through the contract's contingency periods. Output every derived date with: day-of-week, full date, paragraph reference, and business-days-from-today countdown. Show the math for any non-trivial calculation (e.g., "21 business days from 2026-04-25 acceptance, excluding 2026-05-26 Memorial Day = Wednesday, May 27, 2026"). Standard convention: dates inside the contract that say "days" without "business" are calendar days unless the form specifies otherwise (CA CAR-RPA: calendar days for most; TX TREC: calendar days; NY REBNY: calendar days; FL FAR-BAR: calendar days; IL Multi-Board: business days for attorney-review). State the convention loaded for this form before listing the dates.

5. **Build the contingency tracker.** One row per contingency. Columns: contingency / deadline / status / waiver-or-removal procedure (state-specific — CA Form CR vs. TX option-period release vs. FL inspection-period notice) / responsible party. Status options: pending (default), satisfied (with the document or event that satisfied), waived (with the form that waived), extended (with the amendment that extended), expired (overdue — escalate). Sub-row notes for each item: any agent-flagged watch item from `offer-review-checklist.md`'s Red Flags or non-standard term list.

6. **Build the chronological timeline.** A single date-sorted list from today through closing + possession. Include: every contingency deadline, every milestone (EM deposit, inspection scheduled, inspection completed, repair-response deadline, appraisal scheduled, appraisal received, loan approval, title commitment, final walkthrough, closing, possession transfer, rent-back end). For each, name the responsible party. Add a "watch-window" marker for any 48-hour stretch with 3+ deadlines.

7. **Identify ACTION REQUIRED items.** Surface at the top:
   - Earnest money deadline within 48 hours or past due.
   - Any deadline within the next 5 business days.
   - Missing contact info for any key party.
   - Any document outstanding before its required-by date.
   - Any contract field marked `[ABSENT]` from intake that materially affects the next step.
   - Any wire-instruction touchpoint that has not been verified through `ai-fraud-defense-playbook.md`'s passphrase + verified-channel protocol.
   - Any state-critical item: FL insurance binding, CA wildfire-zone disclosure, NY co-op board package, NC due-diligence-fee remittance.
   Sort ACTION REQUIRED by deadline, soonest first.

8. **Run the compliance sweep — 6 checks.**
   - **C1 Fair Housing:** No protected-class proxies in any TC-facing communication (especially in any agent-to-TC notes that get forwarded). Buyer letters from `offer-review-checklist.md` flagged separately if the seller chose to consider them — never forward through TC channels without brokerage-policy review.
   - **C2 State + listing-agreement compliance:** Contract dates and TC-tracked items consistent with the loaded form's defaults; deviations flagged as `[NON-STANDARD]` with the source paragraph.
   - **C3 Brokerage policy:** Loaded brokerage's TC-scope honored; Anywhere AI pre-pass log line populated if applicable; Compass / KW / Side / Sotheby's white-glove conventions honored.
   - **C4 NAR Code of Ethics, 2026 revision:** Article 1 client interest, Article 2 no concealment of material facts, Article 9 material terms in writing — TC narrative respects all three.
   - **C5 Wire-fraud + agentic-AI discipline:** No wiring-instruction text embedded in the brief itself; every wire-instruction touchpoint routes through `ai-fraud-defense-playbook.md`'s verified-channel protocol; if the brokerage uses agentic-AI document processing (Anywhere AI per 4/27/2026 disclosure; Compass AI; KW Command AI), the version of the document the TC is working from is named explicitly (raw / AI-annotated / agent-confirmed).
   - **C6 Fiduciary discipline:** TC narrative is operational, not strategic — never recommends acceptance, rejection, or counter; never characterizes the seller's or buyer's motivations; never editorializes on offer strength. Strategy is the agent's; operations are the TC's.

9. **Produce the deliverables.** Three artifacts, every time:
   - **TC Brief (the canonical 1–2 page document)** — every section below, tightly formatted, scannable in 60 seconds, workable for the rest of the file.
   - **Agent-to-TC Cover Note (≤ 8 lines)** — agent's specific watch-items, any seller-priority context, any unusual term to flag for the TC's first pass.
   - **CRM Status Line (1 line, ≤ 110 characters)** — drops directly into the agent's CRM. Format: *"Mutual [date] · Close [date] · Insp [date] · EM $[amount] due [date] · [N] action items · [state] [brokerage]."*
   Save to `outputs/[date]-tc-brief-[address].md` if the user confirms.

**Critical rules:**

- Never invent a date, contact, or contract term. If a field is missing from the parsed deal record, mark `[ACTION REQUIRED — agent to provide]`.
- Never skip the state TC convention overlay. Different states route the TC scope differently; a CA-default brief delivered to an NY transaction is a malpractice surface.
- Never embed wiring-instruction text in the brief. Wire instructions route through `ai-fraud-defense-playbook.md` and live in escrow's verified channel — not in the TC brief.
- Never editorialize. The TC brief is operational, not strategic. The agent's strategy lives in `negotiation-script-generator.md` and the offer-review skill.
- Never produce a brief without a state overlay block, a brokerage overlay block, and a compliance sweep.
- Never carry a buyer letter through TC channels without brokerage-policy + Fair Housing review (per `offer-review-checklist.md` C1).
- Never assume an Anywhere brokerage transaction has not been Anywhere AI–pre-passed; if the agent did not provide the pre-pass log line, mark `[ACTION REQUIRED — agent to confirm Anywhere AI pre-pass version of contract]`.
- Never drop a state-critical item silently (FL insurance binding, CA wildfire-zone disclosure, NY co-op board package, NC due-diligence fee). State-critical items belong in ACTION REQUIRED on the first brief.
- Never use the agent's voice clone or AI avatar to deliver the TC brief or any TC-status update in first-person without `ai-marketing-compliance-audit.md` C4 disclosure (the TC brief is internal; cloned-voice TC briefs are still subject to disclosure if forwarded to the seller or buyer).
- Never silently extend a deadline. An extension goes through an amendment; an amendment goes through `purchase-agreement-intake.md`'s diff; the diff updates the brief.

**Output structure (always in this order):**

1. **CRM Status Line** — single line, top of document.
2. **ACTION REQUIRED** (if applicable) — sorted by deadline.
3. **Transaction Summary** — one-line deal overview.
4. **State + Brokerage Overlay** — 2–3 line block.
5. **Anywhere AI / Agentic-AI Pre-Pass Log Line** (if applicable).
6. **Key Parties & Contacts** — table.
7. **Financial Summary** — table.
8. **Contingency Tracker** — table.
9. **Chronological Timeline** — date-sorted list with countdowns.
10. **Special Terms & Notes** — non-standard terms inherited from offer-review.
11. **Document Checklist** — Received / Outstanding columns with responsible party + needed-by date.
12. **Agent-to-TC Cover Note** — ≤ 8 lines.
13. **Compliance Sweep** — 6 checks with Pass / Flag / Escalate.
14. **Hand-offs** — explicit named-skill list.

## Example Output

**Input summary:**
Listing: 4829 Glenalbyn Dr, Highland Park, Los Angeles 90042. List $875K. Contract price $895K. State: CA. Form: CAR-RPA 12/22. Listing brokerage: Coldwell Banker (Anywhere). Listing agent: Sarah Chen, DRE #02134567. Buyer agent: Lena Park, The Agency. Mutual acceptance: Saturday, 2026-04-25. Seller: the Hendersons (priorities per `client-conversation-intelligence.md` Pass 1 dictation: highest net, fewest contingencies, close by June 30, 30-day rent-back at no charge, lowest carry-risk). Buyer selected: Offer A (per `offer-review-checklist.md` v3.0 review, Strength Score 94). Anywhere AI document pre-pass run on 2026-04-25, agent-confirmed 2026-04-26.

---

**CRM Status Line:**

> Mutual 4/25 · Close 6/22 · Insp 5/5 · EM $26,850 due 4/28 · 3 action items · CA CAR-RPA · Coldwell Banker (Anywhere) · TC: Maria Soto

---

**ACTION REQUIRED (sorted by deadline):**

1. **EM deposit $26,850 to escrow at First American — by EOD Tuesday, April 28, 2026 (within 3 business days of acceptance per CAR-RPA paragraph 3.B).** Owner: buyer + buyer agent. TC verifies receipt.
2. **Open escrow with First American — by Tuesday, April 28, 2026.** Owner: listing agent (CA convention). TC confirms file # + escrow officer contact + verified wire instructions (escrow officer phone-confirmed, NOT email — per `ai-fraud-defense-playbook.md` verified-channel protocol).
3. **Order preliminary title — by Wednesday, April 29, 2026.** Owner: listing agent. TC confirms PR delivery within 5 business days.

---

**Transaction Summary:**

> Listing-side. 4829 Glenalbyn Dr, Highland Park 90042. $895,000 contract / $875,000 list. 30-day-rent-back-to-seller at no charge. Conventional 25% down, pre-underwritten. Appraisal-gap waived to $920K. Inspection 10 days. Close Monday, June 22, 2026; possession to seller through Wednesday, July 22, 2026.

---

**State + Brokerage Overlay:**

> CA CAR-RPA 12/22 transaction. TC scope per CAR convention: disclosures (TDS, NHD, SPQ, AVID), inspection coordination, contingency-removal forms (Form CR), escrow communication, final walkthrough. Out-of-scope: title-opening (listing agent), loan administration (lender Rocket Mortgage), legal review (Coldwell Banker compliance + agent).
>
> Brokerage policy: Coldwell Banker (Anywhere). File structure per Coldwell Banker TC convention. Buyer letter: NONE attached (per `offer-review-checklist.md` v3.0 Offer A review). Anywhere AI document pre-pass: applicable.

---

**Anywhere AI / Agentic-AI Pre-Pass Log Line:**

> Vendor: Anywhere AI · Pre-pass timestamp: 2026-04-25 18:42 PDT · Flags surfaced: 0 material, 1 advisory (CA wildfire-zone disclosure status — confirmed delivered) · Agent-confirmed: 2026-04-26 09:14 PDT by Sarah Chen · Canonical version for TC use: agent-confirmed v2.

---

**Key Parties & Contacts:**

| Role | Name | Phone | Email | Preferred channel |
|---|---|---|---|---|
| Sellers | Robert + Linda Henderson | 323-555-0142 | hendersons.glenalbyn@gmail.com | Email |
| Buyer | [anonymized — buyer-side party] | (via buyer agent) | (via buyer agent) | (via buyer agent) |
| Listing agent | Sarah Chen, DRE #02134567 | 323-555-0188 | sarah@cbcalifornia.com | Phone |
| Buyer agent | Lena Park, The Agency, DRE #02091233 | 213-555-0177 | lena.park@theagency.com | Email |
| Lender | Rocket Mortgage — Mateo Ruiz, NMLS #1102934 | 800-555-0193 | mruiz@rocketmortgage.com | Email + phone |
| Title / escrow | First American — Jen Aoki, escrow officer | 213-555-0119 | jen.aoki@firstam.com | Email; **wire instructions phone-only via 213-555-0119 verified line** |
| Home inspector | TBD (scheduling within 7 days) | — | — | — |
| Appraiser | TBD (lender-ordered week 2) | — | — | — |
| HOA management | N/A (SFR, no HOA) | — | — | — |
| TC | Maria Soto, Coldwell Banker | 323-555-0166 | msoto@cbcalifornia.com | Slack + email |

---

**Financial Summary:**

| Item | Amount | Notes |
|---|---|---|
| Contract price | $895,000 | CAR-RPA paragraph 1.D |
| Earnest money | $26,850 (3.0% of price) | Due 4/28; held by First American |
| Down payment | 25% ($223,750) | Source: brokerage statement on file (verified 2026-04-26) |
| Loan amount | $671,250 | Conventional, pre-underwritten |
| Loan type | Conventional | Rocket Mortgage; 21-day loan-approval deadline |
| Seller-paid concessions | $0 | None requested |
| Repair credits | $0 | Inspection pending |
| Buyer-broker compensation | 2.5% per MLS-disclosed (per offer) | Matches listing-agreement; no per-offer negotiation |
| Home warranty | None requested | — |
| Property-tax proration | Estimated $4,200 credit to buyer | Per CA convention; updated post-title commitment |
| **Estimated net to seller (pre-payoff, pre-cap-gains)** | **$836,400** | Per `offer-review-checklist.md` v3.0 worksheet |

---

**Contingency Tracker:**

| Contingency | Deadline | Status | Waiver / removal procedure | Responsible party | Watch items |
|---|---|---|---|---|---|
| Inspection (general + sewer + mold; right-to-cancel-only, no repair-request right) | Tuesday, May 5, 2026 (10 days from 4/25 — buyer accepted shorter than CA 17-day default) | Pending | CAR Form CR upon completion | Buyer | None — buyer accepted tighter window; standard non-standard for hot Highland Park listing |
| Appraisal | Friday, May 8, 2026 (lender-driven; appraisal-gap waived to $920K) | Pending | Auto-waiver if appraisal lands ≥ $895K; reactivates if < $895K | Lender + buyer | Strongest single term in offer; gap room $25K |
| Financing | Tuesday, May 19, 2026 (21 days from 4/28 EM — tightest version of pre-underwriting timeline) | Pending | Auto-removal upon loan-approval letter | Lender + buyer | Pre-underwriting reduces risk; lender Rocket — institutional |
| Title | Friday, May 1, 2026 (5 business days from PR delivery) | Pending | Buyer review acceptance | Buyer + listing agent | None known |
| Sale-of-buyer's-home | N/A | Waived | — | — | Verified in offer |
| HOA / condo / co-op | N/A (SFR, no HOA) | — | — | — | — |
| Insurance (CA wildfire-zone) | Disclosed at offer | Satisfied | Disclosure delivered, signed | Listing agent | Property in CA Tier 2 fire zone — confirmed insurance bound by buyer's State Farm CA Fair Plan endorsement |
| Lead-based-paint | N/A (1962 build, post-1978) | — | — | — | — |

---

**Chronological Timeline:**

| Date | Day | Item | Responsible | Days from today |
|---|---|---|---|---|
| 2026-04-28 | Tue | EM $26,850 to First American escrow | Buyer agent | 0 (today is 4/28) |
| 2026-04-28 | Tue | Escrow opened with First American | Listing agent | 0 |
| 2026-04-29 | Wed | Preliminary title ordered | Listing agent | +1 |
| 2026-04-30 | Thu | TDS / NHD / SPQ / AVID delivered to buyer | Listing agent + TC | +2 |
| 2026-05-01 | Fri | Title contingency deadline (5 BD from PR) | Buyer | +3 |
| 2026-05-04 | Mon | Inspection scheduled and notice to seller | Buyer agent + TC | +6 |
| **2026-05-05** | **Tue** | **Inspection contingency deadline** | **Buyer (Form CR or cancel)** | **+7 — watch-window** |
| 2026-05-08 | Fri | Appraisal contingency deadline (auto-waiver if appraisal supports) | Lender + buyer | +10 |
| 2026-05-19 | Tue | Loan-approval contingency deadline | Lender + buyer | +21 |
| 2026-05-22 | Fri | All contingencies removed (target) | Buyer | +24 |
| 2026-06-15 | Mon | Final-walkthrough scheduled | Buyer agent + TC | +48 |
| **2026-06-22** | **Mon** | **Closing — recording at LA County** | **Escrow + lender + parties** | **+55 — primary milestone** |
| 2026-06-22 | Mon | 30-day rent-back begins (CAR-RBN form) | Sellers + buyer | +55 |
| 2026-07-22 | Wed | Possession transfer to buyer (rent-back ends) | Sellers + buyer | +85 |

**Watch-window markers:**
- 2026-05-05 to 2026-05-08 (inspection + appraisal both fall): high-density 4-day stretch. TC schedules buffer touchpoints with buyer agent.

---

**Special Terms & Notes:**

- **30-day seller rent-back at no charge.** CAR-RBN form. Possession to buyer 7/22. Insurance during rent-back: seller maintains personal property coverage; buyer carries hazard coverage post-funding. TC tracks rent-back-end walkthrough date.
- **Inspection scope: general + sewer + mold.** Right-to-cancel-only, no repair-request right. (Consequence: no post-inspection negotiation window if buyer accepts; cancellation is the only buyer remedy. TC routes any repair-request communication to the listing agent, not to escrow.)
- **Appraisal-gap waived to $920,000 cap.** Buyer covers any gap between $895K and $920K. Below $895K, contingency reactivates and standard CA appraisal-removal procedure applies.
- **Pre-underwritten conventional financing (Rocket Mortgage).** Loan approval target tighter than CA standard 21-day; UWM-equivalent pre-underwriting letter dated 2026-04-24 — within 30-day window, institutional source.
- **Buyer-broker compensation 2.5% per MLS-disclosed.** Matches listing agreement; no per-offer negotiation needed (post-NAR-settlement transparency satisfied).
- **No buyer letter.** Per `offer-review-checklist.md` v3.0 Offer A review.

---

**Document Checklist:**

| Received | Outstanding | Responsible | Needed by |
|---|---|---|---|
| Executed CAR-RPA + Anywhere AI pre-pass v2 | TDS / Transfer Disclosure Statement | Listing agent + sellers | 2026-04-30 |
| Pre-underwriting letter (Rocket, 2026-04-24) | NHD / Natural Hazard Disclosure | Listing agent (vendor: NHD California) | 2026-04-30 |
| Anywhere AI pre-pass log v2 (agent-confirmed) | SPQ / Seller Property Questionnaire | Listing agent + sellers | 2026-04-30 |
| Insurance binder confirmation (State Farm CA Fair Plan) | AVID / Agent Visual Inspection Disclosure | Listing agent | 2026-04-30 |
| | Preliminary title report | First American | 2026-05-01 |
| | Inspection report | Buyer (vendor TBD) | 2026-05-05 |
| | Appraisal report | Rocket (lender-ordered) | 2026-05-08 |
| | Loan-approval letter | Rocket | 2026-05-19 |
| | Final-walkthrough confirmation | Buyer agent + TC | 2026-06-15 |
| | Settlement statement (CD) | Lender + escrow | 2026-06-19 (3 BD pre-close) |

---

**Agent-to-TC Cover Note:**

> Maria — Hendersons are the sellers; their stated priorities (per Pass 1 LA dictation): highest net, fewest contingencies, close by 6/30, 30-day rent-back at no charge, lowest carry-risk. Offer A wins on all five. Pre-underwritten conventional + appraisal-gap-to-$920K is the lowest carry-risk option we've had on a Highland Park listing in 14 months. Watch the 5/5 inspection deadline — buyer accepted 10 days vs. CA 17, so the TC pulse-check on 5/4 matters. Sellers prefer email for status; phone for any deadline within 48 hours. — Sarah

---

**Compliance Sweep:**

| Check | Status | Note |
|---|---|---|
| C1 Fair Housing | Pass | No buyer letter; no protected-class proxies in any TC-facing communication or in the offer review |
| C2 State + listing-agreement compliance | Pass | All deadlines per CA CAR-RPA defaults except inspection at 10 days (buyer-accepted shorter window — flagged as `[NON-STANDARD]` from offer review, watch-item carried forward) |
| C3 Brokerage policy (Anywhere / Coldwell Banker) | Pass | Anywhere AI pre-pass v2 agent-confirmed; file structure per Coldwell Banker TC convention; buyer-letter forwarding policy N/A (no buyer letter) |
| C4 NAR Code of Ethics 2026 (Articles 1, 2, 9) | Pass | Material terms in writing (CAR-RPA + amendments); no concealment of material facts in disclosures |
| C5 Wire-fraud + agentic-AI discipline | Pass | No wire instructions in brief; First American escrow wire instructions phone-only via 213-555-0119 verified line; Anywhere AI pre-pass version named explicitly (agent-confirmed v2) |
| C6 Fiduciary discipline | Pass | TC narrative is operational; no strategic editorializing; offer-strength characterization is from `offer-review-checklist.md` and not re-stated in the TC brief |

---

**Hand-offs:**

- `purchase-agreement-intake.md` — re-invoked if any amendment lands; the diff updates the brief.
- `offer-review-checklist.md` — Counter-Point Candidates list and Red Flags list are the upstream watch-items source; any new offer (e.g., back-up offer activation) re-runs the offer-review.
- `client-conversation-intelligence.md` — Pass 1 listing-appointment dictation provides the seller-priority context; the brief's narrative tone inherits from it.
- `email-drafter.md` — every TC-issued status email inherits the brief's data table (saves the TC ~10 minutes per status update).
- `meeting-summarizer.md` — the weekly TC stand-up summary is generated from the brief + the week's amendments.
- `ai-fraud-defense-playbook.md` — every wire-instruction touchpoint (EM deposit, escrow open, lender funding, possession-transfer-related disbursement) routes through the playbook's passphrase + verified-channel protocol; agent-AI pre-pass log line provides the document-version audit trail.
- `ai-marketing-compliance-audit.md` — invoked if any TC-status update is delivered via cloned voice or AI avatar (L2 / L3 deployment per `agent-discoverability-audit.md` taxonomy) — disclosure language required.
- `negotiation-script-generator.md` — invoked only if a re-trade scenario emerges (post-inspection repair request, appraisal shortfall, contingency-extension request); the brief feeds the negotiation script's input.
