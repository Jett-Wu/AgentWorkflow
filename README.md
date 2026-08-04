# AgentWorkflow

[English](#english) · [简体中文](#简体中文)

A lightweight workflow for keeping coding agents aligned across sessions with shared requirements, task state, decisions, and verification.

---

## English

AgentWorkflow is a tool-independent project workflow for developers who use Codex, Claude Code, DeepSeek-based agents, or other coding agents on the same repository.

It defines four lightweight project files:

```text
AGENTS.md
PROJECT.md
TASK.md
DEVLOG.md
```

### Files

| File | Purpose |
|---|---|
| `AGENTS.md` | Stable repository rules, commands, review policy, and completion criteria |
| `PROJECT.md` | Approved requirements and the current system-level view |
| `TASK.md` | The active task, scope, acceptance criteria, status, and next step |
| `DEVLOG.md` | Curated decisions, failed approaches, milestones, and reusable lessons |

Other information remains in its natural source of truth:

- exact changes → Git
- correctness → tests and CI
- dependencies → package and lock files
- API and schema details → code and schema files
- routine task history → commits or an issue tracker

### Workflow files

- [`AGENT_WORKFLOW.md`](AGENT_WORKFLOW.md) — English
- [`AGENT_WORKFLOW_CN.md`](AGENT_WORKFLOW_CN.md) — Simplified Chinese

### Quick start

Copy the preferred workflow file into a new or existing repository, then ask a coding agent:

```text
Read AGENT_WORKFLOW.md.

Inspect this repository and initialize the workflow.
Create or update AGENTS.md, PROJECT.md, TASK.md, and DEVLOG.md.
Use verified repository facts only.
Do not modify product code during initialization.
```

For the Chinese version:

```text
阅读 AGENT_WORKFLOW_CN.md。

检查当前仓库并初始化其中定义的工作流。
创建或更新 AGENTS.md、PROJECT.md、TASK.md 和 DEVLOG.md。
只使用经过验证的仓库事实。
初始化期间不要修改业务代码。
```

### Core principles

1. **One source of truth per question**  
   Requirements, active work, historical rationale, exact changes, and correctness each have a clear owner.

2. **Verify before continuing**  
   A new agent checks the task state against the code, Git diff, and tests instead of trusting previous claims.

3. **Control requirement changes**  
   Agents must not silently rewrite approved project requirements.

4. **Curate history**  
   `DEVLOG.md` stores only decisions and lessons that cannot be recovered reliably from Git.

5. **Prefer executable verification**  
   Tests, CI, linting, type checks, and runtime checks are stronger than prose-only rules.

6. **Scale only when necessary**  
   The default workflow stays small. Parallel task files or execution plans are introduced only when the project actually needs them.

### Suitable for

- solo developers switching between coding agents;
- small and medium software projects;
- multi-session development;
- agent-to-agent task handoffs and reviews;
- projects that need traceability without enterprise process overhead.

### This workflow does not replace

- Git;
- tests and CI;
- an existing issue tracker;
- formal specifications required by regulated or large organizational projects.

---

## 简体中文

AgentWorkflow 是一套与具体工具无关的项目开发工作流，适用于在同一代码仓库中交替使用 Codex、Claude Code、基于 DeepSeek 的编程智能体或其他 coding agent 的开发者。

它通过四个轻量级项目文件，让不同智能体能够共享项目要求、接续当前任务，并保留必要的决策与验证信息：

```text
AGENTS.md
PROJECT.md
TASK.md
DEVLOG.md
```

### 文件职责

| 文件 | 用途 |
|---|---|
| `AGENTS.md` | 稳定的仓库规则、命令、审查策略和完成标准 |
| `PROJECT.md` | 经确认的项目需求和当前系统级概览 |
| `TASK.md` | 当前任务、范围、验收条件、状态和下一步 |
| `DEVLOG.md` | 经过筛选的重要决策、失败方案、里程碑和可复用经验 |

其他信息继续由最合适的工程载体负责：

- 精确修改 → Git
- 正确性 → 测试与 CI
- 依赖版本 → package 和 lock 文件
- API 与 schema 细节 → 代码和 schema 文件
- 普通任务历史 → commit 或 Issue 管理系统

### 工作流文件

- [`AGENT_WORKFLOW.md`](AGENT_WORKFLOW.md) — 英文版
- [`AGENT_WORKFLOW_CN.md`](AGENT_WORKFLOW_CN.md) — 简体中文版

### 快速使用

把对应的工作流文件复制到新仓库或现有仓库，然后告诉编程智能体：

```text
阅读 AGENT_WORKFLOW_CN.md。

检查当前仓库并初始化其中定义的工作流。
创建或更新 AGENTS.md、PROJECT.md、TASK.md 和 DEVLOG.md。
只使用经过验证的仓库事实。
初始化期间不要修改业务代码。
```

### 核心原则

1. **每个问题只有一个事实源**  
   项目需求、当前任务、历史理由、精确修改和正确性分别由明确的载体负责。

2. **接手前先验证**  
   新智能体必须使用代码、Git diff 和测试核对任务状态，不能直接相信上一智能体的完成声明。

3. **受控修改需求**  
   编程智能体不得静默改写已经确认的项目需求。

4. **筛选历史信息**  
   `DEVLOG.md` 只保存无法从 Git 中可靠恢复的重要决策和经验。

5. **优先采用可执行验证**  
   测试、CI、lint、类型检查和运行检查优先于只写在 Markdown 中的规则。

6. **仅在必要时扩展**  
   默认工作流保持精简；只有实际出现并行开发或复杂长任务时，才增加独立任务文件或执行计划。

### 适用场景

- 单人开发者在多个编程智能体之间切换；
- 小型和中型软件项目；
- 跨多个会话持续开发；
- 不同智能体之间的任务交接和代码审查；
- 需要基本可追踪性，但不需要企业级流程的项目。

### 本工作流不能替代

- Git；
- 测试和 CI；
- 已经投入使用的 Issue 管理系统；
- 受监管项目或大型组织要求的正式规格体系。
