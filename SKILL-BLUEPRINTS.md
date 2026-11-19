# Personal AI Development Skills Kit - Detailed Blueprints

## Status and purpose

This document defines what each planned skill includes before any `SKILL.md` files are written. It is a document for review, not an implementation. A skill may be built only after its blueprint is accepted or revised.

The kit targets Codex first. Its portable instructions must remain usable by Claude Code and Cursor adapters later. Python and TypeScript are the first specialized ecosystems; all other skills remain language-neutral.

## Shared contract for every local skill

Every skill will contain these sections:

1. **Trigger and non-trigger** - when the skill should and should not run.
2. **Inputs** - the minimum repository state, user request, and artifacts required.
3. **Process** - a short ordered procedure with clear stopping conditions.
4. **Outputs** - named artifacts or a defined response structure.
5. **Verification** - how the agent proves it completed the work correctly.
6. **Safety and authority** - actions that need user approval and actions the skill must never take on its own.
7. **Examples and evaluation cases** - at least one positive and one negative/edge example.

All skills must distinguish facts from inference, preserve existing user changes, and state uncertainty plainly. They should save a file only when it is useful; temporary exploration must not create project noise.

## Plain-English rule

The kit must write like a helpful engineer talking to a person, not like an AI workflow manual.

- Use ordinary words and explain a technical term when it is needed.
- Do not use abbreviations, labels, or specialist terms without explaining them the first time, unless they are exact code, command, file, library, or standard names the user needs.
- Prefer direct sentences, active voice, and concrete statements over vague process language.
- Keep technical accuracy. Do not replace a needed technical word with a misleading simpler word; explain it briefly instead.
- The `ste100` pass applies to every reader-facing handoff. This rule also applies to every local skill, plan, template, and case study.
- `skill-authoring` must reject a skill that uses avoidable AI/agent jargon or hides an important action behind a label the user cannot understand.

## Workflow map

```text
Start or resume work
  -> project context
  -> targeted research inside the next implementation plan, if unfamiliar or uncertain
  -> decision support, if material options exist
  -> grill requirements
  -> specification
  -> implementation plan (epic, story, or task)
  -> implement and test
  -> review actual diff
  -> reader-ready handoff
  -> retrospective
  -> case study, when the work has reusable lessons
```

Security review and frontend quality are opt-in gates inside planning, implementation, or review when their triggers apply. Skill authoring supports the whole system.

## Required external dependency: `ste100`

The kit will use a separately versioned, licence-reviewed `ste100` skill for reader-facing handoffs. It is not a local replacement for the official ASD-STE100 standard, and the kit must not claim formal standards certification.

The `ste100` pass will:

- Preserve code, file paths, command names, identifiers, test output, and precise technical facts.
- Rewrite the explanatory prose into direct, short, literal English.
- Lead with the outcome and separate result, evidence, risks, and next actions.
- Flag text that it could not simplify without losing technical accuracy.

It will not rewrite raw diffs, code blocks, logs, or quoted error messages. The user can request a more conversational style for a particular handoff, but clarity remains the default.

## 1. `repository-orientation`

**Purpose:** establish reliable project context once per repository and refresh it when the repository changes materially.

**Trigger:** first work in a repository; unclear project commands or conventions; a new major package/application; or a stale project profile.

**Inputs:** repository instructions (`AGENTS.md`, `README`, and equivalent), manifests, lock files, source layout, test/configuration files, and current Git status.

**Process:**

1. Read repository-local instructions before interpreting source code.
2. Identify languages, package managers, primary applications/libraries, test/lint/type-check commands, and delivery tooling.
3. Map top-level architecture and important boundaries without attempting a full code audit.
4. Record confirmed conventions and mark unknowns separately.
5. Present a concise project-context draft for review before saving it as a project file.

**Outputs:** a compact `project-context` profile: purpose, stack, commands, locations, conventions, important constraints, and known unknowns.

**Verification:** every command and path in the profile is traceable to a repository source or marked unverified.

**Does not include:** tracing feature behavior or recommending architecture changes. Use the planning-research phase inside `implementation-plan` and `decision-support` for those.

**Approval boundary:** do not overwrite project guidance automatically.

## Planning research (an internal phase of `implementation-plan`)

**Purpose:** gather only the repository and external context required to make the next implementation plan trustworthy.

**Trigger:** the requested work's change impact, existing behavior, code ownership, data flow, test coverage, dependency behavior, or current fact is unclear.

