# 快速开始指南

ECC for CodeBuddy 快速配置指南。

## 方法 1: 完整配置（推荐）

复制整个目录到你的项目中：

```bash
git clone https://github.com/kenneth2012/helloGit.git
cp -r helloGit/ecc-for-codebuddy /path/to/your-project/
```

使用完整配置：

```bash
codebuddy --system-prompt-file /path/to/your-project/ecc-for-codebuddy/system-prompts/base.md
```

## 方法 2: 按需使用

### 基础编码准则
```bash
codebuddy --system-prompt "$(cat ecc-for-codebuddy/system-prompts/base.md)"
```

### TDD 工作流
```bash
codebuddy --append-system-prompt "$(cat ecc-for-codebuddy/system-prompts/tdd-workflow.md)"
```

### 安全规则
```bash
codebuddy --append-system-prompt "$(cat ecc-for-codebuddy/system-prompts/security-rules.md)"
```

### 代码审查
```bash
codebuddy --append-system-prompt "$(cat ecc-for-codebuddy/system-prompts/code-review.md)"
```

## 方法 3: 专家模式

### 规划专家
```bash
codebuddy --system-prompt "$(cat ecc-for-codebuddy/agents/planner.md)"
```

### TDD 指导
```bash
codebuddy --system-prompt "$(cat ecc-for-codebuddy/agents/tdd-guide.md)"
```

### 安全审查
```bash
codebuddy --system-prompt "$(cat ecc-for-codebuddy/agents/security-reviewer.md)"
```

## 组合使用

### 开发模式（TDD + 安全）
```bash
codebuddy --system-prompt "$(cat ecc-for-codebuddy/system-prompts/base.md)" \
         --append-system-prompt "$(cat ecc-for-codebuddy/system-prompts/tdd-workflow.md)" \
         --append-system-prompt "$(cat ecc-for-codebuddy/system-prompts/security-rules.md)"
```

### 审查模式
```bash
codebuddy --system-prompt "$(cat ecc-for-codebuddy/system-prompts/code-review.md)" \
         --append-system-prompt "$(cat ecc-for-codebuddy/agents/code-reviewer.md)" \
         --append-system-prompt "$(cat ecc-for-codebuddy/agents/security-reviewer.md)"
```

## 快捷方式

创建别名方便使用：

```bash
# ~/.bashrc 或 ~/.zshrc

# 基础开发
alias cb='codebuddy --system-prompt "$(cat ~/ecc-for-codebuddy/system-prompts/base.md)"'

# TDD 开发
alias cb-tdd='codebuddy --system-prompt "$(cat ~/ecc-for-codebuddy/system-prompts/base.md)" --append-system-prompt "$(cat ~/ecc-for-codebuddy/system-prompts/tdd-workflow.md)"'

# 安全审查
alias cb-sec='codebuddy --system-prompt "$(cat ~/ecc-for-codebuddy/agents/security-reviewer.md)"'

# 代码审查
alias cb-review='codebuddy --system-prompt "$(cat ~/ecc-for-codebuddy/system-prompts/code-review.md)"'
```

## 验证配置

运行以下命令验证配置：

```bash
# 检查版本
codebuddy --version

# 测试基础配置
echo "测试 CodeBuddy 配置" | codebuddy --system-prompt "$(cat ecc-for-codebuddy/system-prompts/base.md)"
```

## 适用场景

| 场景 | 推荐配置 |
|------|----------|
| 日常开发 | base.md |
| 新功能开发 | base.md + tdd-workflow.md |
| 代码审查 | code-review.md + code-reviewer.md |
| 安全审查 | security-rules.md + security-reviewer.md |
| 重构 | base.md + refactor-cleaner.md |
| 数据库 | database-reviewer.md |
| Python 项目 | python-reviewer.md |
| Go 项目 | go-reviewer.md |
