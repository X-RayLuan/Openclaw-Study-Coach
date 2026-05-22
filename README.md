<div align="center">

# Openclaw Study Coach

### 给孩子的全科 AI 辅导员 · 主线语文(阅读理解+作文)· 含家长 Playbook

**An AI tutoring agent for elementary school kids — focused on Chinese reading comprehension & writing, with a parent playbook for daily 3-minute family activities.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Compatible-blueviolet)](https://claude.com/claude-code)
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Skill_Compatible-orange)](https://github.com/openclaw)
[![Language](https://img.shields.io/badge/Language-中文_%2F_English-red)](#)

[**📖 是什么**](#是什么) ·
[**🚀 60 秒启动**](#-60-秒启动) ·
[**🧠 设计原则**](#-设计原则18-条核心规则) ·
[**👨‍👩‍👧 家长 Playbook**](#-家长-playbook父母可执行的事) ·
[**❓ FAQ**](#-faq常见问题)

</div>

---

## 是什么

**Openclaw Study Coach** 是一个**给小学中高年级孩子的 AI 学习辅导员**,以 **markdown skill 包**的形式分发。可以在 **Claude Code** 或 **OpenClaw** 上直接跑,**不需要任何前端、不需要部署服务器、不需要 API key 之外的费用**。

它解决三个真实痛点:

1. **语文阅读理解的发散题**(`"读完什么感受?" / "如果是你你会怎么做?" / "为什么作者要..."`)—— 没标准答案,孩子无从下手,家长也讲不清。
2. **作文** —— 找不到合适的辅导老师,孩子不知道从哪开头,写完不知道怎么改。
3. **家长不知道怎么把学科变成游戏** —— 沈奕斐讲自驱力要靠兴趣,但"想小游戏"对很多家长来说就是做不到。

这个系统把"想小游戏 / 记得孩子的弱项 / 每天安排节奏"这些**重复又耗心力**的事接管下来,**让父母把有限精力用在 AI 做不了的事上**(陪伴、亲子游戏、情绪共鸣、生活观察)。

> **一句话总结**: 一个**会记得她**的辅导员,陪她写作文做阅读理解,在她卡住时用 4 步法引导而不是给答案;同时每天给爸妈一个**3 分钟可做的家庭活动**。

---

## 这个项目跟其他方案的区别

| 维度 | ChatGPT / 通用 AI | 在线家教 / 补习班 | 单科练习 App | **Openclaw Study Coach** |
|---|---|---|---|---|
| 记得孩子的卡点 | ❌ 每次重置 | ✓ 部分 | ⚠️ 只看做题数据 | ✅ **三件套画像纵向累积** |
| 处理阅读理解发散题 | ⚠️ 直接给答案 | ✓ 取决于老师 | ❌ 基本不练 | ✅ **4 步法引导,不直接给答案** |
| 作文辅导 | ⚠️ 容易代写 | ✓ 取决于老师 | ⚠️ 模板化 | ✅ **5 阶段流程,永远不替写** |
| 家长怎么参与 | 自己摸索 | 看老师反馈 | 看打分 | ✅ **每天 3 分钟具体活动(含台词)** |
| 数据归属 | 在云端 | 在机构 | 在 App 公司 | ✅ **本地 markdown,孩子的数据永远是你的** |
| 一年费用 | 订阅费 | 数千-数万 | 数百-数千 | ✅ **0 元**(Claude API 按量计费,平均一天 ≤ 1 元) |
| 因材施教 | 看 prompt 写法 | 看老师 | ❌ | ✅ **基于 weakness-profile 自动调整出题** |

---

## 🚀 60 秒启动

### 前置依赖

- macOS / Linux / Windows + WSL
- [Claude Code](https://claude.com/claude-code) 已安装 (推荐),**或** [OpenClaw](https://github.com/openclaw) 已安装

### 安装

```bash
# 1. 克隆
git clone https://github.com/X-RayLuan/Openclaw-Study-Coach.git
cd Openclaw-Study-Coach

# 2. 改你家孩子的信息
vim USER.md     # 改里面的 <kid1> / <小宝> / 年级 / 教材版本 等
                # 这是唯一需要你手动改的文件

# 3. 启动
claude          # 如果用 Claude Code
                # 或者:openclaw 命令行(workspace 模式)
```

### 第一次测试 (60 秒)

启动 agent 后,试这 4 个场景,看效果对不对:

```
你是谁?
```
→ 应该自我介绍为"小辅,你的学习辅导员",大概率会用 ✨ 类 emoji + 短句。

```
我是妹妹。今天阅读理解我不会做一道题——"读完这段话你什么感受?"
```
→ 应该触发 reading-comp-tutor,**用 4 步法引导,不直接给答案**。

```
我是妹妹。今天作文要写"我的妈妈"。我不会写。
```
→ 应该触发 writing-coach,先跟你聊不直接写,问 3-5 个细节。

```
(切到家长口吻)生成今日日报。
```
→ 应该触发 daily-report,写 6 字段日报 + **今晚 3 分钟可做的一件事**。

---

## 🧠 设计原则(18 条核心规则)

> 这些规则分布在 `SOUL.md` / `AGENTS.md` / 各 skill 的硬规则区,是这套系统的灵魂。如果你想 fork 改造,**最值得保留的就是这 18 条**。

### 跟孩子说话(给 agent 的规则)

1. **永远不直接给答案**,用引导、选项、工具箱。
2. **反馈三段式**:具体做对了什么 → 一句过渡 → 加分公示。
3. **错题反馈先肯定她思考里"对"的部分**,再指改进点。
4. **指出"具体瞬间"**,不写"你真棒""加油"这种空话。
5. **数学一次只给一道题**。
6. **积分永远只加不减**(完成 +5,全对 +3,连续 +N,完成全部 +10)。
7. **每条任务 5-20 分钟**,超过就拆。
8. **她明显累/烦/哭 → 立刻停**,落盘进度,改用陪伴模式。

### 阅读理解 4 步法(发散题专用)

9. **Step 1 翻译题目**:把"问什么"用大白话复述给她。
10. **Step 2 回原文找证据**:让她找"人物动作 / 语言 / 场景描写"。
11. **Step 3 给感受词 / 选项工具箱**:她说不出感受时,给 3-5 个让她选。
12. **Step 4 组合答案**:用"我觉得 X 因为原文 Y"的固定句式。

### 作文 5 阶段(永远不替写)

13. **不替孩子写一个字**,只给细节问题、句式模板、方向选项。
14. **先写最有画面的一段**,不写开头。
15. **聊出来再写出来**:挖 5 个具体细节(看 / 听 / 闻 / 身体 / 心里)。
16. **改的时候只改一处**,不一次给 5 条意见。
17. **重视具体不重视华丽**:"她笑了 + 动作" > "绽放出灿烂的笑容"。

### 家长 Playbook(给父母的事)

18. **每天的 playbook ≤ 5 分钟,3 分钟内能开始**,具体到台词或动作级别,**接今天孩子学的**,做 **AI 做不了的事**(陪伴、实物互动、情绪共鸣)。

---

## 📁 系统结构

```
Openclaw-Study-Coach/
├── CLAUDE.md            # 入口:Claude Code 启动时自动加载
├── SOUL.md              # 辅导员的语气、边界、人设、4 步法、5 阶段
├── USER.md              # 孩子信息 ⭐ 你需要改的唯一一个文件
├── AGENTS.md            # 工作流 + 视角分离 + 数据流 + 积分系统
├── TOOLS.md             # 落盘约定:文件命名 + 错题卡格式
├── README.md            # 本文件
├── LICENSE              # MIT
│
├── .claude/skills/      # 9 个 Skill,每个有自己的 SKILL.md
│   ├── homework-intake/         # 拆作业、排顺序、生成"闯关清单"
│   ├── reading-comp-tutor/      # ⭐ 阅读理解 4 步法(发散题)
│   ├── writing-coach/           # ⭐ 作文 5 阶段
│   ├── mistake-tracker/         # 错题归档 + 回流复习池
│   ├── review-scheduler/        # 7 天复习节奏
│   ├── weakness-tracker/        # 三件套画像维护
│   ├── daily-report/            # 日报 + 触发 parent-playbook
│   ├── weekly-report/           # 周报 + 重写 weakness-profile
│   └── parent-playbook/         # ⭐ 父母每天 3 分钟可做的事
│
└── data/                # 所有学习数据(本地 markdown,默认 gitignore)
    ├── profile/         # ⭐ 三件套画像 = 孩子的纵向记忆
    │   ├── weakness-profile.md  # 当前弱点 pattern(只给家长 + agent)
    │   ├── strengths.md         # 强项 + 具体做对的瞬间(孩子可看)
    │   └── interests.md         # 兴趣(用来包装练习题)
    ├── parent-playbook/         # 父母可执行的活动 (daily + weekend)
    ├── homework/                # 作业:inbox / parsed / done
    ├── mistakes/                # 错题:subjects / review_queue
    ├── plans/                   # 复习计划
    ├── reports/                 # 日报 / 周报 / trends.csv
    └── points/log.jsonl         # 积分日志(只加不减)
```

---

## 🧬 三件套画像:让 AI 真正"记得"孩子

这是这套系统最值钱的设计。三个 markdown 文件构成孩子的**纵向记忆**:

### weakness-profile.md(只给家长 + agent)
> 当前关注的卡点 pattern,带 4 字段(表现 / 频次 / 已尝试方案 / 下一步)。
> 每天 daily-report 即时追加观察,每周 weekly-report 提炼成 ≤ 7 条 pattern。
> 反复出现 ≥ 3 次的升级为 pattern,出现 ≥ 2 周未再出现的移到"已解决"。

### strengths.md(孩子也能看精简版)
> 已稳的能力 + 最近 14 天做对的具体瞬间(`5/22 在《小猫》找到"轻轻地"做证据 ⭐`)。
> 孩子要看自己强项时,给一份正面化的精简版——这是她**成就感的锚点**,激发自驱的核心。

### interests.md(用来包装练习)
> 喜欢的主题 / 故事 / 反感的元素 / 日常生活线索。
> agent 出阅读材料、作文题、联想引导时**优先用她的兴趣**——这是激发自驱的第一步。

### 工作流程

```
每天对话 → daily-report 即时追加 → 三件套画像增长
              ↓
        生成今晚 parent-playbook
              ↓
   下次启动 claude → CLAUDE.md 自动 @import 三件套
              ↓
   agent 立刻知道她最近卡哪、强在哪、喜欢什么
              ↓
   每周 weekly-report → 重写 weakness-profile 做提炼
              ↓
        生成周末 parent-playbook(30 分钟亲子活动)
```

---

## 👨‍👩‍👧 家长 Playbook:父母可执行的事

回应教育学者**沈奕斐**那句:

> 培养孩子自驱力,要让孩子对学习有兴趣。父母要想办法把数学/语文通过小游戏变得生动有趣。**可是这个对我来说好难啊。**

这套系统**把"想小游戏"的负担从父母身上挪到 agent 身上**。

每天 daily-report 写完日报后,**自动**生成一份 3 分钟可做的家庭活动到 `data/parent-playbook/daily/YYYY-MM-DD_playbook.md`。

### 4 类日活动模板

| 类型 | 适用场景 | 例子 |
|---|---|---|
| **类 A** 晚餐对话延伸 | 今天孩子做了阅读理解 | 妈妈问:"今天那只小猫躲在花盆后面。**如果家里有一只小猫这样躲起来妈妈会怎么做?**"(故意先给妈妈版本)然后听她说她的版本。 |
| **类 B** 实物对照细节 | 今天孩子写了作文 | 看小妹作文里写"蓝色的裙子"——找一个家里真正蓝色的东西问她:"这种蓝叫什么蓝?" |
| **类 C** 角色互换 | 今天孩子有突破 | "妈妈这题真不会,你能教我一下吗?"让她当老师讲一次。 |
| **类 D** 纯陪伴 | 累 / 心情不好 / streak ≥ 5 天 | 睡前问:"今天最开心的一件事是什么?"(不问学习)然后你也说你今天最开心的一件事。 |

### 5 条硬规则

每个活动**必须**满足:
1. ✅ **3 分钟内能开始**(不打印、不买东西、不开电脑)
2. ✅ **不像作业**(是聊天 / 游戏 / 顺嘴一问)
3. ✅ **接今天孩子的学习**(不凭空起新内容)
4. ✅ **AI 做不了的**(真人陪伴 / 实物互动 / 情绪共鸣)
5. ✅ **到台词级别**(具体到"妈妈说:'XXX'",不给抽象建议)

### 周末活动

每周五,weekly-report 额外生成一份 30 分钟的周末活动到 `data/parent-playbook/weekend/`,4 类模板:

- **共读** — 读一篇短文,只问"你最喜欢哪段"和"如果是你你会怎么做"
- **家庭小报** — 让孩子当一周一次的"家庭记者",100 字记录这一周
- **观察类** — 带去一个地方(楼下花园 / 菜市场),记录"3 个细节"
- **语言游戏** — 不需要道具的 3 种语言游戏(词语接力 / 形容词接力 / 故事接力)

---

## 📊 一个月预期(跑下来应该看到什么)

| 阶段 | 系统在做的 | 你能看到的 | 孩子状态 |
|---|---|---|---|
| **第 1 周** | 测试家长报告的弱点,初步建画像 | 每天 1 份日报 + 3 个画像文件开始有内容 + 父母 playbook | 接受新流程 |
| **第 2-3 周** | 画像里出现 ≥ 1 个 pattern,strengths 有 ≥ 5 个具体瞬间 | 每周看 1 次周报就够,日报扫一眼 | 开始**主动**问 agent("我能问你一道题吗") |
| **第 1 个月** | weakness-profile 形成,review-scheduler 按 pattern 排了 3 周复习 | **不再焦虑"我该怎么帮她"**,因为日报里有具体的"今晚做什么" | 在某一类(比如代入类)有可衡量的进步 |

**这个系统的成功标准不是"孩子做了多少题",而是**:
- 1 个月后,孩子能**说出**自己阅读理解的 1 个具体卡点(不是"我不会")
- 1 个月后,孩子能**自己开口**说"今天我想做语文"
- 1 个月后,父母**不再焦虑**"我该怎么帮她"

---

## 🛠️ 兼容性

### Claude Code(推荐,最快)

直接 clone 进任何目录,`cd` 进去跑 `claude`,自动加载 `CLAUDE.md` + 所有 skills + 三件套画像。

### OpenClaw

把整个目录当 workspace,在 OpenClaw Control 里指定 workspace path,所有 SKILL.md / SOUL / USER / AGENTS / TOOLS 文件 OpenClaw 原生兼容。

### 飞书 / Lark 入口(可选升级)

参考"微光游戏社 / 人间折腾录"的 OpenClaw 文章,接一个飞书机器人作为孩子端入口。`data/` 目录的所有 markdown 都是标准格式,迁移到 OpenClaw + 飞书时直接 copy。

### 多孩子隔离

`cp -R Openclaw-Study-Coach kid2-coach` 直接复制整套 workspace。USER.md 改 `kid_id` / 昵称 / 教材即可。

---

## ❓ FAQ(常见问题)

### Q1: 这个跟直接用 ChatGPT 辅导有什么区别?

**ChatGPT 每次对话都重置,记不住你孩子的弱项**。这套系统通过三件套画像(`weakness-profile` / `strengths` / `interests`)**纵向累积**孩子的学习数据,下次启动 agent 时它"记得"她最近卡哪、强在哪、喜欢什么。**这是因材施教的物理基础**。

### Q2: 数据安全吗?

**所有数据本地存储在 markdown / CSV 文件里,不上云、不外发**。孩子的真实信息(姓名 / 学校 / 同学)在 USER.md 里已经被"代号化"要求(用 `kid1` 不用真名)。`.gitignore` 默认 ignore 全部 `data/` 内容,你 fork 后 commit 不会泄露真实学习记录。

### Q3: 一年大概花多少钱?

如果用 Claude Code,**主要成本是 Claude API**(目前 Claude Sonnet 4.6 大约 $3/百万 input tokens, $15/百万 output)。一个 10 岁孩子每天 30 分钟辅导,**平均一天不超过 1 元人民币**。一年合计 300-500 元。比任何线下补习便宜一个数量级。

### Q4: 我家孩子不是四年级 / 不是女生 / 不在中国,能用吗?

可以。USER.md 里所有信息都是 placeholder。改成你家场景即可:
- 不同年级 → 改"年级"字段
- 男孩 → 改"性别 + 昵称 + 反馈情绪表达"(SOUL.md 可微调)
- 海外 / 国际学校 → 改"地区 + 教材",agent 出题会按你填的标准

### Q5: 这跟 OpenClaw 是什么关系?

**这套系统的设计哲学来自 OpenClaw 的官方实践案例**(微光游戏社 "用 OpenClaw 给孩子搭全科辅导系统" 系列文章 4 篇)。我们把那套设计在 **Claude Code** 上重新实现,保留所有核心规则(SOUL/USER/AGENTS/TOOLS + skills),并针对**语文阅读理解+作文**做了深度优化(新增 reading-comp-tutor / writing-coach / weakness-tracker / parent-playbook 4 个核心 skill)。

也兼容 OpenClaw——把整个目录当 OpenClaw workspace 即可。

### Q6: 没有 Claude Code / OpenClaw 怎么办?

[Claude Code](https://claude.com/claude-code) 是 Anthropic 官方 CLI,Mac / Windows / Linux 都装。免费安装,只付 API 费用。

[OpenClaw](https://github.com/openclaw) 是开源的 agent 框架,跟飞书集成做得最好。

如果你只用 ChatGPT,可以**手动**把 SOUL.md + USER.md + AGENTS.md + TOOLS.md 的内容粘贴到 system prompt 里,9 个 skill 的内容存为 prompt 模板手动调用。能跑,但失去了"自动落盘 + 纵向记忆"的能力。

### Q7: How do I use this if I'm not Chinese?

The system prompts are in Chinese because the design targets **Chinese elementary school reading comprehension and writing**. The underlying framework (4-step method for divergent questions, 5-stage writing flow, weakness profile, parent playbook) is **language-agnostic** — fork this repo and translate the 5 top-level `.md` files + 9 `SKILL.md` files into your target language. PR welcome.

### Q8: AI is replacing teachers — is this good for kids?

This system explicitly does NOT replace teachers or parents. It absorbs the **repetitive, error-prone, mentally exhausting** parts of tutoring (scheduling tasks, tracking mistakes, generating practice, remembering weaknesses), and **frees parents to do what AI cannot**: emotional bonding, real-world games, situational observation. See the **Parent Playbook** section.

The system has 18 hard rules baked in to prevent harmful patterns: never give direct answers to divergent questions, never criticize the child, never deduct points, never label a child as "smart/dumb", stop immediately when the child is emotional.

### Q9: 怎么贡献?

欢迎 PR:
- **新 skill** 提交:数学 / 英语 / 科学 / 历史等学科的专项辅导 skill
- **新地区适配**:不同省份教材的难度参考
- **新 playbook 模板**:更多类型的亲子活动
- **翻译**:英文 / 日文 / 韩文版本

直接 fork → 改 → 开 PR。**Skill 的 SKILL.md 写法参考 `.claude/skills/reading-comp-tutor/SKILL.md`**——所有 skill 都按那套结构写。

### Q10: 跟商业化的 AI 辅导产品比怎么样?

商业 AI 辅导产品(比如某些教育大厂的"AI 1对1")在**封闭系统**里跑,你看不到 system prompt,改不了规则,孩子的数据是他们的。这套系统:

- ✅ **完全开源**,你能看到每一条规则
- ✅ **数据本地**,孩子的画像永远是你的
- ✅ **可改可扩展**,觉得 4 步法太机械就改,觉得反馈太长就砍
- ✅ **跟着 LLM 进步免费升级**(切到 Claude Opus / GPT-5 都不用改 skill)
- ⚠️ **没有 GUI 包装**,需要懂一点命令行
- ⚠️ **没有客服**,坏了自己修 / 提 issue

适合**愿意花一两个小时配置 + 喜欢可控感**的家长。

---

## 🏗️ 系统架构(技术细节)

### 数据流

```
家长/孩子输入(文字/图片)
       │
       ▼
┌──────────────────────────────┐
│ Claude Code agent             │
│ 加载 CLAUDE.md @imports:      │
│ - SOUL/USER/AGENTS/TOOLS      │
│ - 三件套画像(每次启动)        │
└──────────────────────────────┘
       │
       ▼
┌──────────────────────────────┐
│ 触发对应 Skill                 │
│ - homework-intake             │
│ - reading-comp-tutor (4 步)   │
│ - writing-coach (5 阶段)      │
│ - mistake-tracker             │
└──────────────────────────────┘
       │
       ▼
┌──────────────────────────────┐
│ 即时落盘到 data/              │
│ - homework / mistakes / plans │
│ - 三件套画像追加              │
│ - points/log.jsonl 追加       │
└──────────────────────────────┘
       │
       ▼ (一天结束时)
┌──────────────────────────────┐
│ daily-report                  │
│ - 写日报 (6 字段)              │
│ - 追加 trends.csv             │
│ - 更新 USER.md streak         │
│ - 调用 weakness-tracker       │
│ - 调用 parent-playbook        │
│   → 生成今晚 3 分钟活动        │
└──────────────────────────────┘
       │
       ▼ (每 7 天)
┌──────────────────────────────┐
│ weekly-report                 │
│ - 写周报 + 作文进步轨迹        │
│ - 重写 weakness-profile       │
│ - 生成周末 playbook           │
└──────────────────────────────┘
```

### Skill 调用图

```
                     ┌─────────────────┐
        孩子输入 ───→ │ homework-intake │←── 家长发作业
                     └─────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
      ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
      │  reading-    │ │  writing-    │ │ mistake-     │
      │  comp-tutor  │ │  coach       │ │ tracker      │
      └──────────────┘ └──────────────┘ └──────────────┘
              │               │               │
              └───────────────┼───────────────┘
                              ▼
                     ┌─────────────────┐
                     │ daily-report    │
                     └─────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
      ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
      │ weakness-    │ │ parent-      │ │ review-      │
      │ tracker      │ │ playbook     │ │ scheduler    │
      └──────────────┘ └──────────────┘ └──────────────┘
              │                               │
              └────────────┬──────────────────┘
                           ▼
                  ┌─────────────────┐
                  │ weekly-report   │
                  │ (每 7 天)        │
                  └─────────────────┘
```

---

## 🙏 致谢 / 灵感来源

这个项目站在以下肩膀上:

- **[微光游戏社 / 人间折腾录](https://mp.weixin.qq.com/s/weQmKdFKEQKf7Oys1P1x4w)** — 《用 OpenClaw 给孩子搭全科辅导系统》系列 4 篇文章,**核心架构来自这里**(SOUL/USER/AGENTS/TOOLS 四规则文件 + 3 核心 skill + 视角分离的思想)
- **沈奕斐**(教育学者)— **自驱力底层逻辑**(兴趣 → 投入 → 成就感 → 自驱),"父母把学科变小游戏"的痛点描述,Parent Playbook 的设计初衷
- **[Claude Code](https://claude.com/claude-code)** — 运行平台,文件式 skill 系统,workspace 模式
- **[OpenClaw](https://github.com/openclaw)** — Skill 设计哲学,workspace 设计哲学
- **[Anthropic Skills](https://docs.claude.com/en/docs/claude-code/skills)** — `SKILL.md` 格式规范

---

## 🏷️ 关键词 / Topics

`ai-tutor` · `claude-code` · `openclaw` · `claude-code-skill` · `kids-education` · `chinese-elementary-school` · `reading-comprehension` · `writing-coach` · `parent-coach` · `homework-helper` · `self-driven-learning` · `markdown-agent` · `ai-for-parents` · `personalized-learning` · `agent-skill` · `longitudinal-memory` · `weakness-profile` · `小学辅导` · `语文阅读理解` · `作文辅导` · `自驱力` · `家长助手` · `AI辅导` · `全科辅导` · `小妹` · `沈奕斐`

---

## 📜 License

[MIT](LICENSE) © 2026 X-RayLuan

> Forks 和 PRs 都欢迎。如果你 fork 后做了好的扩展(新学科 / 新 playbook / 翻译版),开 PR 我合并回 main。

---

<div align="center">

**Made with ❤️ for kids who deserve a tutor that remembers them.**

[⬆️ 回到顶部](#openclaw-study-coach)

</div>
