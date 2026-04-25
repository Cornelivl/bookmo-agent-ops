# Peec Visibility Operator

## Goal

Set up Hermes as a governed SEO/GEO/GTM optimization operator that reads Bookmo's Peec AI visibility data, turns opportunities into approved implementation plans, executes through narrowly scoped capabilities, monitors 7/14/30 day results, and iterates.

## Why / Impact

Peec AI surfaces AI-search visibility gaps, cited sources, competitive mentions, and action recommendations. Hermes should make that data operational: prioritize the highest-leverage work, draft or implement safe changes, coordinate approvals for public actions, and prove whether each action improved Bookmo's visibility or GTM signal.

## Behavior Contract

### Current Behavior

- The repo contains an initial Hermes/Peec scaffold with MCP config, prompts, a weekly schedule note, runbook, architecture note, approval policy, and curated repo-local shared skills.
- The current flow is read-heavy and memo-oriented: Hermes is expected to read Peec data and write a weekly markdown strategy memo.
- Runtime Hermes setup, Peec OAuth authorization, and the first manual weekly memo are still incomplete.
- Outbound capabilities such as email and social media access are not configured as executable channels.
- There is no durable action ledger that connects a Peec recommendation to an approved task, implementation artifact, measurement baseline, and follow-up result.
- The project currently treats social posting, outreach, Peec mutation, and public publishing as manual-approval actions.

### Desired Behavior

- Hermes connects to Peec AI MCP at `https://api.peec.ai/mcp` through Streamable HTTP/OAuth and verifies access by listing Peec projects.
- Hermes runs a weekly visibility loop and can also run an ad hoc investigation when prompted.
- Hermes gathers project context first: projects, own brand, competitor brands, models, prompts, topics, tags, brand report, domain report, URL report, and Peec action recommendations.
- For Peec actions, Hermes always calls `get_actions` with `scope=overview` first, then drills into `owned`, `editorial`, `reference`, or `ugc` slices before recommending implementation.
- Hermes converts recommendations into candidate tasks with evidence, source links, expected impact, effort, risk, channel, owner, approval requirement, and measurement window.
- Hermes classifies each candidate as `ship`, `draft`, `review`, `manual`, or `ignore` using the action reviewer prompt.
- Hermes may automatically produce public-safe artifacts in this repo: redacted strategy memos, content briefs, GitHub issue drafts, PR drafts, email drafts, social drafts, and measurement notes.
- Hermes separates work into automation lanes:
  - `autopilot`: read data, write public-safe docs, draft non-public artifacts, and update the action ledger.
  - `review`: create GitHub issues, draft PRs, draft content, draft outreach, and draft social/community posts for human review.
  - `explicit approval`: send email, post publicly, publish pages, deploy, mutate Peec configuration, or make public competitor claims.
  - `blocked`: actions requiring missing credentials, unsupported tools, legal/brand review, or unclear source evidence.
- Each action follows a state machine: `candidate` -> `reviewed` -> `approved` or `rejected` -> `drafted` -> `implemented` -> `measuring_7d` -> `measuring_14d` -> `measuring_30d` -> `closed_keep`, `closed_improve`, `closed_retry`, or `closed_ignore`.
- Approved implementation work records a baseline before execution and a follow-up schedule for 7/14/30 day measurement.
- The measurement loop compares Peec visibility, share of voice, sentiment, average position, domain retrieval/citation metrics, URL citation metrics, action scores, and any available GTM evidence such as leads, demos, search-console movement, CRM source notes, or qualified inbound mentions.
- Measurement notes must record Peec data windows and known refresh lag; do not judge an action before Peec has had enough fresh prompt/chat/source data to reflect the change.
- New capabilities are added by allowlist: start read-only, document credentials and approval boundaries, test with non-public drafts, then enable narrow write actions only after the loop proves useful.
- This repo is intentionally public; committed workflow memory must be public-safe and redacted.
- Secrets stay out of Git and live in `~/.hermes/.env` or the host secret manager.
- Sensitive strategy notes, lead details, account identifiers, and channel-specific operational data must stay outside this repo unless redacted.

### Out of Contract

