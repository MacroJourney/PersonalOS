# 技术栈

## 文件格式

- **主要格式**：Markdown (.md)
- 所有文档、模板和配置文件都使用 Markdown
- 兼容任何 Markdown 编辑器

## 推荐工具

### 知识管理
- **Obsidian**（01_Shared/ 工作空间的首选）
  - 支持双向链接、MOC（内容地图）
  - 插件：Periodic Notes、Templater、Dataview、QuickAdd
  - 用于 PDCA 系统和知识管理

### AI 工具
- **Claude Pro / Claude Code** - 主要 AI 助手
- **ChatGPT Plus** - 备选 AI 助手
- **Cursor** - AI 驱动的代码编辑器，用于"氛围编程"
- **VS Code** - 用于编辑核心配置文件

### 自动化（可选）
- **Zapier / Make.com** - 工作流自动化
- **n8n** - 开源自动化（自托管）
- **Dify / Coze** - AI agent 平台

## 文件结构

系统使用**三区架构**：

```
PersonalOS/
├── 00_Core/          # 核心配置（人类控制）
├── 01_Shared/        # 协作区（Obsidian Vault）
├── 02_Human/         # 私人空间
└── 03_AI/            # AI 自主空间
```

## 无需构建系统

这是一个**文档和框架项目**，而非软件应用：
- 无需编译
- 无需安装依赖
- 无需构建命令
- 文件用于阅读、编辑和作为模板使用

## 常用操作

### 创建目录结构

**macOS/Linux：**
```bash
mkdir -p PersonalOS/{00_Core,01_Shared/{memory,rules,skills,projects,logs},02_Human,03_AI}
```

**Windows (PowerShell)：**
```powershell
New-Item -Path "PersonalOS\00_Core","PersonalOS\01_Shared\memory" -ItemType Directory -Force
```

### 在 Obsidian 中打开

1. 打开 Obsidian
2. "打开文件夹作为仓库"
3. 选择 `PersonalOS/01_Shared/`

### 版本控制（可选）

系统可以使用 Git 进行版本控制：
```bash
git init
git add .
git commit -m "Initial PersonalOS setup"
```

## 集成点

- **Claude Projects**：上传核心文件（profile.md、interaction_rules.md）
- **Obsidian 插件**：配置 Periodic Notes、Templater 实现自动化
- **文件同步**：使用 iCloud、Dropbox 或 Git 进行备份

## 平台兼容性

- **macOS**：完全支持
- **Windows**：完全支持
- **Linux**：完全支持
- **移动端**：有限支持（Obsidian 移动应用可访问 01_Shared/）

## 无需编程

系统专为**非技术用户**设计。所有"编程"通过以下方式完成：
- AI 助手（Claude、ChatGPT）
- 使用 AI 工具进行"氛围编程"（Cursor、Claude Code）
- 无需编程知识
