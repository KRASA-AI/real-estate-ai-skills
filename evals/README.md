# Evaluation Framework

This directory contains the framework for measuring and improving skill quality over time.

## Contents

| File/Directory | Purpose |
|---------------|---------|
| `rubric.yml` | Grading criteria — 6 dimensions, weighted scoring |
| `test-cases/` | Input/expected-output pairs for each skill |
| `results/` | Historical evaluation scores (tracked in git) |

## How Evals Work

1. Each skill is run against its test cases
2. Output is graded on 6 dimensions (clarity, specificity, industry fit, output quality, personalization, efficiency)
3. Scores are recorded with timestamps
4. Lowest-scoring skills are flagged for improvement
5. Improved versions are re-evaluated before replacing originals

## Rubric Dimensions

| Dimension | Weight | What it measures |
|-----------|--------|-----------------|
| Clarity | 20% | Is the skill prompt clear and unambiguous? |
| Specificity | 20% | Does it give enough detail for useful output? |
| Industry Fit | 20% | Correct terminology, real workflows, genuine pain points? |
| Output Quality | 20% | Is the output immediately usable in a real business? |
| Personalization | 10% | Does it leverage config.yml effectively? |
| Efficiency | 10% | Minimal back-and-forth to get good output? |

See `rubric.yml` for the full scoring guide.
