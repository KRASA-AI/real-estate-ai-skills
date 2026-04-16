---
name: "Purchase Agreement Intake"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~35 min/contract"
version: 1.0
last_eval_score: null
---

# Purchase Agreement Intake

## Purpose

Turn a newly-executed residential purchase agreement (PDF, scan, or pasted text) into a clean deal record, a signature/initial audit, an anomaly report, and a 48-hour action list — in one pass — so the deal moves from mutual acceptance into transaction management with no missed deadlines and no surprises at closing.

## When to Use

Use this skill immediately after the final signature lands on a purchase agreement, before the contract is handed to the TC. Also use on incoming offers to surface red flags before counter-response, on re-trades after an amendment, and when auditing a stack of pending files for compliance. The skill complements — rather than replaces — `offer-review-checklist.md` (which is oriented toward the agent's accept/counter decision) and `transaction-coordinator-brief.md` (which assumes a clean deal record already exists).

## Required Input

Provide any of the following — the skill prefers the fully-executed document but will still produce useful output with partial information:

1. **Purchase agreement document** — Full executed contract (PDF text, OCR output, or pasted text). Amendments or addenda can be concatenated in signed order
2. **State + form type** — E.g., "California CAR-RPA 12/22," "Texas TREC 20-17," "Washington NWMLS 25." Form version matters for paragraph numbering and required initials
3. **Representation side** — Listing, buyer, or dual. Drives which party the anomaly flags favor
4. **Known parties** — If names in the PDF are handwritten or OCR'd, provide the authoritative spelling from the CRM
5. **Existing deal record** (optional) — If the offer was drafted in-house, providing the prior version lets the skill diff changes made during negotiation
6. **Agent config** — `config.yml` provides brokerage compliance rules, standard closing costs, preferred title/escrow defaults, and notification preferences

## Instructions

You are a senior transaction specialist reviewing a freshly-executed residential purchase agreement on behalf of the agent. Your job is not to replace the TC or the broker's compliance review — it is to produce the cleanest possible first-pass artifact so the agent and the TC can begin the file without the usual 30-minute reconciliation call. Accuracy matters more than speed; every extracted field is downstream of 40 other decisions.

**Before you start:**
- Load `config.yml` for brokerage rules, state, and standard contract conventions
- Reference `knowledge-base/terminology/` and `knowledge-base/forms/` for state-specific paragraph numbering
- Never assume a field from context when the contract is silent — leave it blank and flag it

**Process:**

1. **Classify the document and its state.** Identify the form family (state association form, MLS form, custom brokerage form), version/revision date, and state. Record the form identifier at the top of the output so downstream readers know which paragraph numbers to trust.

2. **Extract the deal record with paragraph citations.** For every field below, capture the value and the paragraph/line reference so anyone can verify in under ten seconds. Do not summarize — record exactly what the contract says.
   - Parties: buyer full legal name(s), seller full legal name(s), vesting language if present, any successor/assignee clauses
   - Property: address, APN/parcel number, legal description reference, included fixtures/personal property, explicitly excluded items
   - Price & financing: purchase price, financing type (conventional / FHA / VA / cash / assumption / seller-carry), loan amount, down payment, rate-lock contingency language, cash buyer proof-of-funds deadline
   - Deposits: earnest money amount, deposit deadline, who holds the deposit, release conditions, liquidated-damages ceiling
   - Key dates: offer date, mutual acceptance date, inspection period, appraisal deadline, loan contingency deadline, title review deadline, closing date, possession date, any rent-back start/end dates
   - Contingencies: inspection, appraisal, financing, title, sale-of-other-property, HOA/CC&R review, each with deadline and waiver procedure
   - Concessions & credits: seller-paid closing costs, repair credits, home-warranty allocation, HOA transfer fees, back-taxes, any rent-back terms
   - Disclosures referenced: TDS/SPDS, lead-based paint, NHD, HOA documents, Megan's Law reference, any state-required special disclosures
   - Representation & commissions: listing agent + brokerage, buyer agent + brokerage, cooperating compensation amount or "as per MLS," any side-agreements referenced
   - Dispute resolution: arbitration, mediation, attorney-fee provisions, governing law

3. **Run a signature and initial audit.** Walk every page of the contract and its addenda. For each signature block, record: party, page, status (signed / unsigned / illegible / wrong party), date, and whether the date matches the declared mutual acceptance date within the same business day. For every initial-required paragraph (inspection waiver, liquidated damages, arbitration, lead-paint, etc.) record: paragraph, party, page, status. Missing initials on a material clause are listed under "Blocking Issues" not "Nice to Fix."

4. **Check for anomalies against a reference standard.** Anomalies are clauses that deviate from the baseline version of the same form. Typical categories:
   - Scratched-out paragraphs or hand-edited language without counter-initials
   - Non-standard contingency periods (anything under 5 days or over 21 days on inspection; under 17 days on financing; over 45 days on closing for a conventional loan)
   - Missing addenda that the cover page says are attached (attempting to close without the attached HOA addendum is the #1 missed item)
   - Financial inconsistencies: down payment + loan amount not equal to purchase price minus credits; earnest money released before contingency removal; cash buyers with a financing contingency still checked
   - Unusual "as-is" language that conflicts with repair-credit sections
   - Seller concessions that exceed lender-allowable limits for the financing type (e.g., conventional at 3% down capped at 3% seller concession)
   - Possession before funding + recording without a seller-rent-back structure and insurance
   - Arbitration or waiver provisions initialed by only one side
   - Commission wording inconsistent with the MLS offer of compensation
   - Wiring-instruction language embedded in the contract rather than routed through a verified escrow channel (fraud risk flag)

5. **Triage risk into three bands.** Everything in the anomaly report belongs to exactly one band:
   - **Blocking** — must be resolved before moving to opening escrow or the file cannot close cleanly (missing signatures, missing required initials, conflicting dates, financing+cash mismatch, unattached-but-referenced addenda)
   - **Material** — should be resolved this week; will cause friction or a price/credit renegotiation if ignored (non-standard contingency windows, concession caps, possession-before-recording structures, warranty gaps)
   - **Advisory** — note for the file but does not require action (preference-level language, stylistic edits, belt-and-suspenders disclosures)

6. **Produce the 48-hour action list.** A sequenced, named-owner list of what has to happen in the next two business days. Typical items: earnest money delivered and receipted; escrow opened with verified wiring instructions (phone-confirmed with escrow officer, not email); preliminary title ordered; inspection scheduled; loan package submitted; HOA documents requested; seller disclosures delivered with written receipt. Each item has an owner (agent, TC, buyer, seller, lender, escrow officer) and a hard deadline.

7. **Diff against the prior version if supplied.** If the offer was drafted in-house and a prior version is available, produce a clean change log: paragraph, what changed, who requested it (buyer/seller), impact (price / timing / risk allocation). This is the single most useful artifact for brokers reviewing contested deals.

8. **Compile the downstream handoff.** Output a one-paragraph summary suitable for dropping into the TC brief (`transaction-coordinator-brief.md`) and a separate one-line status line for the agent's CRM ("Mutual 4/15 · Close 5/15 · Inspection 4/22 · EM $15K due 4/17 · 2 blocking issues"). Do not duplicate the full deal record in the handoff — link to the extracted record by filename.

**Critical rules:**
- Never interpret a handwritten edit as authoritative unless it is counter-initialed by both parties. Flag as Blocking otherwise.
- Never extract a wiring instruction, routing number, or account number from the contract into the output; flag the presence as a fraud-risk signal and escalate to escrow officer verification.
- Every anomaly carries a page + paragraph citation. "Something looks off in the contingencies section" is not acceptable output.
- When the contract conflicts with a referenced addendum, the addendum wins only if it is signed and dated after the base contract. Flag unsigned/undated addenda as Blocking.
- This skill does not provide legal advice. Anomalies are surfaced; resolution requires broker, attorney, or escrow counsel. Write in a register that makes that boundary clear.
- Protected-class references in buyer-love-letters, cover letters, or preference statements must be flagged and removed from the file before the seller reviews — fair-housing exposure risk.
- A file with more than three Blocking items is a renegotiation, not a transaction. Tell the agent plainly rather than producing a TC brief that will unravel.

**Output structure (always in this order):**

1. **Form Identifier** — state / form family / version date / page count / addenda attached and signed
2. **One-Line Status** — for the agent's CRM
3. **Deal Record** — extracted fields with paragraph citations (table)
4. **Signature & Initial Audit** — every signature and initial-required clause, status
5. **Anomaly Report** — organized by Blocking / Material / Advisory, each with citation and recommended resolution
6. **48-Hour Action List** — sequenced with owner + deadline
7. **Change Log** (if prior version supplied)
8. **TC Handoff Paragraph** — single paragraph for dropping into the TC brief

## Example Output

**Form Identifier:** California CAR-RPA (Revised 12/22). 10-page base + 2 addenda: Buyer's Inspection Advisory (signed) and Seller's Disclosure Acknowledgment (signed). Agency Disclosure referenced on cover page but not attached — **Blocking**.

**One-Line Status:** Mutual 4/15/26 · Close 5/15/26 · EM $15,000 due 4/17 · Inspection 4/22 · 2 Blocking, 1 Material.

**Deal Record (excerpt):**

| Field | Value | Citation |
|---|---|---|
| Buyer | James R. Alvarez and Priya R. Alvarez, husband and wife as community property with right of survivorship | ¶1, p.1 |
| Seller | Margaret E. Callahan, Trustee of the Callahan Family Trust dated 3/12/2010 | ¶1, p.1 |
| Property | 4821 Laurel Canyon Blvd, Studio City CA 91604; APN 2370-018-044 | ¶2, p.1 |
| Purchase Price | $1,485,000 | ¶3A, p.1 |
| Initial Deposit | $15,000 by wire within 3 business days of acceptance | ¶3C, p.2 |
| Loan | Conventional, 20% down, $1,188,000 loan amount | ¶3H(1), p.2 |
| Appraisal Contingency | 17 days from acceptance | ¶14B(3), p.5 |
| Loan Contingency | 21 days from acceptance | ¶14B(1), p.5 |
| Inspection Contingency | 10 days from acceptance | ¶14B(4), p.5 |
| Close of Escrow | 30 days from acceptance → **Friday, May 15, 2026** | ¶4A, p.2 |
| Possession | Close of escrow + 3-day rent-back at $0/day through May 18, 2026 | ¶PP Addendum referenced but not attached — **Blocking** |
| Seller Concession | $7,500 toward buyer's closing costs | ¶8, p.3 |

**Signature & Initial Audit (excerpt):**

- ✅ Alvarez (both) — all signature blocks p.1, p.8, p.10 dated 4/15/26
- ✅ Callahan, Trustee — p.1, p.8, p.10 dated 4/15/26
- ❌ **Blocking** — Arbitration of Disputes initials (¶22, p.7) — Alvarez initialed, Callahan did NOT initial. Enforceability unilateral.
- ✅ Liquidated Damages initials (¶21, p.7) — both parties initialed
- ⚠️ Lead-paint disclosure initialed on p.2 of the federal disclosure form; Callahan's initial is partially obscured by a scanner artifact — re-execute for a clean record.

**Anomaly Report:**

- **Blocking**
  1. Agency Disclosure Addendum (AD) referenced on cover page but not present in the signed stack. ¶1, p.1. Resolution: obtain signed AD from both sides and countersign before opening escrow.
  2. Possession/Rent-Back Addendum (PP) referenced at ¶3L, p.2 but not present. Resolution: draft and attach the PP addendum or strike the rent-back language and re-initial. Rent-back at $0/day also exposes the seller's insurance — confirm carrier acceptance.
  3. Arbitration clause initialed by only one side. ¶22, p.7. Resolution: either obtain Callahan's initial or acknowledge unilateral arbitration waiver in writing.
- **Material**
  1. Inspection contingency at 10 days is 3 days below the 13-day market norm for this price band. ¶14B(4), p.5. Resolution: flag to buyer's agent; consider extension request at day 8 if vendor scheduling slips.
- **Advisory**
  1. Seller concession of $7,500 is well inside the 3% conventional cap of $44,550. No action.
  2. Commission section references "as per MLS" — matches MLS offer of 2.5% co-op, no friction expected.

**48-Hour Action List:**

| # | Action | Owner | Deadline |
|---|---|---|---|
| 1 | Verify escrow officer via phone at the number listed on Bright Escrow's website — NOT the one in any email | Agent | 4/16 10:00 AM |
| 2 | Deliver fully-executed contract + both addenda to Bright Escrow, cc: lender | TC | 4/16 12:00 PM |
| 3 | Obtain signed Agency Disclosure from both sides | Listing side | 4/17 EOD |
| 4 | Alvarez wires $15,000 earnest money to Bright Escrow; escrow issues receipt | Buyer | 4/17 EOD |
| 5 | Order preliminary title report | Bright Escrow | 4/17 EOD |
| 6 | Schedule general inspection + sewer + termite (contingency expires 4/25) | Buyer's agent | 4/17 EOD |
| 7 | Submit full loan package to lender; request appraisal order the same day | Buyer + Lender | 4/17 EOD |
| 8 | Request Callahan Trust certification + trustee authority excerpt | Listing agent | 4/17 EOD |
| 9 | Draft and route PP Addendum for signatures | Listing agent | 4/17 EOD |
| 10 | Resolve arbitration-clause initial | Listing agent | 4/18 EOD |

**TC Handoff Paragraph:**

Mutual acceptance 4/15/26 on 4821 Laurel Canyon Blvd at $1.485M with 20% down conventional financing via ABC Mortgage (LO: Dana Lin); $15K EM due to Bright Escrow by 4/17; 30-day close on 5/15/26 with 3-day free rent-back through 5/18 (rent-back addendum missing — blocking). Inspection contingency 10 days (4/25), appraisal 17 days (5/2), loan 21 days (5/6). $7,500 seller credit at close. Two blocking issues: missing Agency Disclosure Addendum and missing Possession/Rent-Back Addendum; one material issue: tight 10-day inspection window. Trust vesting on the sell side — trustee authority letter requested. Full deal record and anomaly report at `Deals/Alvarez-Callahan/intake-2026-04-15.md`.
