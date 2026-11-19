---
name: code-review
description: Review a defined code change and show the actual diff being reviewed. Use for a pull request, a branch comparison, a commit range, or current uncommitted changes. Do not claim a review without a concrete comparison.
---

# Review the changed code

1. State exactly what is being compared: uncommitted changes, two commits, two branches, or a pull request.
2. Render the actual diff and include it, or give the exact command and path that show it.
3. Check the change against its specification or plan when available.
4. Look for correctness problems, missing tests, unsafe error handling, security risks, unclear code, needless complexity, and changes outside the stated work.
5. Report findings as:
   - **Blocker** - must change before merge.
   - **Important** - should change soon.
   - **Note** - useful but not required.
6. Point every finding to the changed file and line. Say what you did not check.

If there are no blockers, say so plainly. Do not edit, commit, merge, or deploy while reviewing unless the user asks.