- Hermes does not send outreach, post publicly, publish website changes, deploy, or mutate Peec configuration without explicit human approval.
- Hermes does not invent recommendations, target domains, competitor claims, or performance results that are not grounded in Peec or verified external evidence.
- Hermes does not replace human GTM judgment for brand positioning, partnership decisions, pricing, or legal review.
- Hermes does not become a custom analytics dashboard in this project.

## Scope / Non-Goals

### In Scope

- Hermes runtime configuration for Peec AI MCP.
- Peec visibility strategist and action reviewer prompts.
- Weekly and ad hoc workflow definitions.
- A durable action ledger for recommendation, approval, implementation, and measurement state.
- Capability planning for GitHub, email, social/community channels, and future tools.
- Approval policy updates for draft-vs-send boundaries.
- Public-safe strategy outputs under `docs/peec/actions/`.
- Public-safe measurement outputs under `docs/peec/measurements/`.
- Optional GitHub issue/PR workflows against `booking-agent-crm` after approval.
- External GTM evidence sources when available, such as Google Search Console, CRM/source tracking, analytics, email replies, or social engagement exports.

### Out of Scope

- Forking Hermes or patching Hermes internals unless an upstream limitation blocks the project.
- Building a custom dashboard.
- Fully automated public outreach or posting.
- Paid ad optimization.
- Production deploy permissions for Hermes.
- Destructive Peec writes such as deleting brands, prompts, tags, or topics.

## Desired Flow (Happy Path)

1. Hermes runs the weekly Peec visibility job on the configured host.
2. Hermes lists Peec projects, resolves the Bookmo project, maps own brand and competitors, and records the active models/topics/tags/prompts.
3. Hermes pulls the last 30 days of brand, domain, URL, and action data, then drills into the highest-opportunity owned, editorial, reference, and UGC actions.
4. Hermes writes a dated strategy memo under `docs/peec/actions/YYYY-MM-DD.md`.
5. Hermes converts the top recommendations into action-ledger entries with evidence, expected impact, risk, approval need, and a 7/14/30 day measurement plan.
6. Hermes asks for approval on any public, mutating, or outbound action.
7. After approval, Hermes creates the smallest useful execution artifact: GitHub issue, PR draft, content brief, email draft, social draft, or manual task.
8. Hermes records the implementation date, artifact links, and baseline metrics.
9. Hermes runs follow-up checks at 7/14/30 days and writes measurement notes under `docs/peec/measurements/`.
10. Hermes classifies the result as keep, improve, retry, ignore, or escalate, then feeds that learning into the next weekly plan.

## Impacted Areas

- `AGENTS.md`
- `README.md`
- `docs/architecture.md`
- `docs/approval-policy.md`
- `docs/runbook.md`
- `docs/projects/peec-visibility-operator/tasks.md`
- `docs/projects/peec-visibility-operator/learnings/README.md`
- `docs/peec/actions/`
- `docs/peec/measurements/`
- `docs/peec/ledger/`
- `hermes/config/mcp/peec.yaml`
- `hermes/config/mcp/*.yaml` for future email, GitHub, browser, and social capabilities
- `hermes/config/schedules/weekly-peec-visibility.md`
- `hermes/prompts/peec-visibility-strategist.md`
- `hermes/prompts/peec-action-reviewer.md`
- `hermes/prompts/*` for future implementation, measurement, and channel-specific prompts
- `workflows/peec-visibility/action-task.schema.json`
- Target implementation repo: `../booking-agent-crm`

## Context / Constraints

- Date refreshed: 2026-04-25
- Repo: `/Users/cornelis/Projects/bookmo-agent-ops`
- Repo visibility: public by design.
- Current Hermes config is a source-controlled template; runtime config lives in `~/.hermes/config.yaml`.
- Peec MCP setup docs confirm the MCP server URL is `https://api.peec.ai/mcp`, with OAuth on first connection.
- Peec MCP tools include read tools for projects, brands, topics, tags, models, prompts, chats, reports, source content, and actions.
- Peec MCP tools also include owner-gated write tools for brands, prompts, tags, and topics; these require explicit approval and should remain excluded until there is a concrete use case.
- Peec docs describe `get_actions` as a two-step flow: call `scope=overview`, then drill into `owned`, `editorial`, `reference`, or `ugc`.
- The Peec blog states MCP was read-only at launch, while current docs list write tools; treat this as version drift and verify live tool availability in Hermes before enabling any write path.
- Machine-wide git automation may auto-stage, commit, and push after agent turns; do not run `git commit` or `git push` manually unless requested.
- Current git status includes unrelated dirty agent config directories and `AGENTS.md`; do not revert them.

