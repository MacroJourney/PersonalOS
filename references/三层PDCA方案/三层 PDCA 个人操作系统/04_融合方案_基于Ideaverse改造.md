# 融合方案：基于 Ideaverse Zero 2.5 + PDCA 三层系统

以 Ideaverse Zero 2.5 为基础框架，融合 PDCA 三层系统的核心设计，形成 Claude + Obsidian 协作系统。

---

## 核心设计理念

### 三个核心原则（继承自03方案）

1. **单一真相源（Single Source of Truth）**
   - 所有数据存在本地 Markdown 文件中
   - Claude 通过读取文件获取完整上下文
   - 避免信息分散在多个系统

2. **约定优于配置（Convention over Configuration）**
   - 通过文件命名、路径、frontmatter 建立结构
   - Claude 根据约定自动理解文件关系
   - 减少手动维护的元数据

3. **渐进式自动化（Progressive Automation）**
   - 第一阶段：手动记录 + Claude 辅助分析
   - 第二阶段：半自动（Obsidian 插件 + 触发式脚本）
   - 第三阶段：全自动（定时任务）

### 融合的核心理念

**为什么选择融合而非替换？**

| Ideaverse 的优势 | PDCA 方案的优势 |
|-----------------|----------------|
| 30+ 插件预配置 | 战略层显式设计 |
| MOC 知识关联体系 | AI 协作原生设计 |
| 成熟的模板和工作流 | 三层 PDCA 循环清晰 |
| Inbox 快速捕获 | 目标对齐机制 |
| 三状态项目管理 | Claude Projects 分工 |

**融合原则**：
- 保留 Ideaverse 的**基础设施**（插件、模板、结构）
- 注入 PDCA 的**核心灵魂**（战略层、AI 协作、循环机制）
- 最小改动，最大复用

---

## 整体架构设计

```
┌─────────────────────────────────────────────────┐
│              人机协作界面层                        │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐      │
│  │ Obsidian │  │  Cursor  │  │ Terminal │      │
│  │  (查看)   │  │  (编辑)  │  │  (触发)  │      │
│  └──────────┘  └──────────┘  └──────────┘      │
└─────────────────────────────────────────────────┘
                      ↕
┌─────────────────────────────────────────────────┐
│              Claude AI Agent 层                  │
│  ┌───────────────────────────────────────────┐  │
│  │  Claude Code + Projects (长上下文能力)     │  │
│  │  ├─ Strategy Coach Project                │  │
│  │  ├─ Project Manager Project               │  │
│  │  └─ Skill Analyzer Project                │  │
│  └───────────────────────────────────────────┘  │
│                                                  │
│  推理能力：                                       │
│  • 读取多文件理解上下文                           │
│  • 识别模式和趋势                                │
│  • 提出质疑和建议                                │
│  • 生成结构化输出                                │
└─────────────────────────────────────────────────┘
                      ↕
┌─────────────────────────────────────────────────┐
│           本地文件系统（数据层）                   │
│                                                  │
│      Obsidian Vault（Markdown + Frontmatter）     │
│                                                  │
│  Ideaverse 框架 + PDCA 增强：                     │
│  ├─ + (Inbox)         快速捕获（Ideaverse）       │
│  ├─ Atlas/            知识管理（Ideaverse）       │
│  ├─ Calendar/         时间维度（Ideaverse）       │
│  ├─ Efforts/          项目和作品（Ideaverse）     │
│  ├─ Strategy/         战略层（PDCA 新增）         │
│  └─ x/                系统资源（Ideaverse）       │
│      └─ x/Prompts/    AI 指令库（融合扩展）       │
│                                                  │
│  插件生态：Dataview + Templater + Periodic Notes │
│           + QuickAdd + Excalidraw + Calendar    │
└─────────────────────────────────────────────────┘
```

### 关键设计决策

**为什么基于 Ideaverse 改造而非从零搭建？**

1. **开箱即用**：30+ 插件已调好，省去配置时间
2. **MOC 体系成熟**：Atlas/Maps 提供强大的知识关联能力
3. **模板丰富**：x/Templates 中有完整的模板库
4. **学习资源**：Ideaverse Pro 2.5 有作者示例可参考

**为什么必须添加 Strategy 层？**

Ideaverse 缺少显式的战略层设计，这是 PDCA 循环的核心：
- Ideaverse 的 Efforts/Areas 是持续关注领域，但没有目标对齐机制
- 没有北极星、年度计划、季度规划的位置
- 没有战略复盘的工作流

**为什么需要扩展 Prompts 目录？**

Ideaverse 已有 `x/x/Prompts/` 目录，但缺少系统化的 AI 协作设计：
- 现有 Prompts 偏向创意思考（如 Finding Blindspots、Imaginary Advisors）
- 需要添加 PDCA 工作流专用的三个 Claude 身份提示词
- 需要定义上下文配置，让 Claude 自动读取相关文件
- 这是人机协作的核心

**Claude Projects的三个身份**
1. **Strategy Coach**：读取战略+所有历史，做方向质疑
2. **Project Manager**：读取项目+每日记录，做进度追踪
3. **Skill Analyzer**：读取能力库+实战案例，做知识提炼

---

## 文件结构设计（融合后）

```
PersonalOS/                          # 基于 Ideaverse Zero 2.5 改造
│
├── 📂 + (Inbox)/                    # [Ideaverse] 快速捕获
│   └── 新想法暂存，定期归档到其他目录
│
├── 📂 Atlas/                        # [Ideaverse] 知识管理
│   │
│   ├── Dots/                        # 原子笔记
│   │   ├── People/                  # 人物笔记
│   │   ├── Things/                  # 事物概念
│   │   ├── Quotes/                  # 引言金句
│   │   ├── Statements/              # 观点主张
│   │   └── Questions/               # 问题探索
│   │
│   ├── Maps/                        # MOC 索引页
│   │   ├── Home.md                  # 导航中心
│   │   └── 按主题的 MOC...
│   │
│   └── Sources/                     # 信息来源
│       ├── Books/                   # 书籍笔记
│       ├── Articles/                # 文章摘录
│       ├── Courses/                 # 课程笔记
│       └── Clippings/               # 网页剪藏
│
├── 📂 Calendar/                     # [Ideaverse] 时间维度
│   │
│   ├── Days/                        # 每日笔记
│   │   └── 2026-01-30.md
│   │       ├── frontmatter: date, week, energy-level
│   │       ├── 今日对齐（关联项目/战略）
│   │       ├── 工作日志（做了什么）
│   │       ├── 学习记录（学到什么）
│   │       ├── 思考碎片（想到什么）
│   │       └── Claude 分析区（晚上自动生成）
│   │
│   ├── Records/                     # 事件记录
│   │   ├── Meetings/                # 会议记录
│   │   ├── Events/                  # 重要事件
│   │   └── Ideas/                   # 灵感记录
│   │
│   └── Reviews/                     # 周期复盘
│       ├── Weekly/                  # 周复盘
│       │   └── 2026-W04-review.md
│       │       |—— frontmatter:week, month
|       |       |—— 本周数据总览
|       |       |—— 三层系统更新
|       |       └── Claude 周报
|       |       
│       └── Monthly/                 # 月复盘（链接到 Strategy/reviews/）
│
├── 📂 Efforts/                      # [Ideaverse] 项目和作品
│   │
│   ├── Areas/                       # 持续关注领域 (AOE)
│   │   ├── Health/
│   │   ├── Career/
│   │   └── Relationships/
│   │
│   ├── Projects/                    # 项目（三状态）
│   │   ├── Active/                  # 进行中的项目
│   │   │   └── project-alpha.md
│   │   │       ├── frontmatter: status, start, deadline, strategy-link
│   │   │       ├── 项目目标（SMART）
│   │   │       ├── 关键任务列表
│   │   │       ├── 进展时间线（日期+更新）
│   │   │       ├── 阻塞点记录
│   │   │       └── Claude 分析区（自动更新）
│   │   │
│   │   ├── Simmering/               # 酝酿中（Ideaverse 特色）的项目
│   │   │   └── 暂时搁置但仍在思考的项目
│   │   │
│   │   └── Sleeping/                # 休眠中的项目
│   │       └── 已完成或无限期暂停的项目
│   │
│   └── Works/                       # 作品输出
│       ├── Articles/                # 文章
│       ├── Videos/                  # 视频
│       └── Newsletters/             # 通讯
│
├── 📂 Strategy/                     # [PDCA 新增] 战略层：1-3个月一次迭代
│   │
│   ├── north-star.md                # 北极星指标（长期不变）
│   │   ├── 我是谁？想成为什么样的人？
│   │   └── 3-5年后的理想状态
│   │
│   ├── annual-plan.md               # 年度计划（每年更新）
│   │   ├── 年度目标（3-5个）
│   │   └── 关键成果指标
│   │
│   ├── quarterly/                   # 季度规划
│   │   ├── 2026-Q1.md
│   │   │   ├── frontmatter: status, start, end, parent
│   │   │   ├── 本季核心目标（1-3个）
│   │   │   ├── 对齐到年度计划
│   │   │   └── 月度检查点
│   │   └── 2026-Q2.md
│   │
│   └── reviews/                     # 战略复盘
│       ├── 2026-01-review.md        # 月度复盘
│       │   ├── Claude 生成的战略质疑
│       │   ├── 数据支撑（自动聚合）
│       │   └── 调整决策
│       └── review-template.md
│
├── 📂 x/                            # [Ideaverse] 系统资源
│   │
│   ├── Meta/                        # [PDCA 新增] 系统元数据
│   │   ├── system-changelog.md      # 系统迭代日志
│   │   │   └── 记录每次调整系统的原因和效果
│   │   │
│   │   ├── ai-conversations/        # 重要 AI 对话存档
│   │   │   ├── 2026-01-strategy-dialogue.md
│   │   │   └── 2026-01-system-design.md
│   │   │
│   │   └── metrics/                 # 效能数据
│   │       ├── monthly-dashboard.md
│   │       └── growth-tracking.md
│   │
│   ├── Packs/                       # 教程包（Ideaverse 原有）
│   │
│   ├── Templates/                   # 模板库
│   │   ├── Daily Note.md            # 每日笔记模板（需调整）
│   │   ├── Weekly Review.md         # 周复盘模板（需调整）
│   │   ├── Project.md               # 项目模板（需调整）
│   │   └── ...其他 Ideaverse 模板
│   │
│   ├── Visuals/                     # 图片资源
│   │   ├── Images/
│   │   └── Excalidraw/
│   │
│   └── x/                           # [融合点] 系统核心
│       │
│       └── Prompts/                 # AI 指令中心
│           │
│           ├── [Ideaverse 原有 10 个 Prompts]
│           │   ├── Prompt - Finding Blindspots.md
│           │   ├── Prompt - Imaginary Advisors.md
│           │   ├── Prompt - Thought Enriching Machine.md
│           │   └── ...
│           │
│           ├── [PDCA 新增 3 个 Prompts]
│           │   ├── Prompt - Strategy Coach.md      # 战略顾问提示词
│           │   │
│           │   ├── Prompt - Project Manager.md     # 项目经理提示词
│           │   └── Prompt - Skill Analyzer.md      # 能力分析师提示词
│           │
│           └── contexts/            # [PDCA 新增] 上下文配置
│               ├── strategy-context.md   # 战略对话需要读取的文件清单
│               ├── project-context.md    # 项目对话需要读取的文件清单
│               └── skill-context.md      # 能力对话需要读取的文件清单
│
├── 📄 Home Base.md                  # [Ideaverse] 仪表盘（Dataview 驱动）
│
└── 📄 README.md                     # 系统使用手册
    ├── 快速开始
    ├── 三层系统说明
    ├── Claude 使用指南
    └── 常见问题
```

