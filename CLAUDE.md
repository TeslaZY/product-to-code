# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository. It serves as the main controller for Product Fullstack Agent plugin.

## Project Overview

Product Fullstack Agent 是一个全栈开发 Agent 插件，集成了产品经理、UI 设计、全栈开发三种角色对应的 skill，让 AI 按照专业标准执行从需求调研、PRD 文档、功能规范、UI/UX 设计、实现架构/方案设计、编码实现、测试、部署上线到迭代的软件开发全流程。

**核心理念：** 用户只需说出产品想法，剩下的需求追问、文档生成、原型设计、代码开发就自动完成。

## Plugin Architecture

```
product-manager-agent/
├── CLAUDE.md                          # 主控文件（本文件）
├── product_manager.md                    # 原始需求文档
├── software-requirements-analysis/         # 需求收集 skill
│   ├── SKILL.md
│   └── assets/
│       ├── changelog-template.md
│       └── software-requirements-template.md
├── ui-prompt-generator/                # UI 提示词生成 skill
│   ├── SKILL.md
│   └── assets/
│       └── ui-prompt-template.md
├── ui-ux-pro/                           # UI/UX 开发 skill
│   └── SKILL.md
├── spec-kit/                             # 规范驱动开发 skill
│   └── SKILL.md
├── superpowers/                          # 软件开发工作流 skill
│   └── SKILL.md
└── uv-skill/                              # Python 依赖管理 skill
    ├── SKILL.md
    └── references/
        └── REFERENCES.md
```

## 工作模式

系统启动时自动检测项目状态，进入对应模式：

| 状态 | 检测条件 | 行为 |
|------|----------|------|
| **0-1 模式** | `Product-Spec.md` 不存在 | 从头开始收集需求 |
| **迭代模式** | `Product-Spec.md` 存在 | 修改/新增功能 |

## 可用命令

用户可以通过以下命令控制开发流程：

| 命令 | 描述 | 触发阶段 |
|--------|------|----------|
| `/new` 或 `/start` | 开始新项目（0-1 模式） | 需求收集 |
| `/status` | 查看当前项目进度 | 任意 |
| `/ui` | 生成 UI 原型提示词 | UI 设计 |
| `/design` | 开始 UI/UX 设计开发 | 前端开发 |
| `/plan` | 创建技术实现方案 | 架构设计 |
| `/develop` | 开始代码开发实现 | 编码实现 |
| `/test` | 运行测试验证功能 | 测试 |
| `/feature <描述>` | 添加新功能（迭代模式） | 迭代开发 |
| `/update <描述>` | 修改现有功能（迭代模式） | 迭代开发 |
| `/review` | 对照产品文档检查功能完整性 | 验收 |

## 完整工作流程

### 0-1 模式（新建项目）

```
1. 用户: /new 或说出想法
   ↓
2. 调用software-requirements-analysis
   - 需求追问（毒舌产品经理）
   - 检测逻辑矛盾
   - AI 增强建议
   ↓
3. 生成 Product-Spec.md
   - 使用 software-requirements-analysis/assets/software-requirements-template.md 模板
   - 生成 Product-Spec-CHANGELOG.md
   ↓
4. 用户: /ui
   ↓
5. 调用 ui-prompt-generator
   - 读取 Product-Spec.md
   - 生成 UI-Prompts.md
   ↓
6. 用户确认原型图（外部工具生成）
   ↓
7. 用户: /plan
   ↓
8. 调用 spec-kit + superpowers:writing-plans
   - 分析技术栈
   - 创建架构设计文档
   ↓
9. 用户: /design
   ↓
10. 调用 ui-ux-pro
   - 根据原型图和功能文档构建前端
   - 如用 Python，使用 uv-skill 管理依赖
   ↓
11. 用户: /develop
   ↓
12. 调用 superpowers:test-driven-development
   - 后端实现
   - 使用 uv-skill 管理依赖
   ↓
13. 用户: /test
   ↓
14. 调用 superpowers:verification-before-completion
   - 运行测试
   - 功能验证
   ↓
15. 部署上线
```

### 迭代模式（修改现有项目）

```
1. 用户: /feature <描述> 或 /update <描述>
   ↓
2. 调用 software-requirements-analysis (迭代模式)
   - 读取现有 Product-Spec.md
   - 收集新需求/变更
   - 冲突检测
   - 更新产品文档
   - 更新 Product-Spec-CHANGELOG.md
   ↓
3. 调用 spec-kit (技术评估)
   - 评估变更的技术影响
   - 确定实现方案
   ↓
4. 用户: /develop
   ↓
5. 调用 superpowers:test-driven-development
   - 实现变更
   ↓
6. 用户: /test
   ↓
7. 调用 superpowers:verification-before-completion
   - 运行测试
   ↓
8. 用户: /review
   ↓
9. 对照产品文档检查功能完整性
```

## 子技能职责

### software-requirements-analysis
- **触发**: `/new`、`/feature`、`/update`
- **输出**: `Product-Spec.md`、`Product-Spec-CHANGELOG.md`
- **核心**: 毒舌追问、0-1/迭代模式切换、AI 增强建议

### ui-prompt-generator
- **触发**: `/ui`
- **输出**: `UI-Prompts.md`
- **核心**: 根据产品文档生成原型图提示词

### ui-ux-pro
- **触发**: `/design`
- **输出**: 前端代码项目
- **核心**: 根据原型图和功能文档构建前端界面

### spec-kit
- **触发**: `/plan`
- **输出**: 技术规范文档、架构设计
- **核心**: Spec-Driven Development、意图驱动开发

### superpowers
- **触发**: `/develop`、`/test`、`/review`
- **输出**: 开发计划、测试代码、实现代码
- **核心**: 测试驱动开发、系统化调试、代码审查

### uv-skill
- **使用**: 任何涉及 Python 的操作
- **输出**: `pyproject.toml`、`uv.lock`、`.venv/`
- **核心**: 强制使用 uv 进行依赖管理

## 关键特性

### 模式自动切换
- 检测 `Product-Spec.md` 是否存在
- 不存在 → 0-1 模式
- 存在 → 迭代模式

### 循环配合流程
- 每次修改先更新文档再写代码
- 文档和代码始终同步

### Human-in-Loop
- 不清楚的地方必须与用户确认
- 设计风格、技术栈选择需用户决策
- 冲突解决需用户选择方案

### AI 增强建议
产品经理主动建议用 AI 简化流程的场景：

| 场景 | AI 增强 |
|------|---------|
| 手动填写大量信息 | AI 智能填充 |
| 复杂判断 | AI 预判断，用户确认 |
| 重复性操作 | AI 批量处理 |
| 格式化内容 | AI 自动格式化 |
| 搜索/筛选 | AI 智能推荐 |
| 内容生成 | AI 生成初稿 |

### 冲突检测
迭代模式下自动检测：
- 新需求与现有功能的冲突
- 技术架构的兼容性
- 数据结构的变更影响

## 注意事项

1. **文档驱动优先**: 所有修改必须同步到文档
2. **质量优先**: 宁可多问一轮，也别留下模糊需求
3. **用户视角**: 每问一个问题，都从用户角度想一遍
4. **技术友好**: 描述功能时，用开发能理解的术语
5. **Human-in-Loop**: 不确定的地方一定要询问用户
6. **uv 管理**: Python 项目必须使用 uv，禁止使用 pip
7. **合理运用 spec-kit 和 superpowers**: 确保开发质量
