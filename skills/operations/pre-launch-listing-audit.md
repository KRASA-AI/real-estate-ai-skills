---
name: "Pre-Launch Listing Audit"
category: operations
tools: [claude, chatgpt]
difficulty: intermediate
time_saved: "~15 min/listing"
version: 1.0
last_eval_score: null
---

# 🚀 Pre-Launch Listing Audit

## Purpose

Generate a comprehensive pre-launch checklist and readiness audit for a new listing, ensuring the entire marketing ecosystem — photography, staging, MLS entry, social media, signage, email campaigns, and agent outreach — is coordinated and activated simultaneously for maximum launch impact.

## When to Use

Use this skill the moment a listing agreement is signed and before the property goes live. It prevents the common mistake of piecemeal launches where photos are ready but the MLS entry is incomplete, or social posts go out before the property is actually available. Critical for competitive markets where first-week showing volume drives offers.

## Required Input

Provide the following:

1. **Property details** — Address, type, price range, key features, target buyer profile
2. **Timeline** — Listing agreement date, target go-live date, any hard deadlines (e.g., seller move-out)
3. **Services booked** — What's already scheduled (photographer, stager, cleaning, etc.)
4. **Marketing channels** — Which platforms the agent uses (MLS, Zillow, social media accounts, email list, brokerage website, etc.)
5. **Team members** (optional) — Who's responsible for what (TC, marketing coordinator, showing agent)

## Instructions

You are a skilled real estate listing launch coordinator and AI assistant. Your job is to create a thorough, time-sequenced pre-launch audit that ensures nothing is missed and everything goes live in sync.

**Before you start:**
- Load `config.yml` from the repo root for company details and preferences
- Reference `knowledge-base/terminology/` for correct industry terms
- Use the company's communication tone from `config.yml` → `voice`

**Process:**

1. Work backward from the go-live date to create a time-sequenced checklist
2. Organize tasks into phases: Pre-Prep (Week 2 before), Prep (Week 1 before), Launch Day, Post-Launch (Week 1 after)
3. For each task, specify: what needs to happen, who owns it, and the deadline
4. Flag dependencies (e.g., "photos must be done before MLS entry can be completed")
5. Include quality checkpoints — moments to review that everything meets standard before going live
6. Generate a launch-day activation sequence (time-ordered list of what goes live and when)

**Checklist categories:**

- **Property Preparation** — Cleaning, staging, repairs, landscaping
- **Visual Assets** — Professional photos, video tour, drone footage, virtual staging, floor plan
- **MLS & Syndication** — MLS entry, syndication feed check, IDX verification
- **Digital Marketing** — Social media posts (scheduled), email blast, website/landing page, paid ads
- **Traditional Marketing** — Signage, flyers, print materials, open house scheduling
- **Agent Network** — Broker tour, pocket listing alerts, referral partner notifications
- **Compliance** — Disclosures, fair housing review of marketing language, required documentation

**Output requirements:**
- Time-sequenced and actionable — every item has a clear deadline and owner
- Formatted as a checklist that can be printed or dropped into a project management tool
- Includes a one-page "Launch Day Runsheet" with hour-by-hour activation plan
- Ready to use with minimal editing
- Saved to `outputs/` if the user confirms

## Example Output

> [This section will be populated by the eval system with a reference example. For now, run the skill with sample input to see output quality.]
