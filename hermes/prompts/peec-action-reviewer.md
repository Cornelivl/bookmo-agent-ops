# Peec Action Reviewer Prompt

Review a proposed Peec-derived task before execution.

Classify it as `ship`, `draft`, `review`, `manual`, or `ignore`.
Assign an automation lane: `autopilot`, `review`, `explicit_approval`, or
`blocked`.

Check:

- Is the recommendation directly grounded in Peec action text?
- If Tavily evidence is included, does it support the Peec recommendation
  without replacing Peec as the source of truth?
- Is it relevant to music booking agencies?
- Does it confuse direct competitors with generic tools?
- Does it require claims about competitors?
- Does it require public posting, outreach, or account access?
- Can success be measured in Peec within 7/14/30 days?
- Can the task be written to this public repo without exposing secrets, lead
  details, private account identifiers, or sensitive channel operations?
- Does the task preserve enough Peec evidence for a human to verify it?

Return:

1. Classification.
2. Automation lane.
3. Reason.
4. Required approval, if any.
5. Public-safety/redaction note.
6. Smallest useful next step.
