---
description: Produce a clean commit message and PR summary for the current change
---

Prepare commit and PR text for the current diff.

Output:

1. Commit message
Use:
`type(scope): concise description`

2. PR title
- short and specific

3. PR summary
Include:
- what changed
- why it changed
- key files touched
- validation performed
- residual risks / follow-ups

Rules:
- Keep it factual
- Do not overstate impact
- Do not say tests passed unless they were actually run and passed
- Keep the scope aligned to the real diff