**Inputs:** a research question, relevant current behavior, repository context, working-tree state, and any user constraints.

**Process:**

1. Restate the exact question and define what evidence would answer it.
2. Inspect only relevant code paths, tests, configuration, dependency usage, and recent history.
3. Trace actual behavior from entry point to observable outcome where practical.
4. Separate observations, inferences, and unanswered questions.
5. Report possible change locations and risks without editing code.

**Outputs:** an evidence/context section inside the next implementation plan: source paths, behavior map, relevant tests, impact/risk assessment, and unresolved questions.

**Persistence rule:** do not create a standalone file by default. Create a clearly named file, for example `research/payment-options.md`, only when the user asks for research as its own deliverable, the result will support multiple plans, or the investigation is substantial enough to need independent review. A subsequent plan links to that file and captures its relevant conclusions.

**Verification:** every factual claim cites a file, command result, documentation source, or is labelled as inference.

**Does not include:** implementation, broad exploratory reading with no planning question, a durable standalone report by default, or a decision among competing approaches.

**Approval boundary:** read-only unless the user separately authorizes a change. It can be used as a standalone research response only when the user asks for research rather than a plan.

## 2. `decision-support`

**Purpose:** help choose a technical or product direction when more than one material option is plausible.

**Trigger:** architecture choices, dependency selection, build-vs-buy, migration approach, API shape, performance/cost trade-off, or a decision with meaningful reversibility risk.

**Inputs:** decision question, constraints, existing research, success criteria, timeline/budget expectations, and non-negotiables.

**Process:**

1. Define the decision, the status-quo option, and the decision owner.
2. Establish decision criteria before ranking options.
3. Gather repository and, when necessary, primary-source external evidence.
4. Compare viable options by benefit, cost, risk, implementation impact, reversibility, and confidence.
5. Recommend an option and state exactly what evidence could change the recommendation.

**Outputs:** an ADR-style decision record with options, trade-offs, recommendation, confidence, dissent/unknowns, and required user decision.

**Verification:** no unsupported score or claim; links and sources are included where external facts matter.

**Does not include:** making material product, security, cost, or architecture decisions on the user's behalf.

**Approval boundary:** a user decision is required before a selected material option is implemented.

## 3. `grill-requirements`

**Purpose:** test whether an idea is sufficiently understood to become a specification.

**Trigger:** a new feature, behavior change, workflow change, unclear bug report, or request with assumptions/unknown scope.

**Inputs:** the user's initial request, repository research, known constraints, and any prior decision record.

**Process:**

1. State the assumed goal in plain language.
2. Ask focused questions, normally one decision at a time, rather than issuing a generic questionnaire.
3. Challenge assumptions about users, current behavior, value, scope, non-goals, failure cases, privacy/security, migration, and success evidence.
4. Identify questions that can be answered through research rather than asking the user.
5. End only when material ambiguity is resolved, explicitly deferred, or accepted as a risk.

**Outputs:** a clarified brief with goals, non-goals, decisions, assumptions, open risks, and acceptance signals.

**Verification:** the brief can be read back to the user as a concrete description of the desired outcome; each deferred uncertainty has an owner or next step.

**Does not include:** detailed task sequencing. Use `implementation-plan` after the specification is accepted.

**Approval boundary:** do not treat an assumption as user approval.

## 4. `specification`

**Purpose:** turn a clarified brief into observable, testable behavior.

**Trigger:** requirements have stabilized enough to define a story or a bounded part of an epic.

**Inputs:** clarified brief, decision records, repository research, product/design constraints, and known interfaces.

**Process:**

1. State the problem, user/actor, goal, and non-goals.
2. Describe happy path, important alternate paths, failures, permissions, data handling, and compatibility/migration behavior as applicable.
3. Define acceptance criteria in observable language.
4. List out-of-scope items and dependencies.
5. Review the specification with the user if it includes material product or architecture choices.

**Outputs:** `specs/<story-or-feature>.md` with behavior, acceptance criteria, edge cases, constraints, and decisions.

**Verification:** every acceptance criterion can be evaluated by a test, inspection, demonstration, or explicit human check.

**Does not include:** file-by-file work assignments or implementation detail unless required to remove a known constraint.

**Approval boundary:** the user approves a material feature specification before implementation planning proceeds.

## 5. `implementation-plan`

