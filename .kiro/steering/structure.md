# 项目结构

## 仓库组织

本仓库包含构建个人 AI 协作系统的**文档和模板**。经过 v2.1 重构，现在组织为清晰的模块化结构。

### 顶层目录

```
PersonalOS/                          # 仓库根目录
│
├── README.md                        # 项目总览和快速开始
├── CHANGELOG.md                     # 版本变更记录
├── CLAUDE.md                        # Claude 相关说明
│
├── docs/                            # 核心文档
│   ├── 00_核心设计.md               # 系统核心设计
│   ├── 01_快速开始.md               # 分步实施指南
│   ├── 02_30天成长计划.md           # 30 天入门计划
│   ├── 03_模板库.md                 # 即用模板集合
│   ├── 04_AI配置完整版.md           # AI 系统提示词
│   ├── 05_FAQ与防坑.md              # 常见问题和避坑
│   └── 06_在仓库中搭建系统.md        # 在仓库中搭建工作空间指南
│
├── templates/                       # 用户可复制的模板
│   ├── 00_Core/                     # 核心配置模板
│   │   ├── profile.template.md
│   │   ├── interaction_rules.template.md
│   │   └── stop_conditions.template.md
│   │
│   ├── CLAUDE.template.md           # CLAUDE.md 模板（Claude Code 引导程序）
│   │
│   ├── 01_Shared/                   # Obsidian Vault 基础结构（空）
│   │   └── .gitkeep                 # 保持目录存在
│   │
│   └── obsidian-vault/              # 完整 Obsidian Vault 参考
│       ├── README.md                # 使用说明
│       ├── Ideaverse Pro 2.5/       # 完整版
│       └── Ideaverse Zero 2.5/      # 精简版
│
├── examples/                        # 示例和最佳实践
│   ├── profile-examples.md          # 底层画像示例
│   ├── rules-examples.md            # 交互规则示例
│   ├── project-workflow.md          # 项目工作流示例
│   └── review-templates.md          # 复盘模板示例
│
├── references/                      # 参考资料（历史方案）
│   ├── README.md                    # 参考资料说明
│   │
│   ├── AI数字分身系统/              # AI 数字分身早期探索
│   │   ├── README.md
│   │   └── AI 数字分身系统/
│   │       ├── ChatGPT 版/
│   │       ├── Claude 版/
│   │       ├── Gemini 版/
│   │       ├── AI数字分身系统工程化设计、技术选型与架构建议.md
│   │       └── 播客逐字稿.txt
│   │
│   ├── 三层PDCA方案/                # 三层 PDCA 方案演化
│   │   ├── README.md
│   │   └── 三层 PDCA 个人操作系统/
│   │       ├── 01_九种方案概览.md
│   │       ├── 02_多AI Agent方案.md
│   │       ├── 03_Claude精简方案.md
│   │       ├── 04_融合方案_基于Ideaverse改造.md
│   │       ├── 背景.md
│   │       └── 聊天记录.md
│   │
│   └── 终极融合方案.md              # 四区工作空间与 PDCA 融合方案（v2.1 前身）
│
├── archive/                         # 归档（不相关内容）
│   ├── README.md                    # 归档说明
│   ├── Other/
│   │   └── Spec工作流.md
│   └── 防拖延系统/
│       ├── Tauri.md
│       ├── 下班后拖延解决方案讨论_Claude版.md
│       ├── 流程图.xml
│       └── 防拖延需求和技术选型聊天记录.md
│
└── .kiro/                           # Kiro 配置
    └── steering/
        ├── tech.md
        ├── structure.md             # 本文档
        └── product.md
```

## 关键文档

### 主要入口点

1. **README.md** - 项目总览，快速了解 PersonalOS
2. **docs/00_核心设计.md** - 核心系统设计和理念
3. **docs/01_快速开始.md** - 分步实施指南

### 核心文档（按阅读顺序）

| 文档 | 用途 | 阅读时间 |
|------|------|----------|
| `docs/00_核心设计.md` | 理解系统设计理念 | 30 分钟 |
| `docs/01_快速开始.md` | 开始搭建系统 | 1 小时 |
| `docs/02_30天成长计划.md` | 30 天入门计划 | 参考 |
| `docs/03_模板库.md` | 查找可用模板 | 参考 |
| `docs/04_AI配置完整版.md` | 配置 AI 助手 | 1 小时 |
| `docs/05_FAQ与防坑.md` | 解决常见问题 | 参考 |
| `docs/06_在仓库中搭建系统.md` | 在仓库中搭建指南 | 1 小时 |

### 模板文件

