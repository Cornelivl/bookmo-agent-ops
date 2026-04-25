# Peec Visibility Operator

## Goal

Set up a Hermes-backed workflow that turns Bookmo's Peec AI visibility data into
a recurring, reviewable growth plan.

## Behavior Contract

The operator reads Peec data, ranks actions, drafts strategy, and asks for
approval before any public or mutating action. It must not publish, send
outreach, post publicly, delete Peec configuration, or deploy without explicit
human approval.

## Desired Flow

1. Hermes runs the weekly Peec visibility job.
2. The operator pulls Bookmo Peec actions and supporting project metadata.
3. It drills into owned and earned opportunities.
4. It writes a dated strategy memo.
5. It proposes next actions and approval questions.
6. After approval, a separate follow-up can create issues, briefs, or PR drafts.

## Scope

- Hermes config templates.
- Peec MCP read-heavy configuration.
- Prompt and schedule scaffolding.
- Approval policy.
- Weekly strategy output format.

## Non-Goals

- Forking Hermes.
- Building a custom dashboard.
- Sending outreach automatically.
- Posting to social/community channels.
- Giving Hermes production deploy permissions.

## Impacted Areas

- Private repo `bookmo-agent-ops`.
- Peec MCP access.
- Optional future GitHub issue/PR workflows.

## Done When

- Private repo exists and contains initial config/docs/prompts.
- Peec MCP setup is documented.
- Weekly Peec visibility schedule is documented.
- Approval policy is explicit.
- A future agent can resume from this tracker.

## Validation / Test Plan

- Confirm repo is private on GitHub.
- Confirm no secrets are committed.
- Confirm `peec.yaml` uses a read-heavy MCP allowlist.
- Confirm Hermes setup docs link to upstream installation, MCP, and cron docs.

## Milestones

- [x] Create repo scaffold.
- [x] Add Hermes MCP templates.
- [x] Add Peec operator prompts and schedule.
- [x] Add approval policy and runbook.
- [ ] Configure Hermes on the runtime host.
- [ ] Authorize Peec OAuth in Hermes.
- [ ] Run first weekly memo manually.

## Current Batch

| Item | Owner | Status | Notes |
| --- | --- | --- | --- |
| Initial repo scaffold | Codex | Done | Created local repo and initial files. |
| GitHub repo creation | Codex | Pending | Create private remote and push initial scaffold. |
| Runtime Hermes setup | Human/Codex | Pending | Requires choosing machine/VPS and completing Hermes interactive auth. |

## Decisions

- Use `bookmo-agent-ops` instead of a Hermes fork.
- Keep Hermes upstream and treat this repo as Bookmo-specific configuration.
- Start with Peec visibility only before adding more loops.
- Use read-heavy MCP access by default.

## Open Questions / Blockers

- Which host should run Hermes long term: local Mac, VPS, or existing ops host?
- Does Hermes support Peec MCP OAuth browser auth cleanly against
  `https://api.peec.ai/mcp` in the target runtime?

## Progress Log

- 2026-04-25: Created initial repo scaffold with Hermes config templates, Peec
  operator prompts, schedule instructions, approval policy, and tracker.

