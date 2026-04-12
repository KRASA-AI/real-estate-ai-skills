# CLAUDE.md — Instructions for AI working in this repo

You are working inside the **Real Estate AI Skills** repository by [KRASA AI](https://krasa.ai).

## What this repo is

A complete AI skills toolkit for real estate agents. It contains:

1. **`init/`** — Run `setup-wizard.md` first. It walks the user through configuring this toolkit for their specific business. The output is `config.yml` at the root.
2. **`knowledge-base/`** — Industry context, terminology, regulations, and best practices. Reference this when generating outputs so you use correct terminology and follow industry norms.
3. **`skills/`** — The prompt library. Each `.md` file is a standalone skill. Read the frontmatter for metadata (category, time saved, etc.) and the body for instructions.
4. **`outputs/`** — Where generated content goes. This directory is gitignored.
5. **`evals/`** — Evaluation framework. Contains the rubric and test cases for measuring skill quality.

## How to use skills

1. Check if `config.yml` exists at the root. If not, run `init/setup-wizard.md` first.
2. Load `config.yml` to get the user's business context (company name, rates, tools, etc.).
3. Load the relevant `knowledge-base/` files for industry context.
4. Run the skill from `skills/` with the user's input.
5. Save output to `outputs/` if the user wants to keep it.

## Key rules

- Always reference `config.yml` for personalization. Use the company name, rates, service area, etc.
- Use industry-specific terminology from `knowledge-base/terminology/`.
- Follow regulations listed in `knowledge-base/regulations/`.
- Be practical and actionable. These skills are for working professionals, not students.
- When in doubt about industry practices, check `knowledge-base/best-practices/`.

## Links

- Industry page: https://krasa.ai/industries/real-estate
- All industries: https://krasa.ai/industries
- KRASA AI: https://krasa.ai