### 文件结构设计原则

1. **层级对应时间尺度**
   - Strategy: 季度/月度（战略校准）
   - Efforts/Projects: 周度（项目推进）
   - Atlas/Dots: 日度积累（知识沉淀）
   - Calendar/Days: 实时记录

2. **Ideaverse 结构复用**
   - 保留 ACE 框架（Atlas-Calendar-Efforts）
   - 保留 Inbox（+）的快速捕获机制
   - 保留 Projects 三状态（Active/Simmering/Sleeping）
   - 保留 MOC 索引系统

3. **PDCA 核心注入**
   - 新增 Strategy/：战略层是 PDCA 的灵魂
   - 扩展 x/x/Prompts/：添加 PDCA 工作流的 AI 协作
   - 调整模板：融入 PDCA 循环元素

4. **Frontmatter 作为元数据层**
   - 用于建立文件关联
   - 方便 Claude 理解结构
   - 支持 Dataview 查询

5. **文件命名约定**
   - 日期格式：`YYYY-MM-DD`
   - 周复盘：`YYYY-WXX.md`
   - 项目：`project-名称.md`

---

## Ideaverse 到 PDCA 的结构映射

理解现有 Ideaverse 结构如何对应 PDCA 三层：

| Ideaverse 原有 | 对应 PDCA 功能 | 融合后的用法 |
|---------------|---------------|-------------|
| `+` (Inbox) | 快速捕获 | 新想法暂存 → 定期归档 |
| `Efforts/Projects/Active` | 项目层 | 进行中的项目，链接到战略 |
| `Efforts/Projects/Simmering` | 项目层 | 酝酿中的项目 |
| `Efforts/Areas/` | 能力层的一部分 | 持续关注的领域 |
| `Calendar/Days/` | 每日记录 | 原子化输入 |
| `Calendar/Reviews/` | 周期复盘 | 周复盘 + 月复盘 |
| `Atlas/Dots/` | 能力层 | 原子知识点沉淀 |
| `Atlas/Maps/` | 知识关联 | MOC 索引页 |
| `Atlas/Sources/` | 信息来源 | 书籍、文章等输入 |
| `x/Templates/` | 模板库 | 需根据 PDCA 调整 |
| `x/x/Prompts/` | AI 协作基础 | Ideaverse 原有创意思考 Prompts |

**新增/扩展结构**：
| 新增/扩展目录 | PDCA 功能 | 说明 |
|---------|----------|------|
| `Strategy/` | 战略层 | 北极星 + 年度 + 季度 + 复盘） |
| `x/x/Prompts/` | AI 协作 | 扩展 Ideaverse 原有 Prompts，添加 PDCA 三个身份 + 上下文配置 |

---

## Ideaverse 与 PDCA Prompts 的协同

### Ideaverse 原有 Prompts 分析

| Ideaverse Prompt | 功能定位 | 与 PDCA 的关系 |
|-----------------|---------|---------------|
| **Finding Blindspots** | 识别论证盲区（修辞学） | 可与 Strategy Coach 结合，用于战略质疑 |
| **Buttressing Blindspots** | 强化论证薄弱点 | 辅助战略决策的论证 |
| **Imaginary Advisors** | 多视角咨询（名人视角） | 可在战略对话中引入多元视角 |
| **Thought Enriching Machine** | 思想提炼和扩展 | 与 Skill Analyzer 功能相近，偏创意 |
| **Thought Unpacking Machine** | 思想拆解 | 辅助深度思考 |
| **Progymnasmata 系列** | 古典修辞学训练 | 写作和表达能力训练 |

### PDCA 新增 Prompts 定位

| PDCA Prompt | 功能定位 | 与 Ideaverse 的差异 |
|------------|---------|-------------------|
| **Strategy Coach** | 系统化战略质疑 | 更聚焦目标对齐、数据驱动，而非纯思辨 |
| **Project Manager** | 项目进度和风险管理 | 全新功能，Ideaverse 无对应 |
| **Skill Analyzer** | 知识沉淀和体系化 | 与 Thought Enriching 相似，但更系统化，直接对接 Atlas 结构 |

### 融合使用策略

**战略层对话**：
```
第1步：用 Finding Blindspots 预热
       → 识别当前战略的论证漏洞

第2步：用 Strategy Coach 深入
       → 基于数据做系统化质疑

第3步：用 Imaginary Advisors 扩展
       → 引入多元视角（如果需要）
```

**能力层沉淀**：
```
日常：用 Skill Analyzer
      → 系统化沉淀到 Atlas/Dots

创意：用 Thought Enriching Machine
      → 发散思考，探索新角度

结合：两者互补，一个系统化，一个创意化
```

**Prompt 文件格式规范**：

遵循 Ideaverse 的格式，PDCA 新增的三个 Prompt 应该这样写：

```markdown
---
up:
  - "[[Prompts MOC (My)]]"
  - "[[Prompts]]"
related:
  - "[[Prompt - Finding Blindspots]]"  # 可关联到相关 Prompt
  - "[[Strategy/north-star]]"          # 可关联到战略文件
created: 2026-01-30
tags:
  - pdca
  - strategy  # 或 project / skill
---

# Prompt - Strategy Coach

## 角色定义
你是一位苏格拉底式的战略顾问...

## 思考框架
...

## 输出格式
...

## 使用说明
...
```

---

## Ideaverse 到 PDCA 的结构映射（续）

## Claude AI Agent 工作流设计

### 核心机制：三个 Projects + 上下文注入

#### Project 1: Strategy Coach（战略教练）

**角色定位**：苏格拉底式提问者，战略盲区识别器

**工作机制**：
```
输入层：
├─ 固定上下文（每次对话自动读取）
│  ├─ Strategy/north-star.md（北极星指标）
│  ├─ Strategy/annual-plan.md（年度计划）
│  └─ 当前季度目标
│
├─ 动态上下文（根据时间触发）
│  ├─ 上月所有项目文件（Efforts/Projects/Active/）
│  ├─ 上月所有每日记录（Calendar/Days/）
│  └─ 上月周复盘（Calendar/Reviews/Weekly/）
│
└─ 系统提示词（x/x/Prompts/Prompt - Strategy Coach.md）
   ├─ 你的角色：战略顾问，不是执行助手
   ├─ 你的任务：质疑而非肯定，发现盲区
   ├─ 思考框架：
   │  • 这些行动真的在接近目标吗？（对齐度检查）
   │  • 投入产出比最高的是哪3件事？（杠杆点识别）
   │  • 哪些是伪工作？（噪音过滤）
   │  • 最大的机会成本是什么？（隐藏代价）
   │  • 如果只能做1件事，应该是什么？（本质提炼）
   └─ 输出格式：
      • 数据总结（客观事实）
      • 关键质疑（5-8个问题）
      • 盲区识别（你可能没看到的）
      • 建议行动（具体可执行）

对话方式：
├─ 触发时机：每月1-3号
├─ 对话长度：30-60分钟深度对话
└─ 输出物：Strategy/reviews/YYYY-MM-review.md
```

**关键设计**：
- 不是简单的数据汇总，而是**深度推理**
- 利用 Claude 的长上下文，一次性读取整月数据
- 通过系统提示词固定思考框架，确保质疑深度
- 对话式而非一次性生成，允许多轮追问

#### Project 2: Project Manager（项目经理）

**角色定位**：进度追踪器，风险预警器，效能优化器

**工作机制**：
```
输入层：
├─ 固定上下文
│  ├─ 所有 Active 项目文件（Efforts/Projects/Active/）
│  └─ 项目模板（x/Templates/Project.md）
│
├─ 动态上下文
│  ├─ 本周所有每日记录（Calendar/Days/）
│  └─ 上周周报（Calendar/Reviews/Weekly/）
│
└─ 系统提示词（x/x/Prompts/Prompt - Project Manager.md）
   ├─ 你的角色：数据驱动的项目经理
   ├─ 你的任务：
   │  • 进度追踪（完成了什么？离目标多远？）
   │  • 风险识别（哪些在拖延？为什么？）
   │  • 依赖分析（项目间是否冲突？）
   │  • 效能分析（时间分配合理吗？）
   └─ 输出格式：
      • 项目健康度仪表盘
      • 风险清单（优先级排序）
      • 下周建议 focus
      • 需要调整的地方

对话方式：
├─ 触发时机：每周五下午
├─ 对话方式：半自动生成周报 + 互动答疑
└─ 输出物：Calendar/Reviews/Weekly/YYYY-WXX.md
```

**关键设计**：
- 横向对比多个项目，识别资源冲突
- 纵向追踪单个项目，识别停滞信号
- 结合每日记录的"实际行动"vs"计划任务"，找到偏差
- 利用 Ideaverse 的三状态项目管理（Active/Simmering/Sleeping）

#### Project 3: Skill Analyzer（能力分析师）

**角色定位**：知识蒸馏器，能力复利放大器

