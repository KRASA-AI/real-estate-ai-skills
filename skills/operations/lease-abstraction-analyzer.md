---
name: "Lease Abstraction Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~45 min/lease"
version: 2.0
last_eval_score: null
---

# Lease Abstraction Analyzer

## Purpose

Turn a residential or commercial lease (PDF, scan, or pasted text) into a clean abstract: a structured deal record with paragraph citations, a CAM/NNN reconciliation worksheet (commercial only), an SNDA / estoppel / assignment exposure flag set, and a triaged anomaly list — in one pass — so the agent, asset manager, or buyer's broker can read the lease in five minutes and know exactly where the financial and legal exposure lives.

## When to Use

Use this skill when (a) a lease document needs to be summarized for a renewal negotiation, (b) you are abstracting a rent roll for an investment-sale package, (c) the buyer of an owner-occupied building has just received the existing tenant lease and needs to know what they are inheriting, (d) you are preparing an estoppel response or a due-diligence file, or (e) a tenant or landlord client has asked for a plain-language read of what their lease actually says. The skill complements `purchase-agreement-intake.md` (which handles purchase contracts) and feeds `transaction-coordinator-brief.md` when an investment sale closes with leases in place.

## Required Input

Provide any of the following — the skill prefers the fully-executed lease but will still produce useful output with partial information:

