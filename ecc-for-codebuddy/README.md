# ECC for CodeBuddy

本目录包含从 Everything Claude Code (ECC) 转换而来的 CodeBuddy 适配版本。

## 目录结构

```
ecc-for-codebuddy/
├── README.md                    # 本文件
├── system-prompts/             # 系统提示词配置
│   ├── base.md                 # 基础编码准则
│   ├── tdd-workflow.md         # TDD 工作流
│   ├── security-rules.md        # 安全规则
│   └── code-review.md          # 代码审查规则
├── agents/                     # 专家代理配置
│   ├── planner.md              # 规划专家
│   ├── architect.md            # 架构专家
│   ├── tdd-guide.md            # TDD 指导
│   ├── code-reviewer.md        # 代码审查
│   ├── security-reviewer.md    # 安全审查
│   ├── build-resolver.md        # 构建修复
│   ├── database-reviewer.md    # 数据库审查
│   ├── python-reviewer.md      # Python 专家
│   └── go-reviewer.md          # Go 专家
├── skills/                     # 技能配置
│   ├── tdd-scaffold.md         # TDD 脚手架
│   ├── security-scan.md        # 安全扫描
│   ├── refactor-clean.md       # 重构清理
│   └── doc-updater.md          # 文档更新
└── quick-start.md              # 快速开始指南
```

## 快速开始

### 方法 1: 直接使用系统提示词

```bash
codebuddy --system-prompt "$(cat system-prompts/base.md)"
```

### 方法 2: 使用文件配置

```bash
codebuddy --system-prompt-file system-prompts/base.md
```

### 方法 3: 追加到现有配置

```bash
codebuddy --append-system-prompt "$(cat agents/planner.md)"
```

## 核心组件

### Agents (专家代理)

| 代理 | 用途 | 使用场景 |
|------|------|----------|
| planner | 实现规划 | 复杂功能、重构 |
| architect | 系统设计 | 架构决策 |
| tdd-guide | 测试驱动开发 | 新功能、Bug 修复 |
| code-reviewer | 代码审查 | 代码质量保证 |
| security-reviewer | 安全审查 | 敏感代码、提交前 |
| build-resolver | 构建修复 | 构建失败时 |
| database-reviewer | 数据库审查 | 架构设计、查询优化 |

### Skills (技能)

| 技能 | 用途 |
|------|------|
| tdd-scaffold | 生成测试脚手架 |
| security-scan | 安全漏洞扫描 |
| refactor-clean | 死代码清理 |
| doc-updater | 文档和代码映射更新 |

## 适用场景

1. **已有项目** - 需要规范化开发流程
2. **团队协作** - 统一编码标准和流程
3. **质量优先** - 需要高测试覆盖率和安全审查
4. **多语言项目** - Python、Go、TypeScript 等

## 与原版 ECC 的区别

| 特性 | 原版 ECC | CodeBuddy 适配版 |
|------|----------|------------------|
| 平台 | Claude Code 插件 | CodeBuddy 系统提示词 |
| Agents | 30+ 专业代理 | 通过提示词模拟 |
| Skills | 182+ 技能 | 核心技能转换 |
| Hooks | 自动钩子 | 需手动触发 |
| 安装 | 插件市场 | 复制配置目录 |
