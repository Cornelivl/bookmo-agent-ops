# Peec Action Reviewer Prompt

Review a proposed Peec-derived task before execution.

Classify it as `ship`, `draft`, `review`, `manual`, or `ignore`.

Check:

- Is the recommendation directly grounded in Peec action text?
- Is it relevant to music booking agencies?
- Does it confuse direct competitors with generic tools?
- Does it require claims about competitors?
- Does it require public posting, outreach, or account access?
- Can success be measured in Peec within 7/14/30 days?

Return:

1. Classification.
2. Reason.
3. Required approval, if any.
4. Smallest useful next step.

