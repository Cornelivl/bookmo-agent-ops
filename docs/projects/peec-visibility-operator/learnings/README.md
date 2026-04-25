# Project Learnings

## Summary

- Long-running setup of a Hermes-backed SEO/GEO/GTM optimization operator using Peec AI MCP.
- Worth capturing because the workflow crosses MCP setup, approval policy, outbound-channel safety, measurement loops, and future agent resumability.
- Append to this file during execution when missing docs, weak prompts, MCP limitations, or validation gaps slow the project down.

## What Helped

- Repo-local `AGENTS.md` defines the operations repo boundary and says long-running work belongs in `docs/projects/<slug>/tasks.md`.
- Existing scaffold already includes Peec MCP config, strategist/reviewer prompts, approval policy, runbook, and architecture docs.
- Peec's public MCP docs provide a clear endpoint, OAuth setup path, tool reference, and action-drilldown workflow.

## What Slowed Things Down

- The existing tracker was useful but too memo-oriented for the expanded closed-loop operator goal.
- Peec public materials contain version drift: a launch blog describes read-only MCP, while current docs list write tools. Live Hermes tool discovery needs to be treated as authoritative.
- The repo is intentionally public, so future outputs need a redaction/public-safety pass before commit.

## Improvement Opportunities

### MCPs / Tools

- Add a local MCP/tool-discovery capture step that records the exact live Peec tool list after OAuth.
- Consider a dedicated action-ledger helper if the ledger becomes repetitive to maintain by hand.

### Skills

- The `project` skill is a good fit for this work because the tracker doubles as plan, state, and resume point.

### AGENTS / Docs

- Once email/social capabilities are chosen, add repo-local guidance for draft-only outbound channels and approval wording.

### Validation / Feedback Loops

- Make baseline capture mandatory before implementation so 7/14/30 day Peec measurement is meaningful.

### Delegation / Subagents

- Future read-heavy research can split cleanly into Peec tool discovery, outbound-channel capability design, and target repo implementation review.

## Recommended Follow-Ups

- Capture live Peec MCP tool discovery output after OAuth.
- Add an action-ledger schema and example entry before the first real implementation.
- Add channel-specific approval checklists for email and social/community drafting.

## Notes For Future Runs

- Treat Peec `get_actions` as the primary next-action signal, but require Bookmo relevance and evidence-quality review before execution.
- Keep public actions human-approved even after the agent proves useful; drafts, redacted docs, and non-public artifacts are the safe automation boundary.
