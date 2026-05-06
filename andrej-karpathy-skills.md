# andrej-karpathy-skills 项目学习笔记

## 项目基本信息

- **仓库地址**: https://github.com/forrestchang/andrej-karpathy-skills
- **作者**: Forrest Chang (@forrestchang)
- **Star 数**: 105,000+ ⭐
- **Fork 数**: 10,300+
- **开源协议**: MIT License
- **灵感来源**: Andrej Karpathy 对 LLM 编码缺陷的深刻洞察

## 项目简介

这不是一个代码库或框架，而是一套**基于 Andrej Karpathy 对 LLM（大语言模型）编程失败模式的深刻洞察**，所提炼出的**四大核心行为准则**。这些准则被封装成一个简单的 `CLAUDE.md` 文件，旨在引导像 Claude 这样的 AI 编程助手，以更专业、更可靠的方式工作。

你可以把它理解为给 AI 助手下的一道"紧箍咒"，或者一份"职场新人入职培训手册"。

## Andrej Karpathy 是谁

Andrej Karpathy 是 AI 领域的大神级人物：
- OpenAI 联合创始人
- 特斯拉前 AI 总监
- 斯坦福 CS 博士
- 百万粉丝的技术博主
- YouTube 上从零手搓 GPT 系列播放量过千万

## LLM 编码的三大通病

Karpathy 尖锐地指出当前大语言模型在编程任务中的三大问题：

1. **错误假设**
   - 模型在未经确认的情况下做出错误假设并一路执行
   - 不管理自身的困惑
   - 不寻求澄清
   - 不暴露不一致性
   - 不呈现权衡
   - 不在应该反驳时反驳

2. **过度复杂化**
   - 过度复杂化代码和 API
   - 堆一堆用不上的抽象
   - 不清理死代码
   - 明明 100 行能搞定的事，非要写 1000 行

3. **随意修改**
   - 有时会改掉那些它们没理解透的注释和代码
   - 哪怕这跟任务根本没关系

## 四大核心原则

### 1. Think Before Coding（先想，再写）

**核心**: 别假设，别隐藏困惑，把权衡摆出来。

- **具体要求**:
  - 不确定就问，别猜
  - 有歧义时列出多个解释，别自己拍板
  - 如果有更简单的方法，大胆说出来
  - 搞不清楚就停下来，说明白哪里不清楚

### 2. Simplicity First（极简优先）

**核心**: 用最少代码解决问题，不搞 speculative 的东西。

- **具体要求**:
  - 不要加没要求的功能
  - 不要给只用一次的代码造抽象
  - 不要加没要求的"灵活性"或"可配置性"
  - 不要为不可能发生的场景写错误处理
  - 200 行能写成 50 行？重写！

- **检验标准**: 资深工程师会夸这个简洁吗？不会就简化。

### 3. Surgical Changes（精准改动）

**核心**: 只碰该碰的，只扫自己的门前雪。

- **具体要求**:
  - 不要"优化"旁边的代码、注释、格式
  - 没坏的东西别重构
  - 匹配现有风格，哪怕你不喜欢
  - 发现无关的死代码？提出来，别直接删

- **检验标准**: 每一行改动都能追溯到用户的请求。

### 4. Goal-Driven Execution（目标驱动）

**核心**: 定义成功标准，循环验证直到达成。

- **具体做法**:
  - 把指令式的任务变成可验证的目标
  - "加个验证" → "先写无效输入的测试，让它们通过"
  - "修这个 bug" → "先写个复现测试，让它通过"
  - "重构 X" → "确保重构前后测试都能过"

- **多步骤任务要有简单计划**:
  ```
  1. [步骤] → verify: [检查]
  2. [步骤] → verify: [检查]
  3. [步骤] → verify: [检查]
  ```

Karpathy 的原话："LLM 特别擅长循环直到达成具体目标……别告诉它该做什么，给它成功标准，然后看着它跑。"

## 如何使用

### 方式 A: Claude Code 插件（推荐）

从 Claude Code 内，先添加 marketplace：

