# MLS AI-Data-Governance — Reference (as of 2026-07-28)

> **Why this exists.** Between 6/12/2026 and 7/15/2026 the "who controls how AI touches MLS data" question — tracked as commentary-only on the watchlist for four monitor cycles (6/29, 7/6, 7/13, 7/20) — produced a second, structurally different PRODUCT/ENTRANT, satisfying the ACT trigger this file's absence had been waiting on. This file is the canonical reference any skill in the repo should cite when its workflow ingests MLS-sourced data into an AI tool — primarily `ai-marketing-compliance-audit.md`, `lead-qualification-bant.md`, `market-analysis-summary.md`, `cma-presentation-generator.md`, `listing-aeo-optimizer.md`, and `agent-discoverability-audit.md`.
>
> **The compliance-relevant fact this file exists to surface:** several of this repo's own skills instruct the user to feed MLS-sourced records (comps, tax-roll cross-references, closed-sales data, listing history) into Claude or ChatGPT for analysis. As of mid-2026, a subset of MLSs have adopted written policies that **prohibit exactly this** without prior written permission. This is not a hypothetical — it is a documented, named MLS policy (see Pattern 2 below). Every skill that ingests MLS data into an AI tool now carries a "verify your MLS's AI-use policy first" caveat.

---

## Two governance patterns, confirmed distinct

### Pattern 1 — Infrastructure / access-control layer

**Canonical example: NorthstarMLS × REcore Solutions — "Project NexusRE"** (introduced 6/12/2026, active development, testing summer 2026).

A patent-pending infrastructure layer sitting between MLS listing data and the websites/apps/AI systems consuming it — a common framework for managing permission, monitoring usage, and maintaining accountability over how AI accesses and interprets listing data. This is a **plumbing-layer** solution: it doesn't tell an AI system "no," it builds the metering and audit trail that lets an MLS grant graduated, monitored access (a usage-metering / broker-credit economic model was part of the original announcement).

### Pattern 2 — Contractual / licensing-policy layer

**Canonical example: Metro MLS, Milwaukee, WI** (Chris Lambrou, CEO — reported by NAR AExperience, 7/15/2026).

Metro MLS — the largest MLS in Wisconsin, serving 9,000+ members across six local REALTOR associations — rewrote its data-licensing agreement to add an explicit AI clause:

> "Metro MLS data may not be used for AI training or machine learning in any way without Metro MLS's express written permission. This includes AI-related derivative datasets and AI processing of MLS data for predictive or generative capabilities."

This is a **contract-layer** solution: a flat prohibition (not a graduated-access system) enforced as a material breach of the existing data-license agreement, with real remedies (contract + other legal remedies). Metro MLS's policy explicitly defines "AI" broadly (LLMs, ML models, neural networks, generative AI, predictive models, automated decisioning systems, recommendation engines, computer vision) and "training" broadly (fine-tuning, testing, validating, improving outputs, creating embeddings/vector databases, creating synthetic or derivative datasets — i.e., **not limited to foundation-model pretraining**; ordinary RAG-style ingestion into a chat tool plausibly falls inside this definition). NAR now publishes a downloadable **"AI Policy Template for Associations"** (nar.realtor/ae/ai-policy-template-for-associations) that other MLSs can adapt — meaning Metro MLS is very unlikely to remain a singleton.

**Why two-source convergence matters:** the pattern is no longer "one MLS's idiosyncratic policy" — it's a governance *category* with two structurally different mechanisms (infrastructure-metering vs. contract-prohibition), and a NAR-distributed template that lowers the cost of a third, fourth, and fifth MLS adopting the contract-prohibition pattern specifically.

---

## What this means for the repo's own skills

This is the first monitor finding in this concept-class with a **direct compliance implication for KRASA's own workflow instructions**, not just an external trend to track. Several skills currently instruct the user to pull MLS-sourced records into an AI tool:

- `lead-qualification-bant.md` Deep Pass — "Adds verified property-level records — MLS/tax roll/county assessor, public price history..."
- `market-analysis-summary.md` — turns "MLS numbers into a clear, honest, and useful market narrative," with the MLS attribution string sourced from `config.yml → mls.attribution`.
- `cma-presentation-generator.md` — builds pricing narratives from MLS comps.
- `listing-aeo-optimizer.md` — Step 8's portal-resident-AI tactic explicitly instructs pushing MLS/IDX-fed structured fields into a form a portal-resident Gemini agent (and, by extension, the agent's own AI tools) can read.

