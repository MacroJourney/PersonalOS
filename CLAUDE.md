# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 仓库概述

**PersonalOS v2.1** - 人机协作个人操作系统搭建指南

- **仓库地址**：https://github.com/MacroJourney/PersonalOS
- **许可证**：Apache 2.0
- **最新更新**：2026-02-02
- **项目性质**：文档与模板库（非代码项目）

这是一个**个人成长和生产力系统的搭建指南**，提供完整的架构设计、配置模板和使用示例，帮助用户建立基于 AI 协作的个人操作系统。

## 核心理念

PersonalOS 是一个**人机协作框架**，而非软件产品。它解决三大个人成长挑战：

1. **方向迷失** → 战略层校准机制（月度/季度战略对话）
2. **执行低效** → 项目层管理机制（周度复盘 + AI 项目经理）
3. **经验流失** → 能力层复利机制（日度沉淀 + 知识网络）

### 核心设计

**两大模块**：
- **人机协作模块**：四区工作空间、权限边界、复利机制、AI 角色分工
- **成长管理模块**：战略层（方向校准）、项目层（目标推进）、能力层（知识积累）

**四区工作空间**：
```
00_Core/        # 游戏规则（人主导，AI 遵守）
01_Shared/      # 协作区（PDCA 系统，AI 可读写）
02_Human/       # 私人空间（AI 不进入）
03_AI/          # AI 自主空间（AI 管理，人观察）
```

**三层 PDCA 循环**：
- **战略层**：月度/季度方向校准
- **项目层**：周度目标推进
- **能力层**：日度知识积累

**三个 AI 角色**：
- **Strategy Coach**：战略顾问，月度复盘
- **Project Manager**：项目经理，周度追踪
- **Skill Analyzer**：能力分析师，日度沉淀

## 目录结构

```
PersonalOS/
│
├── docs/                       # 核心文档（从这里开始）
│   ├── 00_核心设计.md          # ⭐ 系统总体设计 (v2.0, 683 行)
│   ├── 01_快速开始.md          # 实施路径、渐进式启动方案
│   ├── 02_30天成长计划.md      # Week 1-4 完整计划、效果预期
│   ├── 03_模板库.md            # 9 个核心模板及使用说明
│   ├── 04_AI配置完整版.md      # 三个 AI 角色 System Prompts
│   ├── 05_FAQ与防坑.md         # 15 个常见问题 + 5 个反模式
│   └── 06_在仓库中搭建系统.md  # 在仓库内搭建工作空间指南
│
├── templates/                  # 可复制的模板文件
│   ├── 00_Core/               # 核心配置模板
│   │   ├── profile.template.md
│   │   ├── interaction_rules.template.md
│   │   └── stop_conditions.template.md
│   ├── 01_Shared/             # 协作空间占位符
│   └── obsidian-vault/        # Obsidian Vault 模板（Git 排除）
│       └── Ideaverse Zero 2.5/ # 空白基础框架（需自行准备）
│
├── examples/                   # 使用示例和最佳实践
│   ├── profile-examples.md     # Profile 配置示例
│   ├── project-workflow.md     # 项目工作流示例
│   ├── review-templates.md     # 复盘模板示例
│   └── rules-examples.md       # 规则库示例
│
├── references/                 # 历史参考资料（早期探索过程）
│   ├── README.md               # 参考资料说明
│   ├── 终极融合方案.md          # v2.1 前身，最终融合蓝图
│   ├── AI数字分身系统/
│   │   └── AI 数字分身系统/
│   │       ├── AI数字分身系统工程化设计、技术选型与架构建议.md
│   │       ├── 播客逐字稿.txt  # 655 行参考资料
│   │       ├── Claude 版/      # v1.0, v2.0, v2.1 早期搭建指南
│   │       ├── ChatGPT 版/     # ChatGPT 版本早期探索
│   │       └── Gemini 版/      # Gemini 版本早期探索
│   └── 三层PDCA方案/
│       └── 三层 PDCA 个人操作系统/
│           ├── 背景.md          # 项目起源（Twitter 灵感）
│           ├── 聊天记录.md      # 完整设计讨论记录
│           ├── 01_九种方案概览.md（早期探索，已废弃）
│           ├── 02_多AI Agent方案.md（早期探索，已废弃）
│           ├── 03_Claude精简方案.md（早期探索，已废弃）
│           └── 04_融合方案_基于Ideaverse改造.md（⭐ 关键参考）
│
├── Other/                      # 其他工作文档
│   ├── Skills 的意义.md
│   └── 防拖延系统流程图.drawio
│
├── .github/                    # GitHub 配置
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.md
│       ├── feature_request.md
│       └── question.md
│
├── README.md                   # 项目主文档
├── CLAUDE.md                   # 本文件
├── CHANGELOG.md                # 版本历史
├── CONTRIBUTING.md             # 贡献指南
└── LICENSE                     # Apache 2.0 许可证
```