## Done When

- [ ] Hermes is installed or selected on the target runtime host.
- [ ] Peec MCP is configured and OAuth is authorized in Hermes.
- [ ] Hermes can list Bookmo Peec projects and read current Peec visibility data.
- [ ] The weekly workflow can produce one dated, public-safe strategy memo from live Peec data.
- [ ] The action ledger exists and records recommendation, automation lane, state, approval, implementation, baseline, and measurement state.
- [ ] Approval policy clearly separates public-safe docs, non-public drafts, reviewed actions, and explicit-send/public actions.
- [ ] At least one Peec-derived owned/content task is planned and approved.
- [ ] At least one safe implementation artifact is created after approval, such as a GitHub issue, PR draft, or content brief.
- [ ] Measurement follow-ups are scheduled or documented for 7/14/30 days.
- [ ] Measurement notes record the Peec data window, refresh assumptions, and any non-Peec GTM evidence used.
- [ ] Email and social capabilities have a documented phased plan and remain draft-only until explicitly approved.
- [ ] Validation confirms no secrets or sensitive unredacted operational data are committed and MCP allowlists match the intended permission level.
- [ ] A future agent can resume from this tracker without rereading the entire chat.

## Milestones

- [x] Milestone 1 - Create repo scaffold. Acceptance: public agent-ops repo contains initial Hermes docs and config templates. Validate: inspect repo files and no committed secrets.
- [x] Milestone 2 - Add curated repo-local shared skills. Acceptance: portable skill set exists across `.agents`, `.codex`, `.claude`, and `.cursor`. Validate: inspect skill directories.
- [x] Milestone 3 - Add Hermes MCP templates. Acceptance: Peec MCP config points at the documented Streamable HTTP endpoint. Validate: `sed -n '1,220p' hermes/config/mcp/peec.yaml`.
- [x] Milestone 4 - Add Peec operator prompts and schedule. Acceptance: strategist, reviewer, and weekly schedule docs exist. Validate: inspect `hermes/prompts/` and `hermes/config/schedules/`.
- [x] Milestone 5 - Add approval policy and runbook. Acceptance: public/outbound actions require approval. Validate: inspect `docs/approval-policy.md` and `docs/runbook.md`.
- [ ] Milestone 6 - Configure Hermes runtime. Acceptance: Hermes host is selected, config is merged, and `hermes doctor` passes. Validate: run `hermes doctor` on the host.
- [ ] Milestone 7 - Authorize and smoke-test Peec MCP. Acceptance: Hermes can list Peec projects and active tools. Validate: ask Hermes to list tools and list Peec AI projects.
- [ ] Milestone 8 - Produce first live Peec strategy memo. Acceptance: `docs/peec/actions/YYYY-MM-DD.md` exists and is grounded in live Peec data. Validate: manually review cited Peec actions, reports, and approval questions.
- [ ] Milestone 9 - Add durable action ledger. Acceptance: schema/template records evidence, automation lane, state, approval, implementation, baseline, measurement windows, and result classification. Validate: fill it with at least one real Peec recommendation.
- [ ] Milestone 10 - Execute one approved owned/content action. Acceptance: approved artifact exists as an issue, PR draft, content brief, or repo change. Validate: artifact links back to Peec evidence and action ledger entry.
- [ ] Milestone 11 - Add measurement loop. Acceptance: 7/14/30 day follow-up template and schedule exist, including Peec data-window notes and non-Peec GTM evidence slots. Validate: first action has scheduled or documented measurement checkpoints.
- [ ] Milestone 12 - Plan outbound capabilities. Acceptance: email and social access are documented in a capability gate matrix with draft-first behavior, approval gates, credentials, validation steps, and rollback/disable steps. Validate: approval policy and runbook reflect the channel boundaries.
- [ ] Milestone 13 - Closeout and archive. Acceptance: scoped work is complete or remaining items are explicitly descoped. Validate: tracker, learnings, and docs are updated, then archive per project skill.

