---
name: git-workflow
description: Prepare a safe, focused Git commit with a visible diff and user approval. Use when staging, committing, pushing, or organizing Git changes. Do not use for ordinary read-only Git questions.
---

# Prepare Git changes safely

1. Start with `git status` and inspect the relevant diff. Preserve unrelated user changes.
2. Group only related files into one commit. Do not use `git add .` or stage files that you did not inspect.
3. Show the staged diff and propose a short commit message that describes the change.
4. Get explicit approval before running `git commit` if the user has not already approved that exact commit.
5. Get separate explicit approval before pushing, opening a pull request, changing branches, rebasing, resetting, force-pushing, or changing Git configuration.
6. After an approved commit or push, report the commit ID, changed files, and any remaining changes.

Do not discard work, rewrite history, or push to a remote without explicit approval.
