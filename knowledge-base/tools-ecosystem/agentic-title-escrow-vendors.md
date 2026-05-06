# Agentic Title & Escrow AI Vendor Cluster — Reference (as of 2026-05-04)

> **Why this exists.** Between 1/29/2026 and 4/29/2026 the residential-real-estate title & escrow vendor layer crossed from "single-vendor curiosity" to "category-shaped methodology." Five named vendors now ship agentic AI products that touch the same closing surface area (orders, curative work, document review, wire instructions, lender/HOA outreach). This file is the canonical map any skill in the repo can cite when its workflow intersects the title/escrow boundary — primarily `transaction-coordinator-brief.md`, `ai-fraud-defense-playbook.md`, `purchase-agreement-intake.md`, `offer-review-checklist.md`. **Do not treat any single vendor's claimed time savings as benchmark data — those are vendor-shaped figures.**
>
> **Scope.** Residential. Commercial-lease workflows (A.CRE / Topular / RedIQ / Cactus / Lindy AI / Reuters Powered Land / LandGate) are out of scope here.

---

## Vendor map

| # | Vendor | Product | Pattern | First public surface | Vendor-claimed effect | Substrate (where disclosed) |
|---|--------|---------|---------|----------------------|-----------------------|------------------------------|
| 1 | HomeLight | EVA — agentic escrow officer | All-in-one (one agent, 80+ tools, 120-task workflow including funds-wiring) | 4/27/2026 launch + $40M debt financing from BlackRock-managed accounts | Vendor-positioned as "industry's first agentic escrow officer" | Not publicly disclosed |
| 2 | Qualia | Qualia Clear 2.0 + Specialized Agents | Specialized-agent-per-curative-workflow (property-tax verification, entity validation, mortgage payoffs, HOA estoppels) | Qualia Clear debut 9/2025; Clear 2.0 + Specialized Agents framework 4/28–4/29/2026; phone + web agents expected by end of 2026 | "35–50% reduction in file processing time"; CEO Nate Baker positions as path to "80% automated real estate closings by 2026" | Google Cloud — Gemini 2.5 Flash integrated for email/document processing; Gemini 3 incoming |
| 3 | First American | AgentNet® Assist: Title Intelligence | Document-analysis assistant inside the title agent's existing platform (chain-of-title break detection, missing-information flags, data-discrepancy callouts; specific-section references) | 4/29/2026 announcement; internal rollout first, then policy-issuing title agents on the AgentNet platform | "As much as 30 minutes per file" reduction in early usage; "final title determinations remain with the title professional" | Not publicly disclosed |
| 4 | Stewart Information Services | VU Explorer (AI-powered Virtual Underwriter Agent) + secure-login Virtual Underwriter | Knowledge-base Q&A agent over Stewart's proprietary underwriting manuals + bulletins + reference materials | 3/25/2026 announcement; secure-login moved 12/2025 | Not quantified; "designed to support, not replace, underwriting judgment" (Wilhelmina Kightlinger, Chief Underwriting Counsel) | Not publicly disclosed |
| 5 | Propy | Avery (AI Agent for escrow officer functions) | Email-checking + 24/7 transaction-opening + bank-account checks + outbound calls to lenders and HOAs; pursuing AI-led roll-up of title/escrow firms | Announced 1/29/2026 alongside $100M credit facility from Metropolitan Partners Group; subsequent acquisitions (Boss Law in Florida + others, ~$75M active pipeline as of late Q1 2026) | "Faster and fraud-resistant closings combined with onchain title settlement and automated workflows" | Not publicly disclosed |

**Pattern map (memorize before reading any skill that touches title/escrow):**

