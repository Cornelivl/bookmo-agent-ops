# Approval Policy

## Automatic

- Read Peec data.
- Search and extract public web sources through Tavily.
- Summarize actions.
- Rank and classify opportunities.
- Write public-safe local markdown reports.
- Draft content briefs.
- Read `booking-agent-crm` locally to verify whether an owned-page, SEO, docs,
  or GitHub recommendation is feasible.

Automatic outputs committed to this public repo must be redacted and safe for
public viewing.

## Requires Review

- Create GitHub issues.
- Draft PRs against `booking-agent-crm`.
- Draft comparison/alternative pages.
- Draft concrete product-repo implementation tasks for public website, SEO,
  sitemap, Help Center, or docs changes.
- Draft outreach emails.
- Draft social or community posts.
- Mention competitors in public copy.

## Requires Explicit Manual Approval

- Publish public website changes.
- Merge product-repo PRs or deploy `booking-agent-crm`.
- Send outreach.
- Post to Reddit, YouTube, forums, or communities.
- Delete or mutate Peec configuration.
- Add production credentials or deploy infrastructure.

## Never Commit

- Secrets, tokens, or OAuth material.
- Private lead/customer details.
- Sensitive account identifiers or channel operation details.
- Unredacted private Peec evidence that should not be public.

## Default Reject

- Generic CRM recommendations that dilute the music-ops signal.
- False-positive domains such as `bookingholdings.com`.
- Unverified competitor claims.
- Treat Tavily search results as supporting public evidence, not as the source
  of truth for Peec-derived recommendations.
- Any action that cannot be measured or explained.
