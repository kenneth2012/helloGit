# Claude How-To 学习笔记

## 项目基本信息

- **仓库地址**: https://github.com/luongnv89/claude-howto
- **作者**: Luong Nguyen (@luongnv89)
- **Star 数**: 30,100+ ⭐
- **版本**: v2.3.0
- **开源协议**: MIT License
- **核心定位**: 保姆级 Claude Code 学习指南

## 项目简介

Claude How-To 是目前最全面的 Claude Code 开源学习指南，通过 10 个渐进式模块、可视化图表和可复制粘贴的模板，帮助开发者从入门到精通掌握 Claude Code 的全部功能。

**核心理念**: 替代零散的官方文档和碎片化教程，提供一站式、渐进式、实战化的 Claude Code 学习方案。

## 项目特色

### 10 大功能模块

| 模块 | 名称 | 复杂度 | 时长 |
|------|------|--------|------|
| 01 | Slash Commands | ⭐ 入门 | 30 分钟 |
| 02 | Memory | ⭐ 入门 | 30 分钟 |
| 03 | Skills | ⭐⭐ 中级 | 45 分钟 |
| 04 | Subagents | ⭐⭐ 中级 | 1 小时 |
| 05 | MCP | ⭐⭐ 中级 | 1 小时 |
| 06 | Hooks | ⭐⭐ 中级 | 1 小时 |
| 07 | Plugins | ⭐⭐⭐ 高级 | 1.5 小时 |
| 08 | Checkpoints | ⭐ 入门 | 30 分钟 |
| 09 | Advanced Features | ⭐⭐⭐ 高级 | 2 小时 |
| 10 | CLI | ⭐⭐ 入门 | 45 分钟 |

**总学习时长**: 11-13 小时

## 功能覆盖

| 功能 | 内置数量 | 示例 | 总计 | 参考 |
|------|----------|------|------|------|
| **Slash Commands** | 55+ | 8 | 63+ | 01-slash-commands/ |
| **Subagents** | 6 | 11 | 17 | 04-subagents/ |
| **Skills** | 5 | 4 | 9 | 03-skills/ |
| **Plugins** | - | 3 | 3 | 07-plugins/ |
| **MCP Servers** | 1 | 8 | 9 | 05-mcp/ |
| **Hooks** | 25 events | 8 | 8 | 06-hooks/ |
| **Memory** | 7 types | 3 | 3 | 02-memory/ |
| **总计** | **99** | **45** | **119** | |

## 学习路径

```
🧭 自评测验
    ↓
┌─────────────────────────────────────────────┐
│  🟢 Level 1: Beginner — Getting Started    │
│  ├── 1A: Slash Commands + Memory           │
│  └── 1B: Checkpoints + CLI Basics           │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  🔵 Level 2: Intermediate — Building        │
│  ├── 2A: Skills + Hooks                     │
│  └── 2B: MCP + Subagents                   │
└─────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│  🔴 Level 3: Advanced — Power User          │
│  ├── 3A: Planning + Permissions            │
│  └── 3B: Plugins + CLI Mastery             │
└─────────────────────────────────────────────┘
```

## 适用场景

### 适用人群

1. **Claude Code 新手**
   - 刚安装 Claude Code，不知道如何高效使用
   - 想系统学习而非零散搜索

2. **开发者**
   - 想将 Claude Code 集成到项目中
   - 提升开发效率

3. **团队**
   - 需要标准化 Claude Code 配置
   - 共享最佳实践

4. **AI 爱好者**
   - 想深入理解 Claude Code 工作原理
   - 想掌握高级功能

### 不适用场景

- **已有经验的用户**: 如果已经熟悉 Claude Code 基础，这个指南可能过于基础
- **快速查阅**: 推荐直接查阅官方文档，这个项目是系统性学习用的

## 适配 Trae Solo

Claude How-To 主要面向 Claude Code，但其中的原则和概念可以迁移到 Trae Solo：

```markdown
# Claude How-To 理念适配 Trae Solo

## 核心概念迁移

### 1. 项目上下文 (CLAUDE.md)
- 在项目根目录创建 CLAUDE.md
- 定义项目特定的行为规范
- 设置编码标准和约定

### 2. 斜杠命令 (Slash Commands)
Trae Solo 使用自然语言，不需要斜杠命令
- 直接描述你的需求
- 使用清晰的任务描述

### 3. 记忆系统 (Memory)
- 利用项目 Rules 持久化项目知识
- 定期更新项目规范

### 4. 钩子 (Hooks)
Trae Solo 的规则系统可以模拟钩子行为
- 在 Rules 中定义前置检查
- 设置验证规则

### 5. 子代理 (Subagents)
Trae Solo 支持多 Agent 协作
- 使用不同的 Agent 模式
- 委派专业任务

## 学习路径适配

| Claude How-To | Trae Solo 等价 |
|--------------|----------------|
| Slash Commands | 自然语言指令 |
| CLAUDE.md | project_rules.md |
| Skills | Rules 配置 |
| Hooks | Rules 验证 |
| Subagents | 多 Agent 协作 |

## 使用建议

### 快速开始（15 分钟）

```bash
# 1. 克隆指南仓库
git clone https://github.com/luongnv89/claude-howto.git
cd claude-howto

