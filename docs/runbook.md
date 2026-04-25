# Runbook

## Install Hermes

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
hermes setup
hermes model
hermes doctor
```

## Configure Peec MCP

Merge `hermes/config/mcp/peec.yaml` into `~/.hermes/config.yaml`.

Then start Hermes and verify:

```text
Tell me which MCP-backed tools are available.
List my Peec AI projects.
```

If config changes while Hermes is running:

```text
/reload-mcp
```

## Create Weekly Job

Use the command in `hermes/config/schedules/weekly-peec-visibility.md`.

Test immediately:

```text
/cron run <job_id>
```

## Expected Output

The weekly job writes:

```text
docs/peec/actions/YYYY-MM-DD.md
```

The memo should end with approval questions before issue creation, PR drafting,
outreach, publishing, or public posting.