## 用户工作空间（Git 排除）

用户根据文档和模板，在本地创建以下工作空间（已在 `.gitignore` 中排除）：

```
PersonalOS/  # 用户克隆本仓库后
│
├── 00_Core/                    # 核心配置（用户创建）
│   ├── profile.md              # 个人画像
│   ├── interaction_rules.md    # 交互规则
│   ├── stop_conditions.md      # 停止条件
│   └── memory/                 # 记忆系统
│       ├── long_term.md        # 长期记忆
│       ├── recent_rolling.md   # 近期滚动
│       └── compression_rule.md # 压缩规则
│
├── 01_Shared/                  # 协作区（Obsidian Vault）
│   ├── + (Inbox)/              # 快速捕获
│   ├── Atlas/                  # 能力层：知识管理
│   │   ├── Dots/               # 原子笔记（Skills, People, Things...）
│   │   ├── Maps/               # MOC 索引页
│   │   └── Sources/            # 信息来源
│   ├── Calendar/               # 时间维度
│   │   ├── Days/               # 每日笔记
│   │   ├── Records/            # 事件记录
│   │   └── Reviews/            # 周期复盘（Weekly, Monthly）
│   ├── Efforts/                # 项目层：执行管理
│   │   ├── Areas/              # 持续关注领域
│   │   ├── Projects/           # 项目（Active, Simmering, Sleeping）
│   │   └── Works/              # 作品输出
│   ├── Strategy/               # 战略层：方向校准
│   │   ├── north-star.md       # 北极星指标
│   │   ├── annual-plan.md      # 年度计划
│   │   ├── quarterly/          # 季度规划
│   │   └── reviews/            # 战略复盘
│   ├── Meta/                   # 系统元数据
│   │   ├── rules/              # 规则库
│   │   └── ai-conversations/   # 重要 AI 对话存档
│   ├── x/                      # 系统资源
│   │   ├── Templates/          # 模板库
│   │   └── Prompts/            # AI 指令中心
│   └── Home.md                 # 仪表盘
│
├── 02_Human/                   # 私人空间（AI 不进入）
│   ├── drafts/                 # 草稿区
│   ├── notes/                  # 个人笔记
│   ├── personal/               # 私密内容（日记、敏感信息）
│   ├── review_queue/           # 待审核区（AI 产出）
│   └── archive/                # 个人归档
│
└── 03_AI/                      # AI 自主空间（AI 管理）
    ├── workspace/              # AI 工作台
    ├── tools/                  # AI 创建的工具/脚本
    ├── ai_diary/               # AI 的日记
    ├── research/               # AI 的调研资料
    └── _private/               # AI 的私有笔记
```

## 核心文档快速索引

### 新用户开始路径
1. **首次使用**：`README.md` → `docs/01_快速开始.md`（10 分钟或 30 分钟启动）
2. **理解架构**：`docs/00_核心设计.md`（⭐ 强烈推荐完整阅读，683 行）
3. **深入学习**：`docs/02_30天成长计划.md`（4 周渐进式成长计划）
4. **查看示例**：`examples/` 目录（真实配置和工作流）
5. **配置 AI**：`docs/04_AI配置完整版.md`（三个 AI 角色完整 System Prompts）

### 架构理解路径
- **系统总览（含四区工作空间、AI 角色、PDCA 系统）**：`docs/00_核心设计.md`（⭐ 唯一权威来源）
- **模板说明**：`docs/03_模板库.md`

### 历史演进参考
- **最终融合方案**：`references/终极融合方案.md`（v2.1 前身）
- **PDCA 方案演进**：`references/三层PDCA方案/三层 PDCA 个人操作系统/04_融合方案_基于Ideaverse改造.md`（⭐ 关键设计决策）
- **AI 数字分身探索**：`references/AI数字分身系统/AI 数字分身系统/`（早期 Claude/ChatGPT/Gemini 版本探索）
- **早期九种方案**：`references/三层PDCA方案/三层 PDCA 个人操作系统/01_九种方案概览.md`（已废弃，仅供参考）