| 模板 | 用途 |
|------|------|
| `templates/00_Core/profile.template.md` | 创建底层画像 |
| `templates/00_Core/interaction_rules.template.md` | 定义 AI 交互规则 |
| `templates/00_Core/stop_conditions.template.md` | 定义停止条件 |
| `templates/CLAUDE.template.md` | CLAUDE.md 引导程序模板 |
| `templates/obsidian-vault/Ideaverse Pro 2.5/` | 完整 Obsidian Vault 参考 |
| `templates/obsidian-vault/Ideaverse Zero 2.5/` | 精简 Obsidian Vault 参考 |

### 示例文档

| 示例 | 用途 |
|------|------|
| `examples/profile-examples.md` | 查看底层画像示例 |
| `examples/rules-examples.md` | 查看交互规则示例 |
| `examples/project-workflow.md` | 学习项目管理流程 |
| `examples/review-templates.md` | 使用复盘模板 |

### 参考资料（可选阅读）

| 资料 | 用途 |
|------|------|
| `references/AI数字分身系统/` | 了解数字合伙人系统的设计历史 |
| `references/三层PDCA方案/` | 了解 PDCA 系统的演化过程 |
| `references/终极融合方案.md` | 了解四区工作空间与 PDCA 的融合 |
| `references/应用层设计方案.md` | PersonalOS 桌面应用技术规划（未来方向） |

## 四区工作空间

PersonalOS 支持两种使用方式：

### 方式一：在仓库中搭建（推荐）

直接在 PersonalOS 仓库中创建用户工作空间：

```
PersonalOS/                  # 仓库根目录
│
├── 00_Core/                 # 你的核心配置（.gitignore 排除）
│   ├── profile.md
│   ├── interaction_rules.md
│   ├── stop_conditions.md
│   ├── awakening_spell.md
│   └── memory/
│
├── 01_Shared/               # 你的 Obsidian Vault（.gitignore 排除）
│   ├── Atlas/
│   ├── Calendar/
│   ├── Efforts/
│   ├── Strategy/
│   ├── x/
│   └── +/
│
├── 02_Human/                # 你的私人空间（.gitignore 排除）
│   ├── drafts/
│   ├── notes/
│   ├── personal/
│   └── review_queue/
│
├── 03_AI/                   # AI 空间（.gitignore 排除）
│   ├── workspace/
│   ├── tools/
│   ├── ai_diary/
│   └── research/
│
├── docs/                    # 文档（Git 管理）
├── templates/               # 模板（Git 管理）
├── examples/                # 示例（Git 管理）
├── references/              # 参考资料（Git 管理）
└── archive/                 # 归档（Git 管理）
```

**优点**：
- 文档和实际使用在同一个仓库中
- 便于管理和备份
- 可以随时参考文档和模板
- 个人数据通过 `.gitignore` 保持私密

**详细指南**：参考 `docs/06_在仓库中搭建系统.md`

### 方式二：独立工作空间

在其他位置创建独立的用户工作空间：

```
PersonalOS/                  # 用户工作空间（独立位置）
│
├── 00_Core/                 # 核心配置（人类控制）
│   ├── profile.md           # 底层画像（< 2000字，5分类）
│   ├── interaction_rules.md # AI 交互规则
│   ├── stop_conditions.md   # 停止条件
│   ├── awakening_spell.md   # 唤醒咒语
│   └── memory/              # 记忆系统
│       ├── long_term.md     # 长期记忆（稳定的身份、目标、偏好）
│       ├── recent_rolling.md # 近期滚动（最近30天，≤300字）
│       └── compression_rule.md # 压缩规则（近期→长期）
│
├── 01_Shared/               # 协作区（Obsidian Vault）
│   ├── Atlas/               # 知识管理（Ideaverse）
│   │   ├── Dots/            # 原子笔记
│   │   ├── Maps/            # 内容地图（MOC）
│   │   └── Sources/         # 外部资源
│   │
│   ├── Calendar/            # 时间管理
│   │   ├── Days/            # 每日笔记
│   │   ├── Records/         # 记录
│   │   └── Reviews/         # 复盘
│   │       ├── Weekly/      # 每周复盘
│   │       ├── Monthly/     # 每月复盘
│   │       ├── Quarterly/   # 每季度复盘
│   │       └── Yearly/      # 每年复盘
│   │
│   ├── Efforts/             # 项目和领域
│   │   ├── Projects/        # 项目（有终点）
│   │   ├── Areas/           # 领域（持续维护）
│   │   └── Works/           # 作品
│   │
│   ├── Strategy/            # 战略规划（PDCA 战略层）
│   │   ├── north-star.md    # 北极星指标（3-5年方向）
│   │   ├── annual-plan.md   # 年度计划
│   │   ├── quarterly/       # 季度规划
│   │   └── reviews/         # 战略复盘
│   │
│   ├── x/                   # 系统资源
│   │   ├── rules/           # 决策规则库
│   │   ├── ai-conversations/ # 重要 AI 对话
│   │   ├── Templates/       # 笔记模板
│   │   ├── Packs/           # 资源包
│   │   └── Visuals/         # 视觉资源
│   │
│   └── + (Inbox)/           # 快速捕获
│
├── 02_Human/                # 私人空间（AI 不访问）
│   ├── drafts/              # 草稿
│   ├── notes/               # 私人笔记
│   ├── personal/            # 个人事务
│   └── review_queue/        # 待复盘队列
│
└── 03_AI/                   # AI 自主空间
    ├── workspace/           # AI 工作区
    ├── tools/               # AI 工具
    ├── ai_diary/            # AI 日记
    └── research/            # AI 研究
```

