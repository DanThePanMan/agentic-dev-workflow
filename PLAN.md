# Personal AI Development Skills Kit — Plan

## Goal

Create a private, version-controlled, shareable collection of small, composable development skills that improve planning, implementation, verification, and handoff across AI coding agents. The kit will use the open `SKILL.md` convention, target Codex first, and retain a portable core for future Claude Code and Cursor adapters.

This repository is currently in the planning phase: no third-party skill contents will be copied into the kit. Reference collections inform the design; every included skill will be authored, adapted, or explicitly imported with its licence and provenance recorded.

The detailed, review-first definition of every planned skill is in [SKILL-BLUEPRINTS.md](SKILL-BLUEPRINTS.md). That document is the source of truth for scope before implementation starts.

## Reference collections

| Source | What to learn from it | Planned use |
| --- | --- | --- |
| [Anthropic Skills](https://github.com/anthropics/skills) | Canonical skill packaging, progressive disclosure, skill authoring | Use as the structural reference for every local skill. |
| [Superpowers](https://github.com/obra/superpowers) | Intent-first work, testing, debugging, verification | Borrow the lifecycle concept, not a monolithic always-on workflow. |
| [AI Hero / Matt Pocock Skills](https://www.aihero.dev/skills) ([repo](https://github.com/mattpocock/skills)) | Composable flow: interrogate → spec → tickets → test-first implementation → review → retro | Primary reference for small, linked engineering skills and useful written artifacts. |
| [Addy Osmani Agent Skills](https://github.com/addyosmani/agent-skills) | Production lifecycle: define → plan → build → verify → review → ship; quality and accessibility gates | Primary reference for lifecycle coverage and explicit quality gates. |
| [Karpathy Guidelines](https://github.com/multica-ai/andrej-karpathy-skills) | Restraint, clear scope, compact diffs | Reference for simplicity rules. |
| [STE100 skill](https://github.com/clayleopardlabs/ste100-skill) and [ASD-STE100](https://www.asd-ste100.org/) | Controlled, readable technical English | Apply the selected `ste100` skill to handoffs intended for the user to read. Do not claim formal ASD-STE100 certification without a compliant validation process. |
| [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) and [Taste Skill](https://github.com/Leonxlnx/taste-skill) | Intentional, non-generic UI design | Reference only for the optional frontend skill. |

## Design principles

- Prefer a small set of sharply scoped skills over one framework that controls every session.
- Each skill must state when to use it, what it needs, the steps it follows, what it creates, and how to check its result.
- Skills should compose through durable repository artifacts (specs, plans, test evidence, review notes), not hidden conversation context.
- Keep agent-specific commands, hooks, and installers separate from portable skill instructions.
- Make Codex the first supported runtime; keep portable core skills free of Codex-only behavior unless an explicitly labelled adapter supplies it.
- Treat Python and TypeScript as the first supported ecosystems, while keeping general skills language-agnostic.
- Keep the repository private by default, but document installation and contribution conventions so it can be securely shared with selected collaborators.
- Every handoff intended for the user to read must receive an explicit `ste100` clarity pass.
- A code review must show the actual diff it reviewed; findings must point to the relevant changed hunk or line.
- Write every skill, plan, and user-facing note in normal English. Avoid unexplained AI workflow words and abbreviations; use the ordinary word or explain a technical term when it is truly needed.
- Inspect all imported third-party code or scripts before use; preserve licences and provenance.
- Start project-local. Promote a skill to a personal/global kit only after repeated successful use.

## Proposed v1 kit

| Order | Skill | Purpose | Typical output |
| ---: | --- | --- | --- |
| 1 | `repository-orientation` | Establish project commands, conventions, architecture, and constraints. | `docs/agent-context.md` or an update to project guidance. |
| 2 | `decision-support` | Compare viable technical or product options before commitment. | Decision record with options, trade-offs, recommendation, confidence, and reversibility. |
| 3 | `grill-requirements` | Resolve ambiguity, challenge assumptions, and identify non-goals before planning. | Decision record / clarified brief. |
| 4 | `specification` | Turn an agreed brief into observable behavior and acceptance criteria. | `specs/<feature>.md`. |
| 5 | `implementation-plan` | Research the relevant existing behavior, then split the specification into small, ordered, verifiable tasks. | `plans/<feature>.md` with an evidence/context section. |
| 6 | `test-first-implementation` | Implement one small, complete part of the work at a time. | Code, focused tests, and evidence. |
| 7 | `git-workflow` | Prepare a safe, focused Git commit with a visible diff and explicit approval. | Staged diff and proposed commit message. |
| 8 | `debugging` | Reproduce, isolate, fix, and guard against regressions. | Reproduction, root cause, regression test. |
| 9 | `code-review` | Review correctness, maintainability, tests, security, and scope against the actual change. | Rendered or attached diff plus prioritized findings that cite changed files/hunks. |
| 10 | `security-review` | Evaluate auth, input handling, secrets, dependencies, and unsafe operations. | Threats, mitigations, residual risks. |
| 11 | `frontend-quality` | Apply accessibility, responsive behavior, interaction, and visual-quality checks. | UI acceptance checklist and evidence. |
| 12 | `delivery-and-handoff` | Summarize changes, verification, known limitations, and next actions in reader-ready language. | `ste100`-reviewed PR/handoff note with a diff link or embedded diff summary. |
| 13 | `retrospective` | Improve prompts, project context, and skills after a completed implementation or other meaningful outcome. | Small, actionable improvement backlog. |
| 14 | `case-study` | Capture a completed effort, the evidence of its outcome, and reusable lessons. | A clearly named file, for example `case-studies/login-migration.md`. |
| 15 | `skill-authoring` | Create, test, and evolve skills consistently. | Validated skill directory and changelog entry. |

## Discovery and decision flow

Research is a first-class phase, but it is triggered by uncertainty rather than run mechanically on every small change.

```text
existing repository or open decision
  → repository orientation
  → targeted research inside the next implementation plan (when the behavior, impact, or ownership is unclear)
  → external primary-source research inside that plan (when a dependency, platform, standard, or current fact matters)
  → decision support (when there are material alternatives)
  → grill requirements
  → specification and implementation plan
```

### Research inside an implementation plan

`implementation-plan` starts by gathering only the context needed to plan the requested work: relevant repository instructions, code paths, tests, dependency usage, recent history, and working-tree state. It must distinguish observed facts from inferences and identify what it could not verify. The findings become the plan's evidence/context section, not a separate saved research file by default.

### When to save work in a file

- Every epic or story plan is a durable Markdown file with a clear name, for example `plans/add-login.md`.
- Small task plans may be a checked task section inside their parent story plan rather than separate files.
- Planning research normally lives in the evidence/context section of the plan it supports.
- Create a clearly named file, for example `research/payment-options.md`, only when the user asks for a standalone research result, the research is reusable across more than one plan, or the investigation is substantial enough to need separate review.
- A plan that uses a standalone research result must link to it and summarize the planning-relevant conclusions.

### Decision support

`decision-support` helps you choose, rather than merely collecting information. For each viable option it records the problem, constraints, evidence, benefits, costs, risks, implementation impact, reversibility, and confidence. It then gives a recommendation, explains why, and lists the specific question or evidence that could change that recommendation. The user remains the decision-maker for material product, architecture, cost, or security choices.

## Learning loop

The kit will improve through explicit, evidence-based feedback rather than silently rewriting its own instructions.

```text
completed work
  → delivery and handoff
  → retrospective
  → case study (when the work is significant or especially instructive)
  → candidate improvements
  → review and approve
  → update project context, templates, or skills
  → validate the change against prior examples
```

### Retrospective trigger

Run a lightweight retrospective after every successful implementation, completed fix, or completed research/design decision. It should be optional after a purely conversational chat with no durable outcome, so the kit does not create noisy records.

The retrospective records:

- What was intended and what was delivered.
- What evidence verified the result.
- Friction, surprises, rework, and unresolved risks.
- One to three concrete improvement candidates, ranked by expected value.

### Case studies

Create a case study for a substantial feature, difficult bug, unusual failure, or process experiment. Each case study includes context, constraints, decision points, approach, outcome, measurable evidence where available, lessons, and links to the resulting artifacts. The collection becomes a local playbook that future skills can consult.

### Safe self-improvement policy

- Retrospectives may propose changes automatically, but may not silently alter active skills, project guidance, commands, or external settings.
- A candidate becomes an adopted improvement only after review and a recorded rationale.
- Recurring evidence takes priority over a one-off preference; a change should be tested against an existing case study or example before promotion.
- Maintain a changelog so a harmful or ineffective process change can be identified and reverted.

## Review and handoff visibility

### Diff-first code review

The `code-review` skill must establish the comparison range before it evaluates a change (for example, a working-tree diff, branch comparison, or named commits). Its output includes the actual diff, or a stable link/path and exact command that renders it. Each finding identifies the changed file and line or diff hunk it concerns. A review cannot report that it examined changes when no concrete comparison range is available.

### Reader-ready handoffs

Use the selected `ste100` skill on every handoff, delivery note, or retrospective the user is expected to read. The handoff must lead with the outcome, use short direct sentences, explain any unavoidable technical term on first use, and separate facts, verification evidence, risks, and next actions. Internal scratch notes and raw tool output do not need this pass.

The kit will describe these handoffs as "reviewed with the `ste100` skill." It will not state that they are formally compliant with ASD-STE100 unless the required controlled-language validation is available and has passed.

## Planned repository shape

```text
skills/
  <skill-name>/
    SKILL.md
    references/             # only when progressive disclosure is useful
    scripts/                # optional; reviewed and tested
templates/
  spec.md
  implementation-plan.md
  handoff.md
research/                  # standalone research only when requested or reusable
specs/                     # accepted story/feature specifications
plans/                     # epic and story implementation plans
case-studies/              # significant completed work
examples/
  <skill-name>/
docs/
  architecture.md
  compatibility.md
  distribution.md
  provenance.md
tests/
  skill-evals/
```

## Phased delivery

### Phase 1 — Foundation

1. Define the portable `SKILL.md` template and metadata conventions, with Codex-first installation guidance.
2. Create `docs/provenance.md` and record source, licence, and adaptation notes for every externally inspired asset.
3. Create `docs/compatibility.md` and `docs/distribution.md` covering private sharing, versioning, and future Claude Code/Cursor adapters.
4. Select, licence-review, and add the Codex-compatible `ste100` skill as a separately versioned dependency or local adapter.
5. Add a lightweight evaluator/checklist for frontmatter, links, referenced files, unsafe scripts, and reader-facing handoff requirements.

### Phase 2 — Core flow

1. Author `repository-orientation`, `decision-support`, `grill-requirements`, `specification`, and `implementation-plan`.
2. Add project-map and decision-record templates, plus one end-to-end example.
3. Test the handoff from planning research → decision → grilled brief → spec → plan.

### Phase 3 — Engineering quality

1. Author `test-first-implementation`, `debugging`, and `code-review`.
2. Require a defined comparison range and diff evidence in every `code-review` output.
3. Add Python and TypeScript reference checklists for test commands, packaging, dependency management, linting, typing, and common verification steps.
4. Add `security-review` as an opt-in high-risk-change gate.
5. Write scenario-based evaluations for Python and TypeScript bug fixes, small features, and refactors.

### Phase 4 — Specialization and operationalization

1. Add `frontend-quality` only if frontend work is a real recurring need.
2. Add `delivery-and-handoff`, `retrospective`, `case-study`, and `skill-authoring`.
3. Add the evidence-based learning loop, case-study template, improvement backlog, and changelog.
4. Complete the Codex adapter and validate a fresh private installation.
5. Add and validate Claude Code and Cursor adapters without changing the portable core.

## Acceptance criteria for v1

- All core skills pass structural validation and use explicit, unambiguous trigger descriptions.
- A user can complete a feature from brief to reviewed handoff using only kit artifacts.
- Every skill includes a concrete input/output example and a verification checkpoint.
- Every code review includes a concrete comparison range and the actual reviewed diff or a reproducible way to render it.
- Every reader-facing handoff is reviewed with the selected `ste100` skill and clearly separates outcome, evidence, risks, and next actions.
- Every completed implementation produces a lightweight retrospective and any accepted process change is traceable to evidence.
- Significant completed work can be captured as a reusable case study.
- No active skill requires unreviewed network access, credentials, or arbitrary shell execution.
- Third-party material is either not copied or is accompanied by an appropriate licence and provenance entry.
- The kit works with the selected primary agent before compatibility adapters are added.

## Decisions still needed

1. Decide the private sharing mechanism (private Git repository, archive releases, or another approved internal channel).
2. Identify the preferred Python and TypeScript toolchains to support first (for example `uv`/`pytest`/`ruff` and `pnpm`/`vitest`/`eslint`).
3. Choose the first real workflow to try with the kit: `repository-orientation`, `grill-requirements`, or the specification-to-plan chain.