**Purpose:** turn a specification into a safe, ordered, verifiable execution plan.

**Trigger:** an approved specification, planned bug fix, refactor, or operational change needs implementation steps.

**Inputs:** specification or issue, task-specific planning research, chosen decisions, current branch/working-tree state, and required quality gates.

**Process:**

1. Gather and record only the research needed to understand the requested change; include repository and external primary-source evidence when needed.
2. Declare plan level: **epic**, **story**, or **task**.
3. For an epic, create outcomes, story sequence, dependencies, decision points, and integration milestones.
4. For a story, define small vertical tasks with affected areas, expected behavior, tests, verification, rollback/compatibility notes, and ordering.
5. For a task, state exact goal, likely files, guardrails, test, and definition of done.
6. Mark tasks as serial or safely parallel. A task is delegable only if its scope, inputs, outputs, file ownership, and integration point are clear.
7. Identify mandatory gates: security, frontend quality, migration, performance, or human approval.

**Outputs:** an epic or story plan with a clear file name, for example `plans/add-login.md`, with a short evidence/context section, a trace from task to specification acceptance criterion, and a final integration/verification step. Small task plans are normally checked sections in their parent story plan; create a separate task file only when its scope or handoff warrants it.

**Verification:** the plan covers every acceptance criterion; dependencies are ordered; each task has a concrete verification method; parallel work has no overlapping file ownership unless explicitly coordinated.

**Does not include:** automatic implementation or deployment.

**Subagent policy:** subagents are optional, never a default. Use them for bounded research, independent reviews, or isolated tasks. The primary agent owns integration, final verification, and the retrospective.

## 6. `test-first-implementation`

**Purpose:** implement one planned, complete part of the work at a time and prove the requested behavior works.

**Trigger:** an approved task with clear acceptance criteria and a defined verification approach.

**Inputs:** current task, relevant specification criteria, plan, repository commands, working-tree state, and existing tests.

**Process:**

1. Confirm the task boundary and preserve unrelated existing changes.
2. Establish a baseline: reproduce the issue or identify expected current behavior.
3. Add or update the narrowest useful automated test before or alongside the change, according to repository conventions.
4. Make the smallest coherent implementation change.
5. Run focused validation, then the broader required checks.
6. Show the changed files/diff and update task evidence.

**Outputs:** focused code changes, relevant tests, command results, and task completion evidence.

**Verification:** planned acceptance criteria have evidence; tests actually fail or demonstrate the missing behavior before the fix when feasible; no unrelated diff is represented as part of the task.

**Python and TypeScript layer:** use the project's declared tooling first. Initial checklists will cover common patterns such as `pytest`/typing/linting for Python and unit tests/type-checking/linting/build steps for TypeScript, without assuming one package manager or framework.

**Does not include:** deciding to ship, deploying, or silently committing changes.

## 7. `git-workflow`

**Purpose:** prepare a focused Git commit without losing work or sending changes anywhere without approval.

**Trigger:** the user asks to stage, commit, push, organize Git changes, or prepare a pull request.

**Inputs:** current Git status, the relevant diff, the user's intended change, and any existing approval.

**Process:**

1. Check status and inspect the relevant diff before changing Git state.
2. Keep unrelated existing work out of the commit.
3. Stage only inspected, related files. Show the staged diff and a proposed commit message.
4. Get explicit approval before committing unless the user already approved that exact commit.
5. Get separate approval before pushing, opening a pull request, changing branches, rebasing, resetting, force-pushing, or changing Git configuration.

**Outputs:** staged diff, proposed commit message, and, after approval, the commit ID and a report of remaining changes.

**Verification:** the staged diff contains only the intended work and the commit message describes that work.

**Does not include:** discarding work, rewriting history, or sending changes to a remote without approval.

## 8. `debugging`

**Purpose:** find and correct the root cause of a defect instead of treating symptoms.

**Trigger:** a bug, regression, test failure, production report, flaky behavior, or unexplained mismatch between intended and actual behavior.

**Inputs:** symptom, environment/context, logs or error output, reproduction information, repository research, and known recent changes.

**Process:**

1. Define expected versus actual behavior and seek a minimal reproduction.
2. Preserve evidence and classify severity/impact.
3. Form ranked hypotheses; test one hypothesis at a time with targeted evidence.
4. Identify root cause and affected scope.
5. Implement the smallest root-cause fix with a regression test.
6. Verify no related behavior regressed and document residual uncertainty.