**工作机制**：
```
输入层：
├─ 固定上下文
│  ├─ Atlas/Dots/ 全部内容
│  ├─ Atlas/Maps/ 相关 MOC
│  └─ Efforts/Areas/ 关注领域
│
├─ 动态上下文
│  ├─ 今日的"学习记录"和"思考碎片"
│  └─ 最近的项目经验（从 Efforts/Projects/Sleeping 读取）
│
└─ 系统提示词（x/x/Prompts/Prompt - Skill Analyzer.md）
   ├─ 你的角色：知识管理专家
   ├─ 你的任务：
   │  • 从零散经验中提炼可复用知识
   │  • 识别模式：这个和之前哪个经验相关？
   │  • 升维思考：这背后的原理是什么？
   │  • 建议沉淀：应该加到哪个 Dots？还是创建新的？
   │  • 关联 MOC：这属于哪个知识地图？
   └─ 输出格式：
      • 今日知识点提炼（1-3个）
      • 关联分析（和现有哪些 Dots 相关）
      • 沉淀建议（具体到 Atlas/Dots/哪个子目录）
      • MOC 更新建议

对话方式：
├─ 触发时机：每晚复盘时
├─ 对话方式：给 Claude 看今日记录，让它提炼
└─ 输出物：追加到今日笔记 + 更新 Atlas/Dots/
```

**与 Ideaverse 的融合点**：
- 利用 Atlas/Dots 的分类体系（People/Things/Quotes/Statements/Questions）
- 利用 MOC 建立知识关联
- 沉淀到 Atlas 而非独立的 Skills 目录

**关键设计**：
- 每日小积累，避免经验流失
- 自动关联历史知识，形成网络
- 推荐沉淀位置，降低整理成本

---

## 完整工作流演示

### 时间轴视角：一个月的系统运转

#### Day 1（月初）- 战略校准日

**早上（30分钟）：在 Claude Strategy Coach Project 中对话**

```
人：开始本月战略复盘

Claude（自动读取上月所有数据后）：
├─ 数据总结：
│  • 上月完成8个项目任务，完成率72%
│  • 时间分配：工作项目60%，能力建设25%，杂事15%
│  • Atlas 新增知识点：写作+3，思维模型+2
│
├─ 关键质疑：
│  1. 你的季度目标是"建立个人品牌"，但上月60%时间
│     在做外包项目，这两者如何对齐？
│  2. Atlas/Dots 中写作相关的笔记增加了，但 Efforts/Works
│     的文章发布频率反而下降，为什么？
│  3. Efforts/Projects/Simmering 里有3个项目已经"酝酿"
│     超过2周，它们真的会被激活吗？
│  ...（继续5-8个质疑）
│
└─ 盲区识别：
   • 你可能陷入"准备的陷阱"：花太多时间整理 Atlas
     而非实际创作输出
   • Inbox 中积压了12条待处理，信息归档流程需要优化

人（多轮对话，深入思考）：
第1轮 → 为什么会这样？（挖根因）
第2轮 → 如果只能砍掉2个项目，应该砍哪些？（做取舍）
第3轮 → 本月应该如何调整？（定行动）

Claude（生成）：
├─ 调整建议：
│  • 砍掉项目B（投入产出比低）
│  • 外包项目控制在40%时间内
│  • 每周至少发布1篇文章（强制输出）
│
└─ 本月北极星：
   "用写作建立个人品牌"
   关键动作：发布4篇高质量文章

最后：
└─ Claude 自动生成：Strategy/reviews/2026-01-review.md
└─ 人手动更新：Strategy/quarterly/2026-Q1.md（调整目标）
```

**这个环节的价值**：
- 不是简单的"完成了多少"，而是"为什么这样做"
- 用数据逼自己正视战略偏离
- Claude作为外部视角，避免自我欺骗

---

#### Day 2-6（工作周）- 日常执行

**每天早上（5分钟）：在 Obsidian 中打开今日笔记**

```
今日笔记自动生成（Periodic Notes + Templater）：
├─ 今日对齐：
│  • 本月北极星：用写作建立个人品牌
│  • 本周重点：完成文章《XXX》
│  • 今日 focus：完成初稿3000字
│
├─ 任务列表：
│  [ ] 任务1（来自 Active 项目）
│  [ ] 任务2
│
└─ 空白区域等待填充...
```

**工作中（在 Cursor 中编辑文件）**：
```
├─ 打开项目文件：Efforts/Projects/Active/article-xxx.md
├─ 边写边记录进展
└─ 遇到问题时，切到 Claude Project Manager 对话：

   人：这篇文章的案例部分卡住了，不知道写什么

   Claude（读取文章草稿 + Atlas/Dots）：
   ├─ 我看到你在 Atlas/Dots/Things/ 中有
   │  3个类似场景的案例笔记
   ├─ 建议查看 Atlas/Maps/Writing MOC
   └─ 这里给你一个结构...

   → 问题解决，继续写作
```

**晚上（10分钟复盘）：在今日笔记中填写"学习记录"和"思考"**

```
├─ 今日完成：
│  • 完成文章初稿2800字（略低于目标）
│  • 找到了一个新的论证框架
│
├─ 今日学习：
│  • 学到"场景化案例"比"道理讲解"更有说服力
│
└─ 明日计划：
   • 继续打磨案例部分
```

**然后：切到 Claude Skill Analyzer Project**

```
人：分析今日记录（附上今日笔记内容）

Claude：
├─ 知识点提炼：
│  1. "场景化案例"技巧
│     → 建议创建：Atlas/Dots/Statements/场景化案例原则.md
│     → 关联到：Atlas/Maps/Writing MOC
│     → 与你之前的 "具体性原则" 是同一类
│
└─ MOC 更新建议：
   • 在 Writing MOC 中新增 "说服力技巧" 章节

最后：
└─ 根据 Claude 建议，在 Atlas 中创建新笔记
```

**这个环节的价值**：
- 每天自动沉淀，知识不流失
- Claude帮你建立新旧知识的关联
- 低成本（10分钟），高复利（持续积累）

---

#### Day 7（周五）- 周复盘日

**下午5点（15分钟）：在 Claude Project Manager Project 中**

```
人：生成本周周报

Claude（读取本周每日记录 + 项目文件）：
├─ 本周数据：
│  ✅ 完成任务：12/15（80%）
│  📊 项目进展：
│     • article-xxx: 90%完成，周日可发布
│     • project-alpha: 35%→45%
│  📚 Atlas 新增：3个 Dots
│  ⏰ 时间分配：
│     • 写作：40%
│     • 项目开发：35%
│     • 学习：15%
│     • 杂事：10%
│
├─ 项目状态建议：
│  • project-beta 已停滞2周，建议移到 Simmering
│  • side-idea 可以从 Simmering 激活到 Active
│
├─ 风险识别：
│  ⚠️ Inbox 积压增加到15条，需要归档
│  ⚠️ 周三周四能量水平标记为"低"，原因？
│
└─ 下周建议：
   1. 发布 article-xxx 后，立即启动下一篇选题
   2. 周末花30分钟清理 Inbox
   3. 周三周四尝试调整作息，避免能量低谷

最后：
└─ Claude 生成：Calendar/Reviews/Weekly/2026-W04.md
└─ 人根据建议，调整项目状态
```

**这个环节的价值**：
- 自动聚合数据，省去手动翻阅
- 识别你自己可能忽略的模式（如能量低谷）
- 周报不只是"记录"，更是"诊断"

---

#### Day 8-30（重复）

```
├─ Day 8-14：重复日常执行流程
├─ Day 15：周复盘
├─ Day 16-21：日常执行
├─ Day 22：周复盘
├─ Day 23-28：日常执行
└─ Day 29：周复盘 + 为下月战略复盘准备数据
```

---

### 信息流视角：数据如何在系统中流动

#### 流程图总览

```
Inbox (+)
    ↓ 归档
Atlas (知识沉淀) ←──────────────────┐
    ↓ 关联                         │
Calendar/Days (每日记录) ─────────→ Claude 分析
    ↓ 周聚合                        │
Calendar/Reviews (周复盘) ←─────────┘
    ↓ 月聚合
Strategy/reviews (月复盘)
    ↓ 校准
Strategy/quarterly (季度目标)
    ↓ 分解
Efforts/Projects (项目执行)
    ↓ 输出
Efforts/Works (作品发布)

三层循环：
├─ 快回路（每日）：Daily → Claude Skill Analyzer → Atlas
├─ 中回路（每周）：Weekly Review → Claude PM → Projects 调整
└─ 慢回路（每月）：Monthly Review → Claude Coach → Strategy 校准
```

#### 实例：一个知识点的30天演化之旅

```
底层（Calendar/Days）→ 中层（Efforts/Projects）→ 顶层（Strategy）
        ↓                      ↓                       ↓
      原子化                 结构化                   战略化

实例追踪：
────────────────────────────────────────────────────────

Day 1: 在每日笔记中记录
├─ 位置：Calendar/Days/2026-01-15.md
├─ 内容：
│  ## 今日学习
│  • 学到"场景化案例"比"道理讲解"更有说服力
│  • 在写作时用具体故事替代抽象原则，读者理解更快
└─ 标签：#writing #learning

Day 1 晚: Claude Skill Analyzer 分析
├─ 提炼：这是"具体性原则"的应用
├─ 建议沉淀到：Atlas/Dots/Statements/场景化案例原则.md
├─ 关联到：Atlas/Maps/Writing Skill MOC
└─ 结果：
   • 创建 Atlas/Dots/Statements/场景化案例原则.md
   • 更新 Atlas/Maps/Writing Skill MOC（新增链接）
   • 在笔记中添加 frontmatter: used-count: 1

Day 7: 周报时，Claude Project Manager 发现
├─ 读取：Calendar/Reviews/Weekly/2026-W03.md
├─ 分析：
│  • 本周 Atlas/Dots 新增写作相关笔记 +5
│  • Efforts/Projects/Active/article-personal-brand.md 进度停滞
│  • Efforts/Works/Articles/ 本周无新发布
├─ 质疑：
│  • 学习了很多写作技巧，但实际输出在减少
│  • 学习和应用是否脱节？
└─ 建议：
   • 下周强制输出：至少完成 1 篇文章初稿
   • 将新学的"场景化案例"技巧应用到文章中

Day 14: 实际应用
├─ 位置：Efforts/Projects/Active/article-personal-brand.md
├─ 进展更新：
│  ## 2026-01-22 更新
│  • 应用了 [[场景化案例原则]]，用真实故事替代理论讲解
│  • 初稿完成度 80%
└─ 结果：
   • Atlas/Dots/Statements/场景化案例原则.md 的 used-count: 1 → 3
   • 技能从"学到"变成"用到"

Day 30: 月度战略复盘时，Claude Strategy Coach 指出
├─ 读取：Strategy/reviews/2026-01-review.md
├─ 数据总结：
│  • 本月 Atlas/Dots 扩充 +20 个知识点
│  • 但 Efforts/Works/Articles/ 仅发布 1 篇
│  • 季度目标："建立个人品牌" = 至少发布 6 篇文章
│  • 当前进度：1/6（仅 16.7%）
├─ 关键质疑：
│  1. Atlas 知识库虽然扩充了，但对"建立个人品牌"
│     的实际贡献有限——知识在库里不等于影响力
│  2. "场景化案例原则"已经学到并应用，为什么不
│     批量复用到其他文章？
│  3. 你在 Efforts/Projects/Simmering 有 3 个文章选题
│     在"酝酿"，它们真的需要酝酿吗？还是在拖延？
├─ 盲区识别：
│  • 你陷入了"准备的陷阱"：
│    - 花太多时间整理 Atlas（输入）
│    - 花太少时间创作 Works（输出）
│  • 本质问题：用"学习"逃避"创作"的不确定性
└─ 战略调整：
   • 下月重心：从"学习技巧"转向"发布作品"
   • 强制输出：每周至少发布 1 篇文章
   • Simmering 项目限时激活：3 天内必须决定做或放弃
   • Atlas 新增知识点控制在每周 2-3 个（而非无限扩张）

最终影响：
└─ 更新 Strategy/quarterly/2026-Q1.md
   ├─ 原目标：建立个人品牌（模糊）
   └─ 调整后：
      • 2月：发布 4 篇文章（每周 1 篇）
      • 3月：发布 4 篇文章（每周 1 篇）
      • 核心原则：输出优先于输入

────────────────────────────────────────────────────────

这样，一个小的每日学习点"场景化案例原则"，通过三层分析：

├─ 被提炼（能力层 - Atlas）
│  • Day 1: 从每日记录提炼到 Atlas/Dots
│  • 建立结构化知识
│
├─ 被应用（项目层 - Efforts）
│  • Day 7-14: 周复盘质疑 → 强制应用到项目
│  • 从"知道"到"做到"
│
└─ 被战略化（战略层 - Strategy）
   • Day 30: 月复盘发现更深层问题
   • 不是技巧不够，而是输出太少
   • 调整战略：输出优先于输入

最终影响长期方向：从"知识收集者"转向"价值创造者"
```

