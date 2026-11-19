---
name: security-review
description: Review a defined change for security risks. Use when a change handles permissions, user input, data, secrets, dependencies, network access, payments, or file and system actions. Do not use as a substitute for an authorized security assessment.
---

# Check security risks

1. Start with the exact diff and the data or actions it affects.
2. Identify who can use the feature, what they can access, and where untrusted input enters.
3. Check permissions, input handling, secret storage, logging, data exposure, dependency changes, network calls, and destructive actions.
4. For each real risk, explain the changed code involved, likely impact, and a practical fix or test.
5. Separate confirmed problems from concerns that need more information.
6. State any risk that remains after the review and who must accept it.

Do not use credentials, test a live system, run attack tools, or approve a risky release without separate permission.
