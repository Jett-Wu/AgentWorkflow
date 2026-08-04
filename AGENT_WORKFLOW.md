# General Multi-Agent Coding Project Workflow

Use this file when initializing a software project that will be developed with one or more coding agents.

The workflow is tool-independent. It is designed for Codex, Claude Code, DeepSeek-based agents, and similar tools.

Its purpose is to preserve:

- approved project intent;
- current task state;
- reusable decisions and lessons;
- objective verification evidence;

without duplicating information already available from code, tests, configuration, or Git.

---

## 1. Core Files

Maintain these four files in the repository root:

```text
AGENTS.md
PROJECT.md
TASK.md
DEVLOG.md
```

Each file has one responsibility:

| File | Canonical question |
|---|---|
| `AGENTS.md` | How must agents work in this repository? |
| `PROJECT.md` | What must the project achieve, and what is the current system-level truth? |
| `TASK.md` | What is the active task, and where does it stand? |
| `DEVLOG.md` | Which past decisions, failures, and milestones still matter? |

Use existing engineering artifacts for everything else:

| Information | Source of truth |
|---|---|
| Exact code changes | Git diff and commit history |
| Correctness | Tests, CI, type checks, lint, and runtime checks |
| Dependencies and versions | Package and lock files |
| Detailed API or schema truth | Code, schema files, and generated documentation |
| Routine task history | Git commits or an issue tracker |

Do not create additional management files such as `MEMORY.md`, `STATUS.md`,
`PROGRESS.md`, `HANDOFF.md`, `CONTEXT.md`, or `PLAN.md` unless a scaling rule
in this workflow requires one.

---

## 2. Initialization

When applying this workflow to a new or existing repository:

1. Inspect the user request, README, repository layout, configuration files,
   package files, tests, and current Git state.
2. Create or update the four core files using verified facts only.
3. Convert the user's request into a concise requirement baseline in `PROJECT.md`.
   Do not paste the full conversation.
4. Ask the user to approve the requirement baseline before substantial
   implementation when the project is new or materially underspecified.
5. Mark uncertain information as `To confirm`.
6. Do not modify product code during documentation-only initialization.
7. Do not duplicate information already represented reliably by code,
   configuration, tests, or Git.

---

## 3. `AGENTS.md`

### Purpose

`AGENTS.md` is the short repository entry point for every coding agent.

It contains:

- required reading order;
- verified development commands;
- repository-specific constraints;
- review and completion rules;
- pointers to project and task state.

It must not become a project encyclopedia.

### Template

````markdown
# AGENTS.md

## Read first

Before changing code:

1. Read `PROJECT.md`.
2. Read `TASK.md`.
3. Search `DEVLOG.md` only for entries related to the current component or risk.
4. Inspect the relevant code, tests, and current Git diff.

Do not rely on previous chat history.
If documentation conflicts with verified repository behavior, investigate the
conflict and update the stale source within the current task scope.

## Commands

```bash
# Setup
[verified command or To confirm]

# Run
[verified command or To confirm]

# Test
[verified command or To confirm]

# Full check
[verified command or To confirm]
```

## Rules

- Preserve the approved requirements and constraints in `PROJECT.md`.
- Work within the boundaries and acceptance criteria in `TASK.md`.
- Follow existing repository conventions.
- Make the smallest coherent change that satisfies the task.
- Do not perform unrelated refactoring.
- Do not silently change public interfaces, schemas, dependencies,
  architecture, or approved requirements.
- Do not invent repository facts or claim unrun checks passed.
- Add or update tests when behavior changes.
- Never expose or commit credentials, secrets, private keys, or private data.
- Use Git for exact change history.
- Keep management files current, concise, and non-duplicative.

## Work cycle

1. Verify the task against the repository.
2. Clarify ambiguous acceptance criteria before implementation.
3. Implement incrementally.
4. Run relevant checks.
5. Review the diff for regressions, scope creep, and accidental changes.
6. Update `TASK.md` before stopping.
7. Update `PROJECT.md` or `DEVLOG.md` only when their update conditions are met.

