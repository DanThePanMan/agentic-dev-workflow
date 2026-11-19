---
name: implementation-plan
description: Research the relevant existing code, then write a safe, testable plan for a feature, bug fix, or refactor. Use before implementation when the work has more than one step or affects unfamiliar code.
---

# Make the implementation plan

1. Say whether this plan covers a large effort, one feature, or one small task.
2. Check only the context needed for the plan:
   - Project instructions and current Git state.
   - Relevant code paths, tests, configuration, dependencies, and recent changes.
   - Primary external documentation if a current library, platform, or standard fact matters.
3. Separate confirmed facts from reasonable guesses and unanswered questions.
4. If there are meaningful choices, use `decision-support` before choosing a direction.
5. Write a clearly named file, for example `plans/add-login.md`. Use `templates/implementation-plan.md` when it fits.
6. For every step, state:
   - What changes.
   - Likely files or areas of code.
   - How to check it works.
   - Dependencies, risks, and any user decision needed.
7. Link every step to the behavior it supports. Add final checks for the whole change.

Use other agents only when work can be safely split. Give each one a clear question or task, expected result, and separate files where possible. The main agent remains responsible for joining the work, checking it, and reporting the result.

Do not start changing code, commit, deploy, or make a material choice without the user's approval.