```
/plugin marketplace add forrestchang/andrej-karpathy-skills
```

然后安装插件：

```
/plugin install andrej-karpathy-skills@karpathy-skills
```

### 方式 B: CLAUDE.md（单项目）

新项目：

```
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
```

现有项目（追加）：

```
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md >> CLAUDE.md
```

### 方式 C: 使用 Cursor

项目还包含了 Cursor 项目规则（`.cursor/rules/karpathy-guidelines.mdc`），可以在 Cursor 中使用。

### 方式 D: 适配 Trae Solo

Trae Solo 支持通过**规则（Rules）**功能来配置 AI 助手的行为规范。

1. **创建规则文件**：
   在项目根目录创建 `project_rules.md` 或通过 Trae Solo 的规则面板创建新规则。

2. **配置 Karpathy 准则**：
   将以下内容添加到你的规则文件中：

   ```markdown
   # Karpathy 编码准则

   ## 1. Think Before Coding（先想，再写）
   - 不要假设。不要隐藏困惑。把权衡摆出来。
   - 如果不确定，先询问而不是猜测
   - 当存在歧义时，列出多种解释方式
   - 如果有更简单的方法，大胆说出来
   - 当不清楚时，停下来说明哪里不清楚

   ## 2. Simplicity First（极简优先）
   - 用最少的代码解决问题。不要搞投机性的东西。
   - 不要添加未被要求的功能
   - 不要为只用一次的代码创建抽象
   - 不要添加未被要求的"灵活性"或"可配置性"
   - 不要为不可能发生的场景编写错误处理
   - 如果 200 行可以写成 50 行，重写它！

   ## 3. Surgical Changes（精准改动）
   - 只碰该碰的。只清理自己制造的混乱。
   - 不要"优化"旁边的代码、注释或格式
   - 不要重构没有坏的东西
   - 匹配现有风格，即使你不喜欢
   - 如果发现无关的死代码，提出来但不要直接删除
   - 你的变更造成的孤儿代码要清理，但不要清理已存在的死代码

   ## 4. Goal-Driven Execution（目标驱动）
   - 定义成功标准。循环直到验证通过。
   - 把命令式任务转换为可验证的目标
   - 对于多步骤任务，制定简单的计划，每一步都有验证方式
   ```

3. **在 Trae Solo 中启用**：
   - 点击右侧 AI 功能管理设置按钮
   - 进入规则面板，选择你的规则文件或直接粘贴上述内容
   - 推荐使用英语编写规则，效果通常更好

### 方式 E: 适配 CodeBuddy

CodeBuddy 支持通过系统提示词来自定义 AI 行为。

1. **使用系统提示词参数**：
   ```bash
   # 方式一：直接使用 --append-system-prompt 追加准则
   codebuddy --append-system-prompt "
   请遵循以下 Karpathy 编码准则：
   1. Think Before Coding: 不要假设，不要隐藏困惑，遇到不确定先询问
   2. Simplicity First: 用最少的代码解决问题，不添加未被要求的功能
   3. Surgical Changes: 只修改必要的内容，不随意改动无关代码
   4. Goal-Driven Execution: 定义明确的成功标准，确保每一步可验证
   "

   # 方式二：从文件加载系统提示词（推荐用于版本控制）
   # 创建 karpathy-guidelines.txt 文件，写入准则内容
   codebuddy --system-prompt-file karpathy-guidelines.txt
   ```

2. **创建提示词文件**：
   ```bash
   # 创建 karpathy-guidelines.txt
   cat > karpathy-guidelines.txt << 'EOF'
   你是一个遵循 Karpathy 编码准则的 AI 编程助手。

   核心原则：
   1. Think Before Coding - 先思考再编码
      - 不要假设，不要隐藏困惑
      - 遇到不确定先询问，不要猜测
      - 展示多种方案和权衡

   2. Simplicity First - 简单优先
      - 用最少代码解决问题
      - 不添加未被要求的功能
      - 避免过度抽象

   3. Surgical Changes - 精准改动
      - 只修改必要内容
      - 不随意改动无关代码
      - 不重构未损坏的部分

   4. Goal-Driven Execution - 目标驱动
      - 定义明确的成功标准
      - 每一步都可验证
   EOF

   # 使用该文件
   codebuddy --system-prompt-file karpathy-guidelines.txt
   ```