**优点**：
- 工作空间与文档仓库分离
- 更灵活的位置选择
- 适合已有工作空间的用户

## Ideaverse 集成

PersonalOS 的 `01_Shared/` 基于 **Ideaverse Pro 2.5** 框架：

### 核心结构

- **Atlas/** - 知识管理
  - **Dots/** - 原子笔记（Zettelkasten 方法）
  - **Maps/** - 内容地图（MOC）
  - **Sources/** - 外部资源和引用

- **Calendar/** - 时间管理
  - **Days/** - 每日笔记
  - **Records/** - 事件记录
  - **Reviews/** - 定期复盘

- **Efforts/** - 项目和领域
  - **Projects/** - 有明确终点的项目
  - **Areas/** - 持续维护的领域
  - **Works/** - 创作作品

- **+ (Inbox)** - 快速捕获入口

### PDCA 系统增强

PersonalOS 在 Ideaverse 基础上增加了三层 PDCA 系统：

- **Strategy/** - 战略层（季度/年度）
- **x/rules/** - 决策规则库（复利增长）
- **Calendar/Reviews/** - 结构化复盘（持续改进）

### 如何使用 Ideaverse 模板

⚠️ **重要提醒**：Ideaverse Pro 和 Zero 是付费内容，已在 `.gitignore` 中排除，不会被提交到 Git。

用户可以选择：

1. **完整版**：复制 `templates/obsidian-vault/Ideaverse Pro 2.5/` 到 `01_Shared/`
   ```bash
   cp -r templates/obsidian-vault/Ideaverse\ Pro\ 2.5/* 01_Shared/
   ```

2. **精简版**：复制 `templates/obsidian-vault/Ideaverse Zero 2.5/` 到 `01_Shared/`
   ```bash
   cp -r templates/obsidian-vault/Ideaverse\ Zero\ 2.5/* 01_Shared/
   ```

3. **选择性复制**：只复制需要的部分
   ```bash
   cp -r templates/obsidian-vault/Ideaverse\ Pro\ 2.5/Atlas 01_Shared/
   cp -r templates/obsidian-vault/Ideaverse\ Pro\ 2.5/Calendar 01_Shared/
   # ... 根据需要复制其他部分
   ```

4. **完全自定义**：从空白开始构建
   ```bash
   mkdir -p 01_Shared/{Atlas/{Dots,Maps,Sources},Calendar/{Days,Records,Reviews},Efforts/{Projects,Areas,Works},Strategy,Meta,x,+}
   ```

5. **使用其他模板**：如果没有 Ideaverse，可以使用其他 Obsidian 模板或从空白开始

## 文件命名规范

### Markdown 文件

- 使用描述性中文名称
- 用下划线分隔多个词：`个人_档案.md`
- 核心文档使用数字前缀：`00_核心设计.md`

### 日期格式

- 统一使用 ISO 8601 格式：`YYYY-MM-DD`
- 示例：`2026-02-02`
- 每日笔记：`Calendar/Days/2026-02-02.md`

### 版本号

- 附加在文件名末尾：`文档名_V2.1.md`
- 使用语义化版本：主版本.次版本.修订版本

### 模板文件

- 使用 `.template.md` 后缀：`profile.template.md`
- 或存储在 `Templates/` 目录中
- 模板名称应清晰说明用途

## 文档模式

### 文档头部（Front Matter）

推荐在文档开头包含元数据：

```markdown
---
title: 文档标题
version: v1.0
created: 2026-02-02
updated: 2026-02-02
type: guide | reference | template | example
tags: [tag1, tag2]
---
```

### 交叉引用

文档之间使用以下引用方式：

1. **相对路径**（同目录内）：
   ```markdown
   参考 [快速开始](01_快速开始.md)
   ```

2. **完整路径**（跨目录）：
   ```markdown
   参考 [核心设计](docs/00_核心设计.md)
   ```

3. **Obsidian 双向链接**（在 01_Shared/ 中）：
   ```markdown
   参考 [[核心概念]]
   ```

4. **章节锚点**：
   ```markdown
   参考 [核心设计](docs/00_核心设计.md#二系统架构)
   ```

## 使用本仓库

### 对于新用户

**推荐学习路径**：

1. **第 1 天**：阅读 `README.md` 和 `docs/00_核心设计.md`
2. **第 2-3 天**：按照 `docs/01_快速开始.md` 搭建系统
3. **第 1 周**：参考 `docs/02_30天成长计划.md` 建立习惯
4. **第 2-4 周**：使用 `examples/` 中的示例优化系统
5. **第 2-3 月**：深入阅读 `docs/00_核心设计.md` 理解架构设计

**快速开始步骤**：

1. 克隆或下载本仓库
2. 阅读 `README.md` 了解项目
3. 复制 `templates/00_Core/` 中的模板创建配置
4. 复制 `templates/CLAUDE.template.md` 为根目录 `CLAUDE.md`
5. 选择 Ideaverse 模板初始化 `01_Shared/`
6. 在 Obsidian 中打开 `01_Shared/`
7. 配置 AI 工作模式（参考 `docs/04_AI配置完整版.md`）

### 对于现有用户

**升级到 v2.1**：

1. 备份现有工作空间
2. 查看 `CHANGELOG.md` 了解变更
3. 根据新结构调整文件组织
4. 更新 AI 配置文件
5. 测试新功能

### 对于贡献者

**贡献指南**：

1. **保持中文**：所有文档使用简体中文
2. **遵循结构**：不要随意改变目录结构
3. **更新引用**：移动文件时更新所有交叉引用
4. **遵循规范**：遵循文件命名和文档模式
5. **测试模板**：提交前测试所有模板可用性
6. **更新文档**：修改结构时同步更新本文档

**提交流程**：

1. Fork 仓库
2. 创建功能分支
3. 进行修改
4. 测试修改
5. 提交 Pull Request
6. 等待审核

## 目录用途说明

### docs/ - 核心文档

**用途**：PersonalOS 的核心设计和使用文档

**内容类型**：
- 设计理念
- 实施指南
- 使用手册
- 常见问题

**更新频率**：随系统演化更新

### templates/ - 模板库

**用途**：用户可直接复制使用的模板

**内容类型**：
- 配置文件模板
- Obsidian Vault 结构
- 笔记模板

**使用方式**：复制到用户工作空间

### examples/ - 示例文档

**用途**：展示最佳实践和实际使用案例

**内容类型**：
- 配置示例
- 工作流示例
- 模板示例

**学习价值**：帮助理解如何使用系统

### references/ - 参考资料

**用途**：历史方案和设计演化记录

**内容类型**：
- 早期探索文档
- 方案对比
- 设计讨论

**阅读建议**：可选阅读，了解设计背景

### archive/ - 归档内容

**用途**：与 PersonalOS 无关的内容

**内容类型**：
- 废弃方案
- 无关项目

**使用建议**：一般不需要阅读

## 相关系统和方法论

PersonalOS 整合了多个成熟的方法论：

### Ideaverse

- **来源**：Nick Milo 的知识管理框架
- **核心理念**：MOC（内容地图）+ Zettelkasten（原子笔记）
- **在 PersonalOS 中的应用**：`01_Shared/` 的基础结构

### PARA

- **来源**：Tiago Forte 的信息组织方法
- **核心理念**：Projects（项目）、Areas（领域）、Resources（资源）、Archives（归档）
- **在 PersonalOS 中的应用**：部分参考，主要体现在 `Efforts/` 结构

### Zettelkasten

- **来源**：Niklas Luhmann 的笔记方法
- **核心理念**：原子笔记 + 双向链接
- **在 PersonalOS 中的应用**：`Atlas/Dots/` 的笔记方式

### MOC（Maps of Content）

- **来源**：Nick Milo
- **核心理念**：使用地图笔记组织和导航知识
- **在 PersonalOS 中的应用**：`Atlas/Maps/` 的组织方式

### PDCA 循环

- **来源**：戴明循环（Deming Cycle）
- **核心理念**：Plan（计划）→ Do（执行）→ Check（检查）→ Act（调整）
- **在 PersonalOS 中的应用**：三层嵌套 PDCA 系统

### GTD（Getting Things Done）

- **来源**：David Allen
- **核心理念**：捕获、澄清、组织、反思、执行
- **在 PersonalOS 中的应用**：`+ (Inbox)` 快速捕获，`Calendar/Days/` 任务管理

## 版本历史

- **v2.1** (2026-02-02)：重构版本，清晰的模块化结构
- **v2.0** (2024-XX)：融合版本，整合四区工作空间和 PDCA 系统
- **v1.0** (2024-XX)：初始版本，基础框架

详见 `CHANGELOG.md`。

---

**最后更新**：2026-02-07
**版本**：v2.1  
**维护者**：PersonalOS 项目组
