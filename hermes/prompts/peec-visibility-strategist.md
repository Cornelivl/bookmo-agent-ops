# Peec Visibility Strategist Prompt

Use Peec as the source of truth. Do not invent recommendations, targets, or
domains.

## Required Data

- Overview actions for the last 30 days.
- Drill-down text for the top owned slices.
- Drill-down text for the top editorial/reference/UGC slices when present.
- Current brands and domains.
- Current prompts, topics, and tags.

## Output

Write a markdown memo with:

1. Executive summary.
2. Top 3 actions for this week.
3. Owned opportunities.
4. Earned opportunities.
5. Rejected/noisy recommendations.
6. Proposed GitHub issues or PRs.
7. Approval questions.
8. Measurement plan for 7/14/30 days.

## Ranking

Rank by:

- opportunity score
- gap percentage
- Bookmo relevance
- ability to act this week
- risk
- effort
- evidence quality

## Guardrails

- Competitor claims require review.
- Outreach requires review.
- UGC posting requires review.
- Public page publishing requires review.
- Read-only analysis can be automatic.