## Review Pass

### Reviewer Checklist

- Verify the plan does not assume Peec write tools are available or safe before live MCP discovery.
- Verify every public/outbound channel has a draft-only phase before send/post access.
- Verify action scoring cannot select noisy Peec recommendations without Bookmo relevance checks.
- Verify implementation artifacts always preserve the Peec evidence chain.
- Verify measurement uses pre-action baselines instead of only post-action snapshots.
- Verify email/social credentials are not added to Git and are isolated by least privilege.
- Verify the target implementation repo is not modified without explicit task approval.
- Verify social/community posting rules account for platform-specific anti-spam and account-risk concerns.
- Verify competitor claims have a review step and source evidence.

### Findings Folded In

- Added explicit automation lanes so "fully agentic" does not blur public-safe docs, non-public drafting, and public sending/posting.
- Added an action state machine so candidate tasks can be resumed, measured, and closed without ambiguous status labels.
- Expanded measurement beyond Peec-only metrics to include available GTM evidence when it exists.
- Added Peec data-window and refresh-lag requirements so 7/14/30 day reviews are not judged on stale data.
- Added a capability gate matrix requirement for email/social tools before any outbound capability is enabled.

## Execution Rules

- Keep work scoped to the current milestone unless the tracker explicitly expands scope.
- Run validation after each milestone or risky batch and fix failures before advancing.
- Continue working until the scoped project is done or a true blocker requires human input; do not stop after one completed task if more actionable work remains.
- When `Done When` is satisfied and validation is acceptable, archive the project directly; ask only if completion is materially uncertain.
- Unless repo guidance says otherwise, archiving means moving the tracker to `docs/projects/archive/peec-visibility-operator/tasks.md`; create the archive folders if missing.
- Update this tracker whenever the plan changes materially or before ending the run.
- If project-critical ambiguity would stall progress later, ask targeted follow-up questions now and record the answers here.
- Use `Current Batch` as the live execution board and primary resume point.
- If `Current Batch` is empty or stale, rebuild it from the remaining milestones and backlog before continuing.
- Keep `tasks.md` single-writer; delegated work can write topic-based notes under `docs/projects/peec-visibility-operator/resources/`.
- For this project, keep a closeout learnings task that reviews `docs/projects/peec-visibility-operator/learnings/README.md` before archive.
- Before starting delegated work, add or update the delegated row in `Current Batch`.

## Decisions

- Use `bookmo-agent-ops` instead of a Hermes fork.
- Keep Hermes upstream and treat this repo as Bookmo-specific configuration, prompts, approval rules, and workflow memory.
- Start with read-heavy Peec workflows, then add narrowly scoped write/outbound capabilities after a live memo and action ledger prove the loop.
- Treat email and social access as draft-first capabilities; sending or posting requires explicit human approval.
- Use Peec `get_actions` as the primary "what should we do next" signal, but require reviewer classification before execution.
- Record baselines before each approved action so later measurement can attribute change direction more honestly.
- Keep durable public-safe strategy and measurement output in Git, not only in Hermes memory.
- Because the repo is public, keep durable output redacted and public-safe.
- Use the action state machine in this tracker as the canonical lifecycle for Peec-derived work.

## Open Questions / Blockers

- Which host should run Hermes long term: local Mac, VPS, or existing ops host?
- Which Peec project is the canonical Bookmo project if the account exposes more than one?
- Which email account/provider should Hermes use for drafting, and should send access be disabled at the tool layer or controlled only by approval policy?
- Which social/community channels matter first: LinkedIn, X, Reddit, YouTube comments, forums, or others?
- Should GitHub implementation happen as issues only at first, or may Hermes draft PRs against `booking-agent-crm` after approval?
- What is the first success metric target: visibility, share of voice, sentiment, average position, source retrieval, citations, qualified leads, or a blended score?
- What non-Peec GTM evidence is available now, if any: Search Console, analytics, CRM source fields, email replies, social analytics, or manual lead notes?
- Which fields must be redacted from public-safe strategy and measurement outputs?

## Current Batch

