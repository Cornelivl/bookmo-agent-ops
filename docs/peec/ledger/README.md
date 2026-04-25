# Peec Action Ledger

This ledger turns Peec recommendations into a repeatable SEO/GEO/GTM operating loop.

The repo is public, so ledger entries must be public-safe. Do not write secrets,
lead/customer details, private account identifiers, raw prompt lists, exact private
Peec scores, OAuth material, or sensitive channel operations here.

## Lifecycle

Each Peec-derived task moves through this state machine:

`candidate` -> `reviewed` -> `approved` or `rejected` -> `drafted` ->
`implemented` -> `measuring_7d` -> `measuring_14d` -> `measuring_30d` ->
`closed_keep`, `closed_improve`, `closed_retry`, or `closed_ignore`.

## Decision lanes

- `quick_win`: high or medium opportunity, core Bookmo relevance, low risk,
  small effort, reviewable artifact possible this week, and measurable.
- `needs_planning`: strong signal, but requires page architecture, product
  positioning, engineering, design, or claim review.
- `needs_upskilling`: execution depends on standards or norms that must be
  learned/documented first, such as Wikipedia notability, community posting,
  editorial outreach, YouTube production, or technical SEO best practices.
- `repeatable_playbook`: a task class that should become a template after one
  successful manual run.
- `blocked_manual`: requires explicit approval, public posting, outreach,
  publishing, deploys, Peec mutation, unavailable credentials, or unclear source
  evidence.

## Self-improvement rule

Every completed action must produce one learning:

- `keep`: measurable lift or clear strategic value; repeat the pattern.
- `improve`: useful but incomplete; revise the playbook before repeating.
- `retry`: promising but failed because timing, indexing, source quality, or
  execution was weak.
- `ignore`: noisy or low-value; demote similar future recommendations.

Future weekly memos should use the latest ledger outcomes to promote or demote
similar Peec action types before selecting the next task.