**None of these skills currently ask the user to confirm their MLS's data-license agreement permits AI ingestion.** Under a Metro-MLS-style policy, an agent who pastes closed-sales data into Claude to run `market-analysis-summary.md`, or who has their AI assistant cross-reference MLS records for `lead-qualification-bant.md`'s Deep Pass, could be creating a data-licensing violation their MLS considers a material breach — independent of anything about the AI output's quality or accuracy.

**This is a data-input compliance question, not a data-output compliance question.** `ai-marketing-compliance-audit.md` audits AI-generated *marketing deliverables* (the output). This file's concern sits one layer upstream: whether the *act of feeding MLS data into an AI tool* is itself permitted by the MLS's data-license agreement, before any output exists to audit.

**Recommended posture for every MLS-data-consuming skill (adopted 7/28/2026):**

1. Treat "does your MLS have a written AI-use policy?" as a config-worthy fact (`config.yml → mls.ai_use_policy` — not yet a standard field; flag as a config-schema gap until adopted repo-wide).
2. Default to **unknown = assume restricted** for anything that resembles training, fine-tuning, embedding creation, or "AI processing... for predictive or generative capabilities" — ordinary one-off "summarize this comp set" prompting is a lower-risk read (closer to a human analyst reading the data) than bulk ingestion, but the Metro MLS definition is broad enough that a cautious skill should flag rather than assume.
3. Never let this uncertainty block the workflow — flag it as `[VERIFY MLS AI-USE POLICY]` the same way the repo already flags `[VERIFY MLS ATTRIBUTION WORDING]`, and let the human agent resolve it with their MLS.

---

## What this is NOT

- **Not a claim that MLS data can never touch an AI tool.** Most MLSs have no AI-specific policy yet, and even Metro MLS's policy is aimed at training/derivative-dataset creation, not at an agent using a chat assistant to read and summarize a comp set the way they'd use a spreadsheet. The distinction between "AI reads data to help a human do a one-off task" and "AI trains/embeds on data to build a durable derivative asset" is exactly the ambiguity this file flags rather than resolves.
- **Not legal advice.** Whether a given skill's workflow trips a given MLS's policy is a data-license question for the agent's MLS and, where material, their broker or counsel — the repo surfaces the question, not the answer.
- **Not a complete map.** Only two named entrants exist as of this writing (NorthstarMLS/REcore infrastructure-layer, Metro MLS contract-layer). WAV Group Consulting remains the highest-cadence commentary voice tracking this space (four pieces since 1/23/2026) but commentary is not counted toward the ACT trigger — only named PRODUCT/POLICY entrants are.
- **Not stable.** Re-check whenever a third MLS adopts either pattern, whenever NAR's AI Policy Template sees adoption data reported, or whenever a portal (Zillow, Realtor.com, Homes.com) discloses how it reconciles portal-resident AI assistants (which read MLS-sourced feeds) against MLS-level AI-use restrictions.

---

## Sources (canonical first-surface references)

- NorthstarMLS × REcore Solutions, "Project NexusRE" — PR Newswire, 6/12/2026.
- Metro MLS AI-use policy — Danielle Wong Moores, "Make It a Policy to Protect MLS Data From AI Misuse," NAR AExperience, 7/15/2026 (Chris Lambrou, CEO, Metro MLS, interviewed).
- WAV Group Consulting — "Stop Giving AI Another Broker's Listing" (7/3/2026), "AI Is Already Inside Your MLS. The Question Is Who Controls It." (5/18/2026), "Why the MLS Must Remain the Heart of Data Integrity in Real Estate" (3/26/2026), "MLS Data, AI, and the Line Between Innovation and Risk" (1/23/2026).
- NAR "AI Policy Template for Associations" — nar.realtor/ae/ai-policy-template-for-associations.

**Cross-references:**

- Pairs with `tools-ecosystem/agentic-title-escrow-vendors.md` — that file maps agentic AI vendors operating *with* licensed data access inside the closing workflow; this file maps the governance question of *whether* an AI tool has a license to touch MLS data at all.
- Adjacent to `ai-marketing-compliance-audit.md` Section B item 3 (MLS(s) input) — that skill now carries a parallel "MLS AI-Use Policy" check alongside its existing "Brokerage AI Use Policy" check (added 7/28/2026).
