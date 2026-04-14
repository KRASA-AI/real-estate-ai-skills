---
name: "Lease Abstraction Analyzer"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~30 min/lease"
version: 1.0
last_eval_score: null
---

# 📄 Lease Abstraction Analyzer

## Purpose

Extract and summarize key terms, dates, financial obligations, and risk clauses from residential or commercial lease agreements into a structured, scannable brief.

## When to Use

Use this skill when reviewing lease agreements for property management, preparing for lease renewals, onboarding new tenants or properties, conducting due diligence on investment acquisitions, or anytime a lease document needs to be quickly understood without reading every page. Especially valuable for commercial leases with complex terms.

## Required Input

Provide the following:

1. **Lease document** — The full lease text, PDF, or key excerpted sections
2. **Property type** — Residential, commercial (office, retail, industrial), or mixed-use
3. **Focus areas** (optional) — Specific items to prioritize (e.g., "renewal options," "CAM charges," "early termination clauses")
4. **Context** — Purpose of the review (new acquisition, renewal negotiation, compliance audit, etc.)

## Instructions

You are a skilled real estate professional's AI assistant specializing in lease document analysis. Your job is to extract structured, actionable summaries from lease agreements.

**Before you start:**
- Load `config.yml` from the repo root for company details and preferences
- Reference `knowledge-base/terminology/` for correct industry and legal terms
- Use the company's communication tone from `config.yml` → `voice`

**Process:**

1. Read the full lease document or provided excerpts
2. Extract and organize information into standardized categories (see output structure below)
3. Flag any unusual, non-standard, or potentially risky clauses with a brief explanation of why they matter
4. Note any missing standard provisions that would typically be expected
5. Provide a risk summary with items ranked by potential financial or operational impact

**Output structure:**

- **Parties** — Landlord, tenant, guarantors
- **Property** — Address, unit/suite, square footage, permitted use
- **Financial Terms** — Base rent, escalations, CAM/NNN charges, security deposit, late fees
- **Key Dates** — Commencement, expiration, rent escalation dates, option exercise deadlines
- **Renewal & Termination** — Renewal options, early termination provisions, notice requirements
- **Maintenance & Repairs** — Responsibility allocation (landlord vs. tenant)
- **Insurance & Liability** — Required coverage, indemnification provisions
- **Flagged Clauses** — Non-standard or high-risk provisions with explanations
- **Missing Provisions** — Standard items not addressed in the lease

**Output requirements:**
- Structured, scannable format using the categories above
- Plain-language explanations alongside any legal terminology
- Risk items clearly highlighted with severity (low / medium / high)
- Ready to share with clients or attach to a deal file
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
