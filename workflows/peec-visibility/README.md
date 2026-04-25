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

## Weekly Flow

1. Pull overview actions.
2. Drill into owned slices by URL classification.
3. Drill into earned slices:
   - editorial by URL classification
   - reference by domain
   - UGC by domain
4. Normalize each recommendation into `schemas/action-task.schema.json`.
5. Rank and classify each task.
6. Write `docs/peec/actions/YYYY-MM-DD.md`.
7. Ask for human approval before creating GitHub issues or PRs.

## Bookmo Constants

- Project id: `or_f6b948e9-4f91-4a52-944f-c7324fae7ac1`
- Brand id: `kw_8843c6ab-20ed-46a7-85ec-9d29272763dc`
- Canonical domain: `bookmo.ai`

