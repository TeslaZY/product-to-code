# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Project Overview

**Long-Running Product Fullstack Agent** - 基于 [Anthropic Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) 方法论的全栈开发插件。

**核心理念：** 用户只需说出产品想法，Agent 自动完成需求追问、文档生成、原型设计、代码开发。

**Long-Running 模式：** 通过 `task-list.json` 和 `agent-progress.md` 跨多个上下文窗口保持连续性。

## Quick Reference

### 7 Commands

| Command | Purpose |
|---------|---------|
| `/init` | Initialize new project |
| `/continue` | **Core** - Resume work on next task |
| `/progress` | View current progress |
| `/tasks` | List all tasks |
| `/feature <desc>` | Add new feature |
| `/update <desc>` | Modify existing feature |
| `/audit` | Verify completeness before deploy |

### Workflow

```
/init → /continue → /continue → ... → /audit → deploy
```

### Mode Detection

| Condition | Mode |
|-----------|------|
| No `task-list.json` | 0-1 Mode (new project) |
| Tasks pending | Continue Mode |
| `Product-Spec.md` exists + new request | Iteration Mode |
| All tasks passing | Complete Mode |

## Plugin Architecture

```
Long-running_Product_Agent/
├── CLAUDE.md                  # This file (project context)
├── agents/product_manager.md  # Agent execution logic
├── prompts/                   # Session prompts
│   ├── initializer-prompt.md
│   └── coding-agent-prompt.md
├── commands/                  # 7 user commands
├── skills/                    # Skill definitions
├── templates/                 # Task list & progress templates
└── demo/WORKFLOW_DEMO.md      # Complete workflow demo
```

## Key Principles

1. **task-list.json is truth** - Single source of truth for all tasks
2. **One task per session** - Focus on completing one task perfectly
3. **Never modify tasks** - Only mark `passes: false` → `passes: true`
4. **Clean state handoff** - Each session ends with committed, working code
5. **Document everything** - `agent-progress.md` is the memory between sessions

## References

- [Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Claude Quickstarts: Autonomous Coding](https://github.com/anthropics/claude-quickstarts/tree/main/autonomous-coding)
- [demo/WORKFLOW_DEMO.md](demo/WORKFLOW_DEMO.md) - Complete workflow example
- [agents/product_manager.md](agents/product_manager.md) - Detailed execution logic