| Status | Work Item | Role | Resource |
| --- | --- | --- | --- |
| done | Refresh tracker into a full closed-loop Hermes + Peec SEO/GEO/GTM optimization plan | parent | `docs/projects/peec-visibility-operator/tasks.md` |
| done | Run skeptical review pass and fold high-signal risks into the tracker | parent | `docs/projects/peec-visibility-operator/tasks.md` |
| done | Bootstrap project learnings file for future closeout | parent | `docs/projects/peec-visibility-operator/learnings/README.md` |
| todo | Select the Hermes runtime host and verify local runtime prerequisites | parent | `docs/runbook.md` |

## Backlog / Remaining Work

- [ ] Select and document the Hermes runtime host.
- [ ] Define the redaction policy for public-safe strategy, ledger, and measurement outputs.
- [ ] Merge Peec MCP config into `~/.hermes/config.yaml` on the host.
- [ ] Run `hermes doctor` on the host and record the result.
- [ ] Complete Peec OAuth and verify "List my Peec AI projects".
- [ ] Refresh `hermes/config/mcp/peec.yaml` against live tool discovery, including whether write tools appear.
- [ ] Add a Peec source-of-truth prompt that forces `overview` before action drill-down.
- [ ] Create `docs/peec/actions/` memo template.
- [ ] Create `docs/peec/measurements/` follow-up template.
- [ ] Create `docs/peec/ledger/` and define the action state machine fields.
- [ ] Design and add the action ledger schema/template.
- [ ] Produce the first live weekly strategy memo.
- [ ] Review and approve one owned/content action for implementation.
- [ ] Create the first approved GitHub issue, PR draft, or content brief.
- [ ] Add a measurement follow-up schedule for the first approved action.
- [ ] Update approval policy for email/social draft-vs-send boundaries.
- [ ] Add email capability plan with credential location, tool choice, draft-only test, and approval gate.
- [ ] Add social/community capability plan with target platforms, account-risk constraints, draft-only test, and approval gate.
- [ ] Add a capability gate matrix covering Peec, GitHub, email, social/community, browser, and target repo access.
- [ ] Decide which non-Peec GTM evidence sources should be included in measurement notes.
- [ ] Add repo docs if the execution workflow changes materially.
- [ ] Validate no secrets or sensitive unredacted operational data are committed.
- [ ] Review and finalize `docs/projects/peec-visibility-operator/learnings/README.md`.
- [ ] Close out and archive the tracker when scoped work is complete.

## Validation / Test Plan

- Inspect repo guidance: `sed -n '1,220p' AGENTS.md`.
- Confirm Peec config template: `sed -n '1,220p' hermes/config/mcp/peec.yaml`.
- Confirm approval boundaries: `sed -n '1,220p' docs/approval-policy.md`.
- Confirm no secrets or sensitive unredacted operational data are committed: `git status --short` and targeted inspection of env/config/output files.
- On the Hermes host, run `hermes doctor`.
- In Hermes, ask: `Tell me which MCP-backed tools are available.`
- In Hermes, ask: `List my Peec AI projects.`
- For the first memo, manually verify that each recommended task references Peec action/report evidence.
- For the first memo, manually verify that committed content is public-safe and redacted.
- For the first implementation artifact, verify that the action ledger has baseline metrics and follow-up dates before execution.
- For each measurement note, verify that the Peec data window starts after the implementation date or explicitly documents why the measurement is still provisional.
- For outbound channels, test draft creation only before enabling any send/post flow.

## Progress Log

- 2026-04-25: [DONE] Created initial repo scaffold with Hermes config templates, Peec operator prompts, schedule instructions, approval policy, and tracker.
- 2026-04-25: [DONE] Added portable repo-local copies of curated shared skills, including `project`, to `.agents`, `.codex`, `.claude`, and `.cursor`.
- 2026-04-25: [DONE] Refreshed project tracker into a closed-loop Hermes + Peec SEO/GEO/GTM optimization plan with approval-gated email/social capability expansion.
- 2026-04-25: [DONE] Ran skeptical review pass and folded in automation lanes, action state, GTM evidence, Peec refresh-lag handling, and capability-gating requirements.
- 2026-04-25: [DONE] Updated project posture to treat `bookmo-agent-ops` as intentionally public and require public-safe/redacted committed outputs.