**Outputs:** reproduction, root-cause explanation, fix, regression test, verification result, and follow-up risks.

**Verification:** the reproduction/test passes after the fix and either failed before it or otherwise provides clear proof of the corrected behavior.

**Does not include:** speculative refactors hidden inside a bug fix.

**Approval boundary:** incidents with security, data loss, financial, or production-impact consequences may require escalation before remediation.

## 9. `code-review`

**Purpose:** assess a defined change against correctness, scope, maintainability, tests, security, and repository conventions.

**Trigger:** a completed task/story, a pull request, or an explicit request to review a change.

**Inputs:** exact comparison range (working tree, commits, branch range, or pull request), specification/plan if available, tests/results, and known constraints.

**Process:**

1. State the comparison range before reviewing.
2. Render and inspect the actual diff; do not claim a review without one.
3. Check behavior against the specification, then review correctness, tests, error handling, security, maintainability, performance where relevant, and scope discipline.
4. Run or inspect relevant validation evidence.
5. Report findings by severity and point each finding to a changed file and line or diff hunk.
6. Clearly state when no blocking issues were found and what was not reviewed.

**Outputs:** actual diff or stable link/path plus the exact render command, findings, positives, validation status, and remaining limitations.

**Verification:** every finding is supported by the diff, an execution result, or a directly relevant repository source. The report separates blockers from suggestions.

**Does not include:** rewriting the change during review unless a separate fix task is authorized.

**Approval boundary:** code review recommends; it does not merge, commit, or deploy.

## 10. `security-review`

**Purpose:** identify security-sensitive risks before merging or deploying a relevant change.

**Trigger:** authentication/authorization, user-controlled input, data access, secrets, dependencies, network exposure, file/system operations, payments, or destructive actions.

**Inputs:** defined diff/range, data flows, threat context, deployment environment, existing security controls, and relevant dependency changes.

**Process:**

1. Set review scope and identify assets, trust boundaries, actors, and likely misuse paths.
2. Inspect changes for authorization, validation, injection, secret handling, logging/privacy, dependency, and unsafe-operation risks.
3. Rank findings by realistic impact and likelihood.
4. Recommend concrete mitigations and verification tests.
5. Record residual risk and needed human/security-owner decisions.

**Outputs:** concise threat/risk note, findings, mitigations, required tests, and residual-risk statement.

**Verification:** findings map to a concrete code/data flow or configuration path; claims are not inflated beyond evidence.

**Does not include:** penetration testing, exploitation, credential use, production scanning, or security sign-off unless separately authorized.

**Approval boundary:** security-sensitive deployment or accepted residual risk requires an authorized human decision.

## 11. `frontend-quality`

**Purpose:** ensure a user-facing interface meets functional, visual, responsive, and accessible quality expectations.

**Trigger:** a change affects screens, components, layout, interaction, content, visual states, or client-side performance.

**Inputs:** UI specification, design references if any, target viewports, actual changed UI, accessibility requirements, and browser/test tooling.

**Process:**

1. Identify affected states: loading, empty, success, error, disabled, focus, keyboard, narrow/wide viewport, and reduced-motion where relevant.
2. Check semantic structure, labels, keyboard behavior, focus, contrast, responsive layout, and meaningful feedback.
3. Compare actual UI behavior with the specification and visual references.
4. Capture test/screenshot evidence where tooling permits.
5. Report issues with reproduction steps and severity.

**Outputs:** UI quality checklist, visual/automation evidence, findings, and recommended corrections.

**Verification:** automation is treated as a smoke test; critical user paths and manual interaction checks remain explicit.

**Does not include:** inventing a design system or redesigning product behavior without an approved requirement.

## 12. `delivery-and-handoff`

**Purpose:** give the user a concise, trustworthy account of what changed and what they need to know next.

**Trigger:** completed implementation, review-ready change, bug fix, decision completion, or when another person/agent must resume work.

**Inputs:** actual diff/comparison range, specification/plan, test and review results, known risks, deferred work, and deployment status.

**Process:**

1. State the outcome first: completed, partially complete, blocked, or not started.
2. Summarize behavior change rather than merely listing files.
3. Include the actual diff link/path and render command, or a precise summary when the raw diff is already attached.
4. List exact verification evidence and tests not run.
5. State risks, limitations, decisions needed, and recommended next action.
6. Run the explanatory prose through the `ste100` pass without modifying code/diffs/logs.

