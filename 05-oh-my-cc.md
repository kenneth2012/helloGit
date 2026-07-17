# Oh My Claudecode (OMC) 学习笔记

## 项目基本信息

- **仓库地址**: https://github.com/Yeachan-Heo/oh-my-claudecode
- **作者**: Yeachan Heo (@Yeachan-Heo)
- **Star 数**: 8,900+ ⭐
- **版本**: v4.12.1
- **开源协议**: MIT License
- **核心理念**: Multi-agent orchestration（多代理编排），零学习曲线

**标语**: "Don't learn Claude Code. Just use OMC."

## 项目简介

Oh My Claudecode (OMC) 是一个 Claude Code 的多代理编排层，通过技能路由系统让 Claude Code 能够协调专业化的 agents。它让用户无需学习复杂的 Claude Code 命令，只需要用自然语言描述需求，系统会自动选择合适的 agents 来完成工作。

**核心理念**: 不同的任务交给不同的专业 agent，用户只需要说"做什么"，而不需要知道"怎么做"。

## 四大核心系统

```
用户输入 → Hooks（事件检测）→ Skills（行为注入）→ Agents（任务执行）→ State（进度追踪）
```

### 1. Hooks（钩子系统）

检测生命周期事件，触发自动化流程。

### 2. Skills（技能系统）

注入特定行为模式，实现工作流自动化。

### 3. Agents（代理系统）

执行专业化的任务工作。

### 4. State（状态系统）

追踪进度，跨上下文重置保持连续性。

## 19 个专业 Agents

### Build/Analysis Lane（构建/分析线）

覆盖从探索到验证的完整开发生命周期。

| Agent | 默认模型 | 角色 |
|-------|----------|------|
| `explore` | haiku | 代码库发现，文件/符号映射 |
| `analyst` | opus | 需求分析，发现隐藏约束 |
| `planner` | opus | 任务排序，执行计划创建 |
| `architect` | opus | 系统设计，接口定义，权衡分析 |
| `debugger` | sonnet | 根因分析，构建错误解决 |
| `executor` | sonnet | 代码实现，重构 |
| `verifier` | sonnet | 完成验证，测试充分性确认 |
| `tracer` | sonnet | 证据驱动的因果追踪 |

### Review Lane（评审线）

交付前的质量门控。

| Agent | 默认模型 | 角色 |
|-------|----------|------|
| `security-reviewer` | sonnet | 安全漏洞，信任边界，认证/授权审查 |
| `code-reviewer` | opus | 综合代码审查，API 契约，向后兼容性 |

### Domain Lane（领域线）

按需调用的领域专家。

| Agent | 默认模型 | 角色 |
|-------|----------|------|
| `test-engineer` | sonnet | 测试策略，覆盖率，防抖测试加固 |
| `designer` | sonnet | UI/UX 架构，交互设计 |
| `writer` | haiku | 文档，迁移说明 |
| `qa-tester` | sonnet | 交互式 CLI/服务运行时验证 |
| `scientist` | sonnet | 数据分析，统计研究 |
| `git-master` | sonnet | Git 操作，提交，变基，历史管理 |
| `document-specialist` | sonnet | 外部文档，API/SDK 参考查找 |
| `code-simplifier` | opus | 代码清晰化，简化，可维护性改进 |

### Coordination Lane（协调线）

挑战计划，团队协调。

## 核心命令

### 终端 CLI 命令 vs 会话内 Skills

OMC 提供两种不同的界面：

| 功能 | 终端 CLI | 会话内 Skill | 说明 |
|------|----------|--------------|------|
| Setup | `omc setup` | `/setup` 或 `/omc-setup` | 都是真正的入口 |
| Ask providers | `omc ask codex` | `/ask codex` | 都通过相同的 advisor 流程 |
| Team orchestration | `omc team` | `/team` | 不同运行时 |

### 核心命令列表

```bash
# 设置
/setup
/omc-setup
omc setup

# 团队模式
/team 3:executor "修复所有 TypeScript 错误"

/# 自动驾驶
/autopilot "构建一个任务管理的 REST API"

/# 深度访谈
/deep-interview "我想构建一个任务管理应用"

/# 提问
/ask codex "审查这个补丁"

/# 阿尔弗雷德
/alfred "优化数据库查询"
```

## Team Mode（团队模式）

**v4.1.7+ 推荐**

Team 是 OMC 的规范编排界面。允许多个专业 agents 并行工作，协调完成复杂任务。

### 使用示例

```bash
# 启动团队
/team 3:executor "实现用户认证模块"

/# 团队组成
/team 2:analyst + 1:planner "分析支付系统需求"
```

### 团队协作流程

```
1. 定义团队组成（agents 数量和类型）
2. 分配任务
3. 并行执行
4. 汇总结果
5. 验证完成
```

## 适配 Trae Solo

虽然 OMC 主要为 Claude Code 设计，但可以在 Trae Solo 中通过规则模拟其核心概念：

```markdown
# OMC 风格工作流

## 多代理协调

根据任务类型委派给合适的"专家"：

### 分析师模式
- 理解需求的真正意图
- 发现隐藏的约束和假设
- 明确成功标准

### 规划师模式
- 创建执行计划
- 分解任务步骤
- 确定依赖关系

### 执行者模式
- 实现代码
- 遵循规范
- 保持简洁

### 评审者模式
- 代码审查
- 安全检查
- 性能审查

### 测试工程师模式
- 编写测试
- 确保覆盖率
- 验证功能

## 工作流

1. 分析师理解需求
2. 规划师制定计划
3. 执行者实现代码
4. 评审者审查
5. 测试工程师验证
6. 汇总报告
```

