# Content Brief: Bookmo Owned Product / Comparison Page Cluster

Date: 2026-04-25
Status: draft artifact for review
Source memo: `docs/peec/actions/2026-04-25.md`
Public-safe status: redacted for public repository

## Selected task

Create a reviewable content brief for a Bookmo-owned product/comparison landing page cluster, starting with a primary page for music booking agency CRM and artist-management workflow automation.

This is the first task because Peec's strongest current signal is owned-page visibility: product pages, homepage, comparison pages, alternative pages, and listicle-style pages. The brief is a safe first artifact because it does not publish anything, send outreach, mutate Peec, deploy, or modify `booking-agent-crm`.

## Ranking classification

- Category: owned
- Decision lane: quick win for brief; needs planning for implementation/publishing
- Classification: draft
- Automation lane: autopilot for this brief; review before issue/PR/page publication
- State: drafted
- Risk: low for brief, medium for public page implementation
- Effort: small for brief, medium for implementation
- Evidence quality: direct Peec owned-action signal, summarized in the source memo
- Measurement readiness: baseline can be recorded before implementation

## Audience

Primary:

- Music booking agency owners
- Booking agents
- Artist managers and operations leads

Secondary:

- Small agencies evaluating CRM/workflow tools
- Teams comparing general CRMs with music-industry-specific tools
- People researching AI-assisted booking-agent workflows

## Core page intent

The page should help a qualified visitor and an AI answer engine understand:

- What Bookmo is.
- Who Bookmo is for.
- Why music booking agencies need a specialized CRM/workflow layer.
- How Bookmo helps with deals, contracts, artist logistics, advancing, artist mobile app workflows, and inbox-native follow-up.
- Where Bookmo differs from generic CRMs, without making unsupported competitor claims.

## Suggested primary page title options

Pick one after founder review:

1. Music Booking Agency CRM for Deals, Contracts, and Artist Logistics
2. Bookmo: CRM and AI Workflow Automation for Music Booking Agencies
3. Booking Agency CRM Built for Artist Logistics, Advancing, and Follow-Up

## Suggested page outline

### 1. Hero

Goal: explain Bookmo in one sentence.

Draft angle:

Bookmo is a CRM and AI-powered workflow platform for music booking agencies, helping teams manage deals, contracts, artist logistics, advancing, and follow-up from one booking-focused system.

Needs review:

- Confirm exact product wording.
- Confirm whether “AI-powered” is approved for public copy.
- Confirm whether “CRM” or “workflow platform” should lead.

### 2. The problem with generic CRM for booking agencies

Cover:

- Booking work is not only contact management.
- Agents need to manage artist availability, show details, contracts, advancing, settlement/admin context, and follow-up.
- Generic CRMs often require manual customization for booking-specific workflows.

Guardrail:

- Keep this general. Do not name competitors or make unverifiable claims.

### 3. What Bookmo helps manage

Potential sections:

- Deals and opportunities
- Contracts and booking admin
- Artist logistics and advancing
- Artist mobile app workflows
- Inbox-native follow-up
- AI-assisted workflow automation

For each section:

- State the job-to-be-done.
- Explain what Bookmo supports.
- Add one concrete example if approved by founder.

### 4. Who Bookmo is for

Cover:

- Boutique and growing music booking agencies
- Agency owners who need operational visibility
- Booking agents managing many artists and conversations
- Artist-management-adjacent teams coordinating logistics

### 5. Comparison positioning without competitor claims

Safe initial angle:

- Generic CRM: broad and flexible, but not designed around booking-agency workflows by default.
- Booking-specific workflow system: designed around the operational reality of shows, artists, contracts, advancing, and follow-up.
- Bookmo: intended to combine CRM structure with booking-specific AI workflow support.

Needs review:

- Whether to include direct competitor names.
- Which claims are approved.
- Whether comparison pages should be public, private, or staged later.

### 6. FAQ section for AI retrievability

Draft FAQ topics:

- What is a music booking agency CRM?
- Why do booking agencies need specialized CRM software?
- Can Bookmo help with artist logistics and advancing?
- Can Bookmo help manage contracts and booking follow-up?
- How is Bookmo different from a generic CRM?
- Is Bookmo for small booking agencies?

Guardrail:

- Answers should be concise, factual, and based on real product capability.

### 7. Calls to action

Potential CTAs:

- Request a demo
- See how Bookmo works
- Talk to the Bookmo team

Needs review:

- Confirm current GTM motion and preferred CTA.

## Required facts to confirm before public copy

- Exact product category: CRM, AI workflow platform, booking operating system, or another phrase.
- Approved feature list.
- Current product availability and onboarding motion.
- Whether “contracts,” “artist mobile app,” “advancing,” and “inbox-native follow-up” are all public-approved claims.
- Whether Bookmo wants to emphasize Europe, small agencies, AI agents, or all of these.
- Whether direct competitor comparisons are allowed.

## Implementation options after review

Option A: GitHub issue only

- Create an issue in the product repo describing the page, target intent, outline, and acceptance criteria.
- No code changes.

Option B: PR draft

- Draft the page in `booking-agent-crm` after explicit approval.
- Keep it unpublished or behind review until founder approval.

Option C: Content-only doc

- Expand this brief into full copy in this repo first.
- Review claims before moving to the product repo.

Recommended next step: Option A or C.

## Measurement baseline before implementation

Before any public page ships, record:

- Owned homepage opportunity band.
- Owned product-page opportunity band.
- Owned comparison-page opportunity band.
- Whether `bookmo.ai` appears in Peec domain/URL source reports.
- Whether any Bookmo-owned URL is retrieved for the relevant theme cluster.
- Implementation artifact path and publish date once available.

Do not write exact private Peec scores into public files unless explicitly approved.

## Measurement checkpoints

If a page is implemented and published:

- 7d: 2026-05-02
- 14d: 2026-05-09
- 30d: 2026-05-25

At each checkpoint, note Peec data window and likely refresh/indexing lag.

## Approval questions

1. Should the first page be product-led, comparison-led, or homepage-copy-led?
2. Are the feature claims above approved for public copy?
3. Should the page avoid direct competitor names for version one?
4. Should the agent create a GitHub issue in `booking-agent-crm`, or keep this as a content-only doc until after founder review?
5. Is exact Peec scoring still excluded from public repo files by default?