---

## 系统控制机制

### 1. 反馈回路设计

```
快回路（每日）：
├─ 输入：今日记录（Calendar/Days/）
├─ 处理：Claude Skill Analyzer 提炼
├─ 输出：知识沉淀到 Atlas/Dots/
└─ 周期：24小时

中回路（每周）：
├─ 输入：本周每日记录 + 项目进展
├─ 处理：Claude Project Manager 分析
├─ 输出：周报 + 项目状态调整
└─ 周期：7天

慢回路（每月）：
├─ 输入：本月所有数据 + 季度目标
├─ 处理：Claude Strategy Coach 质疑
├─ 输出：战略调整 + 目标修正
└─ 周期：30天

三个回路相互嵌套，形成稳定的自我校正系统。
```

### 2. 触发机制

**时间触发**（Obsidian Periodic Notes + 系统提醒）：
- 每天21:00：提醒做每日复盘
- 每周五17:00：生成周报
- 每月1-3号：战略对话窗口

**事件触发**（手动）：
- 项目完成时：立即做项目复盘，移到 Sleeping
- 遇到重大决策：咨询 Strategy Coach
- 学到重要技能：立即找 Skill Analyzer 沉淀

**阈值触发**（自动预警，通过 Dataview）：
- 某项目连续2周无更新：风险提示
- Inbox 积压超过10条：归档提醒
- 能量水平连续3天标记"低"：状态检查

### 3. 质量控制

**输入质量**：
- 每日记录最低标准：至少3句话
- 项目更新最低频率：每周至少1次
- 所有文件必须有 frontmatter

**处理质量**：
- Claude 的系统提示词定期 review
- 对比 AI 输出和实际执行的偏差
- 记录在 x/Meta/system-changelog.md 中迭代

**输出质量**：
- 周报必须包含"数据+分析+建议"
- 月度复盘必须有"质疑问题"，不只是总结
- Atlas 沉淀必须可复用，不是流水账

---

## 关键设计细节

### 1. Claude 上下文管理策略

**为什么重要**：让Claude理解文件关系

**问题**：Claude 有 200K 上下文限制，如何高效利用？

**策略**：
```
分层注入：
├─ 核心上下文（每次对话必读，~20K tokens）
│  • 系统提示词（x/x/Prompts/Prompt - XXX.md）
│  • 当前目标文件（Strategy/）
│  • 相关模板
│
├─ 动态上下文（根据任务读取，~100K tokens）
│  • 最近N天的每日记录
│  • 相关项目文件
│  • 关联的 Atlas 内容
│
└─ 历史上下文（Claude Projects 自动管理）
   • 之前的对话历史
   • 形成连续记忆

优先级：
├─ 战略对话：优先读取 Strategy/ + Efforts/Projects/，少读 Daily 细节
├─ 项目对话：优先读取项目层 + 本周 Daily，少读历史
└─ 能力对话：优先读取 Atlas + 今日 Daily，少读项目
```

### 2. Frontmatter 元数据设计

**标准格式**：

```yaml
# 战略文件（Strategy/）：
---
type: strategy
level: quarterly / monthly
period: 2026-Q1
status: active / completed
parent: "[[annual-plan]]"
updated: 2026-01-29
---

# 项目文件（Efforts/Projects/）：
---
type: project
status: active / simmering / sleeping
start: 2026-01-15
deadline: 2026-02-28
strategy-link: "[[2026-Q1#目标2]]"
progress: 45%
updated: 2026-01-29
---

# 每日记录（Calendar/Days/）：
---
type: daily
date: 2026-01-29
week: 04
energy: high / medium / low
focus-project: "[[project-alpha]]"
---

# 知识笔记（Atlas/Dots/）：
---
type: dot
category: statement / thing / quote / person / question
tags:
  - writing
  - persuasion
source: "[[Some Book]]"
created: 2026-01-20
used-count: 5
---

# 持续关注领域（Efforts/Areas/）：
---
type: area
name: Writing
tags:
  - skill
  - writing
status: active / archived
created: 2026-01-15
last-review: 2026-01-29
---

# 标准操作流程（Efforts/Areas/Writing/SOP-xxx.md）：
---
type: sop
area: "[[Writing]]"
skill-level: beginner / intermediate / advanced
tags:
  - writing
  - process
steps: 6
created: 2026-01-20
updated: 2026-01-29
used-count: 12
---

# AI 提示词（x/x/Prompts/）：
---
type: prompt
up:
  - "[[Prompts MOC (My)]]"
  - "[[Prompts]]"
related:
  - "[[Prompt - Finding Blindspots]]"
tags:
  - pdca
  - strategy
role: Strategy Coach / Project Manager / Skill Analyzer
created: 2026-01-30
updated: 2026-01-30
---
```

**使用场景**：
- Claude 可以通过 frontmatter 快速理解文件类型和关系
- Dataview 可以自动生成仪表盘和统计
- 脚本可以自动筛选和处理相关文件

**关键字段说明**：

| 字段 | 作用 | 示例 |
|-----|------|------|
| `type` | 文件类型标识 | strategy, project, daily, dot, area, sop, prompt |
| `category` | 细分类别 | statement, thing, quote, person, question |
| `status` | 状态标识 | active, simmering, sleeping, completed, archived |
| `tags` | 标签（支持 Dataview 查询） | #writing, #pdca, #strategy |
| `used-count` | 使用次数（追踪知识复用） | 每次使用后 +1 |
| `strategy-link` | 对齐到战略目标 | `"[[2026-Q1#目标2]]"` |
| `related` | 关联笔记 | `["[[Note A]]", "[[Note B]]"]` |
| `skill-level` | 掌握程度 | beginner, intermediate, advanced |

**Dataview 查询示例**：

在 `Atlas/Maps/Writing Skill MOC.md` 中自动生成能力仪表盘：

````markdown
## 📊 掌握程度追踪

```dataview
TABLE
  used-count as "使用次数",
  skill-level as "掌握程度",
  updated as "最后更新"
FROM "Atlas/Dots" OR "Efforts/Areas/Writing"
WHERE contains(tags, "writing")
SORT used-count DESC
```

## 🔥 高频使用的知识点

```dataview
TABLE
  category as "类型",
  used-count as "使用次数"
FROM "Atlas/Dots"
WHERE contains(tags, "writing") AND used-count > 5
SORT used-count DESC
LIMIT 10
```

## 📋 待完善的 SOP

```dataview
LIST
FROM "Efforts/Areas"
WHERE type = "sop" AND skill-level = "beginner"
SORT created DESC
```
````

### 3. 模板驱动的一致性

**核心理念**：所有重复性工作都有模板，确保格式一致、降低认知负担。

#### 为什么需要模板驱动？

1. **对 Claude 友好**
   - Claude 看到一致的结构，理解更准确
   - 可以基于模板自动提取信息
   - 减少 prompt 中的格式说明

2. **对你友好**
   - 不用每次从零思考"今天该记录什么"
   - 养成一致的记录习惯，质量更稳定
   - 降低开始记录的心理门槛

3. **对自动化友好**
   - 方便脚本批量处理
   - Dataview 查询更可靠
   - 未来升级系统时不需要大量重构

#### 完整模板清单

**继承自 Ideaverse（已有，需调整）**：

