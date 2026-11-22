# Project Learn

一个用于系统学习开源教程和教学型代码仓库的 Agent Skill。

它不会只替你总结 README，也不会按照目录从头机械读到尾。它会先获取真实资料、建立知识和代码地图，再把教程拆成可执行的学习单元，陪你运行、提问、深挖、复盘，并在真正有价值时沉淀笔记。

## 核心闭环

```text
准备真实资料
    ↓
建立知识地图与代码地图
    ↓
制定学习节奏
    ↓
阅读、运行、观察和修改
    ↓
随时提问并深挖细节
    ↓
主动复盘
    ↓
按需记录笔记
```

完成一个教程的标准不是“章节全部看过”，而是能够脱离教程解释核心机制、复现主要流程，并亲自运行或修改至少一个示例。

## 适用场景

- 跟着 GitHub 上的开源教程系统学习。
- 理解教程示例背后的代码架构和调用流程。
- 将一份较长的教程拆成每天可以完成的学习任务。
- 学习过程中随时追问概念、实现、设计取舍和失败模式。
- 将高价值问题、实验结论和排障过程整理成可复用笔记。

本 Skill 面向用户已经选定的教程或仓库，不负责批量搜索和推荐候选项目。

## 它会做什么

### 1. 准备教程资料

- Clone 用户选定的仓库，或读取已经存在的本地目录。
- 记录来源、分支和 commit，确保学习过程有明确版本。
- 检查 README、文档、依赖、示例、测试和主要源码。
- 找出最短可运行路径及必要的前置知识。

### 2. 建立两张地图

**知识地图**

- 教程的学习目标是什么。
- 章节之间有哪些依赖。
- 哪些概念是核心，哪些内容可以暂时跳过。
- 学完后应该具备什么能力。

**代码地图**

- 示例从哪里启动。
- 核心模块分别负责什么。
- 数据和控制如何流动。
- 示例、测试和关键源码分别在哪里。

### 3. 安排学习节奏

教程会被拆成若干个通常为 30-90 分钟的学习单元。每个单元都包含：

- 一个明确目标。
- 阅读和源码范围。
- 必须完成的实践。
- 需要回答的核心问题。
- 可验证的完成证据。
- 预计用时和候选笔记主题。

同一时间只推进一个学习单元。

### 4. 陪伴式学习

每次开始会先说明：

- 当前进度。
- 本次目标。
- 要看的资料和代码。
- 要完成的实践。
- 做到什么才算完成。

推荐的学习顺序是：

```text
先预测 → 阅读 → 运行 → 观察 → 解释 → 修改或练习 → 验证
```

### 5. 随时答疑和深挖

学习主线可以随时被问题打断，但不会因此丢失进度。复杂问题会按需要逐层展开：

1. 一句话说明本质。
2. 解释它解决的问题。
3. 梳理运行过程、数据流或调用链。
4. 指向具体章节、文件和代码符号。
5. 提供最小示例或验证实验。
6. 说明边界条件、常见误解和失败模式。

问题解决后，会回到原来的学习节点。

### 6. 复盘和笔记

完成学习单元后，Skill 会先让学习者凭记忆解释核心机制和验证结果，而不是立即代写总结。

以下内容通常值得记录：

- 教程或项目的整体架构。
- 已经讲清并验证的困难概念。
- 关键调用链、数据流和设计取舍。
- 环境配置、排障过程及可复现命令。
- 修改代码或运行实验得到的结论。
- 容易遗忘的误区、边界和失败模式。

笔记回答的是“我理解并验证了什么”，不是对教程原文的重复改写。

## 安装

### Codex

```bash
git clone https://github.com/beyondaprilzjl-lab/project-learning-skill.git \
  ~/.codex/skills/project-learn
```

调用方式：

```text
$project-learn 学习这个教程：https://github.com/OWNER/REPO
```

也可以直接使用自然语言：

