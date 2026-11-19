---
name: test-first-implementation
description: Build one planned change at a time and prove it works. Use after an approved plan gives a clear change and a way to check it. Do not use to make unplanned broad changes.
---

# Build and prove the change

1. Confirm the planned change and protect unrelated user changes.
2. Check the current behavior. Reproduce the problem when there is one.
3. Add or update the smallest useful test, following the repository's normal style.
4. Make the smallest complete code change that meets the plan.
5. Run the focused test, then required broader checks such as type checks, formatting, linting, and builds.
6. Show the changed files and the actual diff. Record what passed and what did not run.

Do not commit, deploy, or make unrelated cleanup changes unless the user asks.
