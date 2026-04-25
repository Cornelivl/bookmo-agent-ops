# Architecture

Hermes is the runtime for Bookmo's Peec Visibility Operator. This repo owns the
public-safe prompts, schedules, MCP templates, approval policy, and durable
strategy output that guide the operator.

The setup flow is also exported as an SVG for docs surfaces that do not render
Mermaid directly: [`docs/assets/peec-visibility-setup.svg`](assets/peec-visibility-setup.svg).

```mermaid
flowchart TD
    Repo[Bookmo agent-ops repo]
    Template[Peec MCP config templates]
    Prompts[Hermes prompts and schedule]
    Policy[Approval policy]
    Runtime[Hermes runtime]
    LocalConfig[Local Hermes config]
    OAuth[OAuth browser approval]
    Peec[Peec MCP]
    Tavily[Tavily MCP]
    PublicWeb[Public web sources]
    Weekly[Weekly visibility job]
    Memo[Public-safe strategy memo]
    Review[Human approval gate]
    Actions[GitHub issue, PR, content brief, or manual task]
    Measure[Peec 7, 14, and 30 day measurement]

    Repo --> Template
    Repo --> Prompts
    Repo --> Policy
    Template --> LocalConfig
    LocalConfig --> Runtime
    OAuth --> Runtime
    Runtime --> Peec
    Runtime --> Tavily
    Tavily --> PublicWeb
    Prompts --> Weekly
    Runtime --> Weekly
    Weekly --> Memo
    Memo --> Review
    Review --> Actions
    Actions --> Measure
    Measure --> Memo

    classDef repo fill:#eef2ff,stroke:#64748b,color:#0f172a
    classDef runtime fill:#ecfdf5,stroke:#16a34a,color:#052e16
    classDef external fill:#fff7ed,stroke:#f97316,color:#431407
    classDef output fill:#f8fafc,stroke:#94a3b8,color:#0f172a

    class Repo,Template,Prompts,Policy repo
    class Runtime,LocalConfig,Weekly runtime
    class OAuth,Peec,Tavily,PublicWeb external
    class Memo,Review,Actions,Measure output
```

## Runtime Components

- Hermes Agent installed on a local machine or VPS.
- Peec MCP remote HTTP server at `https://api.peec.ai/mcp`.
- Tavily MCP remote HTTP server at `https://mcp.tavily.com/mcp/` for public
  web search and source extraction.
- Optional GitHub MCP or local `gh` CLI.
- Repo-local strategy output under `docs/peec/actions/`.

## Research Boundary

Peec remains the source of truth for visibility actions, opportunity ranking,
and measurement. Tavily is supporting research infrastructure: use it to verify
that recommended public targets exist, extract public page content for review,
find current source citations, and check whether competitor or category claims
are already supported by public evidence.

## State

Durable state lives in Git:

- prompts
- policies
- project tracker
- weekly reports
- schemas

Hermes memory is useful but not authoritative.
