# gstack 学习笔记

## 项目基本信息

**作者**: Garry Tan (Y Combinator CEO)  
**仓库**: https://github.com/garrytan/gstack  
**Star 数**: 100,000+ ⭐  
**开源协议**: MIT License

## 项目简介

gstack 把 Claude Code 变成一支虚拟工程团队——CEO 重新思考产品、工程经理锁定架构、设计师捕捉 AI slop、评审员找生产 bug、QA 打开真实浏览器点击你的应用、发布工程师搞定 PR。15 个 specialists 和 6 个 power tools，全部都是 slash commands，全部都是 Markdown，全部免费！

**核心理念**: 不同的任务需要不同的认知模式。规划不是评审，评审不是发布。如果把这些混在一起，你得到的就是平庸的输出。

## 作者 Garry Tan 是谁

- Y Combinator 现任 CEO
- 曾与数千家创业公司合作，包括 Coinbase、Instacart、Rippling
- Palantir 的早期员工，设计了 Palantir 的 logo
- Posterous（一个博客平台）的联合创始人，后来卖给了 Twitter
- 2013 年在 YC 内部建立了 Bookface

## gstack 核心 Skill

| Skill | 角色 | 作用 |
|-------|------|------|
| `/office-hours` | YC 办公时间 | 6 个强制问题，在写代码前重新思考产品 |
| `/plan-ceo-review` | CEO/创始人 | 重新思考问题，找到请求背后的 10 星产品 |
| `/plan-eng-review` | 工程经理 | 锁定架构、数据流、边界情况、测试覆盖 |
| `/plan-design-review` | 资深设计师 | 交互式计划模式的设计评审，给每个维度评分 0-10 |
| `/design-consultation` | 设计合伙人 | 从零开始构建完整的设计系统 |
| `/review` | 资深工程师 | 找 CI 能过但生产会挂的 bug，自动修复明显的 |
| `/investigate` | 调试员 | 系统化的根因调试，铁律：没有调查就没有修复 |
| `/design-review` | 会写代码的设计师 | 线上视觉审计 + 修复循环，80 项审计清单 |
| `/qa` | QA 主管 | 用真实浏览器测试应用，找 bug 并原子提交修复，为每个修复自动生成回归测试 |
| `/qa-only` | QA 报告员 | 和 `/qa` 一样的方法论，但只报告不修复 |
| `/ship` | 发布工程师 | 同步 main、跑测试、审计覆盖率、推送到远程、开 PR |
| `/document-release` | 技术写作 | 更新所有项目文档以匹配刚刚发布的内容 |
| `/retro` | 工程经理 | 团队感知的每周回顾，个人分解、发布连续、测试健康趋势、成长机会 |
| `/browse` | QA 工程师 | 给 Agent 真实的眼睛，真实的 Chromium 浏览器，真实的点击，真实的截图 |
| `/setup-browser-cookies` | 会话管理器 | 从你真实的浏览器导入 Cookie 到无头会话 |
| `/codex` | 第二意见 | 来自 OpenAI Codex CLI 的独立评审 |

## 四大产品规划模式（CEO 模式）

使用 `/plan-ceo-review` 时有四种模式：

1. **范围扩展（Scope Expansion）**：梦想更大，找到 10 星产品
2. **选择性扩展（Selective Expansion）**：保持当前范围 + 精选扩展
3. **保持范围（Hold Scope）**：在当前范围内最大化严谨性
4. **范围缩减（Scope Reduction）**：砍到本质，MVP 思维

## 核心架构创新

### 1. 持久化浏览器守护进程

gstack 的核心不是 Prompt，而是一个**持久化的无头浏览器守护进程**：

```
Claude Code CLI
  ↓ HTTP POST (Bearer Token 认证)
Bun.serve() 服务器（10 个路由）
  ↓ Playwright CDP 协议
Chromium 无头浏览器（持久标签页 / Cookie）
```

- **首次启动**：约 3 秒（冷启动浏览器）
- **后续每条命令**：约 100ms（HTTP POST + Playwright 动作）
- **30 分钟空闲自动关闭**，下次调用自动重启

### 2. 为什么选 Bun

不是为了追新，而是工程需要：

| 特性 | 解决的问题 |
|------|-----------|
| `bun build --compile` | 编译为 58MB 单文件可执行程序，用户不需要装 Node.js |
| 原生 SQLite | 直接读取浏览器加密 Cookie 数据库，无需 native addon |
| 原生 TypeScript | 开发时零构建步骤，源文件就是执行文件 |
| 内置 HTTP 服务器 | `Bun.serve()` 够用，不需要 Express |

### 3. 无障碍树 Ref 系统

这是 gstack 最优雅的设计之一：

**传统方案的问题**：CSS 选择器在 Shadow DOM、CSP 策略、框架水合时频繁失败。

**gstack 的方案**：用 Playwright 的 accessibility tree 生成引用。

```
# 获取页面快照，看到 @e1, @e2, @e3... 引用
$B snapshot -i

# 直接用引用操作元素
$B fill @e3 "user@example.com"
$B click @e5
```

