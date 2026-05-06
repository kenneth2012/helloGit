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
