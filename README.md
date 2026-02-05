# Weiran Agent Skills

Skills 是包含指令、脚本和资源的文件夹，Claude 可以动态加载它们以提升特定任务的表现。Skills 教会 Claude 以可重复的方式完成特定任务，无论是按照公司规范撰写文档、使用特定工作流分析数据，还是自动化日常任务。

更多信息请参考：
- [What are skills?](https://support.anthropic.com/en/articles/12512176-what-are-skills)
- [Using skills in Claude](https://support.anthropic.com/en/articles/12512180-using-skills-in-claude)
- [How to create custom skills](https://support.anthropic.com/en/articles/12512198-creating-custom-skills)

# 关于本仓库

本仓库包含 Weiran 公司内部使用的 Agent Skills，覆盖产品研发流程中的各类专业场景。Skills 按领域分为多个 Plugin：

| Plugin | 领域 | 命令 |
|--------|------|------|
| **weiran-eng** | 研发流程 | `/weiran-eng:brd-interviewer`, `/weiran-eng:uc-interviewer`, `/weiran-eng:prd-writer`, `/weiran-eng:prd-reviewer`, `/weiran-eng:prd-studio`, `/weiran-eng:api-writer`, `/weiran-eng:api-reviewer`, `/weiran-eng:guardrails-writer`, `/weiran-eng:guardrails-reviewer`, `/weiran-eng:hld-writer`, `/weiran-eng:hld-reviewer`, `/weiran-eng:runbook-writer` |
| **weiran-llm** | AI/LLM 工具 | `/weiran-llm:skill-creator`, `/weiran-llm:prompt-optimizer` |
| **weiran-mrkt** | 营销内容 | `/weiran-mrkt:media-writer` |
| **weiran-bot** | 测试平台（通用版） | `/weiran-bot:case`, `/weiran-bot:case-writing`, `/weiran-bot:pipeline`, `/weiran-bot:tests`, `/weiran-bot:debug`, `/weiran-bot:orchestrator`, `/weiran-bot:workspace` |

# 仓库结构

```
weiran-agent-skills/
├── plugins/                    # 按领域分组的 Plugins
│   ├── weiran-eng/             # 研发流程工具集
│   │   ├── commands/           # CLI 命令（/weiran-eng:xxx）
│   │   └── skills/             # 完整实现
│   ├── weiran-llm/             # AI/LLM 工具集
│   │   ├── commands/
│   │   └── skills/
│   ├── weiran-mrkt/            # 营销内容工具集
│   │   ├── commands/
│   │   └── skills/
│   └── weiran-bot/             # Weiran 测试平台（通用版，跨平台兼容）
│       ├── commands/
│       └── skills/
└── CHANGELOG.md                # 版本变更记录
```

# 在 Claude Code 中使用

## 安装

```
/plugin marketplace add weiran-tech/weiran-agent-skills
```

然后选择要安装的 plugin：
1. 选择 `Browse and install plugins`
2. 选择 `weiran-agent-skills`
3. 选择需要的 plugin：
   - `weiran-eng` - 研发流程（BRD/PRD/HLD）
   - `weiran-llm` - AI 工具（Skill/Prompt）
   - `weiran-mrkt` - 营销内容（自媒体）
   - `weiran-bot` - Weiran 测试平台（通用版，跨平台兼容）
4. 选择 `Install now`

## 使用

安装后，可以通过 `/` 命令调用：

```
/weiran-eng:prd-writer 写一个用户登录功能的 PRD
/weiran-eng:prd-reviewer ./docs/prd-login.md
/weiran-llm:prompt-optimizer 帮我优化这个提示词...
/weiran-mrkt:media-writer 写一篇关于 AI 的公众号文章
```

## 更新

```
/plugin marketplace remove weiran-eng
/plugin marketplace add weiran-tech/weiran-agent-skills
```

# 包含的 Skills

## weiran-eng（研发流程）

| 命令 | 描述 |
|------|------|
| `/weiran-eng:brd-interviewer` | 业务需求访谈专家，通过选择题引导 stakeholder 输出结构化 BRD |
| `/weiran-eng:uc-interviewer` | 用户旅程访谈专家，在 BRD 和 PRD 之间建立对齐检查点 |
| `/weiran-eng:prd-writer` | PRD 写作技能，支持多种类型：新功能、第三方集成、重构、优化 |
| `/weiran-eng:prd-reviewer` | PRD 审查专家，作为「准出门禁」从多角色视角全面审查 |
| `/weiran-eng:prd-studio` | PRD 全自动工作室，自动完成写→审→改→审循环，无需人工干预 |
| `/weiran-eng:api-writer` | API 契约撰写助手，支持 9 种协议，PRD→Contract 100% 覆盖检查 |
| `/weiran-eng:api-reviewer` | API 契约评审门禁，检查完整性/一致性/兼容性 |
| `/weiran-eng:guardrails-writer` | 工程规范编写助手，产出项目级 Guardrails |
| `/weiran-eng:guardrails-reviewer` | 工程规范审查门禁，检查覆盖性与可执行性 |
| `/weiran-eng:hld-writer` | HLD 写作技能，基于 PRD + API Contract 做技术决策 |
| `/weiran-eng:hld-reviewer` | HLD 审查专家，模拟 Design Review 会议，重点检测 PRD→HLD 漂移 |
| `/weiran-eng:runbook-writer` | 运维手册（Runbook）编写协调器，基于 HLD/LLD 产出生产就绪的运维手册 |

## weiran-llm（AI/LLM 工具）

| 命令 | 描述 |
|------|------|
| `/weiran-llm:skill-creator` | Skill 创建指南，帮助创建和优化 Claude Code Skills |
| `/weiran-llm:prompt-optimizer` | AI 提示词优化专家，支持 Claude、ChatGPT、DeepSeek、豆包、智谱、Gemini 等多平台 |

## weiran-mrkt（营销内容）

| 命令 | 描述 |
|------|------|
| `/weiran-mrkt:media-writer` | 自媒体内容创作工作流，支持公众号、知乎、小红书、LinkedIn、Medium、Reddit |

## weiran-bot（测试平台 - 通用版）

跨平台兼容版本，适用于 VS Code Copilot、GitHub Copilot 等 AI 平台。需要配置 weiran MCP Server。

| 命令 | 描述 |
|------|------|
| `/weiran-bot:case` | 测试用例管理 - 创建、配置、更新用例，上传脚本 |
| `/weiran-bot:case-writing` | 测试脚本编写 - 根据需求生成测试用例文档和脚本 |
| `/weiran-bot:pipeline` | 流水线编排 - 创建 Pipeline，配置依赖和 Relay |
| `/weiran-bot:tests` | 测试执行 - 触发 Pipeline 执行，监控状态 |
| `/weiran-bot:debug` | 故障诊断 - 分析失败原因，查看日志 |
| `/weiran-bot:orchestrator` | 测试编排 - 创建门禁、定时计划，提供集成代码 |
| `/weiran-bot:workspace` | 工作空间管理 - 成员管理、权限配置 |

# 创建自定义 Skill

Skill 的创建很简单 - 只需一个包含 `SKILL.md` 文件的文件夹。`SKILL.md` 包含 YAML frontmatter 和 Markdown 指令：

```markdown
---
name: my-skill-name
description: 清晰描述这个 skill 做什么，以及什么时候应该使用它
---

# My Skill Name

[在这里添加 Claude 执行此 skill 时需要遵循的指令]
```

Frontmatter 只需要两个字段：
- `name` - skill 的唯一标识符（小写，用连字符分隔）
- `description` - 完整描述 skill 的功能和使用场景

更多详情请使用 `/weiran-llm:skill-creator`，或参考 [skill-authoring.md](./plugins/weiran-llm/skills/skill-creator/references/skill-authoring.md)。

# 许可证

MIT License - 详见 [LICENSE](LICENSE)

# 联系方式

- Email: engineering@weiran.io
- Website: https://weiran.io
