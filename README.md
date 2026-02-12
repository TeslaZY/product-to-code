# Long-Running Product Fullstack Agent

> 长期运行的全栈开发 Agent 插件 - 基于 Anthropic Long-Running Agents 方法论，从产品想法到上线部署，跨多个上下文窗口稳定运行

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/TeslaZY/Long-running_Product_Agent)

## 概述

Long-Running Product Fullstack Agent 是一个基于 [Anthropic 的 Long-Running Agents 方法论](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) 构建的 Claude Code 插件。它让 AI 能够跨多个上下文窗口稳定运行，完成完整的软件开发流程：

```
需求调研 → 技术规格 → UI/UX 设计 → 架构规划 → 编码实现 → 测试验证 → 代码审查 → 部署交付
```

**核心理念：** 用户只需说出产品想法，剩下的需求追问、文档生成、原型设计、代码开发就自动完成。

**Long-Running 模式：** 每个会话都能从上一个会话继续工作，通过结构化任务列表和进度文件保持连续性。

## 特性

- 🔄 **Long-Running 架构** - 跨多个上下文窗口稳定运行
- 📋 **任务列表系统** - `task-list.json` 作为唯一真实来源
- 🎯 **7 个精简命令** - 用户只需 `/init` → `/continue` → `/audit`
- 📝 **文档驱动开发** - Spec-Driven Development + 文档同步
- 🔧 **自动依赖管理** - `/init` 时自动检测并引导安装
- 🧪 **验证测试** - 每次开始前验证之前的工作仍然正常

## 安装

### 方式一：本地安装（推荐）

```bash
cd /path/to/Long-running_Product_Agent
/plugin install . --name long-running-product-agent
```

### 方式二：通过插件市场安装

```bash
/plugin marketplace add <marketplace-name>
/plugin install Long-running_Product_Agent@<marketplace-name>
```

### 验证安装

```bash
/help
```

应看到 7 个命令：`/init`, `/continue`, `/progress`, `/tasks`, `/feature`, `/update`, `/audit`

## 快速开始

### 0-1 模式（新建项目）

```bash
/init        # 首次会话：初始化项目、收集需求
/continue    # 后续会话：自动执行下一任务
/continue    # 继续执行...
/audit       # 部署前验收
```

### 迭代模式（修改现有项目）

```bash
/feature 添加用户个人资料页面   # 添加新功能
# 或
/update 修改登录流程           # 修改现有功能

/continue    # 实现新任务
/audit       # 验收
```

## 可用命令

| 命令 | 描述 | 使用时机 |
|------|------|----------|
| `/init` | 初始化项目 + 依赖检测 | 开始新项目 |
| `/continue` | **核心命令** - 继续执行下一任务 | 每个后续会话 |
| `/progress` | 查看当前项目进度 | 了解状态 |
| `/tasks` | 列出所有任务和状态 | 查看任务列表 |
| `/feature <描述>` | 添加新功能 | 迭代模式 |
| `/update <描述>` | 修改现有功能 | 迭代模式 |
| `/audit` | 对照产品文档验收 | 部署前 |

## 依赖管理

运行 `/init` 时会自动检测依赖并引导安装：

- **必需**：Git
- **可选**：uv（Python）、specify-cli（规格驱动开发）
- **插件**：superpowers（开发工作流）、ui-ux-pro（UI 设计）

详见 [DEPENDENCIES.md](DEPENDENCIES.md)

## 任务自动执行流程

`/continue` 根据 `task-list.json` 自动执行对应阶段：

| 阶段 | 任务 ID | 自动调用的技能 |
|------|---------|---------------|
| 1. 需求收集 | req-001~004 | software-requirements-analysis |
| 2. 技术规格 | spec-001~004 | spec-kit |
| 3. UI/UX 设计 | ui-001~002 | ui-prompt-generator |
| 4. 架构规划 | arch-001~004 | spec-kit, superpowers:brainstorming |
| 5. 前端开发 | fe-001+ | ui-ux-pro, superpowers:tdd |
| 6. 后端开发 | be-001+ | superpowers:tdd |
| 7. 测试验证 | test-001+ | superpowers:verification |
| 8. 代码审查 | review-001+ | superpowers:code-review |
| 9. 部署交付 | deploy-001~002 | superpowers |

## 项目结构

```
Long-running_Product_Agent/
├── CLAUDE.md                    # 项目级上下文（AI 自动加载）
├── agents/
│   └── product_manager.md       # Agent 执行逻辑
├── prompts/                     # 会话提示词
│   ├── initializer-prompt.md    # 首次会话
│   └── coding-agent-prompt.md   # 后续会话
├── commands/                    # 7 个用户命令
├── skills/                      # 技能定义
├── templates/                   # 任务列表 & 进度模板
├── demo/
│   └── WORKFLOW_DEMO.md         # 完整工作流演示
└── DEPENDENCIES.md              # 依赖说明
```

## 核心原则

1. **task-list.json 是真相** - 任务列表是唯一真实来源
2. **每会话一个任务** - 专注完美完成一个任务
3. **永不修改任务** - 只标记 `passes: false` → `passes: true`
4. **干净状态交接** - 每个会话以可提交、可工作的代码结束
5. **记录一切** - `agent-progress.md` 是会话间的记忆

## 文档导航

| 文档 | 内容 |
|------|------|
| [CLAUDE.md](CLAUDE.md) | 项目级上下文、快速参考 |
| [agents/product_manager.md](agents/product_manager.md) | 详细执行逻辑、会话协议 |
| [demo/WORKFLOW_DEMO.md](demo/WORKFLOW_DEMO.md) | 完整工作流演示 |
| [DEPENDENCIES.md](DEPENDENCIES.md) | 依赖安装说明 |

## 参考资料

- [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Claude Quickstarts: Autonomous Coding](https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding)
- [superpowers](https://github.com/obra/superpowers) - 开发工作流技能
- [ui-ux-pro](https://github.com/nickg/ui-ux-pro) - UI/UX 设计技能

## License

MIT
