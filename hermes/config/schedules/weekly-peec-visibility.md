# Weekly Peec Visibility Schedule

Create this cron job from inside Hermes after MCP is configured:

```text
/cron add "weekly on monday at 09:00" "Use the Peec Visibility Operator instructions from /Users/cornelis/Projects/bookmo-agent-ops/hermes/config/agents/peec-visibility-operator.md, the strategist prompt from /Users/cornelis/Projects/bookmo-agent-ops/hermes/prompts/peec-visibility-strategist.md, the action reviewer prompt from /Users/cornelis/Projects/bookmo-agent-ops/hermes/prompts/peec-action-reviewer.md, the approval policy from /Users/cornelis/Projects/bookmo-agent-ops/docs/approval-policy.md, and the task schema from /Users/cornelis/Projects/bookmo-agent-ops/workflows/peec-visibility/action-task.schema.json. Pull Bookmo Peec actions for the last 30 days, read overview actions first, drill into the top owned/editorial/reference/UGC opportunities, classify candidates with the reviewer criteria, write a public-safe markdown strategy memo under /Users/cornelis/Projects/bookmo-agent-ops/docs/peec/actions/YYYY-MM-DD.md, and end with approval questions for any issue/PR/outreach/social/public work. Do not publish, send outreach, post publicly, delete or mutate Peec data, add credentials, or deploy." --name "Bookmo Peec Visibility Weekly"
```

Use `/cron run <job_id>` immediately after creation to test the output.
