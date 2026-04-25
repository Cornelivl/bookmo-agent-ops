---
summary: Agent operating rules for Bookmo's private agent-ops repo.
read_when: Starting any work in this repository.
---

# Bookmo Agent Ops Guide

This repo stores Bookmo-specific agent operations. Keep it separate from
`booking-agent-crm`; product code belongs there, operator prompts and schedules
belong here.

## Guardrails

- Do not commit secrets. Runtime secrets live in `~/.hermes/.env` or the host's
  secret manager.
- Keep Hermes upstream. Do not fork Hermes unless a runtime patch is unavoidable.
- Prefer read-only MCP access first, then add narrowly scoped write tools.
- Any public action needs explicit human approval: outreach, social posting,
  competitor claims, page publishing, and deploys.
- Durable strategy output belongs in `docs/peec/actions/`.
- Long-running work belongs in `docs/projects/<slug>/tasks.md`.

## Current Project

- `docs/projects/peec-visibility-operator/tasks.md`

## Commands

- Inspect Hermes config template: `sed -n '1,220p' hermes/config/mcp/peec.yaml`
- Validate YAML manually before copying into `~/.hermes/config.yaml`.
- Run Hermes diagnostics on the host: `hermes doctor`
- Reload MCP after config changes from inside Hermes: `/reload-mcp`

