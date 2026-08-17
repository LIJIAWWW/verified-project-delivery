# Verified Project Delivery

[中文](#中文说明) | [English](#english)

A personal Codex skill for evidence-based project execution, truthful status reporting, dependency-aware multi-agent work, merge validation, and concise milestone handoffs.

一个用于 Codex 的个人 Skill：通过可验证证据管理项目进度，真实报告后台状态，协调多 Agent 依赖，并用精简交接减少重复上下文和 Token 消耗。

---

## 中文说明

### 为什么需要它

长期项目和多 Agent 项目容易出现这些问题：

- 把已经结束的任务误报为“后台仍在运行”；
- 把代码骨架、模拟数据或未审核数据当成完整功能；
- 多个任务表面并行，实际存在前后依赖；
- 子任务完成后没有做合并验证；
- 新任务反复读取全部聊天和仓库，浪费上下文与 Token。

`verified-project-delivery` 用一组轻量规则解决这些问题，不强制引入复杂项目管理流程。

### 核心能力

- **证据化状态**：用构建、测试、文件、日志或处理数量支持进度结论。
- **真实运行报告**：没有活跃 Agent、进程或近期产出时，不得声称任务仍在运行。
- **依赖感知并行**：允许合理数量的并行任务，但不把依赖阶段伪装成并行。
- **合并前验证**：子任务的完成消息只是待验证结论；合并前后都运行必要检查。
- **自适应文档**：根据项目规模决定是否创建状态、上下文、接口或数据字典。
- **精简交接**：新任务只读取交接指定的文档和相关代码，不默认重读全部历史。

### 自适应文档

| 项目类型 | 建议文档 |
|---|---|
| 小型、单次修改 | 不创建治理文档 |
| 中型、多步骤项目 | `PROJECT_STATUS.md` |
| 长期项目 | `PROJECT_STATUS.md` + `PROJECT_CONTEXT.md` |
| 多 Agent 项目 | 按需增加 `AGENTS.md` |
| 接口复杂项目 | 按需增加 `API_CONTRACT.md` |
| 数据口径复杂项目 | 按需增加 `DATA_DICTIONARY.md` |

Skill 中的 `assets/` 提供这些文档的轻量模板。已有项目文档不会被直接覆盖。

### 安装

#### 方式一：通过 Codex 安装

在 Codex 中请求：

```text
请从 https://github.com/LIJIAWWW/verified-project-delivery 安装这个个人 Skill。
```

#### 方式二：手动安装

将仓库克隆到个人 Codex Skills 目录：

```powershell
git clone https://github.com/LIJIAWWW/verified-project-delivery.git "$env:USERPROFILE\.codex\skills\verified-project-delivery"
```

如果目标目录已经存在，请先确认其中是否有需要保留的本地修改，再更新或替换。

### 使用示例

初始化或接管长期项目：

```text
使用 $verified-project-delivery 初始化并管理这个项目。
```

检查真实进度：

```text
使用 $verified-project-delivery 审计当前项目进度。
如果没有后台任务运行，请明确说明。
```

完成里程碑交接：

```text
使用 $verified-project-delivery 更新里程碑状态，运行合并验证，
并生成下一任务所需的精简交接。
```

### 状态定义

Skill 使用明确状态区分“已写代码”和“真正完成”：

- `pending`：尚未开始；
- `running`：确有活跃执行和近期产出证据；
- `blocked`：被依赖、决策、权限或资源阻塞；
- `implemented`：代码或内容已落地，但尚未验证；
- `verified`：当前任务的验收检查已通过；
- `integrated`：合并后验证已通过；
- `completed`：用户可见的验收目标已经满足；
- `stopped`：当前没有任务运行。

---

## English

### Why this skill exists

Long-running and multi-agent projects often fail in predictable ways:

- a finished task is incorrectly reported as still running in the background;
- scaffolding, mock data, or unreviewed output is presented as a complete feature;
- dependent stages are described as parallel work;
- delegated work is merged without direct verification;
- new tasks repeatedly load the full conversation and repository, wasting context and tokens.

`verified-project-delivery` addresses these problems with lightweight delivery rules rather than a heavy project-management framework.

### Core capabilities

- **Evidence-based status**: support progress claims with builds, tests, files, logs, or processing counts.
- **Truthful running state**: never claim background execution without an active agent or process and recent output evidence.
- **Dependency-aware parallelism**: parallelize genuinely independent work without imposing a fixed agent limit.
- **Merge validation**: treat delegated completion as a claim and run the relevant checks before and after integration.
- **Adaptive documentation**: create only the project documents justified by project complexity.
- **Concise handoffs**: tell the next task exactly which documents and code to read instead of reloading all history.

### Adaptive documentation

| Project type | Suggested documents |
|---|---|
| Small, bounded change | None |
| Medium, multi-step project | `PROJECT_STATUS.md` |
| Long-running project | `PROJECT_STATUS.md` + `PROJECT_CONTEXT.md` |
| Multi-agent project | Add `AGENTS.md` when needed |
| Non-trivial component interfaces | Add `API_CONTRACT.md` when needed |
| Substantial shared data semantics | Add `DATA_DICTIONARY.md` when needed |

Lightweight templates are available in `assets/`. Existing useful project documents should be merged carefully, never blindly overwritten.

### Installation

#### Option 1: Ask Codex to install it

```text
Install this personal skill from https://github.com/LIJIAWWW/verified-project-delivery.
```

#### Option 2: Install manually

Clone the repository into your personal Codex Skills directory:

```powershell
git clone https://github.com/LIJIAWWW/verified-project-delivery.git "$env:USERPROFILE\.codex\skills\verified-project-delivery"
```

If the target directory already exists, inspect and preserve any local changes before updating or replacing it.

### Usage examples

Start or take over a substantial project:

```text
Use $verified-project-delivery to initialize and manage this project.
```

Audit actual progress:

```text
Use $verified-project-delivery to audit this project's status.
Explicitly state when no background task is running.
```

Create a milestone handoff:

```text
Use $verified-project-delivery to update milestone status, run integration checks,
and produce a concise handoff for the next task.
```

### Status model

- `pending`: not started;
- `running`: active execution with recent evidence;
- `blocked`: waiting on a dependency, decision, permission, or resource;
- `implemented`: changes exist but have not passed verification;
- `verified`: task-level acceptance checks passed;
- `integrated`: merged and integration checks passed;
- `completed`: the user-visible acceptance condition is satisfied;
- `stopped`: no work is currently running.

## Repository structure

```text
verified-project-delivery/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── assets/
    ├── AGENTS.md
    ├── API_CONTRACT.md
    ├── DATA_DICTIONARY.md
    ├── PROJECT_CONTEXT.md
    └── PROJECT_STATUS.md
```

## Contributing

Issues and pull requests are welcome. Keep the skill lightweight: add a rule or resource only when it reduces ambiguity, rework, false status reporting, or context cost.

