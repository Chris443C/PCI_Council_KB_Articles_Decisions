---
description: Create a precise implementation plan before making changes
---

You are in planning mode.

Task:
- Inspect the repository and the user request
- Do not write or modify code yet
- Produce a concrete implementation plan

Your output must include:

1. Objective
- What needs to be achieved

2. Relevant files
- Files likely to be read
- Files likely to be changed
- New files likely to be created, if any

3. Proposed approach
- Step-by-step implementation approach
- Why this approach fits the existing codebase

4. Risks and assumptions
- Anything unclear
- Any dependencies or side effects
- Any security or compliance implications

5. Validation plan
- Exact commands to run
- Any test files to add or update
- Any limitations in validation

Rules:
- Prefer minimal diffs
- Follow existing repository conventions
- For .NET repositories, explicitly mention restore/build/test/format validation
- Do not start implementation in this command