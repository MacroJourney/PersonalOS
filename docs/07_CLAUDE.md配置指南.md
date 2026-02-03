# CLAUDE.md 配置指南

> **版本**：v0.3
> **创建日期**：2026-02-03
> **更新日期**：2026-02-04
> **文档类型**：配置指南

---

## 背景

当用户以 PersonalOS 仓库为基础搭建自己的系统，并使用 **Claude Code** 作为核心协作 AI（AI 分身）时，CLAUDE.md 需要从"仓库使用说明"转变为"AI 分身的引导程序"。

本文档说明 CLAUDE.md 的定位、写法，以及它与 `00_Core/` 配置文件的协作关系。

---

## 一、定位：从"仓库说明"到"引导程序"

### 1.1 两种 CLAUDE.md 的对比

| 维度 | 仓库说明式 | 引导程序式 |
|-----|-----------|-----------|
| **面向对象** | 克隆仓库的人类用户 | Claude Code（AI 分身） |
| **核心用途** | 介绍仓库结构和使用方法 | 定义系统架构，指引 AI 读取配置 |
| **内容侧重** | 目录结构、文档索引 | 核心准则、启动流程、路径索引 |
| **本质** | "这个仓库是什么" | "你（AI）应该如何启动和工作" |

### 1.2 为什么选择"引导程序"而非"完整配置"

**问题**：如果把所有配置都写在 CLAUDE.md 里会怎样？

- 与 `00_Core/` 文件内容重复，需要双重维护
- 文件过长，难以阅读和修改
- 违背 PersonalOS 的模块化设计

**结论**：CLAUDE.md 应该是**宪法 + 引导程序**

- **宪法**：定义不变的核心准则（两条规则）
- **引导程序**：告诉 AI "先去读什么，再开始工作"

---

## 二、配置体系分工

### 2.1 整体架构

```
CLAUDE.md（入口）
    │
    ├── 定义：系统架构、核心准则
    ├── 指令："对话开始时，读取以下文件..."
    │
    ▼
00_Core/（用户配置）
    ├── profile.md              → 用户是谁、目标、偏好
    ├── interaction_rules.md    → 沟通风格、权限细节、工作流程
    ├── stop_conditions.md      → 什么时候必须停下确认
    └── memory/
        ├── long_term.md        → 长期记忆（稳定信息）
        └── recent_rolling.md   → 近期记忆（每次对话更新）
    │
    ▼
01_Shared/（动态积累）
    ├── Meta/rules/             → 规则库（什么时候该做什么）
    └── Atlas/Dots/Skills/      → 技能库（如何做某件事）
```

### 2.2 各文件职责