- **All-in-one escrow-officer pattern.** One agent that does most of the 120-task escrow workflow, including the high-stakes step of wiring funds. **HomeLight EVA** is the canonical example. The fraud-defense surface here is "vendor AI initiated wire" — distinct from the human-initiated-wire surface that `ai-fraud-defense-playbook.md` was originally written against.
- **Specialized-agent-per-curative-workflow pattern.** A roster of agents, each scoped to one curative task (property-tax verification, entity validation, mortgage payoff, HOA estoppel). **Qualia Clear 2.0** is the canonical example. The fraud-defense surface here is "synthetic-email injection into the document-processing pipeline" — a malformed mortgage payoff or HOA estoppel produced by an AI agent acting on a forged inbound email is a different vector than wire-instruction tampering.
- **Document-analysis-assist pattern.** AI surfaces issues (chain-of-title breaks, missing info, data discrepancies) but the human title professional still makes the final determination. **First American AgentNet Assist: Title Intelligence** is the canonical example. The fraud-defense surface here is narrower — closer to the existing fraud-defense playbook than the EVA or Qualia patterns — but still introduces an AI-prepared exception list that a TC or listing agent might be tempted to over-trust.
- **Knowledge-base Q&A agent pattern.** AI answers questions over the underwriter's proprietary manuals + bulletins. **Stewart VU Explorer** is the canonical example. Lowest fraud surface; primary methodology implication is that the title agent's research speed has changed, not the closing workflow shape.
- **Roll-up + onchain-settlement pattern.** AI agent paired with a vehicle for consolidating fragmented title/escrow firms onto a single AI-powered platform. **Propy Avery** is the canonical example. The fraud-defense surface combines vendor-AI-initiated outbound lender/HOA calls (voice-clone exposure) with onchain settlement (a different, blockchain-shaped fraud surface).

---

## Interaction surfaces with the repo

### `transaction-coordinator-brief.md` (admin)

Add an **agentic-AI-pre-pass intake step** before the TC begins manual verification. The intake step needs to ask:

1. Which title/escrow vendor is on the file (HomeLight / Qualia / First American / Stewart / Propy / a non-AI vendor)?
2. Which pattern did the file go through (all-in-one / specialized-agent / document-analysis-assist / KB Q&A / roll-up)? This determines what has already been done vs. what the TC still needs to verify.
3. What is the AI agent's confidence-tier or human-review marker on the file (where surfaced — Qualia surfaces this per specialized agent; First American keeps "final determination with the title professional" baked in; HomeLight does not publicly disclose a confidence layer)?
4. What is the brokerage-side AI handoff (Compass-Anywhere ⅔-of-documents AI / Real reZEN AI / Side App AI / eXp / KW) on the same file? The brokerage-AI side and the title/escrow-AI side may have made conflicting assumptions on the same field.

The TC's verification checklist changes shape depending on the answers. **Do not treat this as a per-vendor checklist** — treat it as a pattern-aware checklist where the pattern (not the vendor) drives the verification posture.

### `ai-fraud-defense-playbook.md` (admin)

Extend the existing **L1 callback / L2 passphrase / L3 dual-control** ladder to two new vector classes:

