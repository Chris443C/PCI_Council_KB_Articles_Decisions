---
description: Diagnose and fix .NET build failures without widening scope
---

Diagnose the current build failure and fix only what is necessary.

Rules:
- Start by identifying the exact failing project, file, and error
- Prefer the smallest viable change
- Do not refactor unrelated code
- Preserve public behaviour unless the bug requires change
- Re-run targeted validation after each meaningful fix

Focus on:
- missing references
- namespace/type mismatches
- nullability errors
- signature drift
- DI registration mismatches
- package/version incompatibilities
- analyzer errors treated as build failures

Output:
1. Root cause
2. Fix applied
3. Validation run
4. Any remaining concerns