## 如何判断它在起作用

这些准则起作用的标志：
- **Diff 中不必要的改动更少** — 只出现请求的改动
- **因过度复杂化导致的重写更少** — 第一次代码就很简单
- **澄清问题在实现之前** — 不是在犯错之后
- **干净、极简的 PR** — 没有顺路的重构或"改进"

## 权衡说明

这些准则偏向**谨慎胜过速度**。对于琐碎任务（简单的拼写修正、明显的单行修改），使用判断力——不是每个改动都需要如此严格。

目标是减少非平凡工作中的代价高昂的错误，而不是减缓简单任务的速度。

## 为什么这么火

1. **戳中真痛点**: 每个用 AI 编程的人都遇到过这些问题
2. **大神背书**: Karpathy 的观察比任何教程都更有说服力
3. **极简实现**: 一个文件就解决问题，不搞复杂
4. **即插即用**: 不用改工作流，直接装上就能用

## 核心洞察

这不是 prompt engineering 的简单进化。这是一个全新的工程维度：**你不只是在编程，你在编程AI的行为**。

10 万星不是给 70 行文字的，是给这个认知的。

---

## 扩展：其他流行 Skill 的适配指南

### gstack (Garry Tan)

#### gstack 简介

**作者**: Garry Tan (Y Combinator CEO)  
**仓库**: https://github.com/garrytan/gstack  
**Star 数**: 100,000+ ⭐

gstack 把 Claude Code 变成一支虚拟工程团队——CEO 重新思考产品、工程经理锁定架构、设计师捕捉 AI slop、评审员找生产 bug、QA 打开真实浏览器点击你的应用、发布工程师搞定 PR。

**核心理念**: 不同的任务需要不同的认知模式。规划不是评审，评审不是发布。如果把这些混在一起，你得到的就是平庸的输出。

#### gstack 核心 Skill

| Skill | 角色 | 作用 |
|-------|------|------|
| `/office-hours` | YC 办公时间 | 6 个强制问题，在写代码前重新思考产品 |
| `/plan-ceo-review` | CEO/创始人 | 重新思考问题，找到请求背后的 10 星产品 |
| `/plan-eng-review` | 工程经理 | 锁定架构、数据流、边界情况、测试覆盖 |
| `/review` | 资深工程师 | 找 CI 能过但生产会挂的 bug，自动修复明显的 |
| `/qa` | QA 主管 | 用真实浏览器测试应用，找 bug 并原子提交修复 |
| `/ship` | 发布工程师 | 同步 main、跑测试、审计覆盖率、推送到远程、开 PR |

#### 适配 Trae Solo

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

---

### Superpowers (Jesse Vincent)

#### Superpowers 简介

**作者**: Jesse Vincent (@obra)  
**仓库**: https://github.com/obra/superpowers  
**Star 数**: 124,000+ ⭐  
**核心理念**: Process over Prompt（流程大于提示词）

Superpowers 是一套完整的 AI 开发方法论 + 可组合技能库，给 AI 套上软件工程的"纪律与护栏"，让它像资深工程师一样**先思考、再规划、后编码、必验证**。

#### Superpowers 核心 Skill

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

#### 适配 Trae Solo

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

#### 快速开始模板

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

---

## 总结：三种方法论对比

| 方法论 | 核心理念 | 适用场景 |
|--------|----------|----------|
| **Karpathy Skills** | 先想再写，简单优先，精准改动，目标驱动 | 日常编码，减少 AI 常见错误 |
| **gstack** | 不同任务用不同认知模式，角色化思考 | 产品驱动的开发，从 0 到 1 项目 |
| **Superpowers** | Process over Prompt，强制 TDD 和流程纪律 | 需要严格工程规范的项目，团队协作 |

你可以根据项目需求选择合适的方法论，或者组合使用！