## Review policy

- **Low risk:** self-review plus relevant automated checks.
- **Medium risk:** explicit diff review plus relevant checks.
- **High risk:** relevant checks plus review by a different agent or fresh context.

High-risk work includes security-sensitive code, authentication, authorization,
data migrations, public API changes, core schema changes, billing, concurrency,
and broad architectural refactors.

## Done means

- The acceptance criteria in `TASK.md` are satisfied.
- Relevant checks were run, or the inability to run them is recorded.
- The final diff contains no unrelated changes.
- Required review is complete.
- `TASK.md` states completion or one exact next step.
````

### Maintenance

Update `AGENTS.md` only when:

- a stable repository command changes;
- a repository-wide constraint changes;
- a recurring agent failure reveals a missing rule;
- the review or completion policy changes.

Remove stale or obvious instructions. Prefer executable checks over prose rules.

Recommended size: approximately 60–120 lines.

---

## 4. `PROJECT.md`

### Purpose

`PROJECT.md` is the project-level contract and system map.

It contains:

1. an approved requirement baseline;
2. controlled requirement amendments;
3. a project-level capability map;
4. the current system-level structure and constraints.

The baseline prevents drift, but it is not permanently immutable. Requirement
changes require explicit approval and an amendment entry.

### Template

````markdown
# PROJECT.md

## Requirement baseline

**Project:** [name]

**Problem:**  
[What real problem must the project solve?]

**Target outcome:**  
[What should exist when the project is successful?]

**Primary users or use cases:**  
[Who uses it and for what? Delete if irrelevant.]

**Core workflow:**  
[One-line end-to-end workflow.]

### Required capabilities

- **R1:** [essential capability]
- **R2:** [essential capability]
- **R3:** [essential capability]

### Non-goals

- **N1:** [explicit exclusion]
- **N2:** [explicit exclusion]

### Project-level success criteria

- **S1:** [observable project-level criterion]
- **S2:** [observable project-level criterion]

### Non-negotiable constraints

- **C1:** [privacy, compatibility, cost, quality, deployment, or other constraint]
- **C2:** [constraint]

> Agents must not silently rewrite this baseline.
> Changes require explicit user approval and an amendment entry.

## Requirement amendments

- **A1 — YYYY-MM-DD:** [approved change, affected IDs, and reason]
- None

## Capability map

| ID | Capability | Status | Evidence |
|---|---|---|---|
| R1 | [capability] | Not started / Partial / Verified | [test, path, release, or None] |
| R2 | [capability] | Not started / Partial / Verified | [evidence or None] |

Mark a capability `Verified` only when objective evidence exists.

## Current system map

**Stage:** [planning / prototype / implementation / integration / stabilization]

**Current workflow:**  
[current end-to-end data or control flow]

**Main components:**

- `[path or component]`: [responsibility and current system-level status]
- `[path or component]`: [responsibility and current system-level status]

**Important interfaces or schemas:**

- `[path or interface]`: [purpose]
- `[path or interface]`: [purpose]

**Confirmed technical choices:**

- [current effective choice]
- [current effective choice]

**Project-level risks or open questions:**

- [issue affecting multiple tasks or project direction]
- None
````

### Traceability

Every implementation task must reference one or more requirement, success, or
constraint IDs:

```text
Related project items: R2, S1, C1
```

A task that cannot be linked to the baseline should be identified explicitly as
maintenance work, technical debt, or an approved requirement change.

### Maintenance

Update `PROJECT.md` when:

- the user approves a requirement change;
- a capability obtains new objective evidence;
- the system workflow or a major component boundary changes;
- a public interface or core schema changes;
- an important technical choice becomes effective;
- a project-level risk appears or is resolved;
- the project enters a new stage.

Do not add task transcripts, detailed file changes, routine bug history, or raw
discussions. Replace stale current-state descriptions instead of appending old
versions.

Recommended size: approximately 120–250 lines.

---

