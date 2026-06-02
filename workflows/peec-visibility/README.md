# Peec Visibility Workflow

This workflow turns Peec recommendations into a weekly Bookmo growth plan.

## Data Source

Peec MCP tools:

- `list_projects`
- `list_brands`
- `list_prompts`
- `list_topics`
- `list_tags`
- `get_actions`
- `get_domain_report`
- `get_url_report`

Tavily MCP tools:

- `tavily-search`
- `tavily-extract`

Use Tavily only for public web research that supports Peec-derived decisions:
validating candidate source pages, extracting public reference content, finding
current citations, and checking the public basis for competitor or category
claims. Do not let Tavily search results create recommendations that are not
grounded in Peec actions.

## Weekly Flow

1. Pull overview actions.
2. Drill into owned slices by URL classification.
3. Drill into earned slices:
   - editorial by URL classification
   - reference by domain
   - UGC by domain
4. Normalize each recommendation into `workflows/peec-visibility/action-task.schema.json`.
5. Classify each task with `hermes/prompts/peec-action-reviewer.md`.
6. Use Tavily to validate public targets and gather public citation links for
   the highest-value candidates when the Peec evidence alone is not enough.
7. Assign an automation lane and state from `action-task.schema.json`.
8. Write a public-safe `docs/peec/actions/YYYY-MM-DD.md` memo.
9. Ask for human approval before creating GitHub issues, drafting PRs, drafting
   outreach, posting publicly, publishing, mutating Peec data, adding
   credentials, or deploying.

## Bookmo Constants

- Project: resolve `bookmo` from `list_projects` at runtime.
- Brand: resolve the Bookmo brand from `list_brands` at runtime.
- Canonical domain: `bookmo.ai`
- Product repo: `/Users/cornelis/Projects/booking-agent-crm`

Use the product repo read-only during autopilot runs to verify whether an
owned-site recommendation maps to a real route, SEO config, sitemap entry, docs
page, or GitHub issue/PR path. Ask for approval before changing product files,
opening issues, drafting PRs, publishing pages, or deploying.