1. **Lease document** — Full executed lease (PDF text, OCR output, or pasted text). Amendments, side letters, riders, and guaranties should be concatenated in signed order
2. **Lease family** — Residential (single-family / multi-family / SFR-portfolio), commercial-office (full-service / modified-gross / industrial-gross), commercial-retail (NNN / percentage / ground), commercial-industrial (NNN / absolute-net), or mixed-use. Family drives which abstraction template applies and what reconciliation math is required
3. **Review purpose** — One of: due diligence on acquisition, renewal negotiation, estoppel response, rent-roll abstraction for an investment package, compliance audit, dispute prep
4. **Representation side** — Landlord, tenant, lender, or buyer of the leased property. Drives which anomaly flags rise to "Blocking"
5. **Rent roll cross-reference** (optional) — If abstracting from a rent roll, provide the rent-roll line for the suite so the abstract can be reconciled against the rent-roll fields
6. **Reference standard** (optional) — A baseline form (BOMA full-service form, AIR-CRE NNN, brokerage's standard residential lease) lets the skill flag deviations precisely
7. **Agent config** — `config.yml` provides brokerage state, market conventions, and notification preferences

## Instructions

You are a senior lease analyst working on behalf of the agent or asset manager. Your job is not to provide a legal opinion — it is to surface every material term and every non-standard clause with a paragraph citation, so the agent and the attorney can have a substantive conversation in twenty minutes instead of two hours. Accuracy beats speed; every extracted field is downstream of a financial decision.

**Before you start:**
- Load `config.yml` for brokerage state, market conventions, and notification preferences
- Reference `knowledge-base/terminology/` for lease-family-specific terminology (CAM pools, gross-up provisions, base-year stops, percentage-rent breakpoints)
- Never assume a field from context when the lease is silent — leave it blank and flag it as "Silent — confirm with counsel" in the anomaly report

**Process:**

1. **Classify the lease family and template.** Identify residential vs. commercial; within commercial, identify the rent structure (full-service / modified-gross / NNN / absolute-net / percentage / ground). Record the lease form (AIR-CRE 2017, BOMA Standard Office Lease, brokerage custom, state-association residential) and the execution date at the top of the abstract. The lease family determines which sections of the output are populated; do not generate an empty CAM table for a residential lease.

2. **Extract the deal record with paragraph citations.** For every field, capture the value and the paragraph/section reference so anyone can verify in under ten seconds. Do not paraphrase economic terms — record the exact lease language. Lease-family-specific fields:

   *All families:*
   - Parties: landlord legal name, tenant legal name, guarantor (if any) with guaranty scope (full / limited / good-guy / burn-off)
   - Premises: address, suite/unit, rentable square footage, usable square footage, load factor (commercial), permitted use, exclusive-use protections (retail)
   - Term: commencement date (signing / delivery / rent-commencement), expiration date, holdover provisions and holdover-rent multiplier
   - Base rent schedule: monthly amount, escalation mechanism (fixed % / CPI / FMV / stepped), escalation dates, full term-total
   - Security deposit: amount, form (cash / LOC / personal guaranty), return conditions
   - Renewal options: number, length, exercise window (must be exercised X months before expiration), pricing mechanism
   - Termination rights: tenant termination fee + notice; landlord recapture; mutual termination triggers
   - Insurance: required coverages, limits, additional-insured endorsement, waiver of subrogation
   - Default and remedies: cure periods (monetary vs. non-monetary), acceleration, attorney-fee clause direction (one-way / two-way)

   *Commercial only:*
   - Operating-expense structure: full-service base year, modified-gross stops, NNN pass-throughs by category (taxes / insurance / CAM / utilities)
   - CAM pool composition: included items, excluded items (admin fee, capital improvements, leasing commissions, ground-lease rent), gross-up provision (occupancy threshold), audit rights (window + scope)
   - Percentage rent (retail): natural breakpoint, artificial breakpoint, gross-sales definition, exclusions, reporting cadence
   - Tenant improvements: TI allowance per RSF, unused-allowance treatment, work letter or turnkey
   - Assignment & subletting: consent standard (sole discretion / not unreasonably withheld), recapture, profit-sharing, permitted transfers (affiliate / corporate restructuring)
   - SNDA / non-disturbance: required, conditional, or absent
   - Estoppel cadence: response window (typically 10 business days)
   - Right of first refusal / right of first offer on adjacent space or the building
   - Casualty and condemnation: termination thresholds, restoration obligations, abatement
   - Use restrictions and exclusives: tenant-protective exclusives, landlord-imposed prohibited uses
   - Signage rights: building / monument / suite, with approval standard
   - Parking: ratio, reserved vs. unreserved, monthly cost, validation rights

   *Residential only:*
   - Rent control / stabilization status (per local ordinance — flag jurisdiction)
   - Pet provisions: allowed, deposit, monthly fee, breed/size restrictions
   - HOA / strata rules incorporated by reference
   - Habitability and repair-responsibility allocation
   - Subletting and short-term rental restrictions (Airbnb language)
   - Landlord-entry notice requirements (state-statutory)
   - Lead-based-paint disclosure (federal — required for pre-1978 buildings)
   - Security-deposit treatment (interest-bearing account where required, return window)

3. **Run the CAM/NNN reconciliation (commercial only).** Build a reconciliation table that ties the lease's economic structure to dollars. For NNN: compute the year-1 effective rent ($/RSF base + $/RSF NNN estimate), the post-escalation year-X effective rent, and the total occupancy cost over the term. For full-service / modified-gross: compute the base-year stop in $/RSF, identify the gross-up provision, and stress-test what happens if building occupancy drops below the gross-up threshold. Flag any of: (a) CAM pool includes capital improvements without amortization, (b) admin fee on top of CAM > 15%, (c) no audit rights or audit window < 90 days, (d) no gross-up clause in a sub-95%-occupied building, (e) management fee charged as a percentage of gross revenue rather than a percentage of operating expenses, (f) ground-lease rent included in CAM pass-through.

4. **Run a signature, initial, and exhibit audit.** For each signature block, record: party, page, status (signed / unsigned / illegible / wrong signatory authority), date. Verify guaranty signature is by the named guarantor in personal capacity (not as an officer of the tenant entity). For each exhibit referenced (Exhibit A site plan, Exhibit B work letter, Exhibit C rules and regulations, Exhibit D guaranty, Exhibit E SNDA), confirm the exhibit is attached and signed where signature is required. Missing-but-referenced exhibits are **Blocking**, not Advisory.

5. **Run the SNDA / estoppel / assignment exposure check.** These three are the most-missed provisions in lease abstracts and the source of most post-acquisition surprises:
   - **SNDA:** Is there a non-disturbance clause? Is it self-executing or does the tenant have to demand and the landlord deliver an SNDA from each lender? If absent, the tenant is exposed to lease termination in foreclosure; the buyer-of-the-building is exposed to a tenant who can walk if a lender forecloses
   - **Estoppel:** What is the response window? What happens if the tenant fails to respond — is there a deemed-estoppel provision? A 10-business-day response window with deemed-estoppel is normal; a 30-day window with no deemed-estoppel is a diligence drag
   - **Assignment:** What is the consent standard? "Sole and absolute discretion" is landlord-favorable; "not unreasonably withheld" is tenant-favorable. Is there a recapture right (landlord can take the space back instead of consenting)? Is there a profit-share on sublet rent above contract rent? Permitted-transfer carve-outs (affiliate, corporate restructuring) are standard and should be present

6. **Triage anomalies into three bands.** Every anomaly belongs to exactly one band:
   - **Blocking** — must be resolved before closing the acquisition or signing the renewal. Examples: missing-but-referenced exhibits, unsigned guaranty, conflicting commencement dates between the lease and the rent commencement notice, CAM pool that pass-throughs leasing commissions or ground-lease rent (illegal in most jurisdictions and unenforceable), holdover at less than 100% of base rent, no SNDA in a building with a pending refinance
   - **Material** — should be resolved this week; will cause friction or a price/term renegotiation if ignored. Examples: 30-day estoppel response without deemed-estoppel, no audit rights on CAM, admin fee > 15%, percentage-rent breakpoint set well below the natural breakpoint, sole-discretion assignment standard with no permitted-transfer carve-out
   - **Advisory** — note for the file but does not require action. Examples: stylistic edits, belt-and-suspenders disclosures, market-rate signage approvals, non-material exhibit numbering errors

7. **Produce the executive abstract.** A one-page summary at the top of the output: lease family, parties, premises, term, base rent at start and end, total occupancy cost over term (commercial), three biggest risks, three biggest opportunities (renewal pricing power, expansion rights, signage upgrades). The agent reads this in 90 seconds; the asset manager reads it in three minutes.

8. **Produce the rent-roll line.** A single line that drops directly into a rent-roll spreadsheet: Suite | Tenant | RSF | Use | Term Start | Term End | Base Rent ($/mo) | Escalation | NNN Est ($/RSF) | Effective Rent ($/RSF) | Options | Notes. This is the artifact the broker uses for the OM.

9. **Compile the downstream handoffs.** For an acquisition, write the one-paragraph lease summary that drops into the TC brief. For a renewal negotiation, write a 5-bullet negotiation playbook (which clauses are worth fighting for, in order of expected ROI). For an estoppel response, write the draft estoppel certificate with each material disagreement footnoted to the abstract.

**Critical rules:**

- Every extracted field carries a paragraph and page citation. "The lease says renewal is at FMV" is not acceptable — write "Renewal pricing: 95% of FMV (¶34.2, p.18)" with the cap mechanism if any
- Never interpret a handwritten edit, side letter, or oral representation as authoritative unless it is in writing, signed by both parties, and dated. Flag as Blocking otherwise
- Never extract a wiring instruction, account number, or routing number from the lease into the output. If wire instructions are embedded, flag as a fraud-risk signal and route to `ai-fraud-defense-playbook.md`
- This skill does not provide legal advice. Anomalies are surfaced; legal interpretation requires attorney review. Write in a register that makes this boundary clear on every output
- Fair-housing exposure: residential lease language that imposes occupancy limits below 2-per-bedroom + 1, that conditions on familial composition, or that restricts service-animal accommodations is flagged and routed to `ai-marketing-compliance-audit.md` for remediation
- A lease with more than three Blocking items is a re-trade conversation, not a clean abstract. Tell the agent plainly rather than producing an executive summary that papers over the issues
- Preserve the lease's actual language in the citations column. Plain-English explanation belongs in a separate "Translation" column, never overwriting the lease's words

**Output structure (always in this order):**

1. **Lease Family & Form Identifier** — family / form / version / execution date / page count / exhibits attached and signed
2. **Executive Abstract** — one-page top-of-file summary
3. **Rent-Roll Line** — single line ready to paste into a rent-roll spreadsheet
4. **Deal Record** — extracted fields with paragraph citations (table)
5. **CAM/NNN Reconciliation** — commercial only, with year-1 and year-X effective rent
6. **Signature, Initial & Exhibit Audit**
7. **SNDA / Estoppel / Assignment Exposure**
8. **Anomaly Report** — Blocking / Material / Advisory, each with citation and recommended resolution
9. **Negotiation Playbook or Estoppel Draft** — depending on review purpose
10. **Handoff Paragraph** — for the TC brief or buy-side broker memo

## Example Output

**Lease Family & Form Identifier:** Commercial-retail NNN. AIR-CRE Standard Industrial/Commercial Multi-Tenant Lease — Net (Form MTN-31, 4-2017 revision). Executed 6/1/2024. 28-page base + 4 exhibits: A site plan (signed), B work letter (signed), C rules & regs (signed), D guaranty (signed by Marcus Chen personally, **confirmed**). Two side letters: 6/15/24 signage clarification (signed both sides), 8/1/24 HVAC repair-cost cap (signed both sides).

**Executive Abstract (excerpt):**

> 5-year NNN lease on 3,200 RSF at 14820 Ventura Blvd Suite 105, Sherman Oaks. Tenant: Ridgeline Coffee Roasters, LLC; Marcus Chen personal guaranty (full, no burn-off). Term 7/1/2024–6/30/2029. Base rent $4.50/RSF/mo year 1 ($14,400/mo) escalating 3%/yr. Year-1 NNN estimate $1.85/RSF/mo ($5,920). Total occupancy cost year 1 = $20,320/mo, $243,840/yr. One 5-year option at FMV with floor of last-month base rent. Three biggest risks: (1) **CAM pool includes capital improvements without amortization** (¶4.2(d), p.7) — Material, capped CAM provision available in market; (2) no SNDA from current lender, building was refinanced 11/2025 (¶17, p.16) — Material; (3) percentage rent at 6% of gross sales over an artificial $850K breakpoint, which is ~12% below the natural breakpoint — landlord-favorable, expect to negotiate. Three biggest opportunities: (1) renewal at FMV with floor — tenant should expect 8–12% market premium on renewal; (2) tenant has right of first refusal on adjacent Suite 107 (¶36, p.21); (3) exclusive-use protection on coffee/espresso retail in the center (¶6.4, p.9) — defensible against later landlord leasing.

**Rent-Roll Line:**

| Suite | Tenant | RSF | Use | Start | End | Base $/mo | Escalation | NNN Est | Eff. $/RSF | Options | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 105 | Ridgeline Coffee Roasters LLC | 3,200 | Coffee retail + roasting | 7/1/24 | 6/30/29 | $14,400 | 3%/yr | $1.85/RSF/mo | $6.35 yr1 | 1 × 5yr @ FMV (floor) | Personal guaranty / Exclusive on coffee / ROFR Suite 107 |

**Deal Record (excerpt):**

| Field | Value | Citation |
|---|---|---|
| Landlord | 14820 Ventura Blvd LP, a CA limited partnership | ¶1.1, p.1 |
| Tenant | Ridgeline Coffee Roasters, LLC, a CA LLC | ¶1.2, p.1 |
| Guarantor | Marcus Chen, individually | Exhibit D, p.30 |
| Premises | Suite 105, 14820 Ventura Blvd, Sherman Oaks CA 91403; 3,200 RSF / 2,950 USF (8.5% load factor) | ¶1.3, p.1 |
| Permitted Use | Specialty coffee retail and on-site bean roasting; no other use without consent | ¶6.1, p.9 |
| Exclusive Use | No other tenant in the center may operate as a "specialty coffee shop" or sell brewed coffee as primary use; exclusion does not apply to incidental sales (e.g., restaurants serving coffee with meals) | ¶6.4, p.9 |
| Term | 60 months: commencement 7/1/2024, expiration 6/30/2029; rent commencement = same as term commencement (no free-rent period) | ¶3, p.4 |
| Base Rent | Year 1 $14,400/mo ($4.50/RSF); 3% annual escalation on each 7/1; Year 5 $16,205/mo | ¶4.1, p.6 |
| NNN | Pro-rata share of taxes, insurance, CAM, utilities; tenant share = 12.4% of building NRA | ¶4.2, p.7 |
| Security Deposit | $30,000 cash held by landlord (no interest); reduces to $20,000 after 24 months on-time payment | ¶5, p.8 |
| Renewal Option | One 5-year option; exercisable 9–12 months prior to expiration; pricing = 95% of FMV with floor at the then-current monthly base rent | ¶34, p.20 |
| ROFR | Right of first refusal on Suite 107 (1,800 RSF adjacent); 10-business-day response window upon landlord notice of bona fide third-party offer | ¶36, p.21 |
| Holdover | 150% of last-month base rent + all NNN; month-to-month at landlord's election | ¶24, p.18 |
| Assignment | Landlord consent not unreasonably withheld; permitted transfers to affiliates and corporate restructuring; recapture right; 50% profit-share on sublet rent over contract rent | ¶12, p.13 |
| Insurance | $2M GL per occurrence / $4M aggregate / $1M product liability; landlord additional insured; waiver of subrogation; tenant property insurance to full replacement value | ¶8, p.11 |
| Casualty | Landlord may terminate if damage > 25% of building or > 50% of premises; tenant may terminate if restoration not complete within 270 days; rent abatement during restoration | ¶9, p.11 |
| Default Cure | Monetary 5 days; non-monetary 30 days; cross-default with affiliate leases | ¶13, p.14 |
| SNDA | Tenant entitled upon written request; landlord shall use commercially reasonable efforts to obtain from each lender; **not self-executing** | ¶17, p.16 |
| Estoppel | 10 business days; **deemed estoppel if tenant fails to respond** | ¶18, p.16 |

**CAM/NNN Reconciliation:**

| Item | Year 1 | Year 5 | Notes |
|---|---|---|---|
| Base Rent ($/RSF/mo) | $4.50 | $5.06 | 3% escalator, ¶4.1 |
| Property Tax (est) | $0.62 | $0.72 | Prop 13 + reassessment risk on building sale |
| Building Insurance | $0.18 | $0.22 | |
| CAM | $0.85 | $1.04 | Includes capital improvements (¶4.2(d)) — see Anomaly Report |
| Admin Fee | $0.20 | $0.23 | 15% of CAM, at the cap |
| Total NNN ($/RSF/mo) | $1.85 | $2.21 | |
| Effective Rent ($/RSF/mo) | $6.35 | $7.27 | |
| Total Occupancy ($/mo) | $20,320 | $23,264 | |
| Total Occupancy ($/yr) | $243,840 | $279,168 | |
| 5-Year Total Occupancy | — | $1,310,000 (approx, undiscounted) | |

CAM audit: tenant has right to audit CAM within 90 days of annual reconciliation, at tenant's cost unless overcharge > 5% in which case landlord pays. **No gross-up provision** — at sub-95% occupancy the tenant absorbs unallocated fixed costs. Building has been ~89% occupied per public marketing data.

**SNDA / Estoppel / Assignment Exposure:**

- **SNDA:** Not self-executing; tenant must request and landlord must use "commercially reasonable efforts." Building was refinanced 11/2025 with a new lender (public deed records). **No SNDA from new lender currently on file.** Material exposure for tenant in the event of foreclosure; recommended action — request SNDA from new lender now, before any payment dispute.
- **Estoppel:** 10-business-day window with deemed-estoppel provision. Standard. No action.
- **Assignment:** "Not unreasonably withheld" — tenant-favorable. Permitted transfers to affiliates and corporate restructuring. Recapture right exists but is paired with a 30-day reconsideration window. 50% profit-share on sublet (above contract rent) is at the tenant-friendly end of market. Acceptable.

**Anomaly Report:**

- **Blocking**
  1. **None.** Lease and exhibits are fully executed. Guaranty signature (Exhibit D) verified as Marcus Chen personal capacity, not LLC officer capacity.
- **Material**
  1. CAM pool includes capital improvements without amortization (¶4.2(d), p.7). Resolution: in renewal negotiation, request capital-improvement carve-out or amortization over useful life with a 4% interest factor. Alternative — request a CAM cap of CPI + 2% on controllable expenses.
  2. No SNDA from current lender after 11/2025 refinance (¶17, p.16). Resolution: tenant submits written SNDA request to landlord within 30 days; landlord has commercially-reasonable obligation to deliver. Document the request via certified mail.
  3. Percentage-rent breakpoint at $850K artificial vs. ~$960K natural (¶4.3, p.7). Resolution: in renewal, push to natural breakpoint or eliminate percentage rent entirely.
  4. No CAM gross-up provision (¶4.2, p.7) in a building running ~89% occupancy. Resolution: model the dollar exposure (~$0.10–$0.15/RSF/mo) and request gross-up to 95% in renewal.
- **Advisory**
  1. Holdover at 150% of base rent + NNN is at market; no action.
  2. Security-deposit step-down to $20K after 24 months on-time payment is tenant-favorable; no action.
  3. Exclusive-use language on "specialty coffee retail" is well-drafted with the incidental-sales exception. No action.

**Negotiation Playbook (for renewal — exercise window opens 7/1/2028):**

| Priority | Ask | Rationale | Likely Outcome |
|---|---|---|---|
| 1 | Cap controllable CAM at CPI + 2%, exclude capital improvements | Largest dollar impact over 5-year renewal; ~$15K/yr exposure | Likely concession in soft retail market |
| 2 | Eliminate percentage rent OR raise breakpoint to natural | Removes 6% tax on growth; competitor rents in market do not include % rent | Possible concession, push for elimination |
| 3 | Lock renewal rent at 92% of FMV (vs. current 95% with floor) | Coffee tenant traffic supports landlord — exclusive value flows both ways | Possible 2–3% concession |
| 4 | Add SNDA self-executing provision | Removes diligence drag on every lender refinance | Often conceded; low landlord cost |
| 5 | Add 60-day cure period for non-monetary defaults (currently 30) | Operational protection for vendor/insurance-renewal slip-ups | Often conceded |

**Handoff Paragraph (for buy-side broker memo on building acquisition):**

Suite 105 (3,200 RSF) is leased to Ridgeline Coffee Roasters LLC under a 60-month NNN lease at $4.50/RSF base + ~$1.85 NNN, escalating 3%/yr through 6/30/2029, with one 5-year option at 95% of FMV (floored at last-month rent). Personal guaranty from Marcus Chen confirmed. Tenant has been in occupancy since 7/1/2024 with on-time payment history per landlord books. Two material lease items the buyer is inheriting: (1) CAM pool includes capital improvements without amortization, which a sophisticated tenant will renegotiate in 2029; (2) no current SNDA from the 11/2025-refinanced lender, recommended to deliver before close to clean the diligence file. Exclusive-use protection on coffee retail and ROFR on adjacent Suite 107 are tenant-favorable but do not encumber the buyer's leasing of other space. Total year-1 effective rent of $20,320/mo is approximately 6% below market for comparable Sherman Oaks corner retail; renewal pricing power exists. Full lease abstract at `Deals/14820-Ventura/lease-abstracts/Suite-105-Ridgeline.md`. Not legal advice; recommend counsel review the SNDA gap and the CAM pool composition before close.
