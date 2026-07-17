# Superpowers 学习笔记

## 项目基本信息

**作者**: Jesse Vincent (@obra)  
**仓库**: https://github.com/obra/superpowers  
**Star 数**: 124,000+ ⭐  
**开源协议**: MIT License  
**核心理念**: Process over Prompt（流程大于提示词）

## 项目简介

Superpowers 是一套完整的 AI 开发方法论 + 可组合技能库，给 AI 套上软件工程的"纪律与护栏"，让它像资深工程师一样**先思考、再规划、后编码、必验证**。

它不是代码生成工具，也不会让 AI 变得更聪明，而是把软件工程最佳实践（TDD、Code Review、Spec-Driven、Git Worktree、子 Agent 协作）全部封装成 AI 可自动执行的 Skills。

**一句话总结**：14 个 SKILL.md 文件 + 一个 session hook，告诉 Agent 在做任何事情之前先读这些。

## 作者 Jesse Vincent 是谁

- 长期开源维护者
- 知名的软件工程师和企业家
- 专注于开发者工具和 AI 辅助开发

## Superpowers 核心 Skill

| 类别 | Skill | 作用 |
|------|-------|------|
| **规划** | brainstorming | 苏格拉底式问答，在编码前理清需求 |
| **规划** | writing-plans | 生成详细的实现计划文档，每个任务 2-5 分钟 |
| **开发** | subagent-driven-development | 每个任务用新的子 Agent，带两阶段评审 |
| **开发** | executing-plans | 批量执行计划，带人工检查点 |
| **测试** | test-driven-development | 强制 RED-GREEN-REFACTOR 循环 |
| **质量** | requesting-code-review | 对照计划评审，关键问题阻塞进度 |
| **Git** | using-git-worktrees | 每个功能用隔离工作区 |
| **调试** | systematic-debugging | 4 阶段根因分析 |

## 完整工作流

一个典型的任务按以下流程进行，每个阶段有自己的 Skill，下一阶段不会开始直到上一阶段完成：

```
1. 头脑风暴（Brainstorming）
   ↓
2. Git Worktree（隔离工作区）
   ↓
3. 写计划（Writing Plans）
   ↓
4. 子 Agent 开发（Subagent Development）
   ↓
5. TDD（强制 RED-GREEN-REFACTOR）
   ↓
6. 代码审查（Code Review）
   ↓
7. 完成（Finishing）
```

## 六大核心原则

### 1. 头脑风暴（Brainstorming）

当你要求 Agent 构建什么时，Superpowers **阻止它立即写代码**，而是：

- 进行苏格拉底式问答，澄清你真正想要构建什么
- 探索你可能没有考虑过的替代方案
- 以可消化的方式呈现设计供你批准
- 在继续前保存设计文档

### 2. 写计划（Writing Plans）

Agent 创建一个详细的实现计划，拆分为小任务（每个 2-5 分钟），每个任务包括：

- 要创建/修改的确切文件路径
- 要写的完整代码
- 验证步骤以确认它工作

### 3. 子 Agent 驱动开发（Subagent-Driven Development）

这是最创新的部分：不是一个 Agent 做所有事情，而是：

- 一个 **协调 Agent** 管理计划
- 为每个任务生成 **新鲜的子 Agent**（干净的上下文，没有累积的困惑）
- 每个子 Agent 的工作获得 **两阶段评审**：规范合规性，然后代码质量
- 关键问题阻塞进度；小问题记录在案

### 4. 测试驱动开发（Test-Driven Development）

Superpowers 强制严格的 RED-GREEN-REFACTOR：

1. 先写一个会失败的测试（RED）
2. 然后写最少的代码让它通过（GREEN）
3. 最后重构（REFACTOR）
4. 提交

**铁律**：如果 Agent 在测试前写代码，Superpowers 会删除它。这是有意为之的意见化设计。

### 5. 代码审查（Code Review）

在任务之间，Agent 对照计划进行评审。当所有任务完成时，它：

- 验证所有测试通过
- 呈现选项：合并、创建 PR、保留分支或丢弃
- 清理 git worktree

### 6. 系统化调试（Systematic Debugging）

如果遇到 bug，按以下四个阶段进行：

1. **根因调查**（不得直接修复）
2. **模式分析**
3. **假设测试**
4. **实现修复**

- **铁律**：3 次失败修复后必须进行架构审查

## 如何使用

### Claude Code（官方插件市场）

```
/plugin install superpowers@claude-plugins-official
```

### Cursor

```
/add-plugin superpowers
```

### Codex

```
Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.codex/INSTALL.md
```

### Gemini CLI

```
gemini extensions install https://github.com/obra/superpowers
```

### OpenCode

```
Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.opencode/INSTALL.md
```

无需配置。Skills 会根据你正在做的事情自动触发。

## Superpowers 2.0 更新

2025 年 10 月发布的 Superpowers 2.0 有重大改进：

- Skills 移到独立的 git repo，便于分享和定制
- 与 Claude 新技能系统完全兼容
- 开发者体验更流畅

## 适配 Trae Solo

在 Trae Solo 中可以通过规则实现 Superpowers 的核心流程：

