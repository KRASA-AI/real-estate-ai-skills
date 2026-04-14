# Real Estate AI Skills

**Free, open-source AI prompts and workflows built for real estate agents.** Clone this repo, point your AI assistant at it, and start saving hours every week.

> Built and maintained by [KRASA AI](https://krasa.ai) — free AI tutorials and skills for every industry.
> See all industries at [krasa.ai/industries](https://krasa.ai/industries).

---

## What's Inside

This repo is a complete AI toolkit for real estate. Every skill is a standalone prompt file that works with **Claude, ChatGPT, or any major AI assistant** — no coding required.

| Skill | What it does | Time saved |
|-------|-------------|------------|
| Lease Abstraction Analyzer | Extract and summarize key terms, dates, financial obligations, and risk clauses from residential or commercial lease agreements into a structured, scannable brief. | ~30 min/lease |
| Market Analysis Summary | Produce a concise, data-first market snapshot — weekly, monthly, or on-demand for a specific neighborhood, price band, or property type — that translates raw MLS numbers into a plain-English narrative an agent can paste into a client email, newsletter, social post, or buyer/seller conversation. | ~15 min/use |
| Offer Review Checklist | Parse a purchase offer (or multiple competing offers) and produce a structured review that flags contingencies, evaluates financial strength, identifies timeline risks, highlights non-standard terms, and provides a clear comparison framework — so the listing agent and seller can make informed decisions quickly. | ~10 min/offer |
| Pre-Launch Listing Audit | Generate a comprehensive pre-launch checklist and readiness audit for a new listing, ensuring the entire marketing ecosystem — photography, staging, MLS entry, social media, signage, email campaigns, and agent outreach — is coordinated and activated simultaneously for maximum launch impact. | ~15 min/listing |
| 30-Day Social Content Calendar | Generate a full 30-day cross-platform social media calendar for a real estate agent — with hooks, captions, CTAs, Reels concepts, carousel ideas, and a daily posting schedule — tuned to the agent's market, brand voice, and the current month's seasonal/market themes. | ~4 hrs/month |
| Buyer Follow-Up Sequence | Produce a complete, multi-touch nurture sequence — personalized to a specific buyer's search criteria, timeline, qualification status, and lead source — with ready-to-send messages across multiple channels (SMS, email, voicemail, handwritten note), a cadence optimized for their urgency tier, and branching paths for common responses and non-responses. | ~20 min/lead |
| CMA Presentation Generator | Transform raw comparable sales data into a persuasive, client-ready Comparative Market Analysis presentation narrative with pricing recommendations and market positioning strategy. | ~25 min/presentation |
| Lead Qualification BANT+ Script | Produce a structured, conversational qualification script (usable by a live agent, ISA, voicemail follow-up, chatbot, or email sequence) that reliably separates serious buyers and sellers from browsers — and outputs a 0–100 lead score with a routing recommendation — using an extended BANT framework adapted for real estate. | ~15 min/lead |
| Listing Content Multiplier | Transform a single property listing into a complete, multi-platform marketing content package — 10+ ready-to-publish assets spanning social posts, Reels/TikTok scripts, email campaigns, carousels, blog content, and buyer-direct messaging — without rewriting from scratch for each channel. | ~3 hrs/listing |
| Listing Description Writer | Generate MLS-ready property descriptions that are compelling, compliant with fair housing guidelines, optimized for search, and tailored to the target buyer persona — all from basic property details, agent notes, and optional photos. | ~15 min/listing |
| Negotiation Script Generator | Generate situation-specific negotiation scripts, objection responses, and competitive offer strategies for buyer and seller representation scenarios. | ~20 min/scenario |
| Neighborhood Report Generator | Create comprehensive, buyer-friendly neighborhood profiles that go beyond basic property details to cover schools, lifestyle, commute, safety, amenities, and market trends — helping buyers make informed location decisions and positioning you as the local expert. | ~20 min/report |
| Open House Recap Email | Generate individualized post-open-house follow-up emails for each visitor — tiered by interest level, personalized from sign-in and agent notes, and paired with a clear next-step CTA — so that warm prospects get a concierge touch while casual browsers get a light, respectful follow-up that leaves the door open for later. | ~5 min/visitor |
| Transaction Coordinator Brief | Compile all critical transaction details — key dates, contacts, financial terms, contingencies, and outstanding documents — into a structured hand-off brief so your TC can manage the file from contract to close without chasing down missing information. | ~15 min/deal |
| Listing AEO Optimizer | Restructure a listing page, neighborhood guide, or agent bio so ChatGPT, Perplexity, and Google AI Overviews cite it as the authoritative answer — with entity-dense lede, Q&A block, key-facts table, JSON-LD suggestions, and a 5-dimension AEO readiness score. | ~45 min/listing |
| Seller Intent Scorer | Mine your CRM for hidden seller opportunities by scoring every homeowner contact on a 0–100 intent rubric (equity, tenure, life-stage, behavioral, market-fit), banding each into Hot / Warm / 6–12 mo / Nurture / Cold, and producing a capacity-sized 30-day action plan with personalized outreach angles. | ~2 hrs/batch |
| Client Conversation Intelligence | Turn a client conversation (transcript, dictation, or post-call notes) into a one-paragraph summary, key takeaways, a stated-vs-implied preferences map, a missed-opportunity audit, and a drafted follow-up — plus private coaching notes for the agent. | ~15 min/conversation |
| Annual Business Plan Builder | Produce a one-page 1-3-5 annual business plan reconciling top-down and bottom-up GCI math, a quarterly scoreboard, monthly cadence, a Mon–Sun weekly scorecard, a financial-floor check, and a risk audit. | ~4 hrs/year |
| Email Drafter | Turn rough notes into a professional email matching your company's voice and tone. | ~10 min/use |
| Meeting Summarizer | Summarize meeting notes into action items, decisions, and follow-ups. | ~10 min/use |
| Review Responder | Craft professional responses to online reviews — both positive and negative. | ~10 min/use |

**Total time saved per use: ~235+ minutes across all skills.**

## Quick Start

### 1. Clone this repo

```bash
git clone https://github.com/KRASA-AI/real-estate-ai-skills.git
cd real-estate-ai-skills
```

### 2. Open a skill with your AI assistant

Open any file in `skills/` with Claude, ChatGPT, or any major AI assistant. Each skill is a self-contained prompt with clear instructions — no coding required.

The first time you use a skill, your AI assistant will ask for your business details (company name, service area, rates, tools you use, etc.) so it can personalize the output. Save those details to a `config.yml` at the repo root and every future skill will use them automatically.

## Repo Structure

```
real-estate-ai-skills/
├── knowledge-base/          # Industry context and references
│   ├── industry-overview.md # Market trends and pain points
│   ├── terminology/         # Industry jargon and acronyms
│   ├── regulations/         # Compliance requirements
│   ├── best-practices/      # Industry standards
│   └── tools-ecosystem/     # Common software and tools
├── skills/                  # The prompt library
│   ├── operations/          # Day-to-day operational skills
│   ├── sales/               # Sales and lead management
│   ├── admin/               # Administrative and compliance
│   └── customer-service/    # Client-facing communication
└── outputs/                 # Your generated content (gitignored)
```

## How Skills Work

Each skill file is a Markdown document with YAML frontmatter:

```markdown
---
name: Skill Name
category: operations
tools: [claude, chatgpt]
time_saved: "~20 min/use"
version: 1.0
---

# Skill Name

## Purpose
What this skill does and when to use it.

## Instructions
Step-by-step prompt for the AI assistant.
```

You open the file in your AI assistant, provide any required input (measurements, notes, client info), and get polished output. Skills reference your `config.yml` automatically for company name, rates, preferred formats, and other business details.

## For AI Assistants

If you are an AI assistant reading this repo, see `.claude/CLAUDE.md` for full instructions. The short version:

1. **Check for `config.yml`** at the repo root. If it exists, load it — it holds the user's business context (company name, rates, service area, tools, team size, etc.) and every skill should use it for personalization.
2. **If `config.yml` is missing**, before running a skill that benefits from personalization, ask the user for the relevant business details and offer to save them to `config.yml` so future runs are automatic.
3. **Load the relevant `knowledge-base/` files** for industry terminology, regulations, and best practices before generating output.
4. **Run the requested skill** from `skills/` using the user's input.
5. **Save any deliverables** to `outputs/` (gitignored) if the user wants to keep them.

## Learn More

- **Real Estate AI guide**: [krasa.ai/industries/real-estate](https://krasa.ai/industries/real-estate)
- **All industry AI skills**: [krasa.ai/industries](https://krasa.ai/industries)
- **About KRASA AI**: [krasa.ai](https://krasa.ai)

## License

MIT — use these skills however you want.
