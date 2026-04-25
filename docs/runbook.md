# Runbook

## Setup Flow

![Peec Visibility Operator setup flow](assets/peec-visibility-setup.svg)

The Mermaid source for this SVG lives at
`docs/assets/peec-visibility-setup.mmd`. The same diagram is embedded in
`docs/architecture.md` for renderers that support Mermaid directly.

## Install Hermes

Azure VM provisioning is tracked separately in the Hermes Cloud infrastructure
repo: `https://github.com/RidSib/Hermes-Cloud`. Use that repo for Terraform and
host bootstrap work; use this repo for the Bookmo operator prompts, schedules,
MCP templates, and public-safe outputs.

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
hermes setup
hermes model
hermes doctor
```

## Model Policy

The local Hermes validation host keeps OpenAI Codex `gpt-5.5` as the default
model for Peec operator work.

Use the default for:

- Peec MCP reads, weekly strategy memos, and action-ledger updates.
- Repo edits, GitHub issue/PR drafting, and workflow automation.
- Work where Codex tool use and local coding behavior are the important part.

Use Claude only as an explicit switch, not as the default:

- `/model opus` for independent strategy critique, positioning review,
  red-team review, or narrative-heavy synthesis.
- `/model sonnet` for lower-cost Claude review, copy critique, and second-pass
  content feedback.

Claude requires Anthropic auth on the Hermes host. Store the credential only in
local Hermes auth or `~/.hermes/.env`; never commit it to this repo.

```bash
hermes auth add anthropic
# or add ANTHROPIC_API_KEY to ~/.hermes/.env
```

The local host also defines these model aliases in `~/.hermes/config.yaml`:

```yaml
model_aliases:
  opus:
    model: claude-opus-4-6
    provider: anthropic
  sonnet:
    model: claude-sonnet-4-6
    provider: anthropic
```

## Configure Peec MCP

Merge `hermes/config/mcp/peec.yaml` into `~/.hermes/config.yaml`.
The Peec endpoint is path-scoped at `https://api.peec.ai/mcp`; keep the
`oauth.preserve_server_url: true` setting from the template so OAuth resource
validation uses the full `/mcp` URL instead of only `https://api.peec.ai`.

Peec uses OAuth for MCP. Do not put Peec credentials in this repo or in
`~/.hermes/.env`; Hermes stores MCP OAuth tokens under its runtime home.

### Azure / Headless Host OAuth

If Hermes runs on an Azure VM, do the first OAuth authorization from an SSH
session on that VM:

```bash
ssh -L 33418:127.0.0.1:33418 <azure-user>@<azure-host>
hermes mcp add peec-ai --url https://api.peec.ai/mcp --auth oauth
```

When Hermes prints the authorization URL, open it in your local browser. The
SSH tunnel forwards the local OAuth callback to the VM. If Hermes reports a
different localhost callback port, reconnect SSH with that port forwarded
instead.

Then start Hermes and verify:

```text
Tell me which MCP-backed tools are available.
List my Peec AI projects.
```

If config changes while Hermes is running:

```text
/reload-mcp
```

## Configure Tavily MCP

Merge `hermes/config/mcp/tavily.yaml` into `~/.hermes/config.yaml`.
Tavily is used for public web research that supports Peec recommendations:
source validation, public citation gathering, current SERP context, and page
content extraction.

Prefer OAuth against `https://mcp.tavily.com/mcp/`. Tavily also supports API-key
configuration, but do not commit an API key or an API-key-bearing MCP URL. If a
Hermes host cannot complete OAuth, store `TAVILY_API_KEY` only in
`~/.hermes/.env` and adapt the host-local config outside this repo.

After merging the template, start Hermes and verify:

```text
Tell me which Tavily MCP tools are available.
Search the public web for Bookmo AI and summarize the top public sources.
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

## Repo Boundary

- Keep Azure/Terraform provisioning in `https://github.com/RidSib/Hermes-Cloud`.
- Keep Bookmo operator instructions, schedules, public-safe reports, and action
  ledgers in this repo.
- Only commit `.example` secret files. Real Telegram, model-provider, Peec,
  GitHub, cloud, or OAuth secrets stay out of Git.
