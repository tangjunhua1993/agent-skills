# Agent Skills 中文说明

**面向 AI 编程代理的工程化技能包。**

Agent Skills 将资深工程师在软件开发中的工作方式沉淀为一组可复用的技能、命令、检查清单和专家角色，让 AI Agent 在需求定义、计划拆解、编码实现、测试验证、代码评审和上线发布等阶段遵循更稳定的工程流程。

这个项目不是普通提示词合集。它更像一套给 AI Agent 使用的“工程工作法”：每个技能都包含触发条件、执行步骤、质量门槛、反偷懒规则和验证要求，帮助 Agent 少走捷径、少跳步骤、少凭感觉交付。

## 项目定位

- 项目名称：Agent Skills
- 当前版本：`1.0.0`
- 适用对象：Claude Code、Cursor、Gemini CLI、OpenCode、GitHub Copilot、Codex 以及其他支持 Markdown 指令或技能文件的 Agent 环境
- 核心目标：让 AI Agent 在完整软件开发生命周期中保持清晰、可验证、可审查的工程行为

## 它解决什么问题

AI 编程代理默认倾向于走最短路径：直接写代码、跳过规格、弱化测试、忽略回滚方案，或者在复杂任务中一次性改太多文件。Agent Skills 的目标是把这些容易失控的行为约束成可执行流程。

它帮助 Agent 做到：

- 先定义需求和边界，再开始写代码
- 把大任务拆成小的、可验证的工作单元
- 用测试、构建、运行结果和日志作为完成证据
- 在合并前进行代码质量、安全、性能和可维护性检查
- 在发布前准备回滚、监控、文档和风险说明

## 核心能力

### 1. 覆盖完整开发生命周期

项目提供 20 个核心技能，覆盖从想法到上线的完整流程。

| 阶段 | 技能 |
| --- | --- |
| 定义 | `idea-refine`、`spec-driven-development` |
| 计划 | `planning-and-task-breakdown` |
| 构建 | `incremental-implementation`、`test-driven-development`、`context-engineering`、`source-driven-development`、`frontend-ui-engineering`、`api-and-interface-design` |
| 验证 | `browser-testing-with-devtools`、`debugging-and-error-recovery` |
| 评审 | `code-review-and-quality`、`code-simplification`、`security-and-hardening`、`performance-optimization` |
| 发布 | `git-workflow-and-versioning`、`ci-cd-and-automation`、`deprecation-and-migration`、`documentation-and-adrs`、`shipping-and-launch` |
| 元技能 | `using-agent-skills` |

### 2. 七个生命周期命令

项目提供 7 个 slash command，用来把常见开发动作映射到对应技能。

| 命令 | 用途 |
| --- | --- |
| `/spec` | 定义需求、目标、约束和验收标准 |
| `/plan` | 拆解实施计划和任务依赖 |
| `/build` | 按薄切片方式增量实现 |
| `/test` | 编写、运行并解释测试结果 |
| `/review` | 进行代码质量评审 |
| `/code-simplify` | 简化复杂代码，降低维护成本 |
| `/ship` | 做发布前检查和上线准备 |

这些命令是入口，底层会触发相应技能和检查规则。

### 3. 三个专家 Agent 角色

项目内置 3 个专家 persona，适合在高风险改动或合并前调用。

- `code-reviewer`：以资深 Staff Engineer 的标准评审代码质量
- `test-engineer`：关注测试策略、覆盖率、可验证性和回归风险
- `security-auditor`：关注安全漏洞、威胁建模、OWASP 风险和边界防护

### 4. 多工具适配

Agent Skills 可以接入多个 Agent 环境：

- Claude Code：通过插件、slash commands 和 skills 使用
- Cursor：通过 rules 或技能内容引用使用
- Gemini CLI：通过 native skills 或 `GEMINI.md` 使用
- Windsurf：通过 rules 配置使用
- OpenCode：通过 `AGENTS.md` 和 skill 工具流程使用
- GitHub Copilot：通过 agent persona 和 copilot instructions 使用
- Codex / 其他 Agent：通过 Markdown 指令文件使用

具体接入方式见 `docs/` 目录下的工具说明。

## 设计原则

### 流程优先

技能不是百科知识，而是 Agent 需要执行的工作流程。每个技能都强调“先做什么、再做什么、什么时候停止、如何证明完成”。

### 验证优先

每个技能都要求提供证据，例如测试通过、构建成功、浏览器运行结果、日志、截图、性能数据或人工可复核的检查结果。

### 反偷懒

技能会显式反驳常见借口，例如：

- “这个改动很小，不需要测试”
- “先写完再整理”
- “稍后再补文档”
- “看起来应该没问题”

这些规则用于避免 Agent 在关键质量门槛上省略步骤。

### 渐进式上下文

每个技能以 `SKILL.md` 为入口，只有在需要时才加载参考资料，避免一次性塞入过多上下文。

## 适合使用的场景

- 从 0 到 1 设计和实现新功能
- 多文件、多模块或跨系统改动
- 需要测试驱动、规格驱动或源码依据的任务
- 前端 UI、API、性能、安全、CI/CD 等专业工程任务
- 发布前质量检查、代码评审和风险确认
- 希望让 AI Agent 更像稳定工程同事，而不是一次性代码生成器

## 不适合使用的场景

- 只需要快速回答一个概念问题
- 非工程类纯写作或内容生成
- 极小的临时代码片段，且不需要维护、测试或评审
- 明确只想快速试验、不希望遵守严格流程的任务

## 推荐使用方式

一个完整任务可以按下面的节奏推进：

1. 用 `/spec` 明确目标、边界和验收标准。
2. 用 `/plan` 拆成小任务，控制改动范围。
3. 用 `/build` 做增量实现，每一步都保持可运行。
4. 用 `/test` 证明行为符合预期。
5. 用 `/review` 检查代码质量、风险和可维护性。
6. 用 `/code-simplify` 清理不必要的复杂度。
7. 用 `/ship` 做发布前检查、回滚准备和上线说明。

如果不使用 slash command，也可以直接引用某个技能文件，例如：

```text
Use skills/test-driven-development/SKILL.md to implement this change with tests.
```

## 项目结构

```text
agent-skills/
├── skills/              # 20 个核心技能
├── agents/              # 3 个专家 Agent 角色
├── references/          # 测试、安全、性能、可访问性等参考清单
├── hooks/               # 会话生命周期 hook
├── .claude/commands/    # Claude Code slash commands
├── .gemini/commands/    # Gemini CLI commands
└── docs/                # 不同工具的接入说明
```

## 版本状态

`1.0.0` 是一个稳定的初始版本，已经具备完整生命周期覆盖、多工具接入、专家 Agent 角色和参考检查清单。后续可以继续补充更多场景化示例、团队落地模板和不同 Agent 平台的原生适配方式。

## License

MIT。