## 5. `TASK.md`

### Purpose

`TASK.md` is the active work contract and handoff state for one task.

It links project intent to implementation and verification.

### Template

````markdown
# TASK.md

## Identity

**Task:** T-[number] — [short name]  
**Related project items:** [R#, S#, C#, or maintenance rationale]  
**Risk:** Low / Medium / High  
**Status:** Ready / In progress / Blocked / Review / Done

## Goal

[One concrete, observable outcome.]

## Boundaries

**In scope:**

- [required work]
- [required work]

**Out of scope:**

- [explicit exclusion]
- [explicit exclusion]

## Acceptance criteria

- [ ] [observable completion condition]
- [ ] [observable completion condition]
- [ ] Relevant automated checks pass.
- [ ] No unrelated changes are introduced.
- [ ] Required review for the stated risk level is complete.

## Plan

1. [step]
2. [step]
3. [step]

Delete this section for a trivial task.

## Current state

**Completed:**

- [meaningful completed result]
- None

**In progress:**

- [unfinished work]
- None

**Exact next step:**

- [one action another agent can execute immediately]

**Blockers:**

- [blocker and what would resolve it]
- None

## Verification

- `[command or manual check]` → Passed / Failed / Not run
- `[command or manual check]` → Passed / Failed / Not run

## Task notes

- [Only decisions, constraints, failed attempts, or facts needed to continue.]
- Delete this section when unnecessary.
````

### Task design

A task should:

- produce one coherent outcome;
- have observable acceptance criteria;
- be small enough for one primary agent to own;
- avoid unrelated refactoring;
- leave the repository in a coherent state;
- reference the project baseline or state a maintenance rationale.

Split a task when it contains independent deliverables or acceptance criteria
that can succeed separately.

### Maintenance

Update `TASK.md`:

- after a meaningful unit of work;
- when boundaries or acceptance criteria change;
- when a blocker or failed approach affects continuation;
- after verification;
- before switching agents or ending a session.

Do not record every command, edit, or thought.

Recommended size: approximately 50–120 lines.

---

## 6. `DEVLOG.md`

### Purpose

`DEVLOG.md` stores historical context that cannot be reconstructed reliably from
Git alone.

It is a curated decision-and-learning log, not an activity diary.

Record only:

- meaningful milestones;
- cross-task decisions and their rationale;
- failed approaches future agents might repeat;
- difficult root causes and reusable lessons;
- changes in project direction.

### Template

````markdown
# DEVLOG.md

## Usage

Search this file by requirement ID, component, decision, or error keyword.
Do not read the entire file by default.

Do not record routine edits, full logs, code diffs, or facts recoverable from Git.

## Entries

### D-[number] — YYYY-MM-DD — [decision, milestone, or lesson]

- **Type:** Decision / Milestone / Failed approach / Root-cause lesson
- **Related:** [R#, task ID, component, issue, or None]
- **Context:** [brief problem or trigger]
- **Outcome:** [what became true]
- **Rationale or lesson:** [why future work should care]
- **Do not repeat:** [failed path or None]
- **Evidence:** [commit, test, issue, benchmark, or path]
````

### Entry threshold

Add an entry only when at least one is true:

- future agents could otherwise repeat a costly mistake;
- a decision constrains more than one future task;
- the project reaches a meaningful capability milestone;
- the root cause is not obvious from the final code;
- the project direction or requirement interpretation changes.

Do not add ordinary implementation progress, minor bug fixes, formatting, or
information already clear from commit messages and diffs.

### Size control

When `DEVLOG.md` grows:

1. merge related entries into phase summaries;
2. remove details that no longer affect future work;
3. retain evidence links or commit references;
4. keep recent and high-impact entries;
5. rely on Git for removed detail.

Recommended active size: approximately 20–40 high-value entries.

---

## 7. Standard Workflow

### Start a new project

1. Initialize the four core files.
2. Ask the user to approve the requirement baseline.
3. Define the first task in `TASK.md`.
4. Establish at least one executable setup, test, or smoke-check command.
5. Begin implementation incrementally.

### Start a new task

1. Read `AGENTS.md` and `PROJECT.md`.
2. Search `DEVLOG.md` for related requirement IDs, components, and failures.
3. Inspect relevant code, tests, `git status`, and the current diff.
4. Replace `TASK.md` with one scoped task.
5. Link the task to project IDs.
6. Define observable acceptance criteria.
7. Assign a risk level.
8. Add a short plan only when needed.

Before replacing a completed `TASK.md`, preserve its work in Git.

### Continue with another agent

1. Read `AGENTS.md`, `PROJECT.md`, and `TASK.md`.
2. Search relevant `DEVLOG.md` entries.
3. Inspect Git state, recent commits, relevant code, and tests.
4. Verify that `TASK.md` matches repository reality.
5. Continue from `Exact next step`.
6. Correct stale documentation before relying on it.

Do not accept another agent's completion claim without evidence.

### Stop or hand off

Before stopping:

1. leave the repository in a coherent state where possible;
2. update task status, verification, blockers, and exact next step;
3. preserve meaningful work in Git;
4. do not create another handoff document;
5. update `DEVLOG.md` only when the entry threshold is met.

### Review and complete

1. Check every acceptance criterion.
2. Run relevant automated and manual checks.
3. Review the final diff.
4. Apply the review policy for the task's risk level.
5. Update `PROJECT.md` if project-level truth changed.
6. Add a `DEVLOG.md` entry only when warranted.
7. Mark the task done and preserve it in Git.

---

## 8. Scaling Rules

### Parallel work

A single root `TASK.md` is suitable only when one task is active at a time.

When two or more agents work concurrently:

1. use one isolated branch or worktree per task;
2. create task-specific files:

```text
tasks/active/T-001-short-name.md
tasks/active/T-002-short-name.md
```

3. assign one primary owner per task;
4. avoid concurrent edits to the same files unless explicitly coordinated;
5. record task dependencies;
6. remove or archive completed task files after their work is preserved in Git.

If an issue tracker already serves as the task system, it may replace task
Markdown files. Do not maintain the same task state independently in both places.

### Complex work

Create a task-specific executable plan only when the work is:

- multi-day or multi-session;
- a broad architectural refactor;
- an irreversible migration;
- dependent on multiple milestones;
- difficult to verify with a short acceptance list.

Example:

```text
plans/T-014-exec-plan.md
```

`TASK.md` should link to the plan rather than duplicate it. Do not create
planning files for routine tasks.

---

## 9. Context and Token Discipline

Default reading order:

```text
AGENTS.md
→ PROJECT.md
→ TASK.md or assigned task file
→ targeted DEVLOG.md search
→ task-relevant code and tests
```

Rules:

- Do not scan the entire repository unless broad discovery is required.
- Do not automatically load the entire `DEVLOG.md`.
- Keep each fact in one canonical place.
- Prefer paths, symbols, tests, and commit references over copied content.
- Remove stale information instead of appending corrections indefinitely.
- Preserve approved intent, not full chat transcripts.
- Use automated checks for enforceable rules.
- Use Git for exact history.
- Use Markdown only for intent, current state, rationale, and evidence links that
  cannot be reconstructed reliably elsewhere.
- Prune management files when they exceed their recommended size.

---

## 10. Responsibility Map

| Question | Canonical source |
|---|---|
| What must the project achieve? | `PROJECT.md` requirement baseline |
| Has a capability been achieved? | `PROJECT.md` capability map and evidence |
| What is the current system-level design? | `PROJECT.md` current system map |
| How must agents work? | `AGENTS.md` |
| What should be done now? | `TASK.md` or the assigned task file |
| Why was an important choice made? | `DEVLOG.md` |
| Which failed approaches should not be repeated? | `DEVLOG.md` |
| What exactly changed? | Git diff and history |
| Does the implementation work? | Tests and automated checks |

If two artifacts answer the same question, remove the duplication.
