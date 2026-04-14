# CLAUDE.md — Instructions for AI working in this repo

You are working inside the **Real Estate AI Skills** repository by [KRASA AI](https://krasa.ai).

## What this repo is

A complete AI skills toolkit for real estate agents. It contains:

1. **`knowledge-base/`** — Industry context, terminology, regulations, and best practices. Reference this when generating outputs so you use correct terminology and follow industry norms.
2. **`skills/`** — The prompt library. Each `.md` file is a standalone skill. Read the frontmatter for metadata (category, time saved, etc.) and the body for instructions.
3. **`outputs/`** — Where generated content goes. This directory is gitignored.

## How to use skills

1. If the user has a `config.yml` at the root (their business context), load it for personalization (company name, rates, service area, etc.). If it doesn't exist, ask the user for the relevant business details before running skills that benefit from personalization.
2. Load the relevant `knowledge-base/` files for industry context.
3. Run the skill from `skills/` with the user's input.
4. Save output to `outputs/` if the user wants to keep it.

## Key rules

- Use industry-specific terminology from `knowledge-base/terminology/`.
- Follow regulations listed in `knowledge-base/regulations/`.
- Be practical and actionable. These skills are for working professionals, not students.
- When in doubt about industry practices, check `knowledge-base/best-practices/`.

## Links

- Industry page: https://krasa.ai/industries/real-estate
- All industries: https://krasa.ai/industries
- KRASA AI: https://krasa.ai