```
x/Templates/
├─ 📝 记录模板（保证输入格式一致）
│  │
│  ├─ Daily Note.md                  # 每日笔记模板
│  │  ├─ Frontmatter（date, week, energy）
│  │  ├─ 今日对齐（本月北极星 + 本周重点）← 新增
│  │  ├─ 工作日志
│  │  ├─ 学习记录
│  │  ├─ 思考碎片
│  │  └─ Claude 分析区                ← 新增
│  │
│  ├─ Weekly Review.md               # 周复盘模板
│  │  ├─ Frontmatter（week, month）
│  │  ├─ 本周数据总览                ← 调整
│  │  ├─ 项目状态总结                ← 新增
│  │  ├─ 三层系统更新
│  │  └─ Claude PM 输出区            ← 新增
│  │
│  ├─ Monthly Review.md              # 月复盘模板（可选）
│  │  └─ 指向 Strategy/reviews/ 的索引
│  │
│  └─ Project.md                     # 项目模板
│     ├─ Frontmatter（strategy-link）← 新增
│     ├─ 项目目标（SMART）
│     ├─ 关键任务列表
│     ├─ 进展时间线
│     ├─ 阻塞点记录
│     └─ Claude 分析区               ← 新增
│
├─ 🎯 战略模板（PDCA 新增）
│  │
│  ├─ North Star.md                  # 北极星模板
│  │  ├─ 我是谁？
│  │  ├─ 想成为什么样的人？
│  │  └─ 3-5年后的理想状态
│  │
│  ├─ Annual Plan.md                 # 年度计划模板
│  │  ├─ Frontmatter（year, status）
│  │  ├─ 年度目标（3-5个）
│  │  └─ 关键成果指标
│  │
│  ├─ Quarterly Plan.md              # 季度计划模板
│  │  ├─ Frontmatter（quarter, parent）
│  │  ├─ 本季核心目标（1-3个）
│  │  ├─ 对齐到年度计划
│  │  └─ 月度检查点
│  │
│  └─ Review.md                      # 战略复盘模板
│     ├─ Frontmatter（period, type）
│     ├─ 数据总结（自动聚合）
│     ├─ 关键质疑（Claude生成）
│     ├─ 盲区识别
│     └─ 调整决策
│
├─ 📚 知识模板（PDCA 新增或调整）
│  │
│  ├─ Dot.md                         # 原子笔记模板
│  │  ├─ Frontmatter（type, category, tags, used-count）← 调整
│  │  ├─ 知识点描述
│  │  ├─ 来源/上下文
│  │  ├─ 相关 MOC                    ← 新增
│  │  └─ 应用案例
│  │
│  ├─ SOP.md                         # 标准操作流程模板
│  │  ├─ Frontmatter（type: sop, area, skill-level, used-count）
│  │  ├─ 适用场景
│  │  ├─ 步骤1-N（详细描述）
│  │  ├─ 检查清单
│  │  └─ 常见问题
│  │
│  └─ Skill MOC.md                   # 技能地图模板
│     ├─ 执行流程（SOPs）
│     ├─ AI 协作（Prompts）
│     ├─ 核心原则（Principles）
│     ├─ 优秀案例（Examples）
│     ├─ 能力树状结构
│     └─ 掌握程度追踪（Dataview）
│
└─ 🤖 AI 协作模板（PDCA 新增）
   │
   ├─ Prompt - Strategy Coach.md    # 战略顾问提示词
   │  ├─ Frontmatter（role: Strategy Coach）
   │  ├─ 角色定义
   │  ├─ 思考框架
   │  ├─ 输出格式
   │  └─ 使用说明
   │
   ├─ Prompt - Project Manager.md   # 项目经理提示词
   │  └─ [同上结构]
   │
   ├─ Prompt - Skill Analyzer.md    # 能力分析师提示词
   │  └─ [同上结构]
   │
   └─ Context Config.md              # 上下文配置模板
      ├─ 固定上下文（必读文件）
      ├─ 动态上下文（条件读取）
      └─ 优先级规则
```

#### 模板的三重作用

**1. 输入模板（保证数据质量）**

```
记录模板：
├─ Daily Note → 确保每日记录包含关键维度
├─ Weekly Review → 确保周报结构完整
├─ Project → 确保项目信息完整
└─ Dot → 确保知识点可复用

效果：
└─ Claude 读取时不会遇到"缺少关键信息"的问题
```

**2. 处理模板（保证 AI 输出质量）**

```
提示词模板：
├─ Strategy Coach → 固定战略质疑的思考框架
├─ Project Manager → 固定周报生成的格式
└─ Skill Analyzer → 固定知识提炼的方法

效果：
└─ 每次 Claude 输出的格式一致，可以直接粘贴使用
```

**3. 输出模板（保证可读性）**

```
输出模板：
├─ 月度复盘模板 → 战略 Review 的标准格式
├─ 周报模板 → Weekly Review 的标准格式
└─ 能力卡片模板 → Dot 笔记的标准格式

效果：
└─ 所有文档风格统一，便于回顾和分享
```

#### 模板驱动的工作流示例

**场景：创建新的每日笔记**

```
不用模板（从零开始）：
1. 创建文件：Calendar/Days/2026-01-31.md
2. 思考：今天该记录什么？怎么组织？
3. 写 frontmatter：需要哪些字段？
4. 写内容结构：想半天
5. 开始记录
   → 时间成本：5-10分钟
   → 每天格式可能不一样

使用模板（Periodic Notes + Template）：
1. 打开 Obsidian（自动创建今日笔记）
2. 模板已自动填充，frontmatter、结构都有
3. 直接填写内容
   → 时间成本：< 1分钟
   → 每天格式完全一致
```

**场景：Claude 生成周报**

```
不用模板（自由发挥）：
你："生成本周周报"
Claude："好的，我总结一下..."
结果：
├─ 每次格式不一样
├─ 可能遗漏关键维度
└─ 需要手动调整格式才能粘贴

使用模板（Prompt 模板）：
你："生成本周周报"
Claude（读取 Prompt - Project Manager.md）：
结果：
├─ 严格按照模板格式输出
├─ 包含所有关键维度（数据、分析、建议）
└─ 可以直接粘贴到 Weekly Review 笔记
```

#### Ideaverse 的模板优势

Ideaverse 已经提供了成熟的模板系统：

**优势1：Templater 插件预配置**
- 支持动态变量（日期、时间、文件名等）
- 支持 JavaScript 脚本
- 支持 prompt（弹窗输入）

**优势2：丰富的模板库**
- x/Templates/ 已有多个现成模板
- 可以直接复用，只需微调

**优势3：QuickAdd 集成**
- 一键创建带模板的笔记
- 快捷键触发

#### 实施建议

**第一阶段（第1个月）：核心模板**
```
优先调整：
✅ Daily Note 模板（每天用）
✅ Weekly Review 模板（每周用）
✅ Project 模板（创建项目时用）
✅ Prompt - Strategy Coach（月度用）

暂时跳过：
⏸ 所有 Dot 子类型模板（太细）
⏸ SOP 模板（等有实际需求再创建）
```

**第二阶段（第2-3个月）：扩展模板**
```
根据实际使用情况，添加：
□ 常用的 Dot 模板
□ SOP 模板
□ 特定场景的提示词模板
```

**第三阶段（第4个月起）：优化模板**
```
基于使用反馈，持续迭代：
□ 调整模板结构
□ 简化冗余字段
□ 添加自动化脚本
```

#### 模板的好处（总结）

| 维度 | 不用模板 | 使用模板 |
|-----|---------|---------|
| **启动时间** | 5-10分钟（从零思考） | < 1分钟（直接填写） |
| **格式一致性** | ❌ 每次不一样 | ✅ 完全一致 |
| **信息完整性** | ⚠️ 可能遗漏关键维度 | ✅ 模板强制包含 |
| **Claude 理解** | ⚠️ 需要额外解释格式 | ✅ 直接理解 |
| **Dataview 查询** | ❌ 难以查询 | ✅ 可靠查询 |
| **心理负担** | 高（要思考怎么写） | 低（填空即可） |
| **长期维护** | 难（格式不统一） | 易（格式统一） |

**核心价值**：模板降低了 80% 的"格式思考成本"，让你专注于"内容本身"。

---

### 4. 模板调整清单

需要调整 Ideaverse 原有模板以融入 PDCA 元素：

| 模板 | 调整内容 |
|-----|---------|
| Daily Note | 添加"今日对齐"（链接战略/项目）、"Claude 分析区" |
| Weekly Review | 添加项目状态总结、Claude PM 输出区 |
| Project | 添加 strategy-link、Claude 分析区 |
| Dot | 添加 MOC 关联字段 |

### 5. 与 Claude Code 的协作方式

**Claude Code 的角色**：
- 在终端中直接读取 Vault 文件
- 批量处理和分析
- 生成结构化输出

**工作流示例**：
```bash
# 在 PersonalOS 目录下启动 Claude Code
cd ~/PersonalOS
claude

# Claude Code 可以：
# 1. 读取整个 Vault 做分析
# 2. 批量更新 frontmatter
# 3. 生成周报/月报
# 4. 检查系统健康度
```

---

## 系统演化路径

### 第一阶段：手动驱动（第1个月）

**目标**：建立习惯，验证方案

```
手动操作：
├─ 每天手动填写每日笔记
├─ 每天晚上手动找 Claude 做复盘
├─ 每周五手动生成周报
├─ 定期手动清理 Inbox
└─ 每月初手动做战略对话

观察指标：
├─ 是否能坚持每日记录？
├─ Claude 的分析是否有价值？
├─ Ideaverse 的模板是否顺手？
└─ 哪些环节最耗时？
```

### 第二阶段：半自动化（第2-3个月）

**目标**：减少重复操作

```
利用 Ideaverse 预配置的插件：
├─ Periodic Notes：自动创建每日/周笔记
├─ Templater：模板自动填充
├─ QuickAdd：快速创建各类笔记
├─ Dataview：自动生成仪表盘
└─ Calendar：可视化时间线

引入 Claude Code：
├─ 一键触发 Claude 分析
├─ 批量处理 Vault 内容
└─ 自动生成报告
```

### 第三阶段：高度自动化（第4个月起）

**目标**：系统自动运转，你专注思考

```
全自动：
├─ 定时任务自动触发 Claude 分析
├─ 数据自动聚合
├─ 报告自动生成
└─ 风险自动预警

你只需要：
├─ 阅读 AI 生成的分析
├─ 回答 AI 提出的问题
├─ 做最终决策
└─ 记录关键思考
```

---

## 效能预期

### 时间成本

| 阶段 | 每日 | 每周额外 | 每月额外 | 总计/月 |
|:---|:---|:---|:---|:---|
| 第1个月 | 25分钟 | 45分钟 | 1.5小时 | ~11小时 |
| 第2-3个月 | 15分钟 | 30分钟 | 1小时 | ~7小时 |
| 第4个月起 | 10分钟 | 20分钟 | 30分钟 | ~5小时 |

*注：比03方案略低，因为复用了 Ideaverse 的现成配置*

### 产出预期

**第1个月**：
- Vault 基本结构搭建完成
- 积累30篇每日记录
- Atlas 沉淀20+ 个知识点
- 完成4次周复盘
- 完成1次战略复盘

**第3个月**：
- Atlas 知识网络初具规模
- 形成3-5个成熟的 MOC
- 项目完成率提升20%
- 战略方向更清晰

**第6个月**：
- 系统完全内化
- 能力放大效应明显
- 可以开始总结方法论

---

## 核心价值主张

这套融合系统的本质：

1. **借力 Ideaverse**
   - 不用从零配置插件
   - 复用成熟的知识管理框架
   - 降低启动门槛

2. **注入 PDCA 灵魂**
   - 战略层保证方向正确
   - 三层循环保证持续迭代
   - AI 协作保证深度思考

3. **Claude 深度集成**
   - 不是问答式使用 AI
   - 而是让 AI 成为系统的一部分
   - 三个身份各司其职

4. **渐进式演化**
   - 第一阶段手动验证
   - 第二阶段半自动
   - 第三阶段高度自动

---

## 实施步骤

### Step 0：方案确认
- [x] 创建本文档
- [ ] 用户确认方案满意