```markdown
# Superpowers 风格工作流

## 强制流程

任何开发任务必须按以下顺序执行，不得跳过：

### 1. 头脑风暴阶段（Brainstorming）
- 在写任何代码前，先进行苏格拉底式问答
- 问清需求背后的真实意图
- 探索替代方案
- 确认设计后再继续
- 保存设计文档

### 2. 计划阶段（Writing Plans）
- 将工作拆分为 2-5 分钟的小任务
- 每个任务包含：
  - 要创建/修改的文件路径
  - 要写的完整代码
  - 验证步骤
- 每个任务独立可验证

### 3. 执行阶段（TDD 强制）
- **必须先写会失败的测试（RED）**
- 然后写最少的代码让测试通过（GREEN）
- 最后重构（REFACTOR）
- 如果先写代码再写测试，撤销代码重写

### 4. 代码审查
- 对照计划检查实现
- 检查编码标准
- 检查架构原则
- 关键问题必须修复才能继续

### 5. 系统化调试
如果遇到 bug：
1. 根因调查（不得直接修复）
2. 模式分析
3. 假设测试
4. 实现修复
- 3 次失败修复后必须进行架构审查

### 6. 完成
- 验证所有测试通过
- 确认是否合并、创建 PR、保留分支或丢弃
- 清理 git worktree
```

## 快速开始模板

你可以在 Trae Solo 中创建一个简单的规则来强制执行基本流程：

```markdown
# Superpowers 轻量级规则

## 任何开发任务前

回答以下问题后再开始编码：
1. 我理解需求了吗？有什么不确定的？
2. 测试策略是什么？
3. 最小可行实现是什么？

## 编码时

- 先写测试，再写实现
- 每个提交都应该是可验证的小步骤
- 不要"顺便"修改无关代码

## 完成前

- 所有测试通过了吗？
- 我刚才做的改动和计划一致吗？
- 有什么我应该清理但没清理的？
```

## 适配 CodeBuddy

CodeBuddy 支持通过系统提示词来强制 Superpowers 的流程纪律：

```bash
# 方式一：直接追加流程准则
codebuddy --append-system-prompt "
请遵循以下 Superpowers 开发流程：

## 强制流程（不得跳过）

1. 头脑风暴阶段 - 在写任何代码前，先进行苏格拉底式问答
2. 计划阶段 - 将工作拆分为小任务，每个包含文件路径、代码、验证步骤
3. TDD 强制 - 必须先写会失败的测试，再写实现
4. 代码审查 - 对照计划检查实现，关键问题必须修复
5. 系统化调试 - 根因调查 > 模式分析 > 假设测试 > 实现修复

铁律：3 次失败修复后必须进行架构审查
"

# 方式二：从文件加载系统提示词
codebuddy --system-prompt-file superpowers-codebuddy.txt
```

### 创建 Superpowers 系统提示词文件

```bash
cat > superpowers-codebuddy.txt << 'EOF'
你是一个遵循 Superpowers 方法论的 AI 编程助手。

## 核心原则

Process over Prompt - 流程大于提示词纪律比聪明更重要。

## 强制开发流程

任何开发任务必须按以下顺序执行，不得跳过：

### 1. 头脑风暴阶段
- 在写任何代码前，先进行苏格拉底式问答
- 问清需求背后的真实意图
- 探索替代方案
- 确认设计后再继续
- 保存设计文档

### 2. 计划阶段
- 将工作拆分为 2-5 分钟的小任务
- 每个任务包含：
  - 要创建/修改的文件路径
  - 要写的完整代码
  - 验证步骤
- 每个任务独立可验证

### 3. TDD 强制阶段
- **必须先写会失败的测试（RED）**
- 然后写最少的代码让测试通过（GREEN）
- 最后重构（REFACTOR）
- 如果先写代码再写测试，撤销代码重写

### 4. 代码审查
- 对照计划检查实现
- 检查编码标准
- 检查架构原则
- 关键问题必须修复才能继续

### 5. 系统化调试
如果遇到 bug，按以下顺序：
1. 根因调查（不得直接修复）
2. 模式分析
3. 假设测试
4. 实现修复
- **铁律**：3 次失败修复后必须进行架构审查

### 6. 完成
- 验证所有测试通过
- 确认是否合并、创建 PR、保留分支或丢弃
EOF

codebuddy --system-prompt-file superpowers-codebuddy.txt
```

## 为什么这么火

1. **解决真实痛点**：原生 Claude Code 经常跳过关键环节，缺乏工程纪律
2. **核心理念有说服力**：Process over Prompt，纪律比聪明更重要
3. **跨平台支持**：Claude Code、Cursor、Codex、OpenCode、Gemini CLI 都支持
4. **极简实现**：只是 14 个 Markdown 文件 + session hook，没有复杂的 SDK
5. **社区验证**：124,000+ GitHub stars，Anthropic 官方插件市场收录

## 社区评价

- *"Laravel Boost 和 Claude with superpowers 正在为我生成一些非常可靠的代码"*
- *"取决于任务权重：原生/superpowers/GSD。总是让 Code Rabbit 评审，对于重要部分我用 Codex MCP 来回检查——纯粹的黄金"*

批评者认为它对某些任务来说过度工程化了，这确实是对的——这取决于你的项目！