**Outputs:** reader-ready handoff or PR note with outcome, changes, diff, verification, risks, and next action.

**Verification:** all claims match execution/review evidence; the handoff passes the `ste100` clarity checklist; it makes no unsupported "done" claim.

**Does not include:** deployment, merge, or external messages unless separately authorized.

## 13. `retrospective`

**Purpose:** learn from a completed outcome and create small, evidence-based process improvements.

**Trigger:** after every completed implementation, fix, research/design decision, or other meaningful outcome. It is optional for chat-only exploration with no decision or saved result.

**Inputs:** goal, plan/spec, execution evidence, review/handoff, time/effort signal if available, user feedback, and friction encountered.

**Process:**

1. Compare intended and actual outcome.
2. Identify what helped, what caused rework, what was missing, and what remains risky.
3. Propose no more than three specific improvements, each with expected value and supporting evidence.
4. Classify improvements as project-context, template, skill, tooling, or process changes.
5. Record candidates in an improvement backlog; do not apply them silently.

**Outputs:** lightweight retrospective and prioritized candidate-improvement list.

**Verification:** each proposed improvement traces to an observed friction or repeated pattern, not a vague preference.

**Does not include:** autonomous changes to active skills, instructions, tools, or external services.

**Approval boundary:** user review is required before adopting a candidate improvement.

## 14. `case-study`

**Purpose:** preserve substantial work as a reusable example that improves future reasoning and skill evaluation.

**Trigger:** a significant feature, difficult bug, unusual failure, meaningful decision, or successful process experiment with lessons worth reusing.

**Inputs:** approved/finished handoff, retrospective, linked artifacts, outcome evidence, and any confidentiality constraints.

**Process:**

1. Confirm the case is worth preserving and contains no sensitive information that should not be retained.
2. Describe context, problem, constraints, key decisions, approach, and outcome.
3. Link the relevant spec, plan, diff, verification, and retrospective.
4. Extract reusable lessons, anti-patterns, and conditions under which those lessons apply.
5. Tag the case by stack, problem type, and skills used.

**Outputs:** a clearly named case-study file, for example `case-studies/login-migration.md`, with evidence links and reusable lessons.

**Verification:** claims link to supporting saved documents or diffs; sensitive values and credentials are absent; conclusions state their scope rather than overgeneralizing.

**Does not include:** a verbose activity log for routine changes.

**Approval boundary:** user review is required before retaining or sharing a case study that includes potentially sensitive context.

## 15. `skill-authoring`

**Purpose:** create, change, test, and retire kit skills without making the kit inconsistent or unsafe.

**Trigger:** a recurring correction, accepted retrospective candidate, new workflow need, compatibility adapter, or a defect in an existing skill.

**Inputs:** approved blueprint/change request, relevant cases and retrospective evidence, target agent compatibility, and dependency/licence information.

**Process:**

1. Confirm that a skill is the right solution rather than project documentation, a template, automation, or a one-off instruction.
2. Write a narrow trigger description, process, inputs, outputs, checks, and authority boundaries.
3. Keep optional references and scripts in progressive-disclosure directories.
4. Add positive, negative, and edge evaluation scenarios.
5. Check the frontmatter (the skill's short name and description), links, referenced files, script safety, portability, plain-English wording, and conflict risk with other skills.
6. Record provenance, compatibility, version, and changelog entry.

**Outputs:** reviewed skill directory, evaluation scenarios/results, provenance entry, compatibility note, and changelog update.

**Verification:** the skill triggers in its intended cases, does not trigger in at least one nearby non-case, and adds measurable value against a prior workflow or case study.

**Does not include:** importing unreviewed third-party instructions/scripts or changing global agent settings without approval.

**Approval boundary:** user approval is required to activate, replace, or retire a core skill.

## Implementation status and next checks

All locally owned skills in this blueprint are now implemented in `.agents/skills/`. Test the kit on a real Python or TypeScript task before treating the instructions as settled.

Before wider use, confirm or change:

- The naming: especially `grill-requirements` and `project-context` terminology.
- Where you want to save specifications, plans, and case studies (`specs/`, `plans/`, `case-studies/`, or another layout).
- The Python and TypeScript toolchains to prioritize.
- The exact `ste100` dependency/version and its licence result.
- Whether handoffs should be Markdown only or also have a pull-request template format.
