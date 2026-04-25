# Architecture

```text
Peec MCP
  -> Hermes Peec Visibility Operator
  -> weekly strategy memo
  -> approval gate
  -> GitHub issue / PR / content brief / manual outreach task
  -> 7/14/30 day Peec measurement
```

Hermes is the runtime. This repo owns Bookmo-specific prompts, schedules, and
decision policy.

## Runtime Components

- Hermes Agent installed on a local machine or VPS.
- Peec MCP remote HTTP server at `https://api.peec.ai/mcp`.
- Optional GitHub MCP or local `gh` CLI.
- Repo-local strategy output under `docs/peec/actions/`.

## State

Durable state lives in Git:

- prompts
- policies
- project tracker
- weekly reports
- schemas

Hermes memory is useful but not authoritative.