### Step 1：复制 Ideaverse Zero 2.5
```bash
cp -r "ideaversePro2.5/Ideaverse Zero 2.5" ~/MyAI/PersonalOS
```

### Step 2：添加 Strategy 层
- 创建 `Strategy/` 目录
- 创建 `Strategy/north-star.md`（北极星指标）
- 创建 `Strategy/annual-plan.md`（年度计划）
- 创建 `Strategy/quarterly/` 子目录
  - 创建 `Strategy/quarterly/2026-Q1.md`（当前季度目标）
- 创建 `Strategy/reviews/` 子目录
  - 创建 `Strategy/reviews/review-template.md`（月度复盘模板）
- 检查 `Calendar/Reviews/` 是否已有 `Weekly/` 和 `Monthly/` 子目录
  - 如没有则创建（Ideaverse Zero 应该已有）
  - `Monthly/` 用于存放指向 `Strategy/reviews/` 的索引笔记

### Step 3：扩展 Prompts 目录
- 在 `x/x/Prompts/` 中添加三个 PDCA Prompts
- 创建 `Prompt - Strategy Coach.md`
- 创建 `Prompt - Project Manager.md`
- 创建 `Prompt - Skill Analyzer.md`
- 创建 `contexts/` 子目录
- 创建上下文配置文件

### Step 4：创建 Meta 目录
- 创建 `x/Meta/` 目录
- 创建 `x/Meta/system-changelog.md`（系统迭代日志）
- 创建 `x/Meta/ai-conversations/` 子目录
- 创建 `x/Meta/metrics/` 子目录
- 创建 `x/Meta/metrics/monthly-dashboard.md`
- 创建 `x/Meta/metrics/growth-tracking.md`

### Step 5：调整现有模板
- 修改 `x/Templates/Daily Note.md`
  - 添加"今日对齐"部分（链接到战略/项目）
  - 添加"Claude 分析区"
- 修改 `x/Templates/Weekly Review.md`
  - 添加"项目状态总结"
  - 添加"Claude PM 输出区"
- 修改 `x/Templates/Project.md`
  - 添加 `strategy-link` frontmatter 字段
  - 添加"Claude 分析区"
- 调整 Dot 模板（如果 Ideaverse 有的话，或创建新模板）
  - 添加 MOC 关联字段
  - 标准化 frontmatter（type, category, tags, created）

### Step 6：调整 Home Base 仪表盘
- 打开 `Home Base.md`
- 在顶部添加战略层快捷入口：
  ```markdown
  > [!star] 🎯 **[[Strategy]]** - 战略中心
  >
  > [[Strategy/north-star|北极星]] | [[Strategy/annual-plan|年度计划]] | [[Strategy/quarterly/2026-Q1|本季目标]]
  ```
- 添加 Dataview 查询显示当前战略对齐状态

### Step 7：更新 README
- 打开 `README.md`
- 添加三层 PDCA 系统说明
- 添加 Claude 使用指南
- 添加快速开始教程

### Step 8：验证
- 在 Obsidian 中打开 Vault
- 确认插件正常加载
- 确认 Strategy/ 目录和 Meta/ 目录正确创建
- 创建测试笔记（Daily Note、Project）
- 测试 Claude Code 读取能力（读取 Strategy 文件）

---

## 待确认问题

在执行前，请确认：

1. **方案是否满意？**
   - 结构是否清晰？
   - 是否遗漏重要内容？

2. **Vault 存放位置**
   - 当前计划放在 `~/MyAI/PersonalOS`
   - 后续迁移到用户目录？

3. **模板详细程度**
   - 是否需要我详细设计每个模板的内容？

4. **Claude 提示词**
   - 是否需要我详细编写三个身份的提示词？

---

## 设计讨论记录

### 2026-01-30：Skills 映射到 Atlas/Dots + Efforts/Areas 的理解

**问题**：为什么03方案的 `Skills/` 要拆分映射到04方案的 `Atlas/Dots/` 和 `Efforts/Areas/`？

**核心洞察**：线性思维 vs 网状思维

#### 03方案：线性聚合（文件夹层级）

```
Skills/writing/
├── sops/              # 标准操作流程
├── prompts/           # AI 提示词
├── examples/          # 优秀案例
├── principles/        # 原则心法
└── _index.md          # 能力树 + 掌握程度
```

**特点**：
- ✅ 一目了然，所有内容物理聚合在一起
- ✅ 结构清晰，四种类型分门别类
- ❌ 只能从 "writing" 这一个维度访问
- ❌ 知识点无法被多个上下文引用

#### 04方案：网状聚合（MOC 多维关联）

**物理存储**（分散但有序）：
```
Atlas/Dots/Statements/     # 原则性知识
├── 场景化案例原则.md
└── 具体性原则.md

Atlas/Dots/Things/         # 具体案例
├── 好的开头案例.md
└── 故事化叙述案例.md

Efforts/Areas/Writing/     # 执行流程（动态）
├── SOP - 文章写作.md
└── SOP - 编辑检查.md

x/x/Prompts/               # AI 协作
├── Prompt - 大纲生成器.md
└── Prompt - 风格编辑器.md
```

**逻辑聚合**（通过 MOC）：
````markdown
# Atlas/Maps/Writing Skill MOC.md

## 📋 执行流程（SOPs）
- [[SOP - 文章写作]]
- [[SOP - 编辑检查]]

## 🤖 AI 协作（Prompts）
- [[Prompt - 大纲生成器]]
- [[Prompt - 风格编辑器]]

## 💡 核心原则（Principles）
- [[场景化案例原则]]
- [[具体性原则]]

## 📚 优秀案例（Examples）
- [[好的开头案例]]
- [[故事化叙述案例]]

---

## 🌳 能力树状结构
- [ ] 基础写作（60%掌握）
  - [x] 文章结构
  - [x] 段落组织
  - [ ] 修辞手法
- [ ] 说服力写作（40%掌握）
  - [x] 场景化案例
  - [ ] 数据论证

---

## 📊 掌握程度追踪（Dataview 自动生成）

```dataview
TABLE 
  used-count as "使用次数",
  level as "掌握程度"
FROM "Atlas/Dots" OR "Efforts/Areas/Writing"
WHERE contains(tags, "writing")
SORT used-count DESC
```

**特点**：
- ✅ 同样一目了然（通过 MOC 聚合）
- ✅ 同样有能力树 + 掌握程度
- ✅ **每个知识点可以被多个 MOC 引用**
- ✅ **可以动态创建新的聚合视图**

````

#### MOC 的真正威力：多维聚合

**场景1：同一个知识点，出现在多个上下文**

```
Atlas/Dots/Statements/场景化案例原则.md
├── 被 Atlas/Maps/Writing Skill MOC.md 引用
├── 被 Atlas/Maps/Persuasion MOC.md 引用（说服力技巧）
├── 被 Atlas/Maps/Storytelling MOC.md 引用（故事化叙述）
└── 被 Efforts/Projects/Active/article-xxx.md 引用（实战项目）
```

**结果**：
- 学习 "说服力" 时，会看到这个原则
- 学习 "故事化叙述" 时，也会看到这个原则
- 写具体文章时，还会看到这个原则
- **知识在多个上下文中被激活，而非孤立存在**

**场景2：动态创建跨领域聚合**

```markdown
# Atlas/Maps/Persuasion MOC.md

## 来自 Writing Skill
- [[场景化案例原则]]
- [[具体性原则]]

## 来自 Thinking Skill
- [[逻辑论证框架]]
- [[反驳预设]]

## 来自 Data Analysis Skill
- [[数据可视化技巧]]
```

**结果**：
- 不需要移动任何文件
- 不需要复制内容
- 5分钟创建新视图
- 发现跨领域的共通原则

#### 完整映射表

| 03方案 Skills 内容 | 04方案映射位置 | 映射理由 |
|-------------------|---------------|---------|
| `writing/principles/` | `Atlas/Dots/Statements/` | 原则性知识 → 观点主张（静态） |
| `writing/examples/` | `Atlas/Dots/Things/` | 具体案例 → 事物概念（静态） |
| `writing/prompts/` | `x/x/Prompts/` | AI提示词 → 独立目录 |
| `writing/sops/` | `Efforts/Areas/Writing/` | 执行流程 → 持续关注领域（动态） |
| `_index.md`（能力图谱） | `Atlas/Maps/Writing Skill MOC.md` | 能力总览 → MOC 聚合 |

#### 核心差异总结

| 维度 | 线性思维（03方案） | 网状思维（04方案） |
|-----|------------------|------------------|
| **组织方式** | 文件夹层级 | MOC 链接 |
| **访问路径** | 单一维度 | 多维度 |
| **聚合方式** | 物理聚合（文件在一起） | 逻辑聚合（链接在一起） |
| **知识复用** | 一个知识点 = 一个位置 | 一个知识点 = 多个上下文 |
| **灵活性** | 低（改结构要移动文件） | 高（改 MOC 只需调整链接） |
| **学习曲线** | 低 | 中 |
| **长期价值** | 中 | 高 |

#### 混合方案（推荐用于过渡）

如果不确定是否适应网状思维，可以：

```
PersonalOS/
├─ Skills/              # 保留03方案的结构（物理聚合）
│  ├── writing/
│  └── thinking/
├─ Atlas/Maps/
│  ├── Writing Skill MOC.md    # 新增（逻辑聚合）
│  └── Persuasion MOC.md       # 新增（跨领域聚合）
```

**工作流**：
- 日常：主要用 Skills 目录（熟悉的线性思维）
- 探索：偶尔用 MOC（发现新的关联）
- 逐步：把 Skills 的内容迁移到 Atlas，用 MOC 聚合

**用户反馈**：
> "我原本想的是03方案中每一个skill都有 sops、prompts、examples、principles以及能力树状结构和掌握程度标记，在我看来更聚合。没有想到你说的可以使用 Skills MOC进行聚合的用法。我还是停留在线性思维了。"

**结论**：
- 理解了 MOC 的多维聚合能力
- 认识到网状思维的灵活性
- 决定采用04方案的 MOC 方式

---

## 附录：Strategy 目录命名设计说明

### 为什么是 `Strategy/` 而非 `1-Strategy/`？

**设计原则：融合而非重构**

在融合 Ideaverse 和 PDCA 系统时，我们面临一个命名选择：

| 方案 | 示例 | 优势 | 劣势 |
|-----|------|------|------|
| 数字前缀 | `1-Strategy/` | 强制排序，突出优先级 | 与 Ideaverse 风格不一致，显得突兀 |
| 无前缀 | `Strategy/` | 风格统一，简洁优雅 | 字母排序靠后 |
| 统一重构 | `1-Strategy/`, `2-Atlas/`, `3-Calendar/`, `4-Efforts/` | 层级清晰 | **破坏 Ideaverse 原有结构**，失去融合意义 |

