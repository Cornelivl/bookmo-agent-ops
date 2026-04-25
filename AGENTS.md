---
summary: Agent operating rules for Bookmo's public agent-ops repo.
read_when: Starting any work in this repository.
---

# Bookmo Agent Ops Guide

This public repo stores Bookmo-specific agent operations. Keep it separate from
`booking-agent-crm`; product code belongs there, operator prompts and schedules
belong here.

## Guardrails

- Do not commit secrets. Runtime secrets live in `~/.hermes/.env` or the host's
  secret manager.
- Do not commit sensitive operational data. Strategy output, measurement notes,
  lead details, account identifiers, and channel plans must be public-safe or
  redacted before they are written here.
- Keep Hermes upstream. Do not fork Hermes unless a runtime patch is unavoidable.
- Prefer read-only MCP access first, then add narrowly scoped write tools.
- Any public action needs explicit human approval: outreach, social posting,
  competitor claims, page publishing, and deploys.
- Durable public-safe strategy output belongs in `docs/peec/actions/`.
- Long-running work belongs in `docs/projects/<slug>/tasks.md`.

## Current Project

- `docs/projects/peec-visibility-operator/tasks.md`

## Docs Router

- Start with `docs/atlas.md` when deciding where a change belongs.
- Use `docs/architecture.md` for the system overview and component flow.
- Use `docs/runbook.md` for setup and operational commands.
- Use `docs/approval-policy.md` for permission boundaries.
- Use `docs/projects/<slug>/tasks.md` for active long-running work.

## Local Skills

This repo intentionally links a small shared-skill set into `.agents`,
`.codex`, `.claude`, and `.cursor` instead of mirroring every machine skill.
Available core skills:

- `project` for long-running project trackers.
- `secret-management` for runtime credentials and host secrets.
- `brave-search` for external research.
- `agent-browser` for browser/UI automation.
- `architecture-docs` for system docs.
- `create-cli` for command/workflow UX.
- `markdown-converter` for document ingestion.

Add more skills only when the workflow needs them.

## Commands

- Inspect Hermes config template: `sed -n '1,220p' hermes/config/mcp/peec.yaml`
- Validate YAML manually before copying into `~/.hermes/config.yaml`.
- Run Hermes diagnostics on the host: `hermes doctor`
- Reload MCP after config changes from inside Hermes: `/reload-mcp`
