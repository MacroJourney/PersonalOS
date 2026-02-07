# Obsidian Vault 模板使用说明

> 版本：v2.1  
> 创建日期：2026-02-02

## ⚠️ 重要版权说明

**Ideaverse Pro 2.5 和 Ideaverse Zero 2.5 是付费内容**，由 Nick Milo 创建并拥有版权。

- 这些模板**不包含在公开的 GitHub 仓库中**（已在 `.gitignore` 中排除）
- 仅供**个人本地使用**
- 如需使用，请访问 [Linking Your Thinking](https://www.linkingyourthinking.com/) 购买正版
- 请勿分享、转售或公开发布这些模板

**本 README 仅作为使用说明**，不包含实际的模板文件。

## 概述

本目录包含两个 Obsidian Vault 模板：

1. **Ideaverse Pro 2.5** - 完整版，包含所有功能和示例
2. **Ideaverse Zero 2.5** - 精简版，只有基础结构

## 如何使用

### 方式 1：直接使用完整模板

```bash
# 复制整个 Ideaverse Pro 2.5 到你的工作空间
cp -r "Ideaverse Pro 2.5" ~/MyPersonalOS/01_Shared
```

**适合**：
- 想要快速开始
- 喜欢完整的功能
- 愿意学习 Ideaverse 系统

### 方式 2：使用精简模板

```bash
# 复制 Ideaverse Zero 2.5 到你的工作空间
cp -r "Ideaverse Zero 2.5" ~/MyPersonalOS/01_Shared
```

**适合**：
- 想要从零开始
- 喜欢极简风格
- 只需要基础结构

### 方式 3：选择性复制

```bash
# 只复制需要的部分
cp -r "Ideaverse Pro 2.5/Atlas" ~/MyPersonalOS/01_Shared/
cp -r "Ideaverse Pro 2.5/Calendar" ~/MyPersonalOS/01_Shared/
# ... 根据需要复制其他部分
```

**适合**：
- 有明确需求
- 想要自定义结构
- 已有部分内容

## Ideaverse Pro 2.5 结构

```
Ideaverse Pro 2.5/
├── +/                    # Inbox（快速捕获）
├── Atlas/                # 知识管理
│   ├── Dots/            # 原子笔记
│   ├── Maps/            # 内容地图（MOC）
│   └── Sources/         # 来源和参考
├── Calendar/             # 时间管理
│   ├── Days/            # 每日笔记
│   ├── Records/         # 记录
│   └── Reviews/         # 复盘
├── Efforts/              # 项目和领域
│   ├── Areas/           # 持续关注的领域
│   ├── Projects/        # 有明确目标的项目
│   └── Works/           # 作品和成果
├── x/                    # 系统资源
│   ├── Templates/       # 笔记模板
│   └── Visuals/         # 图片和资源
└── .obsidian/           # Obsidian 配置
```

## Ideaverse Zero 2.5 结构

```
Ideaverse Zero 2.5/
├── +/                    # Inbox
├── Atlas/                # 知识管理（空）
├── Calendar/             # 时间管理（空）
├── Efforts/              # 项目和领域（空）
└── .obsidian/           # 基础配置
```

## PersonalOS 扩展

如果你使用 PersonalOS 框架，建议添加以下目录：

```bash
# 在 01_Shared/ 下添加
mkdir -p Strategy          # 战略规划
mkdir -p Meta/rules        # 决策规则库
mkdir -p Meta/ai-conversations  # AI 对话记录
```

## Obsidian 插件推荐

### 核心插件（已配置）
- **Daily Notes** - 每日笔记
- **Templates** - 模板系统
- **Backlinks** - 反向链接
- **Graph View** - 知识图谱

### 社区插件（推荐安装）
- **Periodic Notes** - 周/月/季度笔记
- **Templater** - 高级模板
- **Dataview** - 数据查询
- **QuickAdd** - 快速添加
- **Calendar** - 日历视图

## 配置说明

### .obsidian/app.json
- 基础应用设置
- 编辑器配置
- 文件和链接设置

### .obsidian/appearance.json
- 主题设置
- 字体配置
- CSS 片段

### .obsidian/hotkeys.json
- 快捷键配置
- 自定义命令

## 使用建议

### 1. 先熟悉结构
- 花 1-2 天时间浏览模板
- 理解每个目录的用途
- 查看示例笔记

### 2. 逐步采用
- 从 Inbox (+/) 开始
- 逐步使用 Atlas 和 Calendar
- 最后扩展到 Efforts

### 3. 定制化
- 根据需求调整结构
- 创建自己的模板
- 配置插件和快捷键

### 4. 保持简单
- 不要过度复杂化
- 只使用真正需要的功能
- 定期清理和整理

## 常见问题

### Q: 必须使用 Obsidian 吗？
A: 不是必须的。这些都是 Markdown 文件，可以用任何编辑器打开。但 Obsidian 提供了最好的体验。

### Q: Pro 和 Zero 有什么区别？
A: Pro 包含完整的示例和配置，Zero 只有基础结构。Pro 适合快速开始，Zero 适合自定义。

### Q: 可以混合使用吗？
A: 可以。你可以从 Zero 开始，然后从 Pro 中复制需要的部分。

### Q: 如何更新模板？
A: 查看 CHANGELOG.md 了解更新内容，然后选择性地复制新功能到你的工作空间。

## 相关文档

- [../00_Core/](../00_Core/) - 核心配置模板
- [../../docs/01_快速开始.md](../../docs/01_快速开始.md) - 快速开始指南
- [../../docs/00_核心设计.md](../../docs/00_核心设计.md) - 系统核心设计（含四区工作空间、PDCA 系统）

## 支持

如有问题，请查看：
- [../../docs/05_FAQ与防坑.md](../../docs/05_FAQ与防坑.md)
- [../../references/](../../references/) - 参考资料
