# Communication Coach · 表达力教练

一个用对话训练表达能力的 Skill。它不替用户写答案，而是通过**诊断 → 引导 → 重新表达 → 对比**的闭环，让用户逐渐形成自己的表达思路。

> 不替用户表达，而是帮助用户学会表达。
> 不追求一次说得完美，而是让下一次说得更好。

## 它解决什么

- 面对开放问题，不知道说什么。
- 有想法，但说不清重点、顺序乱。
- 表达空泛，缺事实、细节、例子。
- 说话重复、啰嗦、书面腔、像背稿。
- 练的时候会，真实会议/面试/社交场景就卡。
- 想练，但不想上课、打卡、背模板。

## 它不做什么

- 不代写文案、演讲稿、周报。
- 不直接润色成稿。
- 不输出伪精确评分和排名。
- 不讲长篇沟通理论。
- 不做心理诊断或人格评价。

## 安装

把本目录（`SKILL.md` 所在目录）复制到 agent 的 skills 目录，并命名为 `communication-coach`。在**本目录内**运行：

```bash
# Claude Code / 兼容 ~/.claude/skills 的运行时
mkdir -p ~/.claude/skills/communication-coach
rsync -a ./ ~/.claude/skills/communication-coach/

# 或放到当前项目的 .claude/skills/
mkdir -p .claude/skills/communication-coach
rsync -a ./ .claude/skills/communication-coach/
```

安装后入口文件是 `communication-coach/SKILL.md`。目录名建议与 `name: communication-coach` 保持一致，避免部分运行时识别不到。不同运行时对 skills 目录的约定不同，以你的运行时文档为准。

## 怎么用

直接说出你的状态或需求，不需要记命令：

- “我想练表达，但不知道从哪开始。”
- “让我夸一个人，但我不知道夸什么。”
- “我明天开会要发言，帮我练一下。”
- “我说话总是没重点，帮我看看。”
- “我这段表达是不是太啰嗦了？”
- “给我复盘一下，我最近练得怎么样。”

Skill 会根据状态选择：初始诊断、内容生成、逻辑组织、语言表达或场景模拟。

## 一次训练长什么样

```text
给一个具体任务
  → 用户先说
  → 只诊断一个核心问题（引用原话）
  → 给一个可执行的方法
  → 用户用同一题重说
  → 对比两次的可观察变化
  → 记录 + 下次建议
```

默认 10–15 分钟，一次只改一个点。不要求每日打卡。

## 目录结构

```text
communication-coach/
├── SKILL.md                      # 主控：角色、状态机、流程、边界
├── README.md
├── DESIGN.md                     # PRD 映射、设计取舍、限制与下一步
├── modules/                      # 四个训练模块的执行规则
│   ├── content-generation.md
│   ├── logical-organization.md
│   ├── language-expression.md
│   └── scenario-practice.md
├── frameworks/                   # 思考与表达工具
│   ├── expression-frameworks.md
│   ├── thinking-frameworks.md
│   └── observation-framework.md
├── scenario-library/             # 职场/社交/学习场景与追问链
│   ├── workplace.md
│   ├── social.md
│   └── learning.md
├── evaluation/                   # 诊断与反馈规范
│   ├── diagnostic-rubric.md
│   ├── feedback-rules.md
│   └── acceptance-tests.md
├── progression/                  # 训练路径与进度追踪
│   ├── training-path.md
│   └── progress-tracking.md
├── examples/
│   └── dialogue-examples.md      # 关键情境的对话校准
└── templates/
    ├── profile.md
    ├── session-record.md
    └── material-entry.md
```

更完整的 PRD 映射、关键取舍与已知限制见 `DESIGN.md`。

## 设计要点

**1. 教练，不是代答者**
用户没尝试前，不给完整答案。卡住时按 L1–L6 逐级加辅助，一次只升一级。

**2. 一次只改一个点**
每次反馈锁定一个最影响任务、最可改、最有证据的问题。次要问题只记下，不展开。

**3. 诊断优先**
不预设用户该练什么。从表达中选主问题，再决定模块，而不是反过来。

**4. 重复表达优于单次评价**
每次训练必须落到“同一题再说一次”，并对比可观察的变化，而不是只说“有进步”。

**5. 不制造问题**
用户已经说清楚，就明确说“够用”，然后提高难度或换场景。不为了显得专业而挑刺。

**6. 方法逐渐淡出**
结构从“给骨架”到“只给第一句”，再到“用户自己选”，最后不再提结构名称。

**7. 记录服务于下一次**
只存影响训练的信息：当前重点、反复问题、已掌握方法、最近三次。不做仪表盘。

## 数据存在哪

按顺序：

1. 用户指定目录；
2. `COACH_HOME`；
3. `~/.communication-coach/`；
4. 当前目录 `.coach/`（沙箱兜底）。

包含 `profile.md`、`sessions/`、`materials.md`。只在本机，不联网。可随时要求删除。

## 自测

`evaluation/acceptance-tests.md` 包含 7 个核心场景 + 4 个附加测试：

1. 用户不知道说什么
2. 有内容但混乱
3. 表达空泛
4. 表达啰嗦
5. 要求直接给答案
6. 用户已经表现良好
7. 真实场景训练

每个测试都有通过标准与失败信号，改完 Skill 后可直接逐条回归。

## 和 HTML 原型的关系

本仓库是**对话训练 Skill** 的实现，对应需求文档中的 MVP 闭环：诊断、内容生成、逻辑组织、重新表达、记录、自由训练入口。

原型 HTML 是界面与流程的视觉参考；本 Skill 不依赖网页，直接在任何支持 skills 的对话 agent 中使用。若要做成独立产品，可把 `SKILL.md` 的状态机与 `evaluation/` 的规则作为后端教练逻辑，前端沿用原型的训练页、成长记录和素材库。

## 许可

可自由修改用于个人或团队内部训练。若对外分发，请保留训练理念与边界说明。
