---
description: Run validation for the current change and report exactly what passed
---

Validate the current changes.

Default .NET validation sequence:
1. `dotnet restore`
2. `dotnet build`
3. `dotnet test`
4. `dotnet format --verify-no-changes`

If the repository is large, choose the narrowest meaningful scope and state:
- what was run
- what was not run
- why

Your output must include:
1. Commands executed
2. Result of each command
3. Any failing tests, warnings, or analyzer issues
4. Whether the change is ready for review
5. Any additional recommended checks

Rules:
- Never say tests passed unless they actually passed
- Never hide failures
- If something could not be run, say so explicitly