背后原理：
1. 调用 `page.accessibility.snapshot()` 获取 ARIA 树
2. 遍历树，给每个元素分配顺序编号（@e1, @e2...）
3. 为每个元素构建 Locator：`getByRole(role, {name}).nth(index)`
4. 操作前用 `count()` 检测元素是否过期（约 5ms 开销）

这套方案零 DOM 注入、跨框架通用、对 SPA 友好。

## 如何使用

### 步骤 1：安装 gstack（30 秒）

在 Claude Code 中运行：

```
git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup
```

然后在 `CLAUDE.md` 中添加 gstack 配置。

### 步骤 2：添加到你的项目（可选）

```
cp -Rf ~/.claude/skills/gstack .claude/skills/gstack && rm -rf .claude/skills/gstack/.git && cd .claude/skills/gstack && ./setup
```

### 快速开始

1. 运行 `/office-hours` — 描述你正在构建什么
2. 对任何功能想法运行 `/plan-ceo-review`
3. 对任何有变更的分支运行 `/review`
4. 对你的 staging URL 运行 `/qa`

## 适配 Trae Solo

虽然 gstack 主要是为 Claude Code 设计的，但我们可以在 Trae Solo 中通过规则模拟其核心思想：

```markdown
# gstack 风格工作流

## 认知模式切换

根据任务类型切换思考模式：

### CEO 模式（产品规划）
- 不要字面理解需求，重新思考问题本身
- 问：用户真正需要什么？10 星产品是什么样？
- 考虑范围扩展、选择性扩展、保持范围、范围缩减四种模式
- 挑战假设，找出隐藏的真实需求

### 工程经理模式（技术规划）
- 画架构图、数据流图
- 明确边界情况、失败模式
- 制定测试策略
- 把隐性假设暴露出来

### 资深工程师模式（代码评审）
- 像被生产事故烧过一样思考
- 找 N+1 查询、竞态条件、数据一致性问题
- 检查错误处理是否完整
- 不要只看代码风格，要看生产级健壮性

### QA 模式（测试）
- 像真实用户一样点击
- 测试边界情况
- 验证端到端流程
- 每修复一个 bug 就加回归测试

## 工作流建议

1. 先在 CEO 模式下想清楚产品
2. 再在工程经理模式下锁死架构
3. 然后写代码
4. 用资深工程师模式评审
5. 用 QA 模式测试
6. 最后发布
```

## 适配 CodeBuddy

CodeBuddy 支持通过系统提示词来自定义 AI 行为，可以将 gstack 的角色化思维融入其中：

```bash
codebuddy --append-system-prompt "
你是一个遵循 gstack 风格工作的 AI 编程助手。

核心原则：
1. 认知模式切换 - 根据任务类型切换思考模式
   - 产品规划时：像 CEO 一样重新思考问题，找到真正的需求
   - 技术规划时：像工程经理一样锁定架构和数据流
   - 代码评审时：像资深工程师一样找生产级 bug
   - 测试时：像 QA 一样真实点击验证

2. CEO 模式问题（在实现前必须回答）
   - 用户真正需要什么？
   - 什么是 10 星产品？
   - 考虑范围：扩展、选择性扩展、保持或缩减？

3. 评审铁律
   - 找 N+1 查询、竞态条件、数据一致性
   - 检查错误处理完整性
   - 不要只看代码风格，要看生产级健壮性
"

# 方式二：从文件加载系统提示词（推荐用于版本控制）
codebuddy --system-prompt-file gstack-codebuddy.txt
```

### 创建 gstack 系统提示词文件

```bash
cat > gstack-codebuddy.txt << 'EOF'
你是一个遵循 gstack 风格工作的 AI 编程助手。

## 认知模式切换

根据任务类型，在回复前先切换到合适的认知模式：

### CEO 模式（产品规划）
- 不要字面理解需求，重新思考问题本身
- 问：用户真正需要什么？10 星产品是什么样？
- 挑战假设，找出隐藏的真实需求

### 工程经理模式（技术规划）
- 画架构图、数据流图
- 明确边界情况、失败模式
- 制定测试策略
- 把隐性假设暴露出来

### 资深工程师模式（代码评审）
- 像被生产事故烧过一样思考
- 找 N+1 查询、竞态条件、数据一致性问题
- 检查错误处理是否完整

### QA 模式（测试）
- 像真实用户一样点击
- 测试边界情况
- 验证端到端流程

## 工作流建议

1. 先在 CEO 模式下想清楚产品
2. 再在工程经理模式下锁死架构
3. 然后写代码
4. 用资深工程师模式评审
5. 用 QA 模式测试
6. 最后发布
EOF

codebuddy --system-prompt-file gstack-codebuddy.txt
```

## 为什么这么火

1. **YC CEO 背书**：Garry Tan 本身就是创业和产品领域的权威
2. **解决真实痛点**：AI 经常用错误的认知模式处理任务
3. **角色化设计**：15+ 个 specialist，覆盖完整产品周期
4. **工程上的创新**：持久化浏览器、无障碍树 Ref 系统
5. **即用即走**：全部是 slash commands，不用复杂配置

## Garry Tan 的成就

- **60 天写了 60 万行生产代码**，其中 35% 是测试
- **每天 1-2 万行可用代码**，同时兼顾 YC CEO 的全部职责
- **过去 7 天的 `/retro`**：140,751 行新增，362 次提交，约 115K 净增长
