# PersonalOS - 人机协作个人操作系统

[![GitHub](https://img.shields.io/badge/GitHub-MacroJourney%2FPersonalOS-blue?logo=github)](https://github.com/MacroJourney/PersonalOS)
[![License](https://img.shields.io/badge/License-Apache%202.0-green.svg)](LICENSE)
[![Version](https://img.shields.io/badge/Version-v2.1-orange.svg)](CHANGELOG.md)
[![Language](https://img.shields.io/badge/Language-简体中文-red.svg)](README.md)

> 一个基于 AI 协作的个人成长和生产力系统

## 快速开始

### 方式一：在本仓库中直接搭建（推荐）

如果你克隆了本仓库，可以直接在仓库中创建你的工作空间：

```bash
# 1. 克隆仓库
git clone git@github.com:MacroJourney/PersonalOS.git
cd PersonalOS

# 2. 创建用户工作空间
mkdir -p 00_Core/memory/{decisions,learnings,preferences}
mkdir -p 02_Human/{drafts,notes,personal,review_queue}
mkdir -p 03_AI/{workspace,tools,ai_diary,research}

# 3. 初始化配置文件
cp templates/00_Core/profile.template.md 00_Core/profile.md
cp templates/00_Core/interaction_rules.template.md 00_Core/interaction_rules.md
cp templates/00_Core/stop_conditions.template.md 00_Core/stop_conditions.md

# 4. 初始化 Obsidian Vault（需要自行准备 Ideaverse 模板）
# 如果你有 Ideaverse Pro 2.5
cp -r templates/obsidian-vault/Ideaverse\ Pro\ 2.5/* 01_Shared/
# 或从空白开始
mkdir -p 01_Shared/{Atlas,Calendar,Efforts,Strategy,Meta,x,+}

# 5. 在 Obsidian 中打开 01_Shared/
```

**注意**：
- `00_Core/`、`01_Shared/`、`02_Human/`、`03_AI/` 已在 `.gitignore` 中排除，不会被提交
- Ideaverse 模板是付费内容，不包含在公开仓库中

### 方式二：仅使用文档和模板

1. **阅读核心设计**：[docs/00_核心设计.md](docs/00_核心设计.md)
2. **跟随快速开始指南**：[docs/01_快速开始.md](docs/01_快速开始.md)
3. **在其他位置创建工作空间**
4. **复制模板到你的工作空间**：`templates/` 目录
5. **参考 30 天成长计划**：[docs/02_30天成长计划.md](docs/02_30天成长计划.md)

## 核心特性

- 🤝 **四区工作空间**：明确人类和 AI 的协作边界
- 🔄 **三层 PDCA**：战略层 → 项目层 → 能力层的持续改进
- 🧠 **数字合伙人**：载入你灵魂的 AI 协作伙伴
- 📚 **复利机制**：每次协作都积累可复用资产（规则库、技能库、记忆系统）

## 文档结构

```
docs/           # 核心文档（从这里开始）
  ├── 00_核心设计.md
  ├── 01_快速开始.md
  ├── 02_30天成长计划.md
  ├── 03_模板库.md
  ├── 04_AI配置完整版.md
  ├── 05_FAQ与防坑.md
  └── 06_在仓库中搭建系统.md

templates/      # 可复制的模板
examples/       # 示例和最佳实践
references/     # 历史方案和参考资料
```

## 系统要求

- **必需**：Markdown 编辑器
- **推荐**：Obsidian（用于知识管理）
- **AI 工具**：Claude Code / Cursor（推荐），Claude Projects（补充）

## 版本

当前版本：**v2.1** (2026-02-02)

查看完整变更记录：[CHANGELOG.md](CHANGELOG.md)

## 贡献

本项目主要用于个人迭代需求。如有建议，欢迎提 Issue。

## 相关链接

- 📦 **GitHub 仓库**: https://github.com/MacroJourney/PersonalOS
- 📖 **核心文档**: [docs/00_核心设计.md](docs/00_核心设计.md)
- 🚀 **快速开始**: [docs/01_快速开始.md](docs/01_快速开始.md)
- 💡 **示例**: [examples/](examples/)
- 📚 **参考资料**: [references/](references/)

## 致谢

本项目整合了以下优秀方法论：

- **Ideaverse** by Nick Milo - 知识管理框架
- **PARA** by Tiago Forte - 信息组织方法
- **Zettelkasten** by Niklas Luhmann - 笔记方法
- **PDCA** by W. Edwards Deming - 持续改进循环
- **GTD** by David Allen - 任务管理方法

## 许可

Apache License 2.0

详见 [LICENSE](LICENSE) 文件。
