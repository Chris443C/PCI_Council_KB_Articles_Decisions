---
description: Implement an approved change with minimal, reviewable diffs
---

Implement the requested change using the agreed plan.

Rules:
- Follow existing repository patterns first
- Keep diffs minimal and scoped
- Do not edit unrelated files
- Do not introduce new dependencies unless clearly justified
- Preserve security controls, validation, and logging behaviour unless change is intentional

For .NET code:
- Respect nullable reference types
- Use async/await correctly
- Avoid `.Result` and `.Wait()`
- Use constructor injection
- Keep controllers/endpoints thin
- Do not log secrets or sensitive data
- Accept and propagate `CancellationToken` where appropriate

Output expectations:
- Make the code changes
- Summarise what changed
- List any assumptions or incomplete areas
- Do not claim success without validation