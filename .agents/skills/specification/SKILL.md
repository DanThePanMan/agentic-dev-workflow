---
name: specification
description: Write a clear, testable description of a feature or change after its requirements are understood. Use before making an implementation plan for a story or feature. Do not use for a tiny change with no unclear behavior.
---

# Write the specification

1. Start from the agreed brief and any confirmed decisions.
2. Write a clearly named file, for example `specs/add-login.md`. Use `templates/specification.md` when it fits.
3. Describe:
   - The goal and the person or system it helps.
   - What will not change.
   - Normal behavior, important alternatives, and errors.
   - Permissions, data handling, compatibility, and migration when relevant.
   - Checks that prove the change works.
   - Remaining questions and risks.
4. Keep each check observable. A reader should know whether it passed from a test, inspection, or demonstration.
5. Show the specification to the user before planning work that makes a material product or architecture choice.

Do not include a file-by-file coding plan unless it is needed to explain a hard limit.
