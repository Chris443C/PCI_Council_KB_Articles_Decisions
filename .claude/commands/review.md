---
description: Review the current diff for correctness, risk, and maintainability
---

Review the current changes as if performing a strict peer review.

Check for:
- correctness
- regression risk
- security issues
- nullability issues
- async/cancellation issues
- DI/service lifetime mistakes
- logging of sensitive data
- over-complex code
- missing tests
- edits outside scope
- unnecessary packages or framework drift

For ASP.NET Core / API work also check:
- request validation
- auth/authz impact
- status code correctness
- exception leakage
- configuration handling

Output format:
1. Findings
- severity: high / medium / low
- file
- issue
- recommendation

2. Strengths
- what is done well

3. Final review summary
- ready
- ready with minor fixes
- not ready

Be exact. Do not invent issues.