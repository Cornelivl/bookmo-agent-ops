---
summary: Project map for the Bookmo agent-ops repo.
read_when: Starting work or deciding where a change belongs.
---

# Project Atlas

Use this file as the repo router. It tells agents and humans where to start,
which docs own which facts, and where new work should land.

## Start Here

1. Read `AGENTS.md` for repo guardrails, public-safety rules, and available
   local skills.
2. Read this atlas to choose the right doc or workflow area.
3. For long-running work, use `docs/projects/<slug>/tasks.md`.
4. For system shape, use `docs/architecture.md`.
5. For operational steps, use `docs/runbook.md`.

## Domain Map

| Area | Path | Purpose |
| --- | --- | --- |
| Repo guardrails | `AGENTS.md` | Safety rules, skills, and default commands for agent work. |
| System overview | `docs/architecture.md` | How Hermes, Peec MCP, approvals, GitHub, and measurement connect. |
| Runtime setup | `docs/runbook.md` | How to install Hermes, configure Peec MCP, and create the weekly job. |
| Azure infrastructure | `https://github.com/RidSib/Hermes-Cloud` | Separate Terraform/host provisioning repo; keep runtime secrets out of Git. |
| Approval policy | `docs/approval-policy.md` | What can run automatically, what needs review, and what needs explicit approval. |
| Active project tracker | `docs/projects/peec-visibility-operator/tasks.md` | Canonical execution state for the Peec Visibility Operator initiative. |
| Project learnings | `docs/projects/peec-visibility-operator/learnings/README.md` | Durable notes about what helped, slowed work down, or should improve. |
| Peec strategy memos | `docs/peec/actions/` | Public-safe weekly or ad hoc Peec action plans. |
| Hermes MCP config | `hermes/config/mcp/` | Source-controlled MCP templates to merge into `~/.hermes/config.yaml`. |
| Hermes prompts | `hermes/prompts/` | Reusable prompts for strategy, review, measurement, and future workers. |
| Hermes schedules | `hermes/config/schedules/` | Cron/job instructions for recurring agent loops. |
| Workflow schemas | `workflows/peec-visibility/` | Peec workflow documentation and structured task schema. |
| Generated outputs | `outputs/` | Local/generated artifacts; keep public-safe and ignore bulky/raw output. |

## Documentation Rules

- Put navigation and ownership facts in this atlas.
- Put system diagrams and component relationships in `docs/architecture.md`.
- Put exact setup commands in `docs/runbook.md`.
- Put permission boundaries in `docs/approval-policy.md`.
- Put active execution state in `docs/projects/<slug>/tasks.md`.
- Keep public repo content redacted. Do not commit secrets, lead details,
  private account identifiers, or sensitive strategy notes.

## Active Work

- Peec Visibility Operator:
  `docs/projects/peec-visibility-operator/tasks.md`

## Common Next Steps

- Configure Hermes runtime: follow `docs/runbook.md`.
- Review Peec workflow design: read `workflows/peec-visibility/README.md`.
- Add a new recurring loop: create a project tracker under `docs/projects/`,
  then add prompts/config under `hermes/`.
- Add a new tool integration: document the permission boundary first in
  `docs/approval-policy.md`, then add a narrow MCP template under
  `hermes/config/mcp/`.