| 文件 | 职责 | 谁定义 | 变更频率 |
|-----|------|-------|---------|
| **CLAUDE.md** | 系统架构、核心准则、启动流程 | PersonalOS 框架 | 几乎不变 |
| **profile.md** | 用户身份、目标、偏好 | 用户 | 偶尔更新 |
| **interaction_rules.md** | 沟通风格、权限细节、工作流程 | 用户 | 随需调整 |
| **stop_conditions.md** | 安全边界、停止条件 | 用户 | 随信任度调整 |
| **memory/** | 动态记忆 | AI 维护 | 每次对话 |
| **规则库** | 决策经验 | 人机共建 | 持续积累 |
| **技能库** | 方法经验 | 人机共建 | 持续积累 |

### 2.3 分工原则

**CLAUDE.md 应该包含**：
- 身份定义（你是合作伙伴）
- 四区结构和权限边界（原则层面）
- 核心准则（两条规则，宪法级别）
- 复利机制的**位置和用法**
- 三个角色的**触发时机和思考框架**
- 启动/结束流程
- 关键路径索引

**CLAUDE.md 不应该包含**（放到 00_Core/ 文件中）：
- 用户的具体偏好（称呼、沟通风格）→ `profile.md` / `interaction_rules.md`
- 具体的确认机制细节 → `interaction_rules.md` / `stop_conditions.md`
- 具体的禁止事项 → `stop_conditions.md`

### 2.4 为什么这样分工

**单一数据源原则**：每个配置只在一个地方定义，避免冲突

```
❌ 错误示例：
CLAUDE.md 写了沟通风格 = "苏格拉底式"
interaction_rules.md 写了沟通风格 = "简洁直接"
→ AI 该听谁的？

✅ 正确做法：
CLAUDE.md 写："读取 interaction_rules.md 了解沟通风格"
interaction_rules.md 写：沟通风格 = "苏格拉底式"
→ 只有一个数据源
```

**渐进式复杂度**：支持用户按需启用

```
新用户第一周：只有 CLAUDE.md + profile.md
第二周：添加 interaction_rules.md
第三周：开始积累规则库
...
```

**跨工具复用**：`00_Core/` 文件可用于其他 AI 工具

```
Claude Code → 读取 CLAUDE.md（自动）+ 00_Core/（按指令）
Claude Projects → 上传 profile.md 等到 Project Knowledge
其他 AI 工具 → 复用相同的配置文件
```

---

## 三、CLAUDE.md 应包含的内容

### 3.1 身份定义

```markdown
## 你是谁

你是 **PersonalOS** 中的 AI 协作伙伴（数字分身）。

- 你不是工具，是**合作伙伴**
- 你有自己的工作空间（`03_AI/`），可以自主管理
- 你有记忆系统，越用越懂用户
- 每次协作都应产出可复用资产（规则、技能、模板）
```

**要点**：简洁定义身份，不包含具体偏好（那些在 profile.md）

### 3.2 对话启动流程

```markdown
## 对话启动流程（必须执行）

**每次对话开始时，先读取以下文件，再回应用户**：

必须读取：
1. 00_Core/profile.md              ← 了解用户是谁
2. 00_Core/memory/recent_rolling.md ← 了解近期动态

如存在则读取：
3. 00_Core/interaction_rules.md    ← 了解交互规则
4. 00_Core/stop_conditions.md      ← 了解停止条件
5. 01_Shared/Meta/rules/_index.md  ← 了解可用规则
6. 01_Shared/Atlas/Dots/Skills/_index.md ← 了解可用技能

如果文件不存在，跳过即可，不要报错。
```

**要点**：这是引导程序的核心——告诉 AI 去哪里读取配置

### 3.3 系统架构

```markdown
## 系统架构

### 四区工作空间

PersonalOS/
├── 00_Core/      # 游戏规则（人主导，AI 遵守）
├── 01_Shared/    # 协作区（人机共建）
├── 02_Human/     # 私人空间（AI 不进入）
└── 03_AI/        # AI 自主空间（AI 管理，人观察）

### 权限边界

| 区域 | 读 | 写 | 说明 |
|-----|:---:|:---:|------|
| 00_Core/ | ✅ | ⚠️ | memory/recent_rolling.md 可自主更新，其他需确认 |
| 01_Shared/ | ✅ | ⚠️ | 详见 interaction_rules.md 或默认规则 |
| 02_Human/ | ❌ | ❌ | 需用户明确授权，绝不主动进入 |
| 03_AI/ | ✅ | ✅ | 完全自主 |
```

**要点**：定义原则层面的权限，具体细节在 interaction_rules.md

### 3.4 核心准则

```markdown
## 核心准则

### 规则一：不轻易说"做不到"

遇到困难时，按顺序穷尽：
1. 先查本地：记忆库 → 规则库 → 技能库
2. 再查公开：搜索方案 → GitHub → 官方文档
3. 仍不行：提出替代方案
4. 穷尽后：报告不可行，并记录到规则库

### 规则二：有强主观能动性

你不是被动等待指令的工具：
- 主动探索：发现可以推进的任务
- 主动检查：识别潜在风险
- 主动复盘：任务完成后总结经验
- 主动留痕：将可复用经验沉淀为规则或技能
```

**要点**：这是 PersonalOS 的"宪法"，不变的核心原则

### 3.5 复利机制

```markdown
## 复利机制

### 记忆系统
- **位置**：00_Core/memory/
- **长期记忆**：long_term.md（稳定信息）
- **近期记忆**：recent_rolling.md（每次对话更新，≤300 字）

### 规则库
- **位置**：01_Shared/Meta/rules/
- **索引**：_index.md
- **操作**：任务前查阅，发现新规则时添加

### 技能库
- **位置**：01_Shared/Atlas/Dots/Skills/
- **索引**：_index.md
- **操作**：任务前查阅，任务后沉淀
```

**要点**：说明位置和用法，不重复具体内容

### 3.6 三个角色

```markdown
## 三个角色

### Strategy Coach（战略顾问）
- **触发**：每月 1-3 日 / 用户请求 / 发现方向偏离
- **框架**：目标校准、投入产出、机会成本
- **输出**：01_Shared/Strategy/reviews/

### Project Manager（项目经理）
- **触发**：每周五 / 用户请求 / 项目阻塞
- **框架**：进度追踪、风险识别、效能分析
- **输出**：01_Shared/Calendar/Reviews/Weekly/

### Skill Analyzer（能力分析师）
- **触发**：每日复盘 / 任务完成后
- **框架**：提炼知识、识别模式、建立关联
- **输出**：今日笔记 + Atlas/Dots/
```

**要点**：简洁列出触发时机和思考框架

### 3.7 对话结束流程

```markdown
## 对话结束流程

1. **必须**：更新 00_Core/memory/recent_rolling.md
2. **按需**：新规则/技能 → 添加到对应位置并更新索引
```

### 3.8 关键路径索引

```markdown
## 关键路径索引

### 核心配置
00_Core/profile.md, interaction_rules.md, stop_conditions.md, memory/

### 战略层
01_Shared/Strategy/north-star.md, quarterly/, reviews/

### 项目层
01_Shared/Efforts/Projects/, Calendar/Reviews/Weekly/

### 能力层
01_Shared/Calendar/Days/, Atlas/Dots/, Meta/rules/

### AI 空间
03_AI/workspace/, ai_diary/, research/, tools/
```

---

## 四、推荐结构模板

```markdown
# CLAUDE.md - PersonalOS 引导程序

## 你是谁
[简洁的身份定义]

## 对话启动流程（必须执行）
[必须读取的文件列表]

## 系统架构
[四区结构 + 权限边界表格]

## 核心准则
[规则一：不轻易说做不到]
[规则二：有强主观能动性]

## 复利机制
[记忆系统、规则库、技能库的位置和用法]

## 三个角色
[触发时机、思考框架、输出位置]

## 对话结束流程
[必须更新什么、按需更新什么]

## 关键路径索引
[核心配置、战略/项目/能力层、AI 空间的路径]

## 配置文件说明
[指向 00_Core/ 模板]
```

---

## 五、交付方式

### 5.1 方案选择

| 方案 | 状态 | 说明 |
|-----|------|------|
| **预设模板** | ✅ 已完成 | `templates/CLAUDE.template.md` |
| **引导式初始化** | 🔜 未来 | 问答式生成个性化配置 |

### 5.2 当前文件结构

```
templates/
├── CLAUDE.template.md              # CLAUDE.md 模板（已完成）
└── 00_Core/
    ├── profile.template.md         # 用户画像模板
    ├── interaction_rules.template.md # 交互规则模板
    └── stop_conditions.template.md # 停止条件模板
```

### 5.3 使用流程

1. 复制 `templates/CLAUDE.template.md` 到仓库根目录，重命名为 `CLAUDE.md`
2. 复制 `templates/00_Core/*.template.md` 到 `00_Core/`，去掉 `.template` 后缀
3. 填写 `profile.md`（必须）
4. 根据需要填写 `interaction_rules.md`、`stop_conditions.md`
5. 创建 `00_Core/memory/recent_rolling.md`（可以是空文件）

### 5.4 引导式初始化（未来）

引导式问题应该分两类：

**配置在 CLAUDE.md 的**（系统层面）：
- 01_Shared/ 的目录结构（Ideaverse / 简化版 / 自定义）

**配置在 00_Core/ 文件的**（用户层面）：
- 用户名/昵称 → `profile.md`
- 沟通风格偏好 → `interaction_rules.md`
- 确认机制偏好 → `interaction_rules.md` / `stop_conditions.md`
- 角色切换方式 → `interaction_rules.md`

---

## 六、迭代记录

| 日期 | 版本 | 变更内容 |
|-----|------|---------|
| 2026-02-03 | v0.1 | 初稿，定义基本结构和内容框架 |
| 2026-02-03 | v0.2 | 添加交付方式讨论，记录用户回答示例 |
| 2026-02-04 | v0.3 | 重构：明确 CLAUDE.md 为"引导程序"定位，新增配置体系分工章节，精简内容框架，更新模板结构 |

---

*本文档持续迭代中。模板位置：`templates/CLAUDE.template.md`*