**最终选择：`Strategy/`（无前缀）**

#### 核心理由

1. **保持 Ideaverse 的命名风格**
   ```
   PersonalOS/
   ├─ +/              ← 特殊符号（Inbox）
   ├─ Atlas/          ← 单词命名
   ├─ Calendar/       ← 单词命名
   ├─ Efforts/        ← 单词命名
   ├─ Strategy/       ← 单词命名（新增，风格一致）
   └─ x/              ← 单词命名
   ```

2. **字母排序符合实际使用频率**
   
   虽然 Strategy 在字母排序中靠后（S 在 A/C/E 之后），但这反而符合实际工作流：
   
   ```
   日常工作流：
   1. 打开 Calendar/Days（今日笔记）      ← 每天
   2. 查看 Efforts/Projects（今日任务）   ← 每天
   3. 执行工作，沉淀到 Atlas              ← 每天
   4. 月初打开 Strategy 做战略复盘        ← 每月
   
   访问频率：
   ├─ Calendar/Days      每天
   ├─ Efforts/Projects   每天
   ├─ Atlas/Dots         每周
   └─ Strategy/          每月
   ```
   
   Strategy 不需要排在最前面，因为它不是每天访问的内容。

3. **通过其他方式强调战略的重要性**
   
   不依赖文件排序，而是通过：
   
   **a. Home Base 仪表盘置顶**
   ```markdown
   # Home Base
   
   > [!star] **[[Strategy]]** » [[North Star]] | [[Annual Plan]] | [[Quarterly Plans]] | [[Reviews]]
   
   ---
   
   > [!waypoint] **[[Atlas]]** » ...
   > [!calendar] **[[Calendar]]** » ...
   > [!target] **[[Efforts]]** » ...
   ```
   
   **b. Dataview 动态展示**
   ```markdown
   ## 🎯 当前战略对齐
   
   **北极星**：[[Strategy/north-star|我的北极星]]
   **本季目标**：[[Strategy/quarterly/2026-Q1|2026 Q1 目标]]
   **上次复盘**：[[Strategy/reviews/2026-01-review|2026年1月复盘]]
   
   ---
   
   ## 📊 本周项目进展
   ...
   ```
   
   **c. Obsidian Bookmarks/Starred**
   
   将 `Strategy/` 文件夹或关键文件加星标，永远显示在侧边栏顶部。
   
   **d. Folder Note 插件**
   
   在 `Strategy/` 中创建 `Strategy.md` 作为文件夹笔记，作为战略层的统一入口。

4. **可扩展性**
   
   未来如果需要添加其他顶层概念，也用单词命名：
   ```
   PersonalOS/
   ├─ +/
   ├─ Atlas/
   ├─ Calendar/
   ├─ Efforts/
   ├─ Strategy/       ← 战略层
   ├─ Vision/         ← 未来可能添加：愿景层
   └─ x/
   ```

5. **Claude 的理解不受影响**
   
   Claude 通过**文件名语义**而非**排序位置**来理解结构：
   ```
   "Strategy" 这个词本身就足够明确
   vs
   "1-Strategy" 中的 "1" 对 AI 来说是冗余信息
   ```

### 最终结构

```
PersonalOS/                          # 融合后的系统
├─ +/                                # [Ideaverse] Inbox
├─ Atlas/                            # [Ideaverse] 知识层
├─ Calendar/                         # [Ideaverse] 时间层
├─ Efforts/                          # [Ideaverse] 执行层
├─ Strategy/                         # [PDCA 新增] 战略层
└─ x/                                # [Ideaverse] 系统资源
    └─ x/Prompts/                    # [融合扩展] AI 协作
```

**这是 Ideaverse 的 ACE 框架扩展为 SACE 框架**：
- **S**trategy：战略层（新增）
- **A**tlas：知识层
- **C**alendar：时间层
- **E**fforts：执行层

---

### 如果你仍然偏好数字前缀

如果你觉得字母排序不够直观，可以考虑这个妥协方案：

**在 Home Base 中用 emoji 或符号强调**

```markdown
# Home Base

> [!star] 🎯 **[[Strategy]]** - 战略中心
> 
> [[Strategy/north-star|北极星]] | [[Strategy/annual-plan|年度计划]] | [[Strategy/quarterly/2026-Q1|本季目标]]

---

> [!waypoint] 🗺️ **[[Atlas]]** - 知识地图
> [!calendar] 📅 **[[Calendar]]** - 时间线
> [!target] 🎯 **[[Efforts]]** - 项目执行
```

这样既保持了文件系统的简洁，又在视觉上突出了战略的重要性。

---

## 附录：系统提醒配置指南

### 关于"时间触发（Obsidian Periodic Notes + 系统提醒）"

本系统采用**双重触发机制**确保 PDCA 循环不遗漏：

| 机制 | 功能 | 作用 |
|-----|------|------|
| **Obsidian Periodic Notes** | 自动创建周期性笔记 | 确保你**有地方**去记录 |
| **系统提醒** | 定时弹出通知 | 确保你**记得**去做 |

**为什么需要两者？**
- 只有系统提醒 → 你记得做，但每次都要从零创建笔记（低效）
- 只有 Periodic Notes → 笔记自动创建了，但你可能忘记打开（遗漏）
- **结合使用 = 完美工作流** ✨

---

### 一、Obsidian Periodic Notes 配置

**好消息**：Ideaverse Zero 2.5 已经预配置好了这个插件！

#### 验证配置

1. 打开 Obsidian
2. `设置` → `社区插件` → 检查 **Periodic Notes** 是否已启用
3. `设置` → `Periodic Notes` → 查看配置：

```
Daily Notes:
├─ 格式：YYYY-MM-DD
├─ 位置：Calendar/Days
├─ 模板：x/Templates/Daily Note.md
└─ 在启动时打开：✅ 建议勾选

Weekly Notes:
├─ 格式：YYYY-[W]WW
├─ 位置：Calendar/Reviews/Weekly
├─ 模板：x/Templates/Weekly Review.md
└─ 启用：✅

Monthly Notes:
├─ 格式：YYYY-MM
├─ 位置：Calendar/Reviews/Monthly
└─ 启用：可选（战略复盘建议手动创建）
```

#### 工作方式

- **每天打开 Obsidian**：自动创建或打开今天的 Daily Note
- **快捷键**（可在设置中配置）：
  - `Cmd+T`：打开今天的 Daily Note
  - `Cmd+Shift+T`：打开本周的 Weekly Note

---

### 二、macOS 系统提醒配置

#### 方案1：使用 macOS "提醒事项" App（推荐）

##### Step 1：创建 PDCA 列表

1. 打开 macOS **提醒事项** App
2. 点击左下角 `+` → `新建列表`
3. 命名为 `PDCA 系统`
4. 选择颜色：🔴 红色（重要）

##### Step 2：创建每日复盘提醒

1. 在 `PDCA 系统` 列表中点击 `+`
2. 输入：`📝 每日复盘 - 打开 Obsidian 填写今日笔记`
3. 点击 `ⓘ` 详细信息：
   ```
   时间：晚上 21:00
   重复：每天
   优先级：!! 高
   标记：#daily #pdca
   备注：
   1. 打开 Obsidian（会自动跳转今日笔记）
   2. 填写"今日完成""今日学习""明日计划"
   3. 复制内容发给 Claude Skill Analyzer
   4. 粘贴分析结果到"Claude 分析区"
   ```
4. 点击 `完成`

##### Step 3：创建周复盘提醒

```
提醒内容：📊 周复盘 - 生成本周周报

时间：每周五 17:00
重复：每周
优先级：!! 高
标记：#weekly #pdca

备注：
1. 打开 Obsidian
2. 创建或打开本周的 Weekly Review 笔记
3. 在 Claude Project Manager Project 中对话
4. 让 Claude 读取本周所有 Daily Notes + 项目文件
5. 生成周报，粘贴到 Weekly Review 笔记
```

##### Step 4：创建战略复盘提醒

```
提醒内容：🎯 战略复盘窗口（3天内完成）

时间：每月1日 上午9:00
重复：每月
优先级：!!! 非常高
标记：#strategy #pdca

备注：
⏱ 时间要求：30-60分钟深度对话
📅 截止日期：每月3日前完成

工作流：
1. 创建 Strategy/reviews/YYYY-MM-review.md
2. 在 Claude Strategy Coach Project 中对话
3. Claude 读取上月所有数据（Projects + Daily + Weekly）
4. 多轮深度对话：
   - 数据总结
   - 关键质疑（5-8个问题）
   - 盲区识别
   - 调整建议
5. 生成月度复盘文档
6. 更新 Strategy/quarterly/2026-QX.md（如需调整）
```

##### Step 5：可选 - Inbox 清理提醒

```
提醒内容：🧹 清理 Inbox - 归档到 Atlas

时间：每周日 上午10:00
重复：每周
优先级：中
标记：#maintenance #pdca

备注：
1. 打开 Obsidian
2. 检查 +/ (Inbox) 中的积压笔记
3. 将笔记归档到相应位置：
   - 知识点 → Atlas/Dots/
   - 项目想法 → Efforts/Projects/Simmering/
   - 信息来源 → Atlas/Sources/
4. 目标：Inbox 保持 < 5 条
```

---

#### 方案2：使用 macOS "日历" App

适合喜欢可视化时间线的用户。

##### 创建日程

1. 打开 macOS **日历** App
2. 创建新日历：`PDCA 系统`（颜色：红色）
3. 创建重复日程：

**每日复盘**
```
标题：📝 每日复盘
时间：每天 21:00-21:15
重复：每天
提醒：事件开始时
备注：[同"提醒事项"的备注]
```

**周复盘**
```
标题：📊 周复盘
时间：每周五 17:00-17:30
重复：每周
提醒：事件开始时
```

**战略复盘**
```
标题：🎯 战略复盘（预留1小时）
时间：每月1日 14:00-15:00
重复：每月
提醒：当天上午9:00（提前提醒）
备注：3天内完成，不一定在这个时间
```

---

#### 方案3：使用第三方 App

##### a. Due（Mac + iOS）

**优势**：
- 🔥 自动重复提醒（直到你标记完成）
- 📱 跨设备同步
- ⏰ 精确到分钟的重复规则

**配置示例**：
```
每日复盘
├─ 时间：21:00
├─ 重复：每天
├─ 自动重复：每5分钟提醒一次（直到完成）
└─ 音效：重要提醒音
```

