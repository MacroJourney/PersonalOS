# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 仓库概述

这是一个**文档与架构规划仓库**（非代码项目），用于个人 AI 协作系统的设计与规划。

## 核心项目

### AI 数字分身系统（主项目）
人机协作操作系统，核心设计：
- **三区文件架构**：`00_Core/`（规则宪法）、`01_Shared/`（协作区）、`02_Human/`（人类私有）、`03_AI/`（AI 工作区）
- **技术选型**：Electron + React 18 + TypeScript + SQLite + Vercel AI SDK
- 多 AI 供应商支持（Claude、ChatGPT、Gemini）

### 防拖延系统
macOS 应用概念，针对下班后拖延问题的解决方案：
- **技术选型**：Swift + SwiftUI（原生 macOS 应用）vs Tauri（跨平台方案）
- **核心功能**：空闲检测、生产力干预、习惯追踪

### 三层 PDCA 个人操作系统
基于 PDCA 循环的人机协作框架设计，包含三层迭代结构：
- **顶层**：战略层（月度/季度校准方向）
- **中层**：项目层（周度推进目标）
- **底层**：能力层（持续放大核心能力）

灵感来源于 Twitter 推文的思考，强调"可复用、能进化、低消耗的人机协作个人操作系统"。

**方案演进**：
- `01_九种方案概览.md` - 早期探索方案（已废弃）
- `02_多AI Agent方案.md` - 旧方案（已废弃）
- `03_Claude精简方案.md` - 旧方案（已废弃）
- **`04_融合方案_基于Ideaverse改造.md` - ⭐ 最终确定方案**（融合 Ideaverse Zero 2.5 + PDCA 三层系统）

### Ideaverse Pro 2.5（参考 Vault）
Nick Milo 的 **Linking Your Thinking (LYT)** 方法论 Obsidian Vault，作为知识管理参考模板。

**目录位置**：
- `ideaversePro2.5/Ideaverse Pro 2.5/` - 含作者完整内容的示例 Vault
- `ideaversePro2.5/Ideaverse Zero 2.5/` - 空白基础框架（供用户使用）

**核心架构 - ACE Framework**：
```
├── + (Inbox)           # 快速捕获，新想法暂存
├── Atlas/              # 知识地图层
│   ├── Dots/           # 原子笔记：People, Things, Quotes, Statements, Questions
│   ├── Maps/           # MOC (Map of Content) 索引页
│   └── Sources/        # 信息来源：Books, Movies, Clippings, Courses 等
├── Calendar/           # 时间维度
│   ├── Days/           # 每日笔记
│   ├── Records/        # 事件记录：Meetings, Events, Ideas
│   └── Reviews/        # 周期复盘
├── Efforts/            # 行动维度
│   ├── Areas/          # 持续关注领域 (AOE)
│   ├── Projects/       # 项目：Active, Simmering, Sleeping
│   └── Works/          # 作品输出：Articles, Videos, Newsletters
└── x/                  # 系统资源
    ├── Packs/          # 教程包
    ├── Templates/      # 模板库
    └── Visuals/        # 图片、Excalidraw
```

**核心方法论**：
- **ARC Framework**：Add（添加）→ Relate（关联）→ Communicate（输出）
- **MOC (Map of Content)**：主题索引页，连接相关笔记
- **Wayfinders**：导航条，快速跳转核心区域
- **Home Base**：Dataview 驱动的仪表盘视图

**关键插件**：Dataview、Templater、QuickAdd、Periodic Notes、Excalidraw、Calendar

## 关键架构文档

### AI 数字分身系统
- `AI数字分身系统工程化设计、技术选型与架构建议.md` - 主架构文档，含技术选型分析、组件设计、8周 MVP 路线图
- `播客逐字稿.txt` - 655 行参考资料
- **Claude 版搭建指南**（推荐 V2.1）：
  - `Claude 版/AI 数字分身搭建指南_Claude 版V2.1.md` - 三区工作空间设计原则（最新版）
  - `Claude 版/AI 数字分身搭建指南_Claude 版V2.0.md` - 旧版
  - `Claude 版/AI 数字分身搭建指南_Claude 版V1.0.md` - 旧版
- **其他 AI 版本**：
  - `ChatGPT 版/AI 数字分身搭建指南_ChatGPT版V1.0.md`
  - `Gemini 版/Digital_Avatar_Setup_Guide.md`
  - `Gemini 版/Ultimate_Digital_Avatar_Guide.md`

### 三层 PDCA 个人操作系统
- `背景.md` - 项目起源（Twitter 推文灵感）
- `01_九种方案概览.md` - 早期探索的 9 种方案（已废弃）
- `02_多AI Agent方案.md` - 旧方案（已废弃）
- `03_Claude精简方案.md` - 旧方案（已废弃）
- **`04_融合方案_基于Ideaverse改造.md` - ⭐ 最终确定方案**（基于 Ideaverse Zero 2.5 改造，融合 PDCA 三层系统）

### 防拖延系统
- `防拖延需求和技术选型聊天记录.md` - 需求分析与技术讨论
- `下班后拖延解决方案讨论_Claude版.md` - 解决方案设计
- `Tauri.md` - macOS 开发的 Tauri vs Swift 技术对比分析

### 开发工具流程
- `Other/Spec工作流.md` - Spec 驱动开发工作流与工具对比（Spec-Kit、OpenSpec 等）

## AI 交互原则（摘自文档）

1. 绝不轻易说"我做不到"——先查经验库 → 再搜索网络 → 再造工具 → 实在不行才汇报
2. 保持强主动性——主动探索、检查、复盘、留痕

## 开发方式

当此仓库开始写代码时：
- 推荐工作流：**Spec-Kit**（规格驱动开发）
- 基于宪法机制保持 AI 交互一致性
- 本地优先数据架构（不上传云端）
