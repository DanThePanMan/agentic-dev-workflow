---
name: debugging
description: Find the cause of a bug or failing test and prevent it from returning. Use when actual behavior differs from expected behavior or a test fails. Do not use to guess at a fix without evidence.
---

# Find and fix the problem

1. State expected behavior, actual behavior, impact, and the smallest known way to reproduce the problem.
2. Save useful evidence such as errors, logs, input values, and affected versions.
3. List likely causes. Check one cause at a time with a focused test or inspection.
4. Explain the confirmed cause and the code or configuration it affects.
5. Fix the cause, not only the visible symptom. Add a regression test when practical.
6. Run the reproduction and relevant checks again. Report remaining uncertainty.

Do not hide broad refactoring inside a bug fix. Stop and ask before handling a problem with security, data-loss, money, or live-service impact.
