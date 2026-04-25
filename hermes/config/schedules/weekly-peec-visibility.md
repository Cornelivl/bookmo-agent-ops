# Weekly Peec Visibility Schedule

Create this cron job from inside Hermes after MCP is configured:

```text
/cron add "weekly on monday at 09:00" "Use the Peec Visibility Operator instructions from /Users/cornelis/Projects/bookmo-agent-ops/hermes/config/agents/peec-visibility-operator.md and the strategist prompt from /Users/cornelis/Projects/bookmo-agent-ops/hermes/prompts/peec-visibility-strategist.md. Pull Bookmo Peec actions for the last 30 days, drill into the top owned and earned opportunities, write a markdown strategy memo under /Users/cornelis/Projects/bookmo-agent-ops/docs/peec/actions/YYYY-MM-DD.md, and end with approval questions for any issue/PR/outreach work. Do not publish, send outreach, delete Peec data, or deploy." --name "Bookmo Peec Visibility Weekly"
```

Use `/cron run <job_id>` immediately after creation to test the output.

