# Skills Library — Real Estate

This directory contains all AI skills for real estate businesses. Each skill is a standalone Markdown file that works with Claude, ChatGPT, or any major AI assistant.

## Skill Categories

| Directory | Focus |
|-----------|-------|
| `_shared/` | Cross-industry skills (email drafter, meeting summarizer, etc.) |
| `operations/` | Day-to-day operational workflows |
| `sales/` | Sales, estimates, proposals, and lead management |
| `admin/` | Administrative, compliance, and back-office tasks |
| `customer-service/` | Client-facing communication and support |

## Skill File Format

Every skill follows this format:

```markdown
---
name: Skill Name
category: operations|sales|admin|customer-service
tools: [claude, chatgpt]
difficulty: beginner|intermediate|advanced
time_saved: "~X min/use"
version: 1.0
last_eval_score: null
---

# Skill Name

## Purpose
What this skill does and when to use it.

## When to Use
Specific scenarios where this skill saves time.

## Required Input
What the user needs to provide.

## Instructions
The actual prompt / workflow for the AI assistant.

## Example Output
What good output looks like.
```

## How to Use a Skill

1. Make sure you've run the setup wizard (`init/setup-wizard.md`) first
2. Open any skill file in your AI assistant
3. Provide the required input described in the skill
4. The AI will reference your `config.yml` for personalization

## Contributing New Skills

1. Follow the format above
2. Place in the appropriate category directory
3. Add a test case in `evals/test-cases/`
4. Open a PR with a description of what the skill does and why it's useful
