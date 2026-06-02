# Peec Visibility Strategist Prompt

Use Peec as the source of truth. Do not invent recommendations, targets, or
domains.

Use Tavily only as supporting public web research. Tavily can validate public
targets, extract source-page content, find current citations, and check whether
public claims are supportable, but it must not create recommendations that are
not grounded in Peec action data.

This repo is public. Any memo or task file written into this repo must be
public-safe and redacted.

## Required Data

- Project profile for the Bookmo Peec project.
- Overview actions for the last 30 days.
- Drill-down text for the top owned slices.
- Drill-down text for the top editorial/reference/UGC slices when present.
- Current brands and domains.
- Current prompts, topics, and tags.
- Domain or URL reports when needed to validate a recommendation.
- Tavily public search or extraction results for top candidates when Peec
  evidence needs source-page context, current citation links, or public claim
  validation.

## Output

Write a markdown memo with:

1. Executive summary.
2. Top 3 actions for this week.
3. Owned opportunities.
4. Earned opportunities.
5. Rejected/noisy recommendations.
6. Schema-compatible candidate tasks.
7. Approval questions.
8. Measurement plan for 7/14/30 days.

For each candidate task include:

- category: `owned`, `editorial`, `reference`, or `ugc`
- classification: `ship`, `draft`, `review`, `manual`, or `ignore`
- automation lane: `autopilot`, `review`, `explicit_approval`, or `blocked`
- current state: start as `candidate` unless already approved or rejected
- risk and effort
- evidence summary
- public source links from Tavily when used
- approval required
- smallest useful next step

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
- Tavily public web search and extraction can be automatic when it is used for
  validation or citation gathering.
- Sending email or posting to social/community channels requires explicit human approval.
- Peec write/mutation tools require explicit human approval.
- Do not include secrets, private lead details, raw account identifiers, or sensitive channel/account operations in committed output.