## 核心机制详解

### 复利机制

**规则库（Meta/rules/）**：
- 什么时候该做什么的决策指南
- 示例：`time_sensitive_check`（涉及时间时必须确认）、`quality_checklist`（交付前检查清单）

**技能库（Atlas/Dots/Skills/）**：
- 如何做某件事的方法积累
- AI 的"备忘录"，执行任务前查阅
- 示例：`retrospective_framework`（GRAI 四步复盘法）、`weekly_review_protocol`（周复盘标准流程）

**记忆系统（00_Core/memory/）**：
- **长期记忆**：稳定的身份信息、长期目标、核心偏好
- **近期滚动**：最近 30 天的动态记忆（≤300 字）
- **压缩规则**：如何将近期记忆压缩到长期记忆

### 权限边界

| 区域 | AI 可读 | AI 可写 | 备注 |
|-----|---------|---------|------|
| **00_Core/** | ✅ 随时 | ⚠️ 需确认 | 可更新 memory/recent_rolling.md |
| **01_Shared/** | ✅ 全部 | ⚠️ 部分需确认 | Calendar/Days、Atlas/Dots 可自由添加 |
| **02_Human/** | ⚠️ 需授权 | ❌ 不可 | AI 主动不进入，需明确授权 |
| **03_AI/** | ✅ 全部 | ✅ 完全自主 | AI 完全管理，人可观察 |

### 三层反馈循环

| 循环 | 周期 | 输入 | 处理者 | 输出位置 |
|-----|------|-----|--------|---------|
| **快回路** | 日度 | 今日记录 | Skill Analyzer | Atlas/Dots/ |
| **中回路** | 周度 | 本周数据 | Project Manager | Calendar/Reviews/Weekly/ |
| **慢回路** | 月度 | 整月数据 | Strategy Coach | Strategy/reviews/ |

## AI 交互原则

### 两条底层规则（摘自文档）

**规则一：不要轻易说"做不到"**
1. 先查本地：记忆库 / 规则库 / 技能库
2. 再查公开：搜索方案 / GitHub / 教程
3. 仍不行：提出替代方案（降级目标）
4. 穷尽后再报告不可行，并记录到规则库

**规则二：有强主观能动性**
- 主动探索：发现可以推进的任务
- 主动检查：识别潜在风险
- 主动复盘：总结经验教训
- 主动留痕：记录可复用的规则/技能

### AI 是合作伙伴，不是工具
- AI 拥有独立工作区（03_AI/），可自主决策和行动
- AI 有记忆系统，越用越懂你
- AI 有明确的角色分工，不只是通用助手
- 每次任务产出可复用资产（Rules、Skills、Templates）

## 工具配置

### 推荐工具

| 区域 | 推荐工具 | 说明 |
|-----|---------|------|
| **00_Core/** | Cursor / VS Code | 核心配置，方便版本管理 |
| **01_Shared/** | **Obsidian** | PDCA 系统 + 知识管理 |
| **02_Human/** | 任意工具 | 私人空间，自由选择 |
| **03_AI/** | Claude Code | AI 自主管理 |

### Obsidian 核心插件

| 插件 | 用途 | 必要性 |
|-----|------|-------|
| Periodic Notes | 自动创建每日/周笔记 | 必须 |
| Templater | 模板自动填充 | 必须 |
| Dataview | 动态查询和仪表盘 | 推荐 |
| QuickAdd | 快速创建各类笔记 | 推荐 |
| Calendar | 日历视图 | 可选 |

### Claude Projects 配置

为三个 AI 身份分别创建 Claude Project：
- **Strategy Coach Project**：上传 profile.md + Strategy/ 相关文件
- **Project Manager Project**：上传 profile.md + Efforts/Projects/ 相关文件
- **Skill Analyzer Project**：上传 profile.md + Atlas/ 相关文件

详细的 System Prompt 配置见 `docs/04_AI配置完整版.md`

## 知识管理框架（Ideaverse）

**ACE Framework**（Atlas + Calendar + Efforts）：

- **Atlas/**：知识地图层
  - **Dots/**：原子笔记（People, Things, Quotes, Statements, Questions, Skills）
  - **Maps/**：MOC (Map of Content) 主题索引页
  - **Sources/**：信息来源（Books, Movies, Clippings, Courses）

- **Calendar/**：时间维度
  - **Days/**：每日笔记
  - **Records/**：事件记录（Meetings, Events, Ideas）
  - **Reviews/**：周期复盘（Weekly, Monthly）

- **Efforts/**：行动维度
  - **Areas/**：持续关注领域 (AOE)
  - **Projects/**：项目（Active, Simmering, Sleeping）
  - **Works/**：作品输出（Articles, Videos, Newsletters）

**核心方法论**：
- **ARC Framework**：Add（添加）→ Relate（关联）→ Communicate（输出）
- **MOC (Map of Content)**：主题索引页，连接相关笔记
- **Home Base**：Dataview 驱动的仪表盘视图

## 常见使用场景

### 场景 1：首次搭建系统
1. 克隆本仓库：`git clone git@github.com:MacroJourney/PersonalOS.git`
2. 阅读 `docs/01_快速开始.md`，选择 10 分钟或 30 分钟启动方式
3. 根据 `docs/06_在仓库中搭建系统.md`，在仓库内创建工作空间
4. 从 `templates/00_Core/` 复制模板到 `00_Core/`，填写个人配置
5. 初始化 `01_Shared/` 为 Obsidian Vault（基于 Ideaverse 框架）
6. 配置三个 AI 角色（参考 `docs/04_AI配置完整版.md`）

### 场景 2：查找特定模板或示例
- **配置模板**：`templates/00_Core/*.template.md`
- **配置示例**：`examples/profile-examples.md`, `examples/rules-examples.md`
- **工作流示例**：`examples/project-workflow.md`
- **复盘示例**：`examples/review-templates.md`

### 场景 3：理解设计理念
- **核心设计（含四区工作空间、AI 角色、PDCA 系统）**：`docs/00_核心设计.md`（⭐ 必读，唯一权威来源）
- **历史演进**：`references/终极融合方案.md` + `references/三层PDCA方案/三层 PDCA 个人操作系统/04_融合方案_基于Ideaverse改造.md`

### 场景 4：贡献代码或文档
1. 阅读 `CONTRIBUTING.md`
2. 使用 `.github/ISSUE_TEMPLATE/` 创建 Issue
3. 遵循 Apache 2.0 许可证条款

## Git 策略

### 已排除的内容（.gitignore）
- **用户工作区**：`00_Core/`, `01_Shared/`, `02_Human/`, `03_AI/`（保护隐私）
- **Ideaverse 模板**：`templates/obsidian-vault/Ideaverse Pro 2.5/`, `Ideaverse Zero 2.5/`（尊重知识产权，付费内容）
- **系统文件**：`.DS_Store`, `.obsidian/workspace*`, 各类临时文件

### 为什么用户工作区被排除
- **隐私保护**：个人配置、日记、私密笔记不应上传
- **本地优先**：PersonalOS 是本地系统，数据留在本地
- **仓库用途**：本仓库提供指南和模板，不是用户数据存储

## 重要提示

### 对于 Claude Code
- 本仓库是**文档驱动型项目**，没有代码实现
- 重点在于**架构设计**和**用户指南**的准确性和可用性
- 修改文档时，保持与 `docs/00_核心设计.md` 的一致性
- 所有路径引用应使用**相对路径**，方便用户本地克隆使用
- **references/ 是历史参考**，不代表当前系统架构

### 对于用户
- **从 `docs/01_快速开始.md` 开始**，不要直接跳到复杂配置
- **工作区数据不会被 Git 追踪**（已在 `.gitignore` 排除）
- **Ideaverse 模板需自行准备**（付费内容，不包含在仓库中）
- **建议本地备份**：`00_Core/`, `01_Shared/`, `02_Human/`

### 版本说明
- **v2.1**（2026-02-02）：仓库重构，docs/templates/examples/references 分离，新增 GitHub 模板
- **v2.0**（早期）：系统设计完善，30 天成长计划，AI 配置完整版
- **v1.0**（早期）：初始架构设计

## 致谢

本项目整合了以下优秀方法论：
- **Ideaverse** by Nick Milo - 知识管理框架
- **PARA** by Tiago Forte - 信息组织方法
- **Zettelkasten** by Niklas Luhmann - 笔记方法
- **PDCA** by W. Edwards Deming - 持续改进循环
- **GTD** by David Allen - 任务管理方法

## 许可证

Apache License 2.0 - 详见 `LICENSE` 文件

---

**仓库地址**：https://github.com/MacroJourney/PersonalOS
**问题反馈**：使用 `.github/ISSUE_TEMPLATE/` 创建 Issue
**最后更新**：2026-02-03（CLAUDE.md 重写）