- **Vector A — vendor-AI-initiated wire.** Pattern: HomeLight EVA. The wire instruction was assembled by an AI agent, not a human escrow officer. L1 callback discipline must apply to the named human at the vendor (not just the email-sender), L2 passphrase must be pre-shared with the named human (not the AI agent), L3 dual-control must include a human at the vendor co-signing alongside the brokerage's escrow contact. **Do not assume vendor AI's internal anti-fraud controls are sufficient** — the FBI IC3 $275M-in-2025 number is from a baseline before this pattern was at scale.
- **Vector B — synthetic-email injection into the document-processing pipeline.** Pattern: Qualia Clear 2.0 specialized-agent curative workflow. A forged inbound email (allegedly from the lender, the tax authority, the HOA, or the entity-of-record) is processed by a Gemini-grounded curative agent and surfaces a malformed mortgage-payoff figure, a malformed HOA estoppel, or a malformed entity-validation result. Mitigation: callback the original sender via a phone number obtained out-of-band (not the number in the email), require the curative agent's source-trail metadata to be reviewable by the TC and listing agent, and add a fraud-screen flag to any curative output that sits more than $500 outside the prior-month statement / standard-rate baseline.
- **Vector C (lower-priority but explicit).** Vendor-AI-initiated outbound voice calls (Propy Avery's lender/HOA calls). The voice-clone defense ladder applies in reverse — the lender or HOA might want to verify the call back to a named human at the vendor, and the brokerage may need to disclose to clients that some lender/HOA contact was AI-initiated.

### `purchase-agreement-intake.md` (operations)

**Awareness item only — no methodology shift.** Qualia Clear 2.0's curative work upstream of closing changes what the listing/buyer agent should expect to see by the contingency-removal window. Specifically: title-side curative items are likely to be cleared earlier and with less manual coordination than they were pre-2026. Where the purchase agreement defers to title commitment review, the agent should expect the title commitment exhibits to show "AI-assisted curative" markers on Qualia files and "AI-assisted analysis" markers on First American files. Add the awareness item to the title-side checkpoints; do not rewrite the qualitative-judgment layer.

### `offer-review-checklist.md` (operations)

**Awareness item only — no methodology shift.** Side App's offer-extraction tool already runs in-app upstream of the checklist's qualitative work. Add an analogous awareness note for any file routed through a Qualia or First American pre-pass — the listing agent should not double-process the items the title-side AI has already surfaced, but should not abandon the qualitative compliance + fiduciary sweep either.

### `agent-discoverability-audit.md` (sales)

**Brokerage-stack appendix sensitivity.** S6 "Brokerage page + own site" surface check should now also note when the agent's brokerage routes a meaningful share of files through a known title/escrow AI vendor, because that affects the agent's narrative around "what the brokerage handles for me" — useful for the L0–L3 ladder framing. Optional, low-priority appendix item.

---

## What this is NOT

- **Not a vendor recommendation list.** The repo does not endorse any of these vendors. The cluster exists as a methodology reference, not a buying guide.
- **Not benchmark data.** Vendor-claimed time savings (35–50% Qualia, 30 minutes/file First American, 120-task workflow HomeLight) are vendor-shaped figures. ALTA, The Title Report, or a major brokerage's internal data would graduate the methodology from vendor-shaped to dataset-shaped — track for that.
- **Not a complete map.** Doma, Fidelity, Notarize, SoftPro, RamQuest, and other peer vendors have not yet shipped a public agentic AI methodology surface; track for the next peer follow-on.
- **Not stable.** This file should be re-checked any time the landscape monitor surfaces a new peer vendor, a substrate shift, or a dataset-shaped benchmark replacing vendor-shaped figures.

---

## Sources (canonical first-surface references)

- HomeLight EVA — homelight.com / homelightclosingservices.com / Drew Uher (CEO) public posts; The Title Report; HousingWire; ALTA; Inman.
- Qualia Clear 2.0 + Specialized Agents — Qualia Insight blog ("Introducing Qualia Clear 2.0," "How Agentic AI Unlocks New Capacity for Title & Escrow"); ALTA; The Title Report; HousingWire (Nate Baker interview "Here's How Agentic AI is Already Transforming Title and Escrow"); Google Cloud customer page (cloud.google.com/customers/qualia).
- First American AgentNet Assist: Title Intelligence — firstam.com 4/29/2026 announcement; Business Wire 4/29/2026; ALTA "First American Title Introduces AgentNet Assist" (4/30/2026); The Title Report "First American introduces enhanced AI tool to review title search packages"; Mann Report 4/29/2026; Insurance News Net 4/29/2026; Yahoo Finance.
- Stewart VU Explorer — stewart.com 3/25/2026 press release "Stewart Enhances Virtual Underwriter with Secure Access, Advanced Search, and AI-Powered Support"; Business Wire 3/25/2026; ALTA 3/31/2026; Investing.com; Coverager.
- Propy Avery — PR Newswire 1/29/2026 "Propy Raises $100 Million to Reimagine Real Estate Transactions With AI"; HousingWire "Propy secures $100 million for AI-powered closing platform"; Refresh Miami; Pulse2; Propy March 2026 Recap (propy.com).

**Cross-references:**

- Trade publication anchor for the cluster: **The Title Report** (thetitlereport.com) — first to cover both HomeLight EVA and First American AgentNet Assist; ALTA is the secondary anchor.
- Substrate anchor: **Google Cloud Real Estate / Title customer pages + Google Gemini real-estate use-case content** (cloud.google.com/customers/qualia) — only publicly disclosed substrate so far. Compass-Anywhere uses Anthropic + OpenAI per prior-cycle disclosures; HomeLight, First American, Stewart, Propy substrates are not publicly disclosed.