```text
帮我 clone 并学习这个开源教程
继续上次的教程学习
解释一下当前章节的这个细节
把刚才理解的内容记录成笔记
```

### Claude Code

Claude Code 支持标准的 Agent Skills 目录结构。将仓库克隆到个人 Skill 目录后，即可在本机所有 Claude Code 项目中使用。目录规则与加载方式可参考 [Claude Code Skills 官方文档](https://code.claude.com/docs/en/skills)。

macOS、Linux 或 WSL：

```bash
git clone https://github.com/beyondaprilzjl-lab/project-learning-skill.git \
  ~/.claude/skills/project-learn
```

Windows PowerShell：

```powershell
git clone https://github.com/beyondaprilzjl-lab/project-learning-skill.git `
  "$env:USERPROFILE\.claude\skills\project-learn"
```

安装完成后新建 Claude Code 会话；如果当前会话尚未发现该 Skill，可以执行：

```text
/reload-skills
```

直接调用：

```text
/project-learn 学习这个教程：https://github.com/OWNER/REPO
```

也可以直接使用自然语言，Claude Code 会根据 `SKILL.md` 中的 `description` 判断是否需要启用本 Skill：

```text
帮我系统学习这个开源教程：https://github.com/OWNER/REPO
继续上次的教程学习
解释一下当前章节的这个细节
```

`agents/openai.yaml` 是 Codex 使用的展示元数据，Claude Code 不依赖该文件，不会影响 Skill 的发现和调用。`references/` 中的辅助模板会通过 `SKILL.md` 的相对路径按需读取。

### Kimi Code

```bash
git clone https://github.com/beyondaprilzjl-lab/project-learning-skill.git \
  ~/.kimi-code/skills/project-learn
```

新建会话后调用：

```text
/skill:project-learn 学习这个教程：https://github.com/OWNER/REPO
```

Kimi Code 也可以根据 `SKILL.md` 中的描述自动判断何时使用本 Skill。

## 使用示例

### 从一个新教程开始

```text
$project-learn

学习这个教程：
https://github.com/OWNER/REPO

我的目标是理解它的核心机制，并能独立修改一个示例。
每天可以投入 60 分钟。
```

Skill 会依次：

1. Clone 并检查真实仓库。
2. 生成知识地图和代码地图。
3. 说明学习边界和完成标准。
4. 制定顺序学习计划。
5. 给出第一个学习单元。

### 学习过程中追问

```text
为什么这里要使用事件循环，而不是直接同步调用？
```

回答完成后，Skill 会总结结论并返回原来的学习节点。

### 完成一个单元

```text
这个单元做完了，开始复盘。
```

Skill 会先检查你能否独立解释和提供实践证据，再决定是否完成该单元以及是否需要生成笔记。

## 目录结构

```text
project-learning-skill/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── artifact-templates.md
```

- `SKILL.md`：核心行为、流程、路由和验收规则。
- `references/artifact-templates.md`：项目总览、学习计划、单元记录和概念笔记模板。
- `agents/openai.yaml`：Codex 使用的展示名称和默认提示；Claude Code 不依赖该文件。

## 设计原则

- **真实资料优先**：以本地教程、源码和运行结果为依据。
- **实践优先**：不把“读完”当作完成。
- **单线推进**：同一时间只处理一个主要学习单元。
- **问题不打断状态**：深挖问题后回到原学习节点。
- **证据驱动**：事实、源码结论和推断应明确区分。
- **按需记录**：只沉淀已经理解或验证的高价值内容。
- **学习者参与**：Agent 可以辅助运行和排障，但不会代替学习者完成理解。

## 自定义

可以直接修改 `SKILL.md` 调整：

- 单次学习时长。
- 复盘问题的数量和深度。
- 笔记触发条件。
- 教程完成标准。
- 默认语言和表达风格。

修改后建议检查 YAML frontmatter 是否仍然包含有效的 `name` 和 `description`，并确认 `references/` 中的相对链接可访问。
