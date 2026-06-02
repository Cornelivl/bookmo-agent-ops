# Bookmo Agent Ops

Public operations repo for Bookmo's agentic workflows.

This repo is not a fork of Hermes. Hermes is the runtime; this repo owns the
Bookmo-specific configuration, prompts, approval rules, and public-safe workflow
memory. Do not store secrets, lead details, account identifiers, or sensitive
strategy notes here unless they are redacted.

## First Workflow

`Peec Visibility Operator` turns Peec AI visibility actions into a weekly plan:

1. Read Peec projects, brands, prompts, topics, tags, and actions.
2. Drill into owned, editorial, reference, and UGC recommendations.
3. Rank work by opportunity, relevance, effort, risk, and confidence.
4. Produce a public-safe markdown strategy memo under `docs/peec/actions/`.
5. Create issues or draft PRs only after explicit approval.

## Docs

- Repo map: `docs/atlas.md`
- System overview: `docs/architecture.md`
- Runtime runbook: `docs/runbook.md`
- Approval policy: `docs/approval-policy.md`
- Active tracker: `docs/projects/peec-visibility-operator/tasks.md`

## Hermes Setup

Install Hermes from the upstream project:

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
hermes setup
hermes model
```

Hermes stores runtime config in `~/.hermes/config.yaml` and secrets in
`~/.hermes/.env`. The files under `hermes/config/` are source-controlled
templates to merge into the runtime host.

Useful upstream docs:

- Quickstart: https://hermes-agent.nousresearch.com/docs/getting-started/quickstart/
- MCP: https://hermes-agent.nousresearch.com/docs/guides/use-mcp-with-hermes/
- Cron: https://hermes-agent.nousresearch.com/docs/guides/automate-with-cron/

## Safety Model

Default posture:

- Auto: read Peec, draft summaries, write public-safe local strategy docs.
- Auto: read the local `booking-agent-crm` repo for feasibility checks when a
  Peec recommendation maps to owned-site, SEO, docs, or GitHub work.
- Review: create GitHub issues, draft PRs, write content briefs.
- Manual approval: publish public content, send outreach, post in communities,
  merge or deploy product changes, or make competitor claims.
- Never by default: delete Peec data, send emails, post publicly, or deploy.
