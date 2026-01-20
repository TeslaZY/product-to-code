---
name: superpowers
description: Complete software development workflow for coding agents with composable skills ensuring systematic test-driven development. Supports brainstorm, write-plan, and execute-plan commands
---

# Superpowers

Superpowers 是为编码代理设计的完整软件开发工作流，基于一组可组合的"技能"和确保代理使用它们的初始指令构建而成。

## 核心理念

Superpowers 将开发过程转变为结构化的工作流：当发现你在构建某些东西时，它不会立即跳到编写代码，而是退一步询问你真正想要做什么。一旦从对话中提取出规范，它会以足够短、易于阅读和理解的块向你展示。在你批准设计后，代理会制定一个清晰的实施计划。

**遵循原则：**
- **测试驱动开发** - 始终先编写测试
- **系统化而非临时** - 流程优于猜测
- **降低复杂性** - 简洁作为主要目标
- **证据优于声明** - 在宣称成功之前进行验证

## 安装

### Claude Code（通过插件市场）

```bash
# 注册市场
/plugin marketplace add obra/superpowers-marketplace

# 安装插件
/plugin install superpowers@superpowers-marketplace

# 验证安装
/help
```

### 更新

```bash
/plugin update superpowers
```

## 核心工作流

Superpowers 由多个自动触发的技能组成工作流：

### 1. brainstorming（头脑风暴）

**触发时机：** 在编写代码之前激活

**功能：**
- 通过问题细化粗略的想法
- 探索替代方案
- 以分段方式呈现设计以供验证
- 保存设计文档

**命令：** `/superpowers:brainstorm`

### 2. writing-plans（编写计划）

**触发时机：** 拥有批准的设计后激活

**功能：**
- 将工作分解为小任务（每个 2-5 分钟）
- 每个任务都有确切的文件路径、完整的代码、验证步骤

**命令：** `/superpowers:write-plan`

### 3. test-driven-development（测试驱动开发）

**触发时机：** 实施期间激活

**功能：**
- 强制执行 RED-GREEN-REFACTOR 周期
- 编写失败的测试，观察它失败
- 编写最少的代码，观察它通过
- 提交
- 删除在测试之前编写的代码

### 4. systematic-debugging（系统化调试）

**触发时机：** 遇到 bug 或错误时激活

**功能：**
- 4 阶段根本原因过程
- 根本原因追踪
- 纵深防御
- 基于条件的等待技术

### 5. requesting-code-review（请求代码审查）

**触发时机：** 任务之间激活

**功能：**
- 根据计划进行审查
- 按严重程度报告问题
- 关键问题会阻止进度

### 6. verification-before-completion（完成前验证）

**触发时机：** 声称修复完成时激活

**功能：**
- 运行验证命令
- 确认问题真正被修复
- 确保输出与预期匹配

## 可用的斜杠命令

| 命令 | 描述 |
|------|------|
| `/superpowers:brainstorm` | 交互式设计细化 |
| `/superpowers:write-plan` | 创建实施计划 |
| `/superpowers:execute-plan` | 批量执行计划 |

## 技能库

### 测试
- **test-driven-development** - RED-GREEN-REFACTOR 周期

### 调试
- **systematic-debugging** - 4 阶段根本原因过程
- **verification-before-completion** - 确保它真正被修复

### 协作
- **brainstorming** - 苏格拉底式设计细化
- **writing-plans** - 详细的实施计划
- **executing-plans** - 带检查点的批量执行
- **requesting-code-review** - 预审查检查清单
- **receiving-code-review** - 响应反馈
- **using-git-worktrees** - 并行开发分支
- **finishing-a-development-branch** - 合并/PR 决策工作流

### 元
- **writing-skills** - 遵循最佳实践创建新技能
- **using-superpowers** - 技能系统介绍

## 工作流程示例

### 完整开发周期

1. **启动头脑风暴** - 使用 `/superpowers:brainstorm` 定义你想要构建的内容
2. **批准设计** - 审查并批准代理呈现的设计方案
3. **编写实施计划** - 使用 `/superpowers:write-plan` 创建详细的任务分解
4. **执行计划** - 使用 `/superpowers:execute-plan` 开始自动化实施

## TDD 红绿周期

```
RED → 编写失败的测试
 GREEN → 编写最少的代码使其通过
 REFACTOR → 重构，保持测试通过
```

## 调试 4 阶段过程

1. **观察** - 记录错误和症状
2. **假设** - 生成可能的原因
3. **验证** - 测试每个假设
4. **修复** - 实施解决方案并验证
