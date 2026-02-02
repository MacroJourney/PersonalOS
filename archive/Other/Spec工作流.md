我问：
Claude Code 如何实践 Spec 工作流？

AI 回答：
Claude Code 实践 Spec 工作流的完整指南如下：

## 核心理念

Spec 工作流是一种规范驱动的开发方法，将功能开发分为四个连续阶段：**需求（Requirements）→ 设计（Design）→ 任务（Tasks）→ 实现（Implementation）**，确保在编码前明确目标，降低开发不确定性。[^1] [^2]

## 快速开始

### 1. 初始化项目结构

```bash
# 创建必要的目录
mkdir -p .claude/commands/spec
mkdir -p spec
``` [Source](https://github.com/papaolaba/spec-based-claude-code)

### 2. 基本工作流程

```bash
# 创建新规范
/spec-create feature-name "功能描述"

# 或使用分步流程
/spec:new user-authentication       # 初始化规范
/spec:requirements                  # 创建需求文档
/spec:approve requirements          # 批准需求
/spec:design                        # 创建设计文档
/spec:approve design                # 批准设计
/spec:tasks                         # 创建任务列表
/spec:approve tasks                 # 批准任务
/spec:implement                     # 开始实现
``` [^2] [^3]

## 核心命令详解

### 规范管理命令

| 命令 | 功能 | 用法 |
|:---|:---|:---|
| `/spec-create` | 一键自动化完成需求→设计→任务 | `/spec-create feature-name "描述"` |
| `/spec-execute` | 执行指定任务 | `/spec-execute 1 feature-name` |
| `/spec-status` | 显示所有规范的进度 | `/spec-status` |
| `/spec-list` | 列出所有规范 | `/spec-list` |
| `/spec:switch` | 切换活动规范 | `/spec:switch 001-user-auth` | [^4] [^2]

### Bug 修复工作流

```bash
/bug-create issue-name "Bug描述"    # 记录问题
/bug-analyze                        # 分析根本原因
/bug-fix                           # 实施修复
/bug-verify                        # 验证解决方案
``` [^1]

## 文件结构

```
/spec/
├── 001-user-authentication/
│   ├── requirements.md          # 需求文档
│   ├── design.md               # 技术设计
│   ├── tasks.md                # 任务列表
│   ├── .requirements-approved  # 批准标记
│   ├── .design-approved
│   └── .tasks-approved
├── 002-payment-integration/
└── .current-spec               # 当前活动规范
``` [Source](https://github.com/papaolaba/spec-based-claude-code)

## 四个阶段详解

### 阶段1：需求（Requirements）
- 功能概述和用户故事
- 验收标准（Acceptance Criteria）
- 功能需求（P0/P1/P2优先级）
- 非功能需求、约束条件
- 成功指标 [^2]

### 阶段2：设计（Design）
- 架构概览（带 Mermaid 图表）
- 技术栈决策
- 数据模型和 API 设计
- 安全性和性能考虑
- 部署架构 [Source](https://github.com/papaolaba/spec-based-claude-code) [^5]

### 阶段3：任务（Tasks）
- 原子化任务分解
- 时间估算和依赖关系
- 使用 Markdown 复选框跟踪进度
- 每个任务包含测试用例 [Source](https://github.com/papaolaba/spec-based-claude-code)

### 阶段4：实现（Implementation）
```bash
# 按阶段执行
/spec:implement 1              # 执行第一阶段
/spec:update-task "任务描述"   # 标记任务完成
``` [Source](https://github.com/papaolaba/spec-based-claude-code)

## 最佳实践

### 1. 阶段纪律
* ✅ 按顺序完成各阶段
* ✅ 批准前彻底审查
* ❌ 不要跳过阶段
* ❌ 未批准规范前不要实现

### 2. 使用 Steering 文档
```bash
/spec-steering-setup  # 创建项目上下文文档
# 生成：product.md（产品方向）、tech.md（技术标准）、structure.md（项目结构）
```
这些文档为所有规范提供持久的项目上下文，确保一致性。[^3] [^6]

### 3. 推荐模型搭配
- 使用 **Claude Opus 4** 生成规范文档（`/spec-create`）
- 使用 **Claude Sonnet 4** 执行实现（`/spec-execute`） [^4] [^3]

### 4. 版本控制集成
```bash
git commit -m "spec(001): complete requirements phase"
git commit -m "impl(001): complete user model (tasks 3-5)"
git checkout -b feature/001-user-authentication
``` [Source](https://github.com/papaolaba/spec-based-claude-code)

## 适用场景

| 场景 | 推荐方法 |
|:---|:---|
| 新功能，需求明确 | `/spec-execute` 或单独任务命令 |
| 复杂/实验性功能 | `/spec-execute`（手动控制） |
| 现有代码的 Bug | Bug 工作流（`/bug-create` → `/bug-verify`） |
| 学习代码库 | 手动执行单个命令 |
| 生产部署 | 完整规范工作流 + 完成审查 | [^4]

## 核心优势

* 🎯 **提前发现问题** - 编码前识别需求模糊
* 🎮 **保持控制** - 每阶段审查批准后再进行
* 🔄 **安全迭代** - 修改规范不丢失上下文
* 🧠 **保持 AI 专注** - 规划与编码分离
* 📚 **构建知识库** - 文档化决策和上下文 [Source](https://github.com/papaolaba/spec-based-claude-code)

通过这种结构化方法，Spec 工作流将专业软件开发实践引入 AI 辅助编程，在最大化生产力的同时保持开发控制。

[^1]: https://www.aivi.fyi/aiagents/introduce-Claude-Code-Spec-Workflow
[^2]: https://github.com/papaoloba/spec-based-claude-code
[^3]: https://www.npmjs.com/package/@pimzino/claude-code-spec-workflow
[^4]: https://github.com/Pimzino/claude-code-spec-workflow
[^5]: https://joshuaopolko.com/claude-code-specification-workflow-mcp/
[^6]: https://blog.promptlayer.com/claude-code-spec-workflow/
[^7]: https://docs.claude.com/zh-CN/docs/claude-code/common-workflows

我问：
除了 spec-based-claude-code 还有其他工具吗

AI 回答：
除了 **spec-based-claude-code** 和 **claude-code-spec-workflow**，还有多种优秀的 Claude Code 工作流工具和框架：

## 核心工作流框架

### 1. **SuperClaude**
专业级开发框架，包含 19 个专用命令和 9 个认知角色。

**核心特性：**
- **70% 代币使用优化** - 高效处理大型项目
- **Git 检查点系统** - 无上下文丢失的回退
- **9 个认知角色** - 架构师、前端、后端、安全专家等
- **完整生命周期命令** - `/build`、`/test`、`/review`、`/deploy`、`/design`
- **100% 本地运行** - 无服务器依赖，开源 MIT 许可

**安装：**
```bash
git clone https://github.com/NomenAK/SuperClaude.git
cd SuperClaude
./install.sh
``` [^1]

### 2. **Claude CodePro**
Max Ritter 开发的专业环境，功能全面但"重量级"。

**核心特性：**
- **Spec 驱动工作流** - 规范优先开发
- **TDD 强制执行** - 测试驱动开发
- **跨会话内存** - 保持上下文连续性
- **语义搜索** - 智能代码导航
- **质量钩子** - 自动化质量检查
- **模块化规则集成** [^2]

### 3. **ContextKit**
系统化开发框架，将 Claude Code 转变为主动开发伙伴。

**核心特性：**
- **4 阶段规划方法论**
- **专业质量代理**
- **结构化工作流** - 首次尝试产出生产就绪代码 [^2]

## 自治与编排工具

### 4. **Ralph for Claude Code**
Frank Bria 开发的自治 AI 开发框架。

**核心特性：**
- **迭代工作直至完成** - 自主执行项目
- **智能退出检测** - 防止无限循环
- **速率限制与断路器模式** - API 过度使用保护
- **tmux 实时监控集成**
- **75+ 综合测试** [^2]

### 5. **Claude Code Flow**
ruvnet 开发的代码优先编排层。

**核心特性：**
- **自主跨递归代理循环**
- **写、编辑、测试、优化代码**
- **代码优先编排** [^2]

### 6. **Claude Squad**
smtg-ai 开发的多代理管理终端应用。

**核心特性：**
- **独立工作区管理多个 Claude Code**
- **同时处理多任务**
- **支持 Codex 和其他本地代理（包括 Aider）** [^2]

## 文档与上下文管理

### 7. **Claude Code Development Kit**
Peter Krueck 开发的集成系统。

**核心特性：**
- **3 层文档架构** - 基础/组件/功能
- **自动加载文档** - 命令执行时自动包含相关文档
- **MCP 集成** - Context7 + Gemini 实时更新
- **专业钩子系统** - 安全扫描、上下文注入、通知
- **多代理工作流编排** [^3]

### 8. **/context-prime**
elizaOS 开发的上下文加载工具。

**功能：**
- 加载仓库结构全面理解项目
- 建立开发上下文
- 定义协作参数 [^2]

## MCP 服务器集成

Claude Code 支持通过 **Model Context Protocol (MCP)** 连接外部工具：

**常用 MCP 能力：**
- **问题跟踪器集成** - JIRA、GitHub Issues
- **监控数据分析** - Sentry、Statsig
- **数据库查询** - PostgreSQL、MySQL
- **文档查找** - Context7
- **UI 组件生成** - Magic
- **浏览器自动化** - Puppeteer [^4]

**MCP 服务器安装示例：**
```bash
# 添加 GitHub MCP 服务器
claude mcp add --transport http github https://api.githubcopilot.com/mcp/

# 在 Claude Code 中使用
> "Review PR #456 and suggest improvements"
``` [^4]

## AI 代理框架替代品

如果需要更通用的 AI 工作流框架：

| 框架 | 类型 | 特点 |
|:---|:---|:---|
| **LangChain** | 代码优先 | 多步推理链、丰富生态 |
| **Semantic Kernel** | 代码优先 | .NET/Python SDK、规划器 |
| **n8n** | 可视化 | 低代码工作流设计 |
| **Flowise** | 可视化 | 无代码 AI 工作流 |
| **CrewAI** | 混合型 | 多代理协作系统 |
| **AutoGen** | 代码优先 | Microsoft 出品，多代理对话 | [^5] [^6]

## 竞品对比

### **Cursor 的替代品**
- **Qodo** - 企业级多仓库理解，PR 助手
- **Tabnine** - 隐私优先，快速补全
- **Kiro** - **Spec 优先开发**，适合大型企业，强调审计追踪 [^7] [^8]

## 推荐组合

### 轻量级方案
```bash
SuperClaude + MCP 服务器（Context7 + GitHub）
```

### 企业级方案
```bash
Claude Code Development Kit + SuperClaude + 
MCP 服务器（JIRA + Sentry + Database）
```

### 多任务方案
```bash
Claude Squad + Ralph for Claude Code
```

### 规范驱动方案
```bash
spec-based-claude-code 或 claude-code-spec-workflow +
ContextKit
```

这些工具各有侧重，可根据团队规模、项目复杂度和开发流程选择合适的组合。SuperClaude 适合个人开发者快速上手，Claude Code Development Kit 适合大型项目的文档管理，而 Ralph 和 Claude Squad 适合需要自治和并行处理的场景。

[^1]: https://superclaude.org
[^2]: https://github.com/hesreallyhim/awesome-claude-code
[^3]: https://github.com/peterkrueck/Claude-Code-Development-Kit
[^4]: https://code.claude.com/docs/en/mcp
[^5]: https://www.shakudo.io/blog/top-9-ai-agent-frameworks
[^6]: https://blog.n8n.io/ai-agent-frameworks/
[^7]: https://www.builder.io/blog/cursor-alternatives-2026
[^8]: https://www.qodo.ai/blog/cursor-alternatives/

我问：
speckit 和 openspec 怎么样？与 上面你说的工具有什么区别？哪个更好？

AI 回答：
## Spec-Kit 和 OpenSpec 深度对比

两者都是规范驱动开发工具，但设计理念和适用场景截然不同：

## 核心差异对比表

| 维度 | **Spec-Kit**（GitHub） | **OpenSpec**（Fission AI） |
|:---|:---|:---|
| **开发者** | GitHub 官方 | Fission AI |
| **语言/依赖** | Python + uv 包管理器 | TypeScript（npm install） |
| **设计目标** | **新项目（0→1）** | **现有代码库（1→N）** |
| **工作流阶段** | **5 阶段**：Constitution → Specify → Plan → Tasks → Implement | **3 阶段**：Proposal → Review → Archive |
| **安装命令** | `uv tool install speckit` | `npm install -g openspec` |
| **初始化** | `specify init <project>` | `openspec init` |
| **AI 命令数量** | 8 个自定义命令 | 3 个自定义命令 |
| **文档规模** | ~800 行（详尽） | ~250 行（精简） |
| **哲学** | 处方式（Prescriptive）- 手把手指导 | 极简式（Minimalist）- 快速迭代 |
| **自动分支** | ✅ 自动创建 Git 分支 | ❌ 需手动创建 |
| **执行速度** | 较慢（更多验证步骤） | **更快**（更少开销） | [^1]

---

## Spec-Kit 详细解析

### 核心命令（5 阶段工作流）

```bash
# 阶段 0：项目治理原则（一次性设置）
/speckit.constitution  # 创建 .specify/memory/constitution.md

# 阶段 1：功能规范
/speckit.specify       # 定义"做什么"和"为什么"

# 阶段 2：澄清需求（可选）
/speckit.clarify       # AI 提问澄清模糊点

# 阶段 3：技术计划
/speckit.plan          # 选择技术栈、架构决策

# 阶段 4：任务分解
/speckit.tasks         # 生成可执行任务列表

# 阶段 5：实施
/speckit.implement     # 按任务执行代码生成
``` [^2] [^3]

### 独特特性：Constitution（宪法文件）

**最重要的创新**：`.specify/memory/constitution.md` 作为项目"非协商原则"的长期记忆。

**用途示例：**
```bash
/speckit.constitution 构建响应式Web应用、现代设计、
                       clean code、简洁UX、安全优先、
                       不生成测试代码
```

**效果：**
- 一次设置，全项目生效
- 所有后续规范自动遵循这些原则
- 类似"围墙"约束 AI 行为 [^4] [^5]

### 文件结构
```
specs/
├── 001-user-auth/
│   ├── spec.md          # 功能规范
│   ├── plan.md          # 技术计划（含架构图）
│   ├── tasks.md         # 任务列表
│   └── design.md        # 设计决策（可选）
.specify/
├── memory/
│   └── constitution.md  # 项目宪法
└── scripts/             # 自动化脚本
``` [Source](https://github.com/Fission-AI/OpenSpec)

### 适用场景
✅ **绿地项目（Greenfield）** - 从零开始构建  
✅ **需要严格合规的项目** - 医疗、金融等行业  
✅ **团队协作** - 明确的角色分离（产品经理/开发者）  
✅ **初学者友好** - 详细指导和验证步骤  
✅ **复杂域逻辑** - 需要深度规划 [^6]

---

## OpenSpec 详细解析

### 核心命令（3 阶段工作流）

```bash
# 1. 创建变更提案
/openspec:proposal <feature-name>
# 或自然语言：Create an OpenSpec change proposal for...

# 2. 应用变更（直接实施）
/openspec:apply <change-name>

# 3. 归档完成的变更
/openspec:archive <change-name>

# 查看状态
openspec view      # 交互式仪表板
openspec list      # 列出活动变更
openspec validate  # 验证规范格式
``` [Source](https://github.com/Fission-AI/OpenSpec) [Source](https://openspec.dev)

### 独特特性：Delta 格式（变更增量）

OpenSpec 使用"补丁式"规范，只记录变更部分：

```markdown
## ADDED Requirements
### Requirement: Two-Factor Authentication
#### Scenario: User enables 2FA
GIVEN user has verified email
WHEN user enables 2FA in settings
THEN system SHALL send verification code

## MODIFIED Requirements
### Requirement: Login Flow
(包含完整的更新文本)

## REMOVED Requirements
### Requirement: Legacy Password Reset
```

**优势：**
- 变更历史清晰可追溯
- 避免维护重复的完整规范
- 快速理解每次变更的影响 [Source](https://github.com/Fission-AI/OpenSpec)

### 文件结构
```
openspec/
├── project.md           # 项目上下文（一次性设置）
├── specs/               # 当前真相（Source of Truth）
│   └── auth/
│       └── spec.md
├── changes/             # 提议的变更
│   └── add-2fa/
│       ├── proposal.md  # 变更描述
│       ├── tasks.md     # 任务列表
│       └── specs/
│           └── auth/
│               └── spec.md  # Delta（仅变更部分）
└── archive/             # 已完成变更
``` [Source](https://github.com/Fission-AI/OpenSpec)

### 适用场景
✅ **遗留代码维护（Brownfield）** - 已有 90% 的项目  
✅ **快速迭代** - 最小化流程开销  
✅ **小团队/个人开发** - 角色可能重叠  
✅ **高级开发者** - 不需要详细指导  
✅ **频繁变更追踪** - 优秀的版本管理 [^1]

---

## 与前述工具的核心区别

### 与 spec-based-claude-code 对比

| 特性 | spec-based-claude-code | Spec-Kit | OpenSpec |
|:---|:---|:---|:---|
| **批准机制** | ✅ 每阶段手动批准 | ⚠️ 审查但无强制批准 | ❌ 无批准步骤 |
| **分支策略** | 手动管理 | 自动创建分支 | 手动管理 |
| **文档详细度** | 中等 | **最详细** | 最精简 |
| **灵活性** | 高（可跳过阶段） | 低（强制流程） | 最高 |

### 与 SuperClaude 对比

| 维度 | SuperClaude | Spec-Kit | OpenSpec |
|:---|:---|:---|:---|
| **核心价值** | **开发辅助**（命令、角色） | **规范驱动** | **变更管理** |
| **代币优化** | ✅ 70% 减少 | ❌ 无优化 | ✅ 精简输出 |
| **学习曲线** | 低 | 中 | 最低 |
| **适用范围** | 通用开发 | 新项目 | 现有项目 |

**可组合使用：**
```bash
SuperClaude（开发命令） + Spec-Kit（规范管理） = 完整工作流
```

---

## 哪个更好？实战建议

### 选择矩阵

| 你的情况 | 推荐工具 | 理由 |
|:---|:---|:---|
| **全新项目从零开始** | **Spec-Kit** | Constitution 机制确保架构一致性 |
| **现有代码添加功能** | **OpenSpec** | Delta 格式精准跟踪变更 |
| **团队 > 5 人** | **Spec-Kit** | 详细文档利于协作 |
| **独立开发/小团队** | **OpenSpec** | 最小化开销 |
| **需要严格合规** | **Spec-Kit** | 验证步骤更完善 |
| **快速原型验证** | **OpenSpec** | 3 步完成 vs 5 步 |
| **学习规范驱动** | **Spec-Kit** | 手把手指导 |
| **已熟悉 SDD** | **OpenSpec** | 去除冗余流程 |
| **复杂多仓库** | spec-based-claude-code | 更强的控制力 | [^6] [^1]

### 性能对比（实测数据）

| 指标 | Spec-Kit | OpenSpec |
|:---|:---|:---|
| **安装时间** | 30 分钟 | 5 分钟 |
| **初始设置输出** | 800 行 | 250 行 |
| **工作流步骤** | 5 步 | 3 步 |
| **执行速度** | 较慢（验证多） | **快 30-50%** |
| **文档审查时间** | 长（信息密集） | 短（信息精炼） | [^1]

---

## 实践建议

### 混合策略（最佳方案）

```bash
# 项目初期使用 Spec-Kit
specify init my-project
/speckit.constitution  # 设定项目原则
/speckit.specify      # 核心功能规范

# 日常迭代使用 OpenSpec
npm install -g openspec
openspec init
/openspec:proposal add-new-feature  # 快速添加功能
```

**理由：**
- Spec-Kit 的 Constitution 提供长期指导
- OpenSpec 的轻量级适合频繁变更
- 结合两者优势 [^6]

### 工具链组合推荐

**企业级完整方案：**
```
Spec-Kit（规范） + SuperClaude（开发） + MCP 服务器（集成）
```

**敏捷小团队：**
```
OpenSpec（变更管理） + Claude Code Development Kit（文档）
```

**个人开发者：**
```
OpenSpec（简单快速） 或 spec-based-claude-code（灵活控制）
```

---

## 总结：没有"最好"，只有"最适合"

| 如果你是... | 选择 | 原因 |
|:---|:---|:---|
| **GitHub 重度用户** | Spec-Kit | 官方支持，生态整合 |
| **速度至上主义者** | OpenSpec | 最快上手和执行 |
| **流程控制狂** | spec-based-claude-code | 强制批准机制 |
| **追求极致优化** | SuperClaude | 代币使用优化 |
| **首次尝试 SDD** | Spec-Kit | 教育性指导 |

**核心洞察：**  
Spec-Kit 像"架构师"（深思熟虑），OpenSpec 像"敏捷教练"（快速迭代），spec-based-claude-code 像"项目经理"（严格把关）。根据项目阶段和团队文化选择，或者组合使用以发挥各自优势。

[^1]: https://hashrocket.com/blog/posts/openspec-vs-spec-kit-choosing-the-right-ai-driven-development-workflow-for-your-team
[^2]: https://github.com/github/spec-kit/blob/main/README.md
[^3]: https://speckit.org
[^4]: https://www.youtube.com/watch?v=8xXV4FeaF9M
[^5]: https://codestandup.com/posts/2025/github-spec-kit-tutorial-constitution-command/
[^6]: https://www.nosam.com/spec-driven-development-openspec-vs-spec-kit-vs-bmad-which-ones-actually-worth-your-time/
[^7]: https://www.youtube.com/watch?v=-9obEHJkQc8
[^8]: https://www.youtube.com/watch?v=H991whT_qNA

我问：
附件是我的一个需求，与 Claude 讨论后的内容记录。请你帮我分析一下，上面你所说的各种 Spec 工作流，哪个更合适？

AI 回答：
根据你提供的需求文档，我来详细分析最适合的 Spec 工作流工具：

## 项目特征分析

### 你的项目属性

| 维度 | 特征 | 影响 |
|:---|:---|:---|
| **项目类型** | ✅ **Greenfield（新项目）** | 从零开始构建 |
| **需求明确度** | ✅ **非常详细** | 完整PRD+用户旅程+技术方案 |
| **技术栈** | ✅ **已确定** | Swift/SwiftUI/AppKit |
| **复杂度** | 🟡 **中等** | 核心功能清晰，有扩展计划 |
| **开发阶段** | 📋 **PRD完成，准备开发** | 需要转化为可执行任务 |
| **团队规模** | 👤 **个人/小团队** | 从讨论看是个人项目 |
| **开发周期** | ⏱️ **4-6周MVP** | 需要高效执行 |

---

## 推荐方案：**Spec-Kit（GitHub）** 🏆

### 为什么最适合你？

#### ✅ 优势匹配度分析

**1. 新项目完美契合**
```bash
# Spec-Kit 专为 0→1 项目设计
specify init focus-guardian
```
- 你的项目是全新开发，没有历史代码负担
- Spec-Kit 的 5 阶段流程正好匹配"需求→实现"全流程

**2. Constitution 机制解决核心问题**
```bash
/speckit.constitution
```

你可以设定项目"宪法"，作为所有后续开发的指导原则：
```markdown
# Focus Guardian 开发原则

## 技术标准
- 使用 Swift 5.9+，SwiftUI 优先，必要时使用 AppKit
- 数据存储使用 SwiftData（macOS 13+）
- 所有异步操作使用 async/await
- UI 遵循 Apple Human Interface Guidelines

## 代码规范
- 变量命名使用驼峰命名法
- 每个函数必须有注释
- 关键逻辑必须有单元测试

## UI/UX 原则
- 全屏界面必须优雅，不能有性能问题
- 所有动画时长 < 300ms
- 字体使用 SF Pro 系列
- 主色调蓝色 #007AFF

## 数据安全
- 所有数据本地存储，不上传云端
- 敏感操作必须有确认机制
- 紧急退出限制每周 3 次
```

**这个机制的威力**：
- 一次设定，全项目生效
- AI 生成的所有代码自动遵循这些原则
- 避免后期返工和风格不一致

**3. 5 阶段流程与你的 PRD 完美对接**

| Spec-Kit 阶段 | 你当前的材料 | 如何使用 |
|:---|:---|:---|
| 0️⃣ Constitution | 无 | 从 PRD 中提取技术标准和原则 |
| 1️⃣ Specify | ✅ 已有完整 PRD | 直接输入或分模块输入 |
| 2️⃣ Plan | 🟡 部分有（技术栈已定） | AI 生成详细架构设计 |
| 3️⃣ Tasks | ❌ 缺失 | AI 自动分解为可执行任务 |
| 4️⃣ Implement | ❌ 待开发 | 按任务逐步实现 |

**4. 自动任务分解能力**

你的 PRD 有 6 周开发计划，但缺少**具体的编码任务**。Spec-Kit 可以：

```bash
/speckit.tasks
```

自动生成类似这样的任务列表：
```markdown
## Phase 1: 核心空闲检测（Week 1）
- [ ] Task 1.1: 创建 IdleDetector 类
  - 实现 getSystemIdleTime() 方法
  - 集成 IOKit 框架
  - 测试：验证空闲时间获取准确性
  
- [ ] Task 1.2: 实现后台监控循环
  - 每 30 秒检查一次
  - 使用 Timer.publish
  - 测试：验证不会造成性能问题

- [ ] Task 1.3: 时间条件判断逻辑
  - 判断工作日 vs 周末
  - 判断时间段（18:00-23:00）
  - 测试：边界情况测试
```

---

### 具体实施步骤

#### 阶段 0：初始化项目（10 分钟）
```bash
# 1. 安装 Spec-Kit
uv tool install speckit

# 2. 初始化项目
specify init focus-guardian

# 3. 设定项目宪法
/speckit.constitution

# 然后告诉 AI：
"""
这是一个 macOS 应用，使用 SwiftUI + AppKit。
核心原则：
1. 性能优先 - 后台 CPU < 5%
2. 数据本地化 - 不上传任何数据
3. UI 遵循 Apple HIG
4. 代码必须有注释和测试
5. 安全第一 - 权限最小化
"""
```

#### 阶段 1：输入规范（30 分钟）
```bash
/speckit.specify
```

**你有两种输入方式**：

**方式 A：整体输入（推荐）**
```
将我提供的完整 PRD 文档分为 3 个功能模块：
1. 核心检测与触发模块
2. UI 交互与项目管理模块
3. 数据统计与报告模块

为每个模块生成独立的 spec
```

**方式 B：分模块输入**
```bash
# 先做核心功能
/speckit.specify

"""
功能名称：空闲检测与全屏触发

核心需求：
1. 后台监控键盘/鼠标活动
2. 空闲 > 8 小时（可配置）标记为离开
3. 用户重新激活时，判断是否在工作日 18:00-23:00
4. 如果符合条件，触发全屏界面

用户故事：
作为一个拖延症患者，我希望在下班回家开始使用电脑时，
被强制引导做出选择，以避免沉迷娱乐。

验收标准：
- 空闲检测误差 < 5 秒
- 触发判断准确率 100%（时间/日期）
- 全屏界面出现延迟 < 1 秒
"""
```

#### 阶段 2：生成技术计划（30 分钟）
```bash
/speckit.plan
```

AI 会基于你的 PRD 生成：
```markdown
## 技术架构

### 系统组件
┌─────────────────────────────────────┐
│         App Entry Point             │
│       (FocusGuardianApp)            │
└──────────────┬──────────────────────┘
               │
       ┌───────┴────────┐
       ▼                ▼
┌──────────────┐  ┌──────────────────┐
│ IdleMonitor  │  │ FullScreenWindow │
│  Service     │  │    Manager       │
└──────────────┘  └──────────────────┘
       │                ▼
       │          ┌──────────────────┐
       │          │   SwiftUI Views  │
       │          └──────────────────┘
       ▼
┌──────────────────────────────────────┐
│         SwiftData / Core Data        │
│   (UserSession, Project, Settings)   │
└──────────────────────────────────────┘

### 关键决策
1. 使用 SwiftData（需 macOS 13+）vs Core Data
   - 选择：SwiftData（现代化，类型安全）
   
2. 全屏窗口实现
   - 使用 NSWindow + .fullScreen 模式
   - Level 设为 .floating 保持最上层
   
3. 空闲检测
   - IOKit.pwr_mgt 框架
   - 后台 Timer 每 30 秒检查一次
```

#### 阶段 3：任务分解（20 分钟）
```bash
/speckit.tasks
```

生成 6 周的详细任务清单，每个任务都可执行：
```markdown
## Week 1: 基础架构

### 1.1 项目初始化 (2小时)
- [ ] 创建 Xcode 项目（macOS App, SwiftUI）
- [ ] 配置 SwiftData
- [ ] 设置基本文件结构
- [ ] 配置 .gitignore

### 1.2 空闲检测模块 (6小时)
- [ ] 创建 IdleDetector.swift
- [ ] 实现 getSystemIdleTime() 
- [ ] 单元测试
- [ ] 创建 IdleMonitorService
- [ ] 实现状态机（idle → active）

### 1.3 时间判断逻辑 (4小时)
- [ ] 创建 TimeConditionChecker
- [ ] 实现工作日判断
- [ ] 实现时间段判断
- [ ] 边界测试（跨天、跨周）

## Week 2: 全屏界面 (略)
...
```

#### 阶段 4：逐步实现（4-6 周）
```bash
# 执行第一个任务
/speckit.implement

# AI 会自动：
1. 读取 spec 和 plan
2. 按照 tasks 顺序执行
3. 生成代码
4. 创建测试
5. 提交 Git
```

---

## 与其他工具的对比

### 为什么不选 OpenSpec？

| 对比项 | OpenSpec | 你的项目 | 结论 |
|:---|:---|:---|:---|
| 适用场景 | **现有代码库** | 全新项目 | ❌ 不匹配 |
| 变更模式 | Delta（增量） | 从零构建 | ❌ 用不上 |
| 文档复杂度 | 250 行（精简） | 需要详细指导 | ❌ 太简化 |

**OpenSpec 的设计哲学是"快速添加功能到现有系统"，而你是"从头构建完整系统"。**

### 为什么不选 spec-based-claude-code？

| 对比项 | spec-based-claude-code | 你的需求 | 结论 |
|:---|:---|:---|:---|
| 批准机制 | 每阶段手动批准 | 个人项目，可以灵活调整 | 🟡 可用但偏重 |
| 自动化程度 | 需要手动管理 | 希望更自动化 | ⚠️ 增加负担 |
| Git 分支 | 手动创建 | 自动化更好 | ❌ 麻烦 |

**适用场景**：如果是团队项目或需要严格审批，spec-based-claude-code 更好。但你的个人项目不需要这么严格。

---

## 最终推荐方案

### 🥇 主力方案：**Spec-Kit**

```bash
# 完整工作流
specify init focus-guardian
/speckit.constitution    # 设定开发原则
/speckit.specify        # 输入 PRD（分模块或整体）
/speckit.plan          # 生成技术方案
/speckit.tasks         # 分解任务
/speckit.implement     # 逐步实现
```

**适合原因：**
- ✅ 新项目最佳实践
- ✅ Constitution 保证代码一致性
- ✅ 自动任务分解节省时间
- ✅ GitHub 官方支持，生态好

### 🥈 增强方案：**Spec-Kit + SuperClaude**

```bash
# 先安装 SuperClaude
git clone https://github.com/NomenAK/SuperClaude.git
cd SuperClaude && ./install.sh

# 开发时使用
/build              # SuperClaude 的构建命令
/review             # 代码审查
/test               # 测试生成
--persona-security  # 安全专家模式（检查权限问题）
```

**组合优势：**
- Spec-Kit 管理规范和流程
- SuperClaude 提升代码质量（70% 代币优化）
- SuperClaude 的 Persona 模式适合你的场景：
  - `--persona-security`：检查权限和数据安全
  - `--persona-frontend`：优化 SwiftUI 界面
  - `--persona-architect`：审查架构设计

---

## 实战建议

### Phase 1：准备阶段（今天完成）

```bash
# 1. 安装工具
uv tool install speckit

# 2. 准备材料
将你的 PRD 分为 3 个模块：
- 模块 1：空闲检测与触发（核心）
- 模块 2：全屏 UI 与交互（复杂）
- 模块 3：数据统计（独立）

# 3. 设定 Constitution
总结你的技术原则，写成简洁的 20 条规则
```

### Phase 2：第一个模块（本周）

```bash
# 只做核心功能
/speckit.specify "空闲检测与全屏触发"
/speckit.plan
/speckit.tasks
/speckit.implement

# 目标：Week 1-2 任务完成
```

### Phase 3：迭代开发（后续）

```bash
# 每周完成一个模块
# 使用 Spec-Kit 的独立 spec 管理
```

---

## 总结：选择决策树

```
你的项目是新项目吗？
  ├─ 是 → 需求详细吗？
  │       ├─ 是 → 【选 Spec-Kit】✅
  │       └─ 否 → 先完善 PRD
  │
  └─ 否（现有代码） → 【选 OpenSpec】

是否需要严格审批？
  ├─ 是（团队/企业）→ 【选 spec-based-claude-code】
  └─ 否（个人/小团队）→ 【选 Spec-Kit】✅

是否需要代码优化？
  └─ 是 → 【组合：Spec-Kit + SuperClaude】✅
```

**你的答案：Spec-Kit（必选）+ SuperClaude（可选）**

开始行动吧！有任何具体实施问题，随时问我 💪