# 2. 复制第一个斜杠命令到你的项目
mkdir -p /path/to/your-project/.claude/commands
cp 01-slash-commands/optimize.md /path/to/your-project/.claude/commands/

# 3. 在 Claude Code 中测试
# 启动 Claude Code 并输入：/optimize
```

### 学习顺序建议

1. **先学习基础** (1-2 小时)
   - Slash Commands
   - Memory
   - CLAUDE.md

2. **再学中级功能** (3-4 小时)
   - Skills
   - Hooks
   - MCP

3. **最后高级特性** (5-6 小时)
   - Subagents
   - Plugins
   - Advanced Features

## 核心资源

### CATALOG.md - 功能目录
完整的 Claude Code 功能参考手册

### LEARNING-ROADMAP.md - 学习路线图
交互式学习路径和自我评估

### 交互式技能

```bash
# 在 Claude Code 中运行
/self-assessment
```
交互式测验，评估你的熟练程度并生成个性化学习路径。

## 为什么选择 Claude How-To

1. **系统性学习**: 11-13 小时的完整学习路径
2. **可视化教学**: Mermaid 图表展示工作原理
3. **实战导向**: 可复制粘贴的模板
4. **持续更新**: 与 Claude Code 版本同步
5. **自我评估**: 内置测验系统

## 适配 CodeBuddy

Claude How-To 的核心概念可以迁移到 CodeBuddy：

```bash
# 方式一：追加学习指南核心理念
codebuddy --append-system-prompt "
请遵循以下 Claude How-To 开发理念：

## 项目上下文
- 在项目根目录创建 CLAUDE.md
- 定义项目特定的行为规范
- 设置编码标准和约定

## 开发原则
1. 理解需求后再编码
2. 使用测试驱动开发
3. 保持代码简洁
4. 遵循项目规范

## 验证检查
- 运行 lint 检查
- 执行单元测试
- 验证类型安全
- 检查安全漏洞

## 提交规范
- 提交前确保所有检查通过
- 使用语义化提交信息
- 关联相关 Issue
"

# 方式二：从文件加载
codebuddy --system-prompt-file claude-howto-codebuddy.txt
```

### 创建 Claude How-To 系统提示词文件

```bash
cat > claude-howto-codebuddy.txt << 'EOF'
你是一个遵循 Claude How-To 理念的 AI 编程助手。

## 核心概念

### 1. 项目上下文 (CLAUDE.md)
- 定义项目特定的行为规范
- 设置编码标准和约定
- 明确成功标准

### 2. 理解优先
- 在写任何代码前，先理解真正的需求
- 发现隐藏的约束和假设
- 明确成功标准

### 3. 测试驱动开发
- 先写会失败的测试
- 然后写最少的代码让测试通过
- 最后重构优化

### 4. 验证检查
- 运行 lint 检查
- 执行单元测试
- 验证类型安全
- 检查安全漏洞

## 开发工作流

### Level 1: 入门
- 使用自然语言清晰描述需求
- 创建项目上下文文件
- 使用基本开发流程

### Level 2: 中级
- 深入理解框架模式
- 使用 Hooks 进行自动化检查
- 使用 Subagents 进行复杂任务分解

### Level 3: 高级
- 创建自定义 Skills
- 构建自动化工作流
- 团队协作最佳实践

## 提交规范

- 提交前确保所有检查通过
- 使用语义化提交信息
- 关联相关 Issue
- 保持提交历史清晰

## 学习资源

Claude How-To 提供系统性学习路径：
- 10 个渐进式功能模块
- 11-13 小时完整学习时长
- 119 个实战示例
- 自我评估测验系统
EOF

codebuddy --system-prompt-file claude-howto-codebuddy.txt
```

## 与其他资源对比

| 特性 | Claude How-To | 官方文档 | 博客文章 |
|------|--------------|----------|----------|
| 覆盖范围 | 全面 | 全面 | 片面 |
| 学习曲线 | 渐进 | 陡峭 | 平缓 |
| 实用性 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ |
| 深度 | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐ |
| 趣味性 | ⭐⭐⭐⭐ | ⭐ | ⭐⭐⭐⭐ |
| CodeBuddy 支持 | ✅ | N/A | ❌ |

## 总结

**Claude How-To 不是技能库，而是学习指南！**

它教会你如何使用 Claude Code 的各种功能，而不是提供现成的技能包。学习完成后，你可以：
- 熟练使用所有 Claude Code 功能
- 理解不同功能的适用场景
- 创建自己的 Skills 和 Commands
- 构建适合项目的自动化工作流