## 适配场景

### 适用场景

1. **复杂项目**
   - 需要多个专业领域的协作
   - 从 0 到 1 的新项目
   - 大型重构任务

2. **质量要求高**
   - 需要专业代码审查
   - 安全敏感的应用
   - 需要全面测试的项目

3. **团队协作**
   - 模拟团队工作流程
   - 多人项目的代码整合
   - 跨职能协作

### 不适用场景

1. **简单任务**
   - 单个文件修改
   - 拼写错误修正
   - 简单脚本编写

2. **资源受限**
   - API 调用成本考虑
   - 需要快速迭代

## 适配 CodeBuddy

OMC 的多代理协调概念可以通过 CodeBuddy 的系统提示词来实现：

```bash
# 方式一：追加 OMC 核心概念
codebuddy --append-system-prompt "
请遵循以下 Oh My Claudecode 多代理协调原则：

## 多代理协调

根据任务类型委派给合适的专家模式：

### 分析师模式
- 理解需求的真正意图
- 发现隐藏的约束和假设
- 明确成功标准

### 规划师模式
- 创建执行计划
- 分解任务步骤
- 确定依赖关系

### 执行者模式
- 实现代码
- 遵循规范
- 保持简洁

### 评审者模式
- 代码审查
- 安全检查
- 性能审查

### 测试工程师模式
- 编写测试
- 确保覆盖率
- 验证功能

## 工作流

1. 分析师理解需求
2. 规划师制定计划
3. 执行者实现代码
4. 评审者审查
5. 测试工程师验证
6. 汇总报告
"

# 方式二：从文件加载
codebuddy --system-prompt-file omc-codebuddy.txt
```

### 创建 OMC 系统提示词文件

```bash
cat > omc-codebuddy.txt << 'EOF'
你是一个遵循 Oh My Claudecode 多代理编排原则的 AI 编程助手。

## 核心理念

不同的任务交给不同的认知模式，用户只需要说"做什么"，而不需要知道"怎么做"。

## 多代理协调

### 分析师模式
- 理解需求的真正意图
- 发现隐藏的约束和假设
- 明确成功标准

### 规划师模式
- 创建执行计划
- 分解任务步骤
- 确定依赖关系

### 执行者模式
- 实现代码
- 遵循规范
- 保持简洁

### 评审者模式
- 代码审查
- 安全检查
- 性能审查

### 测试工程师模式
- 编写测试
- 确保覆盖率
- 验证功能

### QA 模式
- 像真实用户一样点击
- 测试边界情况
- 验证端到端流程

### Git Master 模式
- Git 操作，提交，变基，历史管理
- 保持提交历史清晰

## 工作流建议

1. 分析师理解需求
2. 规划师制定计划
3. 执行者实现代码
4. 评审者审查
5. 测试工程师验证
6. QA 模式最终测试
7. Git Master 整理提交
8. 汇总报告

## 零学习曲线

只需要用自然语言描述你的需求，我会自动选择合适的处理模式。
EOF

codebuddy --system-prompt-file omc-codebuddy.txt
```

## 与其他工具对比

| 特性 | OMC | ECC | Karpathy Skills | gstack | Superpowers |
|------|-----|-----|----------------|--------|-------------|
| Agents 数量 | 19 | 48 | 0 | 15 | 0 |
| 多代理编排 | ✅ | ❌ | ❌ | ❌ | ❌ |
| 团队模式 | ✅ | ❌ | ❌ | ❌ | ❌ |
| CodeBuddy 支持 | ✅ | ✅ | ✅ | ✅ | ✅ |
| 学习曲线 | 低 | 高 | 低 | 中 | 中 |
| 适用项目 | 复杂 | 大型 | 小型 | 中型 | 中型 |

## 快速开始

### 安装

```bash
# Claude Code 内
/plugin marketplace add https://github.com/Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode

# NPM 路径
npm i -g oh-my-claude-sisyphus@latest
```

### 设置

```bash
# Claude Code 会话内
/setup
/omc-setup

# 终端
omc setup
```

### 使用

```bash
# 自然语言自动驾驶
/autopilot "构建一个 REST API 来管理任务"

# 深度访谈理解需求
/deep-interview "我想构建一个任务管理应用"

# 团队协作
/team 2:executor "修复所有 TypeScript 错误"
```

## 核心理念

1. **零学习曲线**: 不需要学习复杂的 Claude Code 命令
2. **专业分工**: 不同任务交给不同的专业 agent
3. **自动编排**: 系统自动选择最合适的 agents
4. **团队协作**: 模拟真实团队的工作方式

## 为什么选择 OMC

1. **简化使用**: 只需要说"做什么"，不需要知道"怎么做"
2. **专业能力**: 19 个专业 agents 覆盖各个领域
3. **团队协作**: 模拟真实团队的工作流程
4. **持续迭代**: v4.12.1，121+ PRs 持续更新
5. **跨平台**: 支持 Claude Code、Codex 等多种工具
