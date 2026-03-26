---
description: Add focused tests for the current behaviour change
---

Add or update tests for the current change.

Rules:
- Use the repository’s existing test framework and style
- Prefer deterministic, focused tests
- Cover behavioural change, not implementation trivia
- Avoid unnecessary mocking if a simpler test is possible
- Name tests clearly

For .NET:
- keep unit tests fast
- use integration tests only when justified
- avoid brittle timing-based tests
- include null/edge/error-path coverage where relevant

Output:
1. Test files added or updated
2. Behaviours covered
3. Remaining gaps, if any