##### b. Things 3（Mac + iOS）

**优势**：
- 🎯 项目和任务一体化管理
- 📅 Today/Upcoming 视图清晰
- 🔗 可以创建"晚间复盘"区域

**配置示例**：
```
项目："PDCA 系统"
├─ 每日复盘（重复：每天晚上）
├─ 周复盘（重复：每周五下午）
└─ 战略复盘（重复：每月1日）
```

##### c. Obsidian 插件：Reminder

**优势**：
- 📝 在 Obsidian 内部管理提醒
- 🔗 直接关联笔记
- 📋 与任务系统集成

**配置示例**：
在任意笔记中（如 `Home Base.md`）：
```markdown
## 🔔 系统提醒

- [ ] 每日复盘 ⏰ 21:00 🔁 每天
- [ ] 周复盘 ⏰ 每周五 17:00 🔁 每周
- [ ] 战略复盘 ⏰ 每月1日 09:00 🔁 每月
```

---

### 三、完整工作流示例

#### 场景1：每日复盘（21:00）

```
1. 21:00 - macOS 通知弹出
   ┌─────────────────────────────────┐
   │ 🔔 提醒事项                      │
   │ 📝 每日复盘 - 打开 Obsidian...  │
   │ [稍后提醒] [完成]                │
   └─────────────────────────────────┘

2. 点击通知 → 打开 Obsidian
   └─ Periodic Notes 已创建 Calendar/Days/2026-01-31.md

3. 今日笔记内容（模板自动填充）
   ├─ ## 今日对齐
   │  • 本月北极星：[自动链接]
   │  • 本周重点：[自动链接]
   │
   ├─ ## 今日完成（你填写）
   │  • 完成文章初稿 3000 字
   │  • 修复项目 Bug 2 个
   │
   ├─ ## 今日学习（你填写）
   │  • 学到"场景化案例"技巧
   │
   ├─ ## 明日计划（你填写）
   │  • 打磨文章案例部分
   │
   └─ ## Claude 分析区（空白）

4. 复制"今日完成"+"今日学习"部分

5. 切换到 Claude Skill Analyzer Project
   └─ 粘贴内容，发送："分析今日记录"

6. Claude 返回分析
   ├─ 知识点提炼：1-3 个
   ├─ 关联分析：与哪些 Dots 相关
   ├─ 沉淀建议：具体文件路径
   └─ MOC 更新建议

7. 粘贴到"Claude 分析区"

8. 根据建议（可选）
   └─ 创建 Atlas/Dots/Statements/场景化案例原则.md

9. 标记"提醒事项"为完成
   └─ 整个流程 10-15 分钟
```

#### 场景2：周复盘（每周五17:00）

```
1. 17:00 - macOS 通知
   ┌─────────────────────────────────┐
   │ 🔔 日历                          │
   │ 📊 周复盘                        │
   │ [查看] [稍后]                    │
   └─────────────────────────────────┘

2. 打开 Obsidian
   ├─ 可能已自动创建 Calendar/Reviews/Weekly/2026-W05.md
   └─ 如没有，手动创建（使用 Weekly Review 模板）

3. 打开 Claude Code（或 Claude Projects）

4. 在终端执行（或在 Claude 对话框输入）：
   "生成本周周报，读取以下文件：
   - Calendar/Days/2026-01-27.md 至 2026-01-31.md
   - Efforts/Projects/Active/ 所有项目
   - 上周周报对比"

5. Claude 返回周报
   ├─ 本周数据总览
   ├─ 项目进展
   ├─ 项目状态建议（Active/Simmering 调整）
   ├─ 风险识别
   └─ 下周建议

6. 粘贴到 Weekly Review 笔记

7. 根据建议调整项目状态
   └─ 移动文件到不同目录（Active → Simmering）

8. 标记"提醒事项"为完成
   └─ 整个流程 15-20 分钟
```

#### 场景3：战略复盘（每月1-3号）

```
1. 每月1日 09:00 - macOS 通知
   ┌─────────────────────────────────┐
   │ 🔔 提醒事项                      │
   │ 🎯 战略复盘窗口（3天内完成）     │
   │ [查看详情] [稍后]                │
   └─────────────────────────────────┘

2. 安排时间（不一定立即做）
   └─ 找一个完整的 30-60 分钟时间段

3. 准备工作
   ├─ 创建 Strategy/reviews/2026-01-review.md
   └─ 打开 Claude Strategy Coach Project

4. 多轮深度对话（30-60分钟）

   第1轮：数据总结
   你："开始本月战略复盘"
   Claude：[读取上月所有数据，生成总结]

   第2轮：质疑
   Claude：[提出 5-8 个质疑问题]
   你：[逐一回答，深入思考]

   第3轮：盲区识别
   Claude：[指出可能的盲区]
   你：[反思，确认或反驳]

   第4轮：调整建议
   Claude：[提出具体可执行的调整]
   你：[讨论可行性，做决策]

5. 生成月度复盘文档
   └─ Claude 自动生成 Markdown，你保存到文件

6. 更新战略文件（如需要）
   ├─ Strategy/quarterly/2026-Q1.md（调整目标）
   └─ Strategy/annual-plan.md（重大调整）

7. 标记"提醒事项"为完成
   └─ 整个流程 30-60 分钟
```

---

### 四、故障排查

#### 问题1：Periodic Notes 没有自动创建笔记

**原因**：
- 插件未启用
- 模板路径错误
- 文件夹不存在

**解决**：
```
1. 检查插件启用：设置 → 社区插件 → Periodic Notes ✅
2. 检查模板路径：设置 → Periodic Notes → 模板位置
   └─ 应该是：x/Templates/Daily Note.md
3. 检查文件夹存在：Calendar/Days/ 是否存在
4. 手动创建一次笔记，测试模板是否正常
```

#### 问题2：系统提醒没有弹出

**原因**：
- 系统通知被关闭
- App 通知权限未开启
- 设备处于勿扰模式

**解决**：
```
macOS 设置：
├─ 系统偏好设置 → 通知
├─ 找到"提醒事项"或"日历"
└─ 确保：
   • 允许通知 ✅
   • 通知样式：横幅（持续显示）
   • 声音 ✅
   • 勿扰模式豁免 ✅（可选）
```

#### 问题3：提醒太频繁，感觉被打扰

**解决**：
```
调整提醒时间：
├─ 每日复盘：从 21:00 调整到你的实际作息时间
├─ 周复盘：从周五 17:00 调整到周六上午（如果你周五忙）
└─ 战略复盘：使用"窗口提醒"而非固定时间
   例：每月1日提醒，但可以在1-3日任意时间完成
```

#### 问题4：忘记标记完成，导致提醒积压

**解决**：
```
1. 使用 Due App 的自动重复功能
   └─ 每5分钟提醒一次，直到你完成

2. 或在"提醒事项"中设置：
   └─ 优先级：高
   └─ 通知音：重要音效
   └─ 在其他设备上也提醒（iPhone/iPad）
```

---

### 五、进阶：自动化触发（第三阶段）

当你熟练使用系统后（第4个月起），可以尝试更高级的自动化：

#### 使用 macOS Shortcuts（快捷指令）

**场景：一键启动每日复盘**

```applescript
快捷指令名称："PDCA 每日复盘"

动作1：打开 App "Obsidian"
动作2：等待 2 秒
动作3：执行 AppleScript：
   tell application "System Events"
       keystroke "t" using command down
   end tell
动作4：显示通知 "已打开今日笔记，请填写复盘内容"
```

**触发方式**：
- 设置快捷指令的自动化：每天 21:00 自动运行
- 或：Siri 语音触发："嘿 Siri，每日复盘"

#### 使用 Keyboard Maestro

**场景：自动化周复盘流程**

```
触发器：每周五 17:00

动作流：
1. 打开 Obsidian
2. 创建本周 Weekly Review 笔记
3. 打开 Claude Code（终端）
4. 自动输入命令（不执行）：
   "生成本周周报，读取 Calendar/Days/2026-W05 的所有文件"
5. 等待你按 Enter 执行
```

#### 使用 Hazel（文件监控）

**场景：检测 Inbox 积压**

```
监控目录：+/ (Inbox)

规则：
如果：文件数量 > 10
则：
1. 发送通知："Inbox 积压超过 10 条，请归档"
2. 标记"提醒事项"中的"清理 Inbox"为高优先级
```

---

### 六、推荐配置总结

#### 最小配置（必需）

```
✅ Obsidian Periodic Notes 插件（Ideaverse 已配置）
✅ macOS 提醒事项：
   • 每日复盘（21:00）
   • 周复盘（每周五 17:00）
   • 战略复盘（每月1日）
```

#### 推荐配置

```
✅ 最小配置
✅ Inbox 清理提醒（每周日）
✅ macOS 日历可视化（可选）
✅ Obsidian Reminder 插件（在笔记中管理提醒）
```

#### 进阶配置（第4个月起）

```
✅ 推荐配置
✅ Due App（自动重复提醒）
✅ macOS Shortcuts（一键启动复盘）
✅ Keyboard Maestro（自动化工作流）
```

---

### 七、效果预期

#### 第1个月：建立习惯

```
目标：
├─ 每日复盘完成率 ≥ 80%（每周至少 5 天）
├─ 周复盘完成率 = 100%（每周五必做）
└─ 战略复盘完成率 = 100%（每月必做）

可能的挑战：
├─ 忘记填写每日笔记
├─ 提醒时间不合适
└─ 感觉流程繁琐

解决：
└─ 调整提醒时间到适合自己的时间
└─ 简化流程（第一个月可以只记录，不求完美）
```

#### 第2-3个月：形成惯性

```
目标：
├─ 每日复盘完成率 ≥ 90%
├─ 不需要提醒也会主动打开 Obsidian
└─ Claude 分析开始产生实际价值

效果：
├─ Atlas/Dots 积累 50+ 个知识点
├─ 项目完成率提升 10-20%
└─ 开始感受到"知识复利"
```

#### 第4个月起：系统内化

```
目标：
├─ 系统成为思维方式的一部分
├─ 开始探索自动化优化
└─ 可以向他人分享你的系统

效果：
├─ 不需要刻意提醒，自然会复盘
├─ 能力放大效应明显
└─ 战略方向越来越清晰
```

---

**💡 核心建议**：

1. **从最小配置开始**，不要一次性配置所有功能
2. **先建立习惯**（坚持30天），再优化流程
3. **提醒时间可调整**，找到最适合自己的节奏
4. **不求完美**，80分的坚持 > 100分的偶尔

**记住**：系统是为你服务的，而不是你为系统服务。如果某个环节感觉不顺畅，就调